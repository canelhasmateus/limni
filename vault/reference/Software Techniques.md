

# Circuit Breakers

An idea brought from electrical engineering, where circuit breakers are used to completely shut down currents when the  characteristics such as voltage reach outside of the operating thresholds.

It prevents meltdown by simply stopping everything just before hitting critical conditions.

Implemented by tools such as Hystrix, istio, conduit, linkerd , consul. 


# Breakpressure Mechanisms

[[todo]]

# Rate Limiting
    
A simple premisse: avoid having one client starve the others.

The usual implementation is simple: Limit the number of requests a client can do in an specified period of time. 

However, the naive implementation leads to some interesting ramifications. 

If the origin services is overloaded, even following the allowed quota can be too much to handle.

If the rate limit is aggresive, we end up wasting resources: We could have handled the request, but pre-emptively refused to.
 
This comes from the static nature of such rate limiting. Better implementations can be devised by aplication of [[Queueing Theory#Capacity Planning]]

# Tools

[[todo]]        . 
        . Loeads to evolving tools
            .. Circuity breaks
            .. Backpressure mechanisms 
            .. Hystrix, istio, conduit, linkerd , consul
