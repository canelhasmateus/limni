---
created_on: 2023/01/17 05:51
kind:
tags:
---

# StructuredDocumentation

Reading this gives me a bit of insight into the point I mentioned to you about transparency:

There exists a hierarchy of contexts an individual is immersed in. For someone that will read through that implementation, these might be:

- Org-level - Docs through confluence, Reading through other projects and realizing this is a common approach
  - Team-Level - Asking a colleague
    - Project-level - Reading through similar implementations
      - Unit-Level - Reading through implementation + tests
        - Class-Level - Reading through the implementation/function

The insight is that thinking through this context:

- `Discoverability` is the ability to be aware of the context hierarchies that surround a particular problem
- `Documentation` no longer is a satisfiability problem, and becomes an optimization problem:  Don't just describe the behavior, but minimize the context necessary to understand it

In this case, Unit/File-Level is good enough here, so no problems on this front.

How do we `bake in` documentation and discoverability? Not sure, but having a more concrete definition definitely is a step forward to understanding and solving the problem.
