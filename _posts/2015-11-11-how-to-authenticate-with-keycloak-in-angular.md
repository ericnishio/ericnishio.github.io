---
layout: post
title: How to Authenticate with Keycloak in Angular
permalink: /blog/how-to-authenticate-with-keycloak-in-angular/
---

Since the Keycloak.js library is in charge of handling authentication and
redirecting the user between Keycloak's login UI and your application, it
always needs to run first.

This is how Keycloak handles authentication:

1. Keycloak.js is loaded and run in your application.
2. Keycloak checks if the user is authenticated.
3. If not, it redirects the user to Keycloak's login interface.
4. On success, it redirects the user back to your application.

This happens on every page refresh so we need to handle authentication first
and only after that manually bootstrap Angular.

If you've previously "auto-bootstrapped" Angular in your index.html file with
`ng-app="yourApp"`, go ahead and remove the line.

Make sure you've loaded Keycloak's JavaScript library.

Then initialize Keycloak:

{% highlight javascript %}
angular.element(document).ready(() => {
  window._keycloak = Keycloak({
    // your Keycloak JSON configuration
  });

  window._keycloak
    .init({
      onLoad: 'login-required'
    })
    .success(() => {
      angular.bootstrap(document, ['yourApp']); // manually bootstrap Angular
    });
});
{% endhighlight %}

I'd also recommend you create a simple wrapper for the global `_keycloak`
variable to keep your code more modular and easier to refactor in the future:

{% highlight javascript %}
angular.module('yourApp').factory('keycloak', $window => {
  return $window._keycloak;
});
{% endhighlight %}

Now you can inject `keycloak` whenever you need to access your Keycloak state,
e.g. `keycloak.authenticated` or `keycloak.token`.

Example:

{% highlight javascript %}
angular.module('yourApp').controller('MyCtrl', ($scope, keycloak) => {
  $scope.isTokenExpired = keycloak.isTokenExpired;
});
{% endhighlight %}

{% highlight html %}
<div ng-controller="MyCtrl">
  <p ng-show="!isTokenExpired()">Your token is still valid.</p>
</div>
{% endhighlight %}
