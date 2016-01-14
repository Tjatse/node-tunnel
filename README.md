# node-tunnel - HTTP/HTTPS Agents for tunneling proxies
[![Build Status](https://travis-ci.org/Tjatse/node-tunnel.svg)](https://travis-ci.org/Tjatse/node-tunnel) [![NPM version](https://badge.fury.io/js/node-tunnel.svg)](http://badge.fury.io/js/node-tunnel)
## Example

```javascript
var tunnel = require('tunnel2');

var tunnelingAgent = tunnel.httpsOverHttp({
  proxy: {
    host: 'localhost',
    port: 3128
  }
});

var req = https.request({
  host: 'example.com',
  port: 443,
  agent: tunnelingAgent
});
```

## Installation

    $ npm install tunnel2

## Usages

### HTTP over HTTP tunneling

```javascript
var tunnelingAgent = tunnel.httpOverHttp({
  maxSockets: poolSize, // Defaults to 5

  proxy: { // Proxy settings
    host: proxyHost, // Defaults to 'localhost'
    port: proxyPort, // Defaults to 80
    localAddress: localAddress, // Local interface if necessary

    // Basic authorization for proxy server if necessary
    proxyAuth: 'user:password',

    // Header fields for proxy server if necessary
    headers: {
      'User-Agent': 'Node'
    }
  }
});

var req = http.request({
  host: 'example.com',
  port: 80,
  agent: tunnelingAgent
});
```

### HTTPS over HTTP tunneling

```javascript
var tunnelingAgent = tunnel.httpsOverHttp({
  maxSockets: poolSize, // Defaults to 5

  // CA for origin server if necessary
  ca: [ fs.readFileSync('origin-server-ca.pem')],

  // Client certification for origin server if necessary
  key: fs.readFileSync('origin-server-key.pem'),
  cert: fs.readFileSync('origin-server-cert.pem'),

  proxy: { // Proxy settings
    host: proxyHost, // Defaults to 'localhost'
    port: proxyPort, // Defaults to 80
    localAddress: localAddress, // Local interface if necessary

    // Basic authorization for proxy server if necessary
    proxyAuth: 'user:password',

    // Header fields for proxy server if necessary
    headers: {
      'User-Agent': 'Node'
    },
  }
});

var req = https.request({
  host: 'example.com',
  port: 443,
  agent: tunnelingAgent
});
```

### HTTP over HTTPS tunneling

```javascript
var tunnelingAgent = tunnel.httpOverHttps({
  maxSockets: poolSize, // Defaults to 5

  proxy: { // Proxy settings
    host: proxyHost, // Defaults to 'localhost'
    port: proxyPort, // Defaults to 443
    localAddress: localAddress, // Local interface if necessary

    // Basic authorization for proxy server if necessary
    proxyAuth: 'user:password',

    // Header fields for proxy server if necessary
    headers: {
      'User-Agent': 'Node'
    },

    // CA for proxy server if necessary
    ca: [ fs.readFileSync('origin-server-ca.pem')],

    // Server name for verification if necessary
    servername: 'example.com',

    // Client certification for proxy server if necessary
    key: fs.readFileSync('origin-server-key.pem'),
    cert: fs.readFileSync('origin-server-cert.pem'),
  }
});

var req = http.request({
  host: 'example.com',
  port: 80,
  agent: tunnelingAgent
});
```

### HTTPS over HTTPS tunneling

```javascript
var tunnelingAgent = tunnel.httpsOverHttps({
  maxSockets: poolSize, // Defaults to 5

  // CA for origin server if necessary
  ca: [ fs.readFileSync('origin-server-ca.pem')],

  // Client certification for origin server if necessary
  key: fs.readFileSync('origin-server-key.pem'),
  cert: fs.readFileSync('origin-server-cert.pem'),

  proxy: { // Proxy settings
    host: proxyHost, // Defaults to 'localhost'
    port: proxyPort, // Defaults to 443
    localAddress: localAddress, // Local interface if necessary

    // Basic authorization for proxy server if necessary
    proxyAuth: 'user:password',

    // Header fields for proxy server if necessary
    headers: {
      'User-Agent': 'Node'
    }

    // CA for proxy server if necessary
    ca: [ fs.readFileSync('origin-server-ca.pem')],

    // Server name for verification if necessary
    servername: 'example.com',

    // Client certification for proxy server if necessary
    key: fs.readFileSync('origin-server-key.pem'),
    cert: fs.readFileSync('origin-server-cert.pem'),
  }
});

var req = https.request({
  host: 'example.com',
  port: 443,
  agent: tunnelingAgent
});
```

## License

This module is released under the [MIT License](http://www.opensource.org/licenses/mit-license.php).
