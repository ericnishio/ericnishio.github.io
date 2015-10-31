---
layout: post
title: How to Add .success() and .error() to Angular Promises
permalink: /blog/add-success-and-error-to-angular-promises/
---

When it comes to asynchronous JavaScript and promises, I prefer .success() and .error() to the default .then() syntax. But you may have noticed that even though Angular does sometimes expose these helper methods, the $q service (which is Angular's de-facto API for writing promises) does not provide these methods for you out of the box. If you wish to use them in your own functions, you'll have to supply the syntactical sugar yourself.

## promiseFactory.js

First let's create a factory that will be responsible for creating deferred objects and for adding the .success() and .error() methods to promises. The following block of code is the bread and butter of this tutorial.

{% highlight javascript %}
angular.module('App').factory('promiseFactory', function($q) {
  return {
    decorate: function(promise) {
      promise.success = function(callback) {
        promise.then(callback);
        return promise;
      };
      promise.error = function(callback) {
        promise.then(null, callback);
        return promise;
      };
    },
    defer: function() {
      var deferred = $q.defer();
      this.decorate(deferred.promise);
      return deferred;
    }
  };
});
{% endhighlight %}

Now, instead of calling $q.defer(), you can use *promiseFactory.defer()* to create a deferred object that comes decorated with the .success() and .error() methods we wrote earlier.

## Example

We will inject our *promiseFactory* into a hypothetical authManager factory whose role is to handle user authentication. We will then create an asynchronous login() function that allows users to sign in using the $http service.

The .success() and .error() methods will come in handy later when we want to neatly separate logic for successful login events as well as failed attempts when calling the function from a controller.

{% highlight javascript %}
angular.module('App').factory('authManager', function($http, promiseFactory) {
  return {
    login: function(username, password) {
      var dfd = promiseFactory.defer();
      $http.post('/api/login', {username: username, password: password})
        .then(function(res) {
          dfd.resolve(res);
        }, function(err) {
          dfd.reject(err);
        });
      return dfd.promise;
    }
  };
});
{% endhighlight %}

We can now make use of the .success() and .error() methods in our login controller.

{% highlight javascript %}
angular.module('App').controller('LoginCtrl', function($scope, authManager) {
  $scope.login = function() {
    authManager.login($scope.username, $scope.password)
      .success(function(res) {
        sessionStorage.setItem('authToken', res.authToken);
      })
      .error(function(err) {
        $scope.error = err;
      });
  };
});
{% endhighlight %}
