---
layout: post
title: Compile LESS Files with Grunt
permalink: /blog/compile-less-files-with-grunt/
---

Grunt is a Node task runner that can be configured to detect file changes and
subsequently perform user-defined operations. By leveraging these features,
we can have Grunt compile LESS files into CSS automatically.

## Step 1: Install Node.js

[Download a Node installer](http://nodejs.org/download/) and run it.
Installation packages are available for Mac, Windows, Linux, and SunOS.
Alternatively, you can compile and install it from source.

## Step 2: Install Grunt

Globally install Grunt using the Node package manager:

```
$ npm install -g grunt-cli
```

## Step 3: Create a Gruntfile.js

Now create a file called *Gruntfile.js* in your project directory.

Then copy and paste in the example configuration shown just below this
paragraph. You'll just need to change the (commented) lines that define
which files Grunt should keep an eye on, as well as the source and destination
paths to the LESS and CSS files.

Example:

{% highlight javascript %}
module.exports = function(grunt) {
  require('jit-grunt')(grunt);

  grunt.initConfig({
    less: {
      development: {
        options: {
          compress: true,
          yuicompress: true,
          optimization: 2
        },
        files: {
          "css/main.css": "less/main.less" // destination file and source file
        }
      }
    },
    watch: {
      styles: {
        files: ['less/**/*.less'], // which files to watch
        tasks: ['less'],
        options: {
          nospawn: true
        }
      }
    }
  });

  grunt.registerTask('default', ['less', 'watch']);
};
{% endhighlight %}

Note that providing `/**/*` in the watch path will watch files recursively
under that directory.

## Step 4: Configure the package file

If you do not have an existing *package.json* file in your project directory,
create one:

```
$ cd YOUR_PROJECT_DIRECTORY
$ npm init
```

Once you have a valid *package.json* file, execute:

```
npm install grunt grunt-contrib-less grunt-contrib-watch jit-grunt --save-dev
```

This will install the required packages and add them to package.json.

## Step 5: Start Grunt

```
$ grunt
```

While Grunt is running, it will compile your stylesheets every time you commit
changes to one of your LESS files. Go ahead and give it a try.

As you keep configuring more tasks, your Gruntfile.js can easily grow into an
unmanageable beast so I suggest you also take a look at [how to split your
Gruntfile.js into bite-sized pieces]
(http://ericnish.io/blog/how-to-neatly-separate-grunt-files/)
while you still can.
