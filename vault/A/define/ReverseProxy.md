# ReverseProxies

In a common [[NetworkProxy]], the server ends up not knowing the originating client. We can, however, invert this situation, making #client unaware of the destination #server.

This has several use cases, many prevalent in [[SoftwareMicroservices]] and [[SystemsDistributed]] architectures, such as:

* [[Caching]]
* [[LoadBalancer]]
* [[Ingress]]
* Canary [[IndexSoftwareDeploy]]
* Ingress:
  * Hey, you talk to me sir,  and if you wanna access the pictures API, I can route requests.

As a reverse proxy, when receiving a [[ProtocolTLS]] handshake #request, we can choose to act in several ways.

The first one is to respond to the client with the proxy's own [[TLSCertificate]] and TLS Parameters. This is called [[TLSTermination]]. This necessitates, however, that the Private[[EncryptionKey]] and certificate be in the reverse proxy. This raises major concerns:

* The proxy has the ability to #decode the underlying contents
* The proxy can act as a representative of the certificate holder.

We can circumvent such concerns by making the reverse proxy #transparently forward the TLS request without decrypting its content. This makes it operate just like a [[ModelOSI]] #Layer4 proxy

> This is called [[TLSPassthrough]].

It can continue routing #encrypted requests by means of [[ServerNameIndication]]

A #Layer7 proxy needs to understand the request, making it incapable of forwarding the #packets as they come. It has to receive and acknowledge each one, and internally assemble the request to do its decisions.

It can, afterward, establish a [[ProtocolTCP]] request to the downstream server and send the packets.

* It is very common to `tamper` with the requests when doing this, e.g add requests #headers

* Since it is operating at Layer 7 via [[ProtocolHTTP]] - a stateless #protocol - it is very possible that further requests establish a new TCP connection with the same server or even other servers.

```mermaid

sequenceDiagram
    Client->>Proxy: Request Packet 1
    Client->>Proxy: Request Packet 2
    Client->>Proxy: Request Packet 3
    Client->>Proxy: Request Packet 4
    Client->>Proxy: Request Packet 5    
    Proxy->>Server: Request Packet 1
    Proxy->>Server: Request Packet 2
    Proxy->>Server: Request Packet 3
    Proxy->>Server: Request Packet 4
    Proxy->>Server: Request Packet 5
    Note right of Server: Processing
    Server->>Proxy: Response Packet 1
    Server->>Proxy: Response Packet 2
    Server->>Proxy: Response Packet 3    
    Proxy->>Client: Response Packet 1
    Proxy->>Client: Response Packet 2
    Proxy->>Client: Response Packet 3
```

A Layer 4 proxy doesn't need to wait to assemble the whole request:  it can immediately send the packets to the downstream server.

Additionally, further requests re-utilize the same previously established TCP connection: TCP is NOT a #stateless protocol.

This means that Layer 4 proxies can be faster and more #efficient than their counterparts.  This also means less #flexibility: We can't do intelligent things while proxying blindly.

> This is a realization of the [[PatternTradeoff]]

```mermaid

sequenceDiagram
    Client->>Proxy: Request Packet 1
    Proxy->>Server: Request Packet 1
    Client->>Proxy: Request Packet 2
    Proxy->>Server: Request Packet 2
    Client->>Proxy: Request Packet 3
    Proxy->>Server: Request Packet 3
    Client->>Proxy: Request Packet 4
    Proxy->>Server: Request Packet 4
    Client->>Proxy: Request Packet 5    
    Proxy->>Server: Request Packet 5
    Note right of Server: <br/> Processing <br/>
    Server->>Proxy: Response Packet 1
    Proxy->>Client: Response Packet 1
    Server->>Proxy: Response Packet 2
    Proxy->>Client: Response Packet 2
    Server->>Proxy: Response Packet 3    
    Proxy->>Client: Response Packet 3


```

___

## Tools

* [[ToolHAProxy]]
* [[ToolEnvoy]]
* [[ToolNgix]]
* [[ToolIstio]]
* [[ToolLinkerd]]
* [[ToolCaddy]]

___

## References

* <https://www.youtube.com/watch?v=iLHhL-vAPqo>
* <https://www.youtube.com/watch?v=SqqrOspasag>
* <https://www.youtube.com/watch?v=ylkAc9wmKhc>
