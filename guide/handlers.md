Handlers
========

Purpose
-------

Handlers are Erlang modules that represent a resource.

Handlers must process the request and send a reply. The nature of the
reply will vary between handlers.

Different kinds of handlers can be combined in a single module. This
allows a module to handle both websocket and long-polling code in a
single place, for example.

Protocol upgrades
-----------------

Cowboy features many different handlers: HTTP handlers, loop handlers,
websocket handlers, REST handlers and static handlers. All of them
have a common entry point: the `init/3` function.

By default, Cowboy considers your handler to be an HTTP handler.

To switch to a different protocol, like, for example, Websocket,
you must perform a protocol upgrade. This is done by returning
a protocol upgrade tuple at the end of `init/3`.

The following snippet upgrades the handler to `my_protocol`.

``` erlang
init(_Any, _Req, _Opts) ->
    {upgrade, protocol, my_protocol}.
```

The `my_protocol` module will be used for further processing of the
request. It requires only one callback, `upgrade/4`.

@todo Describe `upgrade/4` when the middleware code gets pushed.
