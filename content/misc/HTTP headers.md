---
tags:
  - http
---

HTTP headers contain additional information about the request or response and provide instructions or metadata for the communication between the client (such as a web browser) and the server.

## Main categories

There are two main categories: end-to-end headers and hop-by-hop headers.
These categories define how headers are treated and handled by intermediaries (such as proxies or caches) along the communication path between the client and the server.

**End-to-end headers** are intended to be transmitted to the ultimate recipient of the request or response. They must be forwarded by any intermediary along the way and are typically used to convey information that is relevant to the end-user or the final server. 
These headers are not removed or modified by intermediaries unless explicitly required.

**Hop-by-hop headers** are meaningful only for a single HTTP connection and are not forwarded by intermediaries to subsequent connections. Each intermediary (proxy, cache, or gateway) independently processes hop-by-hop headers for its own purposes. Hop-by-hop headers are used to manage the connection, control the behavior of intermediaries, or carry information specific to that particular connection. 
These headers are generally removed by intermediaries and not seen by the end recipient.

The RFC2616 defines the list of hop-by-hop headers : Connection, Keep-Alive, Proxy-Authenticate, Proxy-Authorization, TE, Trailer, Transfer-Encoding, Upgrade, Via, Warning

You can add other hop-by-hop headers with the `Connection` header.

There is a CVE related to the usage of Connection header : CVE-2022-1388

# Evolution with HTTP/2 and HTTP/3

HTTP/2 introduced significant changes to the underlying protocol, including the framing layer, multiplexing, and header compression. In HTTP/2, the concept of hop-by-hop headers is not explicitly defined as it was in HTTP/1.1. 
Instead, HTTP/2 uses a binary framing layer that allows headers to be sent as a part of the initial request/response and subsequently compressed and multiplexed over a single connection. 
The framing layer handles the management and processing of headers, eliminating the need for explicit hop-by-hop headers.


#quartz 