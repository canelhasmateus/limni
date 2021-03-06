# 2022-07-03

<http://danluu.com/3c-conflict/>

<https://easyperf.net/blog/2022/05/28/Performance-analysis-and-tuning-contest-6>

<https://lemire.me/blog/2022/06/06/data-structure-size-and-cache-line-accesses/>

Recently I've worked on a fast wordcount program for a programming contest[0]. I ran into the typical issues where some data structures should be padded to be a small power of 2 size so that accesses to array elements do not cross cache lines[1]. Later, when sort of playing around with the program, I noticed that I could make it ~3% slower by changing my bump allocator to align all allocations to 4k boundaries or make it ~5% faster by changing my bump allocator to add a small number of cache lines (1 works pretty well but 5 and 11 seem to work better) of padding to each allocation. Since I had sort of paid attention in computer architecture class I expected that this was due to set associativity in the cache. Still, I was surprised to see effects this large from this sort of change in a program that calls the bump allocator fewer than 300 times, doesn't really have any obvious "process the same indices of a bunch of arrays" access patterns, and cannot run into this issue by processing the same field of each element of an array of very large structs because it does not contain any very large structs.
One person I mentioned this to pointed me to TFA, which the best writeup of these issues I've seen, so I submitted it.

It seems like the full picture of "how not to ruin your day by allocating and sizing stuff" is something like this: Structs should be power of 2 sized, up to the cache line size, which is probably 64 bytes for the device you're reading this on unless it's an M1 mac and then it's 128. As the article points out, the next bunch of bits (6-9 of them in the article, but maybe more today) after the bottom 6 or 7 determine the set the cache line belongs to, so you want to put different values into those, which means that if you have some struct larger than your cache line size, and you want to have an array of those things and maybe traverse that array and access the same member of each element of the array, then you would do well to make sure that the size of that thing is an odd multiple of the cache line size, or at least not a large power of 2 multiple of the cache line size. In addition, if you would like to allocate a bunch of buffers, and you commonly access the fronts of your buffers more than the middles or the backs, then you would do well to make sure that the fronts of your buffers end up in many different sets. As far as I know, no off-the-shelf allocator will do this for you (i.e. if you repeatedly ask your allocator for 4MB buffers, they will all be at least 4k-aligned, and this is very bad for you), so you'll have to do it yourself. I'd love to have someone point out an off-the-shelf allocator that will go out of its way to avoid returning only 4k-aligned buffers though.



___
<https://www.causal.app/blog/scaling>

If we multiply two variables of 1B cells of 64 bit floating points each (~8 GiB memory) into a third variable, then we have to traverse at least ~24 GiB of memory. If we naively assume this is sequential access (which hashmap access isn???t) and we have SIMD and multi-threading, we can process that memory at a rate of 30ms / 1 GiB, or ~700ms total (and half that time if we were willing to drop to 32-bit floating points and forgo some precision!).

