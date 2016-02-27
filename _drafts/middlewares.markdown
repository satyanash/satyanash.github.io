---
layout: post
title: "Middlewares"
---

A **Middleware** is somewhat ambiguous term that means different things to different people. This article hopes to show how middlewares are implemented in different languages and their frameworks.

* According to Wikipedia, Middlewares are defined as: *computer software that provides services to software applications beyond those available from the operating system.* 
* Java enterprise middlewares are integration layers that provide reusable abstracted access to combinations of data sources which can then be consumed by the business logic.
* In most popular modern web development frameworks, a Middleware is a *hook* into the request-response cycle allowing the execution of a common piece of code before/after a request is processed.

We'll see what **Middleware** means in commonly used languages and platforms for web development and how they can be implemented in other languages.

## Rack Middlewares

Rack is a widely used interface between webservers and Ruby frameworks.
A Rack Middleware here is simply a piece of code that processes each and every incoming request before calling the next middleware in the *rack* to do it's job.
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

You can find further [details here](http://www.rubydoc.info/github/rack/rack/master/file/README.rdoc)

## Django Middlewares

Django is one of the most popular Python frameworks for web development.
As per Django's official documentation: *Middleware is a framework of hooks into Django’s request/response processing. It’s a light, low-level “plugin” system for globally altering Django’s input or output.*

Django allows you to define Middlewares by duck-typing a class with specific well-documented methods.
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

You can find further [details here](https://docs.djangoproject.com/en/1.9/topics/http/middleware/)

## Java EE Filters

Analogous functionality to Python and Ruby Middlewares is achieved through the use of Filters as specified in the Java Servlet 2.3 specification (2001).

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
It is also similar to the Rack and Django middlewares in that you can *hook* into the request/response cycle.
In addition: it also supports application and router level separation of middlewares, which is not easily doable with Rack or Django.
You can also mount middlewares onto specific routes, while ignoring other ones without having to write code manually for checking each route.

Here is a sample route for timing a request:

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

You can find further [details here](http://expressjs.com/en/guide/using-middleware.html).

## Golang Middlewares with Negroni

Negroni is a small library that allows you to implement Middleware functionality with minimal code.

