This is a modified version of itty.py which attempts to add support for the HTTP 'Accept:' request header.

example code:

::

  @get('/')
  @accept('application/x-plist')
  def index(request):
      return "here we would return a binary plist\n"
  
  @get('/')
  @accept('application/json')
  def index(request):
      return "here we would return JSON\n"
  
  @get('/')
  @accept('text/plain')
  def index(request):
      return "here we would return plain text\n"
  
  @get('/')
  def index(request):
      return "this is the default (returns text/html)\n"

output:

::

  $ wget -q -O - --header='Accept: application/x-plist' http://localhost:8080
  here we would return a binary plist
  $ wget -q -O - --header='Accept: application/json' http://localhost:8080
  here we would return JSON
  $ wget -q -O - --header='Accept: text/plain' http://localhost:8080
  here we would return plain text
  $ wget -q -O - --header='Accept: text/html' http://localhost:8080
  this is the default (returns text/html)
  $ wget -q -O - --header='Accept: */*' http://localhost:8080
  this is the default (returns text/html)
  $ wget -q -O - --header='Accept: some/junk' http://localhost:8080
  this is the default (returns text/html)

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