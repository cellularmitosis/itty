This is a modified version of itty.py which attempts to add support for the HTTP 'Accept:' request header.

example code:

::

  @get('/')
  @accept('text/plain')
  def index(request):
      return "Hello, World!\n"
  
  @get('/')
  @accept('text/xml')
  def index(request):
      return '<?xml version="1.0"?><greeting>Hello, World!</greeting>\n'
  
  @get('/')
  @accept('application/json')
  def index(request):
      return '{ "greeting": "Hello, World!" }\n'
  
  @get('/')
  def index(request):
      return "<html><body>Hello, World!</body></html>\n"


output:

::

  $ wget -q -O - --header='Accept: text/plain' http://localhost:8080
  Hello, World!
  
  $ wget -q -O - --header='Accept: text/xml' http://localhost:8080
  <?xml version="1.0"?><greeting>Hello, World!</greeting>
  
  $ wget -q -O - --header='Accept: application/json' http://localhost:8080
  { "greeting": "Hello, World!" }
  
  $ wget -q -O - --header='Accept: text/html' http://localhost:8080
  <html><body>Hello, World!</body></html>


This is just a first stab to flesh out the idea.

Limitations (i.e. things which could be improved upon):

* You have to define your methods in order from most specific to least specific.
* Wildcards and 'q' aren't supported yet.

Feel free to take this idea and run with it.  Have fun!
Jason Pepas
jason@pepas.com


=======
itty.py
=======

The itty-bitty Python web framework.

``itty.py`` is a little experiment, an attempt at a Sinatra_ influenced
micro-framework that does just enough to be useful and nothing more.

Currently supports:

* Routing
* Basic responses
* Content-types
* HTTP Status codes
* URL Parameters
* Basic GET/POST/PUT/DELETE support
* User-definable error handlers
* Redirect support
* File uploads
* Header support
* Static media serving

Beware! If you're looking for a proven, enterprise-ready framework, you're in
the wrong place. But it sure is a lot of fun.

.. _Sinatra: http://sinatrarb.com/


Example
=======

::

  from itty import get, run_itty
  
  @get('/')
  def index(request):
      return 'Hello World!'
  
  run_itty()

See ``examples/`` for more usages.


Other Sources
=============

A couple of bits have been borrowed from other sources:

* Django

  * HTTP_MAPPINGS

* Armin Ronacher's blog (http://lucumr.pocoo.org/2007/5/21/getting-started-with-wsgi)

  * How to get started with WSGI


Thanks
======

Thanks go out to Matt Croydon & Christian Metts for putting me up to this late
at night. The joking around has become reality. :)