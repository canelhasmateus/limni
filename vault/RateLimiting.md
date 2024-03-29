---
tags:
    - queue
    - network
    - concept
---

# RateLimiting

Avoid competition to a [[FiniteResource]] of servers between clients, by predefining usage quotas.

The naive implementation is simple: Limit the number of requests a client can do in a specified period. This has some interesting ramifications:

- If the origin services are overloaded, even following the allowed quotas can be too much to handle. [[SaturationPoint]]
- If the limiting is aggressive, we end up wasting resources: We could have handled the request, but pre-emptively refused to. [[Efficiency]]

This conundrum comes from the static nature of this implementation.
Better implementations can be devised by application of [[QueueTheory]] and [[CapacityPlanning]].
[[StaticDynamic]]

## References

# todo
