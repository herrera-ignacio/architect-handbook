# Collisions
## Definition
When different keys convert to the same integer, it is called a collision. Without handling collisions, older keys will get overridden and data will be lost.
## Collision resolution
There are [multiple ways](https://en.wikipedia.org/wiki/Hash_table#Collision_resolution) to handle collisions.
### Chaining 
We store linked lists inside the hash map's array instead of the elements themselves. The linked list nodes store both the key and the value.
If there are collisions, the collided key-value pairs are linked together in a linked list. Then, when trying to access one of these key-value pairs, we traverse through the linked list until the key matches.