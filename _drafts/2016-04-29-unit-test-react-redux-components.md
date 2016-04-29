---
layout: post
title: How to Unit Test React Redux Components
permalink: /blog/how-to-unit-test-react-redux-components/
---

The cleanest way to unit test a React component is to create a pure
component whose entire state is passed to it as props. This allows
you to test the component in isolation without having to first set
up the entire application state.

First, let's create our pure component.

{% highlight javascript %}
import React, {Component} from 'react';
import {bindActionCreators} from 'redux';
import {connect} from 'react-redux';

import {likeComment} from './redux-actions';

export class BlogComment extends Component {
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

export default connect(mapStateToProps, mapDispatchToProps)(BlogComment);
{% endhighlight %}

The key point here is that we're exported two things in this module: the
Redux-connected component as a default export **and** the base component as
a named export.

The only difference between these two exports is that the Redux-connected
component is decorated to receive its props through Redux, whereas the base
component only assumes that it will somehow receive the props.

Since we are specifically unit testing a component and making sure it works
correctly, we do not need to care as to where it gets its state from as long as it
always receives it as props.

This makes it very easy to mock the state in unit tests since we can simulate
various states and actions merely by passing our own fake versions as props.

So we can use the Redux-connected component (default export) within the
application itself and load up the pure version (named export) for unit tests,
like so:

{% highlight javascript %}
import React from 'react';
import {mount} from 'enzyme';
import {expect} from 'chai';
import sinon from 'sinon';

import {BlogComment} from './blog-comment';

describe('BlogComment', () => {
  it('should display body', () => {
    const props = {
      body: 'Nice post!',
      author: 'Tiffany Wu',
      numberOfLikes: 10,
      likeComment: () => {}
    };

    const wrapper = mount(<BlogComment ...props />);
    const body = wrapper.find('.blog-comment__body');

    expect(body).to.have.text(true);
  });

  it('should dispatch action when clicking like', () => {
    const props = {
      body: 'Nice post!',
      author: 'Tiffany Wu',
      numberOfLikes: 10,
      likeComment: sinon.spy()
    };

    const wrapper = mount(<BlogComment ...props />);

    wrapper.find('button').simulate('click');

    expect(props.likeComment.calledOnce).to.equal(true);
  });
});
{% endhighlight %}
