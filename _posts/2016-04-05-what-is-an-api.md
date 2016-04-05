---
layout: post
title: What is an API?
permalink: /blog/what-is-an-api/
---

*API* is a nebulous term for rookies. The expression used everywhere but its
definition appears to differ in various contexts. People talk about public
APIs, RESTful APIs, email APIs, or the Java API.

An API is essentially just a set of controls you can interact with. It can
literally be anything that can be interacted with.

To put it in a more familiar context, a car‘s dashboard could be seen as an
API. You are given a set of controls that you can use to achieve various
effects, like rotating the steering wheel clockwise to turn the front wheels
toward the right.

When you write a function for a computer program, you are also creating or
*exposing* an API. The function is a piece of code that can be interacted
with:

```js
function steer(degrees) {
  // Logic for steering the car
}
```

Interaction takes place when we call the function:

```js
steer(-90);
```

When we make an API call, we are asking the API to perform an operation for
us. In essence, we’re delegating that operation to a specific part of the
program that is capable of handling and carrying out the request.

As long as we know what the API does and what it needs, we don’t necessarily
need to study what the API does behind the scenes.

You, as the driver, only need to know that turning the steering wheel will
change the car’s direction provided that it’s in motion. You don’t need to know
how the engine works or what mechanics are involved under the hood.

Say, you want to use a third-party email delivery service like
[SendGrid](https://sendgrid.com) for dispatching registration emails for your
Node.js application. SendGrid provides a Node.js library that acts as an
API between the email service and your application. This means that you only
need to know how to format your message and which function to call:

```js
const sendgrid = require('sendgrid')('abc123');

sendgrid.send({
  subject: 'Your account has been created!',
  from: 'noreply@example.com',
  fromname: 'MyService',
  replyto: 'noreply@example.com',
  to: 'you@example.com',
  text: 'Please sign in to start using the service.'
});
```

As you can see, the API call is very minimal and does not contain any logic.
The actual logic has been abstracted out by SendGrid’s API which means that
you as the application developer can delegate the delivery job to the
service by only providing the essential data. This also makes switching APIs
easy by merely adjusting the API call.
