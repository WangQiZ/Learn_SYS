# Main Idea
1. Reverse engineer shared L2 cache and timing properties.
2. Build conflict sets
3. Covert Channel Attack & Side Channel Attack

# Reverse Engineer
1. Physical Page gets cached at the GPU connected to the memory where it is placed + remote GPU could access local memory via NVLink -> Shared L2 Cache

2. Fill the L2 Cache with _ldcg() -> timing properties

# Cache Eviction Sets
## Pointer Chase Experiment

1. find a target address and measure access time
2. from 1 to x access other address
3. if target address is evicted -> find a element in eviction set
4. change target find other eviction set

