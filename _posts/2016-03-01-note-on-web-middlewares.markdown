---
layout: post
title: "A Note on Web Middlewares"
date: 2016-03-01T14:21:53+05:30
tags: software
---

The word **Middleware** is an ambiguous term that means different things to different people.
We'll try to find out what 'Middleware' means in commonly used frameworks and platforms for web development and how they are implemented.

* According to Wikipedia, middlewares are defined as: *computer software that provides services to software applications beyond those available from the operating system.* 
* Enterprisy definitions for the word 'Middleware' are scattered across the web, each more vague than the previous.
* In most popular modern web development frameworks, a middleware is a *hook* into the HTTP request-response cycle allowing the execution of a common piece of code before/after a request is processed.

Do note that the code samples are intended only for implementation comparison in various languages.
They may not be ideal for production use and may skirt some best practices.

## Rack Middlewares

Rack is a widely used interface between webservers and Ruby frameworks.
A [Rack middleware](http://www.rubydoc.info/github/rack/rack/master/file/README.rdoc) here is simply a piece of code that processes each and every incoming request before calling the next middleware in the *rack* to do it's job.
Once all middlewares are processed, the final response is returned to the webserver.
In the case of multiple middlewares, they are processed in the order they are added to the rack.

Here is a sample Rack middleware that times the request:

~~~ ruby
class TimerRackMiddleware
  def initialize(app)
    @app = app
  end

  def call(env)
    @start = Time.now
    @status, @headers, @body = @app.call(env)
    @duration = ((Time.now - @start).to_f * 1000).round(2)

    puts "#{env['REQUEST_METHOD']} #{env['REQUEST_PATH']} - Took: #{@duration} ms"
    [@status, @headers, @body]
  end
end
~~~

So in this middleware, the start point is taken, then the actual call to the Server is made with `@app.call(env)`, then the logger outputs the logging entry and finally returns the response as `[@status, @headers, @body]`

## Django Middlewares

Django is one of the most popular Python frameworks for web development.
As per Django's [official documentation](https://docs.djangoproject.com/en/1.9/topics/http/middleware/): *Middleware is a framework of hooks into Django’s request/response processing. It’s a light, low-level “plugin” system for globally altering Django’s input or output.*

Django allows you to define middlewares by duck-typing a class with specific well-documented methods.
Here is a sample Django middleware class that times the request:

~~~ python
class TimerMiddleware(object):
    def process_request(self, request):
        request._request_time = datetime.now()
 
    def process_template_response(self, request, response):
        response_time = request._request_time - datetime.now()
        response.context_data['response_time'] = abs(response_time)
	print("{} {} - Took: {} ms".format(request.method, request.path, abs(response_time)))
        return response
~~~

Here, the `process_request()` method is called for each request, before Django decides which view to execute.
On the other hand, `process_template_response()` is called just after the view has finished executing, which prints the timer information.

## Java EE Filters

Analogous functionality to Django and Rack middlewares is achieved through the use of Filters as specified in the [Java Servlet 2.3 specification](http://www.javaworld.com/article/2074918/java-web-development/servlet-2-3--new-features-exposed.html) (2001).

Here is a sample `Filter` implementation that times the request:

~~~ java
public class TimerFilter implements Filter {

  public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
      throws ServletException, IOException {
    long startTime = System.currentTimeMillis();
    chain.doFilter(request, response);
    long elapsed = System.currentTimeMillis() - startTime;

    if (request instanceof HttpServletRequest) {
      String name = ((HttpServletRequest) request).getRequestURI();
      String method = ((HttpServletRequest) request).getMethod();

      System.out.println(method + " " + method + " - Took: " + elapsed + " ms");
    }
  }
}
~~~

In this filter, the `chain.doFilter(request,response)` calls the next filter in the chain and waits for it to be processed.
Once the request is processed, the response is generated and the filter returns.


## Express Middlewares

Express is a web development framework for the Node.js platform.
[Middlewares in Express](http://expressjs.com/en/guide/using-middleware.html) are similar to the Rack and Django middlewares in that you can *hook* into the request/response cycle.

In addition: it also supports application and router level separation of middlewares, which is not easily doable with Rack or Django.
You can also mount middlewares onto specific routes, while ignoring other ones without having to write code manually for checking each route.

Here is a sample application level route for timing a request:

~~~ javascript
var app = Express();

app.use(function(req, res, next) {
    var start = Date.now();
    res.on('finish', function() {
        var duration = Date.now() - start;
	console.log("%s %s - Took: %s ms", req.method, req.path, duration);
    });
    next();
});
~~~

Here the call to `next()` passes the control to the next middleware function in this stack.

## Naming Concerns


The Java world is the only one that calls this function a 'Filter'. This is probably because it was one of the first specs to come up with this kind of feature.

Interestingly, the [Introductory blog for Rack](http://chneukirchen.org/blog/archive/2007/02/introducing-rack.html) (2007) by Christian Neukichen actually calls them filters, but also mentions the term middleware.

The origin of the term middleware in the context of the web seems to have come from the [WSGI spec](https://en.wikipedia.org/wiki/Web_Server_Gateway_Interface#Specification_overview) where it used for pieces of code that implement both ends of the API.

# So now what? 

Wanting to run common pieces of code before and after handling an HTTP request seems to be the most common definition for 'Middleware'.

These naming inconsistencies resulted in some confusion for me, especially when switching between multiple languages.
This blog post should serve as an online record of the naming problem.
