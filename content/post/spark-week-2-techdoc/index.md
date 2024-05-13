---
title: Encora Spark Week 2. Apprentice Technical Log Doc
date: 2024-05-13
math: true
---

# Five LeetCode solutions

## OVERVIEW

I will present my solutions to five coding challenges assigned to my team during the second week of the Encora Spark Apprenticeship program. The problems are:

- [LRU Cache](https://leetcode.com/problems/lru-cache/) _(medium)_
- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) _(medium)_
- [Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/) _(hard)_
- [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/) _(hard)_
- [Number of unequal triplets in aray](https://leetcode.com/problems/number-of-unequal-triplets-in-array/) _(easy)_

For the "Medium" and "Hard" problems, we collaborated as a team, brainstorming together while one of us implemented the solution. The "Easy" problem was solved individually. I will describe each problem and its solution individually in this same blog.

## 1. LRU Cache _(medium)_

### Context

“Design a data structure that follows the constraints of a Least Recently Used (LRU) cache. The functions get and put must each run in O(1) average time complexity. Keys and values of items are integers less than 10^5, and the capacity is less than 3000 items”

A (LRU) cache provides a fast lookup and retrieval storage with limited capacity. The cache is being filled by every new element that appears. When the cache reaches its capacity, the oldest item used is evicted to make room for the new element.

### Solution

For efficient lookup, we will utilize an array-based cache, where each index corresponds to a key, and A[i] points to a data structure storing the associated value. To maintain the temporal order of elements, we use a doubly linked list. Each time an element is added or accessed, it is moved to the head of the list, implicitly shifting the other elements back. This modification has a constant time complexity since we only need to update the 'next' and 'prev' pointers of the affected elements. When it comes to evicting an element, we simply remove the current tail of the list. Nodes will be structured as follow:

```javascript
Node {
  key
	value
	next
	prev
}
```

We define a Node data structure to represent each element in the cache, where 'key' and 'value' are integers, and 'next' and 'prev' are pointers to other nodes or null. Our cache will be an array of these nodes:

```javascript
Cache = [Node_0, Node_1, ..., Node_10_000]
```

To initialize the cache, we allocate memory for the array, set references to the head and tail of the doubly linked list, and initialize a counter to keep track of the number of elements in the cache, initially set to 0.

To facilitate the put and get operations, we need two auxiliary functions to manage the doubly linked list. Each time an element is added or accessed; it will be `pushedToHead`. There are four cases to consider:

```javascript
function pushToHead(node) {
  // 1. first new element
  if (head == null || tail == null) {
 	  head = node;
 		tail = node;
  	tail.next = tail;
 		break;
   }
   // 2. element is already the head
   if (head == node) break;
   // 3. element is in the tail
   if (tail == node) {
    head.next = node;
    node.prev = head;
 		tail = node.next;
 		node.next = null;
 		head = node;
 		break;
   }
   // 4. element is between other elements
   if (node.prev != null) node.prev.next = node.next;
   if (node.next != null) node.next.prev = node.prev;
   node.next = null;
   node.prev = head;
   head.next = node;
   head = node;
}
```

We also need a function to delete the tail as follow:

```javascript
function popTail() {
  if (tail == null) return -1;
  if (tail == head) {
    int lrukey = tail.key;
   	head = null;
   	tail = null;
   	return lrukey;
    }
  int lrukey = tail.key;
  tail = tail.next;
  return lrukey;
}
```

The reason we are returning the key is because once the tail is deleted, we need to update the corresponding reference in the cache array to null, indicating that the element is no longer present in the cache.

With these two auxiliary functions, the call to ‘get’ gets trivial:

```javascript
function get(int key) {
 	node = cache[key];
 	if (node == null) {
 		return -1;
 	}
 	pushToHead(node);
 	return node.value;
}
```

And the call of ‘put’ only deals with two cases:

```javascript
function put(int key, int value) {
  node = cache[key];
  if (node != null) { 		// 1. Element already exists
 	  node.value = value;
   	pushToHead(node);
   	break;
    }

   	node = new Node(key, value);   // 2. Element is new in the cache
   	if (count >= capacity) {.      // 3. But the cache is full
  		int lrukey = popTail();
  		cache[lrukey] = null;
  		count--;
    }
    cache[key] = node;
   	pushToHead(node);
    count++;
```

### Alternative Solutions

This solution uses an array for efficient lookup O(1), taking advantage of the constrained range of integer keys. However, if the keys were of a different data type or the range was significantly larger, a HashMap or dictionary with a hash function would be more appropriate. The performance trade-offs depend on the programming language being used. In Java, this array-based approach outperforms HashMap solutions, as evidenced by its top 5% runtime and memory performance among 1.6 million submissions. In the other hand, in JavaScript, using arrays resulted in a performance loss compared to dictionary-based solutions.

## 2. Longest Substring Without Repeating Characters _(medium)_

### Context

“Given a string `s`, find the length of the longest substring without repeating characters.”
Constraints:
{{< math>}} $0 <= |s| <= 5 * 10^4$ {{< /math}}
`s` consists of English letters, digits, symbols and spaces.

### Solution

The solution uses a technique called the "Sliding Window" with a runtime and memory of O(n). We initiate the window at the beginning of the string and expand it from the right end with each new character encountered. If we detect a repeating character within the window, we move the left start of the window one step ahead to the first occurrence of that character, excluding it from the window and ignoring every substring in it that won’t pass the condition. This process continues until we've iterated through the entire string, ultimately finding the longest substring without repeating characters.

To efficiently check if a new character is already present within the window substring, we utilize an array of size 128, where the hash function corresponds to the ASCII value of each character, given the constraints. The value should be the index where that character was last seen (its position in the complete string), or –1 if it's not contained by the substring.

```javascript
function lengthOfLongestSubstring(s) {
  if (s.length() <= 1) return s.length();
 	longest = 0, start = 0;
  lastSeen = new int[128]; 			      // filled with -1s
 	for (int end = 0; end < s.length(); end++) {
 		char = s[end]
 		idx = unicode(char)
 		if (lastSeen[idx] != -1) { 	      // char is already in the substring
 		 	seenAt = lastSeen[idx];
 			if (seenAt >= start) 	          // move the window by the start side
 				start = seenAt + 1;
 		}
   lastSeen[idx] = end;			          // increase the window end
   int sublength = end - start + 1;
   if (sublength > longest)  		     // update longest if other is found
 		longest = sublength;
  }
 	return longest;
}
```

### Alternative Solutions

This solution uses an array for efficient lookup, taking advantage of the constrained range of ASCII Unicode's. But without that constraint, a HashMap should be used for generality. This implementation is Java’s top 5% performance in runtime and top 10% in memory usage from 16.5M solutions. A brute force solution has the runtime complexity of `O(n^2)` when enumerating every possible substring.
