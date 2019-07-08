# @chromaui/localtunnel

localtunnel exposes your localhost to the world for easy testing and sharing! No need to mess with DNS or deploy just to have others test out your changes.

Great for working with browser testing tools like browserling or external api callback services like twilio which require a public url for callbacks.

## installation

```
yarn add @chromaui/localtunnel
```

## API

The localtunnel client is also usable through an API (for test integration, automation, etc)

### localtunnel(port [,opts], fn)

Creates a new localtunnel to the specified local `port`. `fn` will be called once you have been assigned a public localtunnel url. `opts` can be used to request a specific `subdomain`.

```javascript
var localtunnel = require('@chromaui/localtunnel');

var tunnel = localtunnel(port, function(err, tunnel) {
    if (err) ...

    // the assigned public url for your tunnel
    // i.e. https://abcdefgjhij.localtunnel.me
    tunnel.url;
});

tunnel.on('close', function() {
    // tunnels are closed
});
```

### opts

- `subdomain` A _string_ value requesting a specific subdomain on the proxy server. **Note** You may not actually receive this name depending on availability.
- `local_host` Proxy to this hostname instead of `localhost`. This will also cause the `Host` header to be re-written to this value in proxied requests.

### Tunnel

The `tunnel` instance returned to your callback emits the following events

| event   | args | description                                                                          |
| ------- | ---- | ------------------------------------------------------------------------------------ |
| request | info | fires when a request is processed by the tunnel, contains _method_ and _path_ fields |
| error   | err  | fires when an error happens on the tunnel                                            |
| close   |      | fires when the tunnel has closed                                                     |

The `tunnel` instance has the following methods

| method | args | description      |
| ------ | ---- | ---------------- |
| close  |      | close the tunnel |

## other clients

Clients in other languages

_go_ [gotunnelme](https://github.com/NoahShen/gotunnelme)

_go_ [go-localtunnel](https://github.com/localtunnel/go-localtunnel)

## server

See [localtunnel/server](//github.com/localtunnel/server) for details on the server that powers localtunnel.

## License

MIT
