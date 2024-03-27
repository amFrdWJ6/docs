# Hash Tables (maps)
associative arrays (k-v pairs)  
Usage: databases, cache, session mgmt, route handling, k-v configs

**Be aware**: 
- a hash function has to provide uniform distribution across the hash table and be performant
- a high load factor increases the likelihood of collisions and can degrade performance => resize the hash table

## Collision handling
[wiki: collision resolution](https://en.wikipedia.org/wiki/Hash_table#Collision_resolution) for more complex handling


Basic handling:
- **chaining**: simple to implement
  - **linked list**
  - **dynamic arrays**: python's lists
  - **BST ( AVL Trees, Red-Black Trees)**
- **open adressing**: finds an empty slot in the array when a collision occurs, more performant
  - **linear probing**: probes for the next empty slot by checking index i+1, then i+2 and so on
  - **quadratic probing**: probes for the next empty slot by using a quadratic function
  - **double hashing**: uses a second hash function to determine the probe step size (aka offset)

## Implementation
- build-in `Map` is similar to HT
```TypeScript
```