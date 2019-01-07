# Distributed and Shared Memory

In a distributed memory system, each process has it's own local memory
that it can access. If processes need to share data amongst eachother,
they need to communicate with eachother. In a shared memory system,
the processes have access to a shared memory pool they all can access.

# Cache

Small, fast SRAM memory between processor and main memory, typically
on-chip. It contains copies of main memory words for fast access.
- Cache hit: accessed word in cache, get it fast
- Cache miss: word not in cache, load from slower main memory

A cache line holds a copy of a block of adjacent memory words,
from 16 bytes and up (differes with cache levels).

Kinds of cache misses:

- Cold miss: data was never in cache
- Capacity miss: data was evicted earlier when capacity was exceeded
                (fully associative caches)
- Associativity miss: data was evicted earlier because of cache set
                      conflict (set-associative and direct-mapped)

## Memory update

Strategies:

- Write-through: writing is done both to cache and main memory
- Write-back: write only to cache entry, and write to main memory
              when cache block is replaced.

A cache management system is

- Coherent if a read access to a memory location always reproduces the
    value corresponding to the most recent write access to that location.
    (no access to stale values)
- Consistent if all copies of a memory location in all 
    caches are identical.

To ensure cache coherence, a cache coherence protocol is used:

- Write-update protocol: all copies are updated in all caches, must be
    finished before next access.
- Write-invalidate: after writing, declare all other copies invalid.

