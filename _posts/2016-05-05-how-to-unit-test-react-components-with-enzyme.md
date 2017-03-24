---
layout: post
title: How to Unit Test React Components with Enzyme
permalink: /blog/how-to-unit-test-react-components-with-enzyme/
---
In this tutorial I'll show you how to set up a test suite for your React
application by leveraging
[Enzyme](http://airbnb.io/enzyme/),
[Mocha](https://mochajs.org/),
[Chai](http://chaijs.com/),
and [jsdom](https://github.com/tmpvar/jsdom).

First, let's install the tools:

(I'm assuming you've already installed React.)

{% highlight bash %}
$ npm install --save-dev enzyme mocha chai chai-enzyme chai-jsx jsdom babel babel-core
{% endhighlight %}

Create a bootstrap file with the following contents:

{% highlight javascript %}
// test/index.js

import chai from 'chai'
import chaiEnzyme from 'chai-enzyme'
import chaiJsx from 'chai-jsx'
import {jsdom} from 'jsdom'

chai.use(chaiEnzyme())
chai.use(chaiJsx)

global.document = jsdom('<!doctype html><html><body></body></html>')
global.window = document.defaultView
global.navigator = global.window.navigator
{% endhighlight %}

This will initialize your testing environment and create a virtual DOM where
the test runner will be able to mount your components. It will also decorate
Chai's assertion library to support JSX and Enzyme.

Next, let's add a `test` script to package.json:

{% highlight javascript %}
// package.json

{
  "scripts": {
    "test": "NODE_ENV=test mocha --compilers js:babel-core/register --require test/index.js \"./src/**/*.test.js\""
  }
}
{% endhighlight %}

Running this script will boot up Mocha, load the bootstrap file, and run any
test files in src that match the pattern `*.test.js*`.

Now let's create a new React component.

{% highlight javascript %}
// src/components/hello.js

import React, {Component} from 'react'

export class Hello extends Component {
  render() {
    return <p>Hello world.</p>
  }
}
{% endhighlight %}

...and an accompanying test file:

{% highlight javascript %}
// src/components/hello.test.js

import React from 'react'
import {render} from 'enzyme'
import {expect} from 'chai'

import {Hello} from './hello'

describe('Hello', () => {
  it('should render text', () => {
    const wrapper = render(<Hello />)

    expect(wrapper).to.have.text('Hello world.')
  })
})
{% endhighlight %}

Finally, let's run the test suite:

{% highlight bash %}
$ npm test
{% endhighlight %}

> If you have components that connect to a Redux store, you might also want to
> check out my other guide where I show you [how to disconnect a React
> component from a Redux store and unit test it separately](/blog/how-to-unit-test-react-redux-components/).
