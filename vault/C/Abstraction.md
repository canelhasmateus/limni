<https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/>
TCP attempts to provide a complete abstraction of an underlying unreliable network, but sometimes, the network leaks through the abstraction and you feel the things that the abstraction can’t quite protect you from. This is but one example of what I’ve dubbed the Law of Leaky Abstractions:

All non-trivial abstractions, to some degree, are leaky.

like all abstractions, leak, and the only way to deal with the leaks competently is to learn about how the abstractions work and what they are abstracting. So the abstractions save us time working, but they don’t save us time learning.

___
<https://www.joelonsoftware.com/2001/12/11/back-to-basics/>

Shlemiels. They are often hidden by your libraries. Looking at a column of strcats or a strcat in a loop doesn’t exactly shout out “n-squared,” but that is what’s happening.

memory mapped files
memory allocators

For homework, think about why Transmeta chips will always feel sluggish. Or why the original HTML spec for TABLES was so badly designed that large tables on web pages can’t be shown quickly to people with modems. Or about why COM is so dang fast but not when you’re crossing process boundaries. Or about why the NT guys put the display driver into kernelspace instead of userspace.

These are all things that require you to think about bytes, and they affect the big top-level decisions we make in all kinds of architecture and strategy.
