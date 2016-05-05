---
layout: post
title: Set Up Jasmine and Karma for AngularJS
permalink: /blog/set-up-jasmine-and-karma-for-angularjs/
---

Globally install *karma-cli* on your computer:

{% highlight bash %}
$ sudo npm install -g karma-cli
{% endhighlight %}

Add *karma* and *karma-jasmine* to your project's dependencies.

{% highlight bash %}
$ npm install karma jasmine karma-jasmine --save-dev
{% endhighlight %}

Create your Karma configuration file:

{% highlight bash %}
$ karma init
{% endhighlight %}

When running init, you can mostly go with the suggested settings (by repeatedly
hitting enter). After the init script has completed, you should manually
append your project files to the `files` array in `karma.conf.js`, like so:

{% highlight javascript %}
files: [
  'bower_components/angular/angular.js',
  'bower_components/angular-mocks/angular-mocks.js',
  'js/app.js',
  'tests/*.js'
],
{% endhighlight %}

The above configuration assumes that your application depends on the Angular
core and that your main application logic resides in `js/app.js`, and that your
Jasmine unit tests are kept in the `tests/` directory. The `angular-mocks.js`
file provides some convenient mock services that will make unit testing on
Angular easier.

To test things out, create an example test file called `example.js` in the
`tests/` directory with the following contents:

{% highlight javascript %}
describe('example test', function() {
  it('should be true', function() {
    expect('foo').toBe('foo');
  });
});
{% endhighlight %}

When you're done, save the file, and run Karma:

{% highlight bash %}
$ karma start
{% endhighlight %}
