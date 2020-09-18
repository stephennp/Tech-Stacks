## Best practices

References: <https://www.datadoghq.com/pdf/Understanding-the-Top-5-Redis-Performance-Metrics.pdf>

### Tracking memory usage to resolve performance issues

- If you are using Redis without periodical snapshots, your instance is at risk of not
only losing its data on shutdown but also being partially swapped in and out when
memory usage exceeds 95% of total available memory.Enabling snapshots requires Redis to create a copy of the current dataset in memory
before writing it to disk. As a result, with snapshots enabled memory swapping
becomes risky if you are using more than 45% of available memory,  this can be
exacerbated further by more frequent updates to your Redis instances. You can
reduce Redis’ memory footprint and thus the risk of swapping using the following
tricks:
  - Use a 32-bit Redis instance if your data fits in less than 4GB
  - Use hashes when possible
  - Set expirations for keys
  - Evict keys

### Number of commands processed: total_commands_processed

- The total_commands_processed metric gives the number of commands
processed by the Redis server. Commands come from the one or more clients
connected to the Redis server. Each time the Redis server completes any of the over
140 possible commands from the client(s).  Here are three ways to
address latency issues caused by high command volume and slow commands:
  - Use multi-argument commands
  - Pipeline commands:
  - Avoid slow commands for large sets

### Latency

- Once you have determined that latency is an issue, there are several measures you
can take to diagnose and address performance problems:
  - Identify slow commands using the slow log
  - Monitor client connections
  - Limit client connections
  - Improve memory management
  - Metric correlation

### Fragmentation Ratio

-The mem_fragmentation_ratio metric gives the ratio of memory used as seen
by the operation system (used_memory_rss) to memory allocated by Redis
(used_memory).

- Formula: mem_fragmentation_ratio = Used Memory RSS / Used Memory
- The used_memory and used_memory_rss metrics both include memory
allocated for:
• User-defined data: memory used to store key-value data
• Internal overhead: internal Redis information used to represent different
data types

### Eviction

- The evicted_keys metric gives the number of keys removed by Redis due to
hitting the maxmemory limit. maxmemory is explained in more detail on page 9.
Key evictions only occur if the maxmemory limit is set.
- When evicting a key because of memory pressure, Redis does not consistently
remove the oldest data first. Instead, a random sample of keys are chosen and
either the least recently used key (“LRU12 eviction policy”) or the key closest to
expiration (“TTL13 eviction policy”) within that random set is chosen for
removal.
- Reducing evictions can be a straightforward way to improve Redis performance.
Here are two ways to decrease the number of evictions Redis must perform:
  - Increase maxmemory limit
  - Partition your instance
    - hash partitioning
    - client side partitioning
    - proxy partitioning

## MEMORY MANAGEMENT

### MEMORY HELP

- "MEMORY DOCTOR                        - Outputs memory problems report"
- "MEMORY USAGE <key> [SAMPLES <count>] - Estimate memory usage of key"
- "MEMORY STATS                         - Show memory usage details"
- "MEMORY PURGE                         - Ask the allocator to release memory"
- "MEMORY MALLOC-STATS                  - Show allocator internal stats"
- Set a memory usage limit to the specified amount of bytes.
 When the memory limit is reached Redis will try to remove keys
 according to the eviction policy selected (see maxmemory-policy).

  - If Redis can't remove keys according to the policy, or if the policy is
 set to 'noeviction', Redis will start to reply with errors to commands
 that would use more memory, like SET, LPUSH, and so on, and will continue
 to reply to read-only commands like GET.

  - This option is usually useful when using Redis as an LRU or LFU cache, or to
 set a hard memory limit for an instance (using the 'noeviction' policy).

  - WARNING: If you have slaves attached to an instance with maxmemory on,
 the size of the output buffers needed to feed the slaves are subtracted
 from the used memory count, so that network problems / resyncs will
 not trigger a loop where keys are evicted, and in turn the output
 buffer of slaves is full with DELs of keys evicted triggering the deletion
 of more keys, and so forth until the database is completely emptied.

  - In short... if you have slaves attached it is suggested that you set a lower
 limit for maxmemory so that there is some free RAM on the system for slave
 output buffers (but this is not needed if the policy is 'noeviction').

### maxmemory <bytes>

- MAXMEMORY POLICY: how Redis will select what to remove when maxmemory
 is reached. You can select among five behaviors:

- volatile-lru -> Evict using approximated LRU among the keys with an expire set.
- allkeys-lru -> Evict any key using approximated LRU.
- volatile-lfu -> Evict using approximated LFU among the keys with an expire set.
- allkeys-lfu -> Evict any key using approximated LFU.
- volatile-random -> Remove a random key among the ones with an expire set.
- allkeys-random -> Remove a random key, any key.
- volatile-ttl -> Remove the key with the nearest expire time (minor TTL)
- noeviction -> Don't evict anything, just return an error on write operations.

- LRU means Least Recently Used
- LFU means Least Frequently Used

- Both LRU, LFU and volatile-ttl are implemented using approximated
 randomized algorithms.

- Note: with any of the above policies, Redis will return an error on write
       operations, when there are no suitable keys for eviction.

       At the date of writing these commands are: set setnx setex append
       incr decr rpush lpush rpushx lpushx linsert lset rpoplpush sadd
       sinter sinterstore sunion sunionstore sdiff sdiffstore zadd zincrby
       zunionstore zinterstore hset hsetnx hmset hincrby incrby decrby
       getset mset msetnx exec sort

 The default is:

### maxmemory-policy noeviction

- LRU, LFU and minimal TTL algorithms are not precise algorithms but approximated
 algorithms (in order to save memory), so you can tune it for speed or
 accuracy. For default Redis will check five keys and pick the one that was
 used less recently, you can change the sample size using the following
 configuration directive.

- The default of 5 produces good enough results. 10 Approximates very closely
 true LRU but costs more CPU. 3 is faster but not very accurate.
