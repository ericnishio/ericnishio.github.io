---
layout: post
title: Automatic created_at & modified_at with Angular and Firebase
permalink: /blog/automatic-created-at-and-modified-at-with-angular-and-firebase/
---

Instead of "manually" updating a record's created_at and modified_at timestamps inside multiple controller methods, we can more conveniently override the *$firebaseObject.$save()* and *$firebaseArray.$add()* methods which will automatically handle these timestamp properties for every record.

For this, you will need to have the [AngularFire](https://github.com/firebase/angularfire) library installed.

Then just decorate AngularFire's *$firebaseArray* and *$firebaseObject* factories like so:

## created_at

{% highlight javascript %}
angular.module('YOUR_MODULE').config(function($provide) {
  $provide.decorator('$firebaseArray', function($delegate, $window) {
    var add = $delegate.prototype.$add;

    $delegate.prototype.$add = function(newData) {
      newData.created_at = $window.Firebase.ServerValue.TIMESTAMP;
      return add.call(this, newData);
    };

    return $delegate;
  });
});
{% endhighlight %}

The above code will add a *created_at* property to all new records before creating and appending them to a collection with $firebaseArray.$add().

## modified_at

{% highlight javascript %}
angular.module('YOUR_MODULE').config(function($provide) {
  $provide.decorator('$firebaseObject', function($delegate, $window) {
    var save = $delegate.prototype.$save;

    $delegate.prototype.$save = function() {
      this.modified_at = $window.Firebase.ServerValue.TIMESTAMP;
      return save.call(this);
    };

    return $delegate;
  });
});
{% endhighlight %}

This decorator will update the *modified_at* property before calling $firebaseObject.$save().

It's important to note that Firebase provides a canonical timestamp value via *Firebase.ServerValue.TIMESTAMP*, so make sure to always use it instead of the browser's local timestamp.
