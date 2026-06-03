# Exam

You should know all theory presented at the lecture: definitions of data structures and operations on them, all theorems and proofs thereof. The exam is oral with written preparation. You will get one major and one minor question from the following list.

## Major questions

- Define the Splay tree. Describe operations Splay, Find, Insert, and Delete. Compare Splay trees with other data structures, in particular balanced search trees. State and prove the theorem on amortized complexity of the Splay operation.
- Define the (a,b)-tree. Describe operations Find, Insert, and Delete. Analyze their complexity in the worst case. Compare (a,b)-trees with other data structures, in particular balanced search trees.
- Define I/O model for caches and compare cache-aware and cache-oblivious algorithms. Formulate a cache-oblivious algorithm for transposition of a square matrix. Analyze its time complexity and I/O complexity.
- Describe hashing with chains and analyze its complexity. Define c-universal and k-independent systems of hash functions and provide constructions of such systems. Give an example when k-independent system in needed and c-universality does not suffice.
- Describe and analyze hashing with linear probing (under fully random hashing function). Compare this hashing with other data structures, in particular based on other hashings.
- Define multi-dimensional range trees and describe the type of queries it supports. Analyze time and space complexity of their construction and complexity of range queries.
- Define suffix arrays and LCP arrays. Describe and analyze algorithms for their construction. Give an example of their application.
- Describe locks and atomic operations CAS and LL/SC. Describe and analyze a lock-free stack including the memory management. Explain the ABA problem and its solution.

## Minor questions

- Describe a flexible array with growing and shrinking. Analyze its amortized complexity.
- Define the lazily balanced trees BB\[alpha]. Analyze their amortized complexity. Give an example of their application.
- Design operations Find, Insert, and Delete on a Splay tree. Analyze their amortized complexity. (It suffices to state the complexity of Splay operation without proof.)
- State and prove the theorem on amortized complexity on Insert and Delete on (a,2a-1)-trees and (a,2a)-trees.
- Analyze k-way Mergesort in the cache-aware model. Which is the optimum value of k?
- State and prove the Sleator-Tarjan theorem on competivity of LRU.
- Describe a system of hash functions based on scalar products. Prove that it is a 1-universal system from $Z_p^k$ to $Z_p$.
- Describe a system of linear hash functions. Prove that it is a 2-independent system from $Z_p$ to $[m]$.
- Construct a k-independent system of hash functions from $Z_p$ to $[m]$.
- Construct a 2-independent system of hash functions for hashing of strings of length at most L over an alphabet $[a]$ to a set of buckets $[m]$.
- Describe the cuckoo hashing and state the theorem on its complexity (without proof).
- Describe hashing with linear probing and give overview of results on its complexity.
- Describe and analyze the Bloom filter. Give an example of its application.
- Show how to perform 1-dimensional range queries on binary search trees.
- Define k-d trees and show that they require $\Omega(\sqrt n)$ time per 2-d range query.
- Show how to use suffix array and LCP array for finding the longest common substring of two strings.
- Describe parallel (a,b)-trees with the use of locks.
