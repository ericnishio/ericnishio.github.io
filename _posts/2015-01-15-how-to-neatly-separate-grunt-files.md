---
layout: post
title: How to Neatly Separate Grunt Files
permalink: /blog/how-to-neatly-separate-grunt-files/
---

I recently had a Gruntfile.js containing more than 500 lines of configuration
code. It had grown to a point where I was reluctant to even open the file, let
alone make any further modifications to it—a clear indication that the code had
long lost its maintainability.

Now, after splitting the bad boy into separate modules, I'm able to
effortlessly inspect clearly presented config files without having to scan and
shuttle between disjointed code segments in a single file.

In this tutorial I'll share with you the minimal approach I took to tidy up my
Grunt setup.

## Get the Plugins

Let's start off by installing two killer plugins that allow us to load custom
tasks and configurations from multiple source files.

And by the way, jit-grunt is also a great performance booster that eliminates
all `grunt.loadNpmTasks()` statements.

{% highlight bash %}
$ npm install jit-grunt load-grunt-config --save-dev
{% endhighlight %}

## Directory Structure

You may choose to lay out your directories and files differently, but the
examples in this tutorial assume that you follow this structure:

{% highlight bash %}
.
├── grunt
│   ├── config
│   │   └── watch.js
│   └── tasks
│       └── default.js
└── Gruntfile.js
{% endhighlight %}

## Gruntfile.js

{% highlight javascript %}
// Gruntfile.js

module.exports = function(grunt) {
  var path = require('path');

  require('load-grunt-config')(grunt, {
    configPath: path.join(process.cwd(), 'grunt/config'),
    jitGrunt: {
      customTasksDir: 'grunt/tasks'
    },
    data: {
      foo: 'bar' // accessible with '<%= foo %>'
    }
  });
};
{% endhighlight %}

Gruntfile.js should remain minimal.

The load-grunt-config plugin allows you to define variables in the `data`
object, which you can later access by using the `<%= foo %>` notation. But I
would advise against abusing it because you will want to keep your config files
independent. Note that you can reference package.json with `<%= package %>` out
of the box.

The overarching goal is to minimize Gruntfile.js and keep your task-specific
configurations in the `grunt/config` directory, and custom tasks under
`grunt/tasks`.

## Configs

Now let's create a configuration file for a task called `watch` (which you
should be familiar with).

{% highlight javascript %}
// grunt/config/watch.js

module.exports = {
  sass: {
    files: ['sass/**/*.{sass,scss,css}'],
    tasks: ['sass']
  }
};
{% endhighlight %}

Essentially, watch.js is just a simple Node module that contains the
configuration object Grunt will use for a task called `watch`. It's important
to note that you must always name your configuration files after the
corresponding Grunt task, verbatim. So a config file for an `ngAnnotate` task
should be named `ngAnnotate.js`.

Since the code is just a plain Grunt configuration object, you can simply copy
and paste all your existing task configs into their own module files.
Everything should still work without further refactoring, assuming that your
config files do not reference any variables that were previously declared in
Gruntfile.js. Such variables should be moved to the `data` object mentioned
earlier, and references replaced with `<%= propertyName %>`.

## Custom Tasks

Finally, let's create a custom default task. Similar to config files, a custom
task file is a module that exports a task. But instead of exposing an object,
it exports a function containing `grunt` as an argument.

{% highlight javascript %}
// grunt/tasks/default.js

module.exports = function(grunt) {
  grunt.registerTask('default', ['sass', 'watch']);
};
{% endhighlight %}

Again, you can just simply copy and insert any existing tasks into these
exported functions, which will then be automatically handled by jit-grunt.

I'm hoping to hear your thoughts on how to further improve the setup. Let me
know in the comment section below. Thanks!
