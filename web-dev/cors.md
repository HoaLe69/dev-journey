# What is it?

[MDN - Cross-origin resource sharing](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CORS)

CORS is a browser security mechanism that prevents malicious requests from loading resource
from different origin (scheme (https/ http), domain, port). It's an HTTP-header based.
It just happens on the browsers.

## How it works?

It works by adding new `HTTP` header that let servers decided to 
which origins are permitted to read that information from a web server.

Additionally, for some requests that cause effect on server data such as `DELETE`, or requests
include custom header. The browser will initially send a `preflight` request in order to check
that the server will permit the actual request.

## Headers ??

`Access-Control-Allow-Origin` : http://localhost:8000
`Access-Control-Allow-Methods` : POST, PUT, DELETE, ...
`Access-Control-Allow-Headers`: Content-type
`Access-Control-Max-Age` : 86400 (seconds) (for caching), good for performance

## What request use CORS?

- Invocations of `fetch()` or `XMLHttpRequest`.
- Web font
- WebGL textures
- Images/Video frames drawn to a canvas using `drawImage()`
- CSS shapes from images

## Alternative CORS?

- Here is the architecture where I don't use CORS.

There is a Nginx server between client and server.
And Nginx server will same `origin` as `client`.
Because the CORS issue doesn't happen for same origin and just on the client side.

```MDN
Client(https://example.com) -----> Nginx(https://example.com/hello) ----> Backend 
```

**Some downsides**

- You now have to manage Nginx config.
- There is a bit latency because the request has to pass through an extra layer.

## Questions

1. Why does it only happen on the browsers not testing tools like postman?

- It's client side security feature, not server or api itself. It prevents 
malicious site from using your credentials to make a secret, unauthorized request to your
server

For example: A malicious site successfully get your cookies, and then they send a request
to server and when the request back to browser, it will be block by browser. And they not be able
to see it.
