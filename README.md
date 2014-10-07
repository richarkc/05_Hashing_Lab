05_Hashing_Lab
==============

Implement a hash table in C++

Requirements
------------

1. `keyExists`, `find`, `remove`, and `size` should all be O(1)
2. `add` should be reasonably fast. Use linear probing to find an open slot in the hash table. This will be O(1), on average, except when `grow` is called.
3. `grow` should be O(n)
4. Do not leak memory


Reading
=======
"Open Data Structures," Chapter 5, except for 5.2.3. http://opendatastructures.org/ods-cpp/5_Hash_Tables.html

Questions
=========

#### 1. Which of the above requirements work, and which do not? For each requirement, write a brief response.

1. Yes, all these methods should take constant time. Size simply returns a variable so indefinitely O(1). The only thing that affects the running time of add, find, and remove is the linear probing, which should most likely stay in the range of 1 or 2 cycles to probe for the correct item, so they should all stay O(1) as well, unless the hash function is terrible and is mapping all items to the same spot(for example).
2. Add is also O(1), provided that grow is not called, for the same reason as above. 
3. Grow() is O(n), given that the program must iterate completely through the old array and rehash all of the old values to the new hash table.
4. Variables are properly deleted in the destructor and in grow().

#### 2. I decided to use two function (`keyExists` and `find`) to enable lookup of keys. Another option would have been to have `find` return a `T*`, which would be `NULL` if an item with matching key is not found. Which design do you think would be better? Explain your reasoning. You may notice that the designers of C++ made the same decision I did when they designed http://www.cplusplus.com/reference/unordered_map/unordered_map/

The former is a better design decision. First off, you have the improved functionality of being able to check if the keyExists, if for some reason the user wanted to only check for that. In terms of only find() it's much better to check if the actual keyExists and if it does not throwing an exception, allowing for more information to the user than simply giving back null. You could check for null in the code implementing this table, but it's much cleaner to catch an exception.

#### 3. What is one question that confused you about this exercise, or one piece of advice you would share with students next semester?

Advice I would share: Watch your deleted items, and make sure it's not causing any bugs in your code when items collide.