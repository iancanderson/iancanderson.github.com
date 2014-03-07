---
category: devblog
published: false
layout: post
---

They say that the best way to learn something is to teach it or write about it.  This is one of those attempts.  I'm a "professional" web developer.  I known how to write rails apps.  However, when it comes to understanding the basic plumbing of the web, I'm lacking.

Consider a form for posting a tweet:

<form action="/tweets" method="post">
  <input type="text" name="tweet_body" />
  <input type="submit" value="Tweet" disabled="disabled" />
</form>

Sure, I know how to create a form in html.  And I also know how to intercept the form data within the context of a web application, sanitize the user input, and even create a Tweet record in a database.  I know what you're thinking.  This guy IS a professional.

The glue in-between the html form and the rails app is what I'm currently curious about.

## 1.) The browser prepares the request
Say this is the form html:

  {% highlight html %}
  <form action="/tweets" method="post">
    <input type="text" name="tweet_body" />
    <input type="submit" value="Tweet" />
  </form>
  {% endhighlight %}

When a user clicks the tweet button, the names (from the name attribute) and values in the form are encoded by the browser into a single string.  This string will become the message body.

## 2.) The request is made

Once the browser encodes the form data, it makes an HTTP request to the server.
An HTTP request contains:
* A request line, in this case __POST /tweets HTTP/1.1__
* Headers
* An empty line
* A message body (optional)

## 3.) The server parses the request

The Rails router examines the format of the URL and delegates control to the appropriate controller.
Parameters built into the url or as part of a request body are parsed and set into the controller's 'params' method.

## 4.) Rails prepares a response

The controller action, as chosen by the Rails router, is executed.
(Usually) a template is rendered, which dynamically determines the response body.

## 5.) The browser receives the response

# HTTP methods and mime types
