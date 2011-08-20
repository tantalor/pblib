pblib
=====

A simple library that implements a pingback client.  The library supports
version 1.0 of the pingback library, based upon the specification published
at http://www.hixie.ch/specs/pingback/pingback.

Pingback can now be implemented by using one of the following functions:

    def autoPingback(sourceURI, reST = None, HTML = None):
        """Scans the input text, which can be in either reStructuredText or HTML
        format, pings every linked website for auto-discovery-capable pingback
        servers, and does an appropriate pingback."""

    def pingback(sourceURI, targetURI):
        """Attempts to notify the server of targetURI that sourceURI refers to
        it."""
        ...

Implementing a pingback server is beyond the scope of this library simply
because of the very application-specific nature of a server.  However, it is
also trivially easy to create a pingback server by using Python's
SimpleXMLRPCServer module.  The following simple framework could be used
by a CGI script to implement a pingback server:

    def pingback(sourceURI, targetURI):
        '''Do something interesting!'''
        return "arbitrary string return value."

    import SimpleXMLRPCServer
    handler = SimpleXMLRPCServer.CGIXMLRPCRequestHandler()
    handler.register_function(pingback, "pingback.ping")
    handler.handle_request()

It would still be necessary to provide an X-Pingback HTTP header which pointed
at the given CGI script.

License
-------

Copyright (c) 2003, Mathieu Fenniak
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are
met:

* Redistributions of source code must retain the above copyright notice,
this list of conditions and the following disclaimer.
* Redistributions in binary form must reproduce the above copyright notice,
this list of conditions and the following disclaimer in the documentation
and/or other materials provided with the distribution.
* The name of the author may not be used to endorse or promote products
derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE
LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
POSSIBILITY OF SUCH DAMAGE.
