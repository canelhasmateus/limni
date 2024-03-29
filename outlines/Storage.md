---
tags:
    - concept
    - software
---

# Storage

## Properties

In storage, Durability is the guarantee that data can be accessed after a failure. It is not a binary property: it should be defined as the modes of failures you want your data to survive.

- Usually, there is some performance penalty for durability;
- Rarely tested - involves cutting power, which is disruptive and hard to automate.

Volatile Storage:

- Something that goes away when you reboot. Storage that is attached to your instance:
- When your instance is terminated, you lose all of this data.

Non-Volatile:

- Survives a reboot.
- Hard disk.

![[BlockStorage]]
![[DocumentStorage]]
![[FileStorage]]
