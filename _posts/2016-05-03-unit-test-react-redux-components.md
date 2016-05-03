---
layout: post
title: How to Unit Test React Redux Components
permalink: /blog/how-to-unit-test-react-redux-components/
---

*Please check out the
[official Enzyme/Mocha guide](http://airbnb.io/enzyme/docs/guides/mocha.html)
if you're unsure how to set up a React test suite with Enzyme and Mocha.*

The cleanest way to unit test a React component is to serve a pure
component whose entire state is passed to it as props. In other words,
the component's props are its only dependency. There is no implicit
state or environment that the component needs to operate in. Instead,
the component only reads the props, and is agnostic about their origins.

This pattern allows you to isolate the component and test it without having
to fabricate the entire application state and underlying architecture in your
tests.

Here's an example of a pure component:

{% highlight javascript %}
import React, {Component, PropTypes} from 'react';
import {bindActionCreators} from 'redux';
import {connect} from 'react-redux';

import {likeComment} from './redux-actions';

export class BlogComment extends Component {
  static get propTypes() {
    return {
      body: PropTypes.string,
      author: PropTypes.string,
      numberOfLikes: PropTypes.number,
      likeComment: PropTypes.func
    };
  }

  render() {
    return (
      <div className="blog-comment">
        <div className="blog-comment__body">{this.props.body}</div>
        <div className="blog-comment__author">{this.props.author}</div>
        <div className="blog-comment__footer">
          <span>{this.props.numberOfLikes} like(s)</span>
          <button type="button" onClick={this.props.likeComment}>Like</button>
        </div>
      </div>
    );
  }
}

// Everything below here is just glue that binds the pure component to a
// certain part of the Redux store, thus telling the component to take its
// props from a Redux store.

function mapStateToProps(state) {
  return {
    body: state.blogComment.body,
    author: state.blogComment.author,
    numberOfLikes: state.blogComment.numberOfLikes
  };
}

function mapDispatchToProps(dispatch) {
  const actions = {
    likeComment
  };

  return bindActionCreators(actions, dispatch);
}

// And finally we export the Redux-connected component, which still is the
// exact same pure component as before, but we've explicitly told it to read
// the props from the Redux store:

export default connect(mapStateToProps, mapDispatchToProps)(BlogComment);
{% endhighlight %}

The key point here is that we've exported two things in this module: the
Redux-connected component as a *default export* (importable without curly
braces) and the base component as a *named export* (importable with curly
braces).

The only difference between these two exports is that the Redux-connected
component is decorated to receive its props through Redux, whereas the base
component only assumes that it will receive the props somehow. Naturally,
the Redux-connected component will be used by the real application whereas
the pure, base version can be used in unit tests.

Since we are specifically unit testing a component and making sure it works
correctly as an independent program, we should not need to care whether it
will receive its state via Redux or another origin, as long as the state is
given to it as props.

This makes it very easy to mock the state in unit tests since we can simulate
various states and actions merely by passing our own fake versions as props.

As an additional safe-guard, we've declared a set of prop types for our four
props to ensure that *body* and *author* will contain string values,
*numberOfLikes* will be assigned a number, and *likeComment* will be a
function. If the component receives props that fail to satisfy these criteria,
it will raise a warning.

We can now use the pure component (named component) for unit tests like so:

{% highlight javascript %}
import React from 'react';
import {mount} from 'enzyme';
import {expect} from 'chai';
import sinon from 'sinon';

import {BlogComment} from './blog-comment';

describe('BlogComment', () => {
  it('should display comment body', () => {
    // This is where we create a mock state/props
    const props = {
      body: 'Nice post!',
      author: 'Tiffany Wu',
      numberOfLikes: 10,
      likeComment: () => {}
    };

    const wrapper = mount(<BlogComment {...props} />);
    const body = wrapper.find('.blog-comment__body');

    expect(body).to.have.text(props.body);
  });

  it('should dispatch action when clicking like', () => {
    const props = {
      body: 'Nice post!',
      author: 'Tiffany Wu',
      numberOfLikes: 10,
      likeComment: sinon.spy()
    };

    const wrapper = mount(<BlogComment {...props} />);

    wrapper.find('button').simulate('click');

    expect(props.likeComment.calledOnce).to.equal(true);
  });
});
{% endhighlight %}

The main thing to note here is that we've created an object called *props*
which simply contains all of the four props required by our component, and
we're explicitly passing them to the component by using the object spread
operator. This is our mock state, but since our base component is pure, it
behaves exactly the same way it would when receiving the state from a Redux
store.
