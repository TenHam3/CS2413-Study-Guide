# CS2413-Study-Guide

1. Syntax and Concepts
- What is the syntax to declare a pointer in C++?
- A: data type* variableName;
- What is the depth of Node A in this binary tree? 
- A: However many edges there are in the path from Node A to the root node
2. Basic Data Structure Operations
- In the stack, what does the “push” function (normally) do?
- A: The push function adds the element to the top of the stack/the next available cell in the array
- In the hash table, what does the “hash” function (normally) do?
- A: The hash function takes a key as input and outputs a number corresponding to the index of the bucket that the key is supposed to be hashed to
3. Basic Techniques
- What is the search sequence of binary search on this array?
- A: The search sequence is the sequence of values you check when comparing the middle index element to the target value
- What is the traverse sequence of in-order traverse on this binary tree?
- A: In-order traverse checks nodes in the following order: left subtree, root node, right subtree. This means that the tree will be traversed starting from the leftmost nodes and ending on the rightmost nodes.
4. C++ Code Writing
5. C++ Code Reading
6. Efficiency and Properties
- What is the height of the shortest binary tree we can build to store n nodes?
- A: The height of the shortest binary tree we can build to store n nodes is $\log{(n + 1)} - 1$. This is because the shortest binary tree is achieved when we have a full and complete binary tree, that is, every level of the binary tree is filled with nodes. This means that the number of nodes, n, is equal to the maximum number of nodes it can be for a given binary tree with height h, which is $2^{h + 1} - 1$. Adding 1 to both sides, then taking the logarithm of both sides yields $\log{(n + 1)} = h + 1$. Subtracting 1 from both sides gives us the minimum height of a binary tree with the given number of nodes n, which is $h = \log{(n + 1)} - 1$.  
- Suppose we can add a new node to the head or tail of a singly linked list. Which option is more efficient?
- A: Adding to the head is more efficient since you are already at the insertion point and only need to do the insertion process at the head whereas you would have to traverse the entire linked list and then execute the insertion process if you were to add a new node at the tail.
7. Design and Analysis Questions

## Topic 1: C++ Programming

### Basic 
![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/c3e40ec5-94ee-4ac3-afa5-3d41ac374c73)

### Pointers

- When modifying data through a function, you have to pass in a pointer to the variable as an argument of the function (address of the variable using & operator also works).
- Use -> to access public class members of a pointer, use . operator on objects of the class
- Pointers can be used as array names and can access any index using the same syntax (p[index]).

### Dynamic Memory Allocation

- Dynamicaly allocated memory is stored in the heap
- When you dynamically allocate memory, it always returns a pointer to the object or data type that is dynamically allocated
- To "delete" a memory chunk means freeing the memory chunk for other variables to use in the future, but does not mean erasing the data currently there. Cannot access this data through the pointer when deleted. Data is still technically there in the memory chunk until it gets overwritten later on.
- 

### Memory Used by Functions
- Functions take memory in the stack each time they are called
    - This means recursive functions will take more space in the stack memory since multiple function calls will be stored in the stack until the base case is reached and function calls start completing and getting popped off the stack
- Any variables declared in the function will stay in the same memory location, even if the function is called multiple times in separate instances in the code
    - If a function declares in integer variable and initializes it to a given integer argument, the same memory location will be occupied by the integer declared in the function and thus any changes to the variable, even by later function calls, will reflect on the same integer from that memory location

## Topic 2: Linked List

### Singly Linked List

- Links memory fragments
- When removing from the middle, first travel to the node before the node you want to remove, then save the node you want to remove in a pointer, update the current node's next pointer to point at the removed node's next pointer, and delete the node you want to remove. Alternatively, after traveling to the node before the node you want to remove, you can save the next-next node in a pointer, delete the current node's next pointer, and then rebuild the link using the pointer you saved
- Efficiency for adding to head vs adding to tail is that adding to the head is more efficient in a singly linked list since you don't have to traverse through the list to get to the insertion point

### Doubly Linked List

- Efficiency for adding to head vs adding to tail is the same for doubly linked list since you have a pointer to both the head and tail in a doubly linked list
- In general, adding is more efficient on doubly linked lists than it is singly linked lists because of the tail pointer from the doubly linked list, allowing for not only O(1) adding for the head, but also the tail whereas the time complexity for adding to the tail of a singly linked list is O(n)

### Circular Linked List

- Circular singly linked lists are linked lists that have the tail node point back to the head
- Application in scheduling can be seen in things such as turn taking in chess

## Topic 3: Stacks and Queues

- Stacks can be implemented using arrays or linked lists, LIFO
    - For the array-based implementation, all you need is an integer to keep track of the index of the top element and resize the array if necessary
    - For the linked list implementation, you need to push and pop from the head of the list
- Stacks can be applied in scheduling like keeping track of words that a user has typed so that they can undo the most recent changes
- Queues are implemented using linked lists and are FIFO
    - The front of the queue is represented by the tail of the linked list
    - The back of the queue is represented by the head of the linked list
- Queues can be applied for the breadth-first search algorithm
- Pop only removes the element from the top of the stack/front of the queue and does not return the element being popped off (void return type)

## Topic 4: Hash Tables

### Direct Address Table

- Motivation includes a data structure where we can efficiently search for any element in the data structure given some sort of key
- DATs are arrays where elements are placed in the same index as their key
- A limitation of DATs are that it does not use memory efficiently (i.e. if there is a key way larger than the rest of the elements or the range of keys is large and there aren't many values in between the largest and smallest values, it will require a larger array to fit every element in the table, resulting in many empty cells and wasted space)

### Hash Table

- Improves on the time-space limitation of DATs by adding in a hash function
- Key terms include:
    - Hash function: a function that takes a key as input and outputs an integer corresponding to the index of the bucket the key is meant to be placed in
    - Hash code: the resulting hash value of a particular key that is output by the hash function
    - Hashing: the process of mapping keys to hash values
    - Hash table/Bucket array: the array that holds all the keys after being hashed
- Collisions are when multiple keys get hashed to the same index
    - When keys get hashed to an occupied cell during a probing process, these are not collisions and should not be counted when counting the number of collisions for adding a sequence of keys
- Two ways of dealing with collisions: separate chaining and open addressing
- Load factor: $\lambda = \frac{n}{N}$
    - n is the number of objects stored in the table
    - N is the size of the table
    - Range of $\lambda$ for separate chaining is [0, $\infty$] because extra objects are stored outside the table, which means for a finite table size N, there could theoretically be possibly infinite objects n stored outside the table
    - Range of $\lambda$ for open addressing is [0, 1] because all objects are stored inside the table
    - We want a hash table to have a small $\lambda$ to gain efficiency and have guarantees such as
          - quadratic probing is guaranteed to find an empty cell if $\lambda < 0.5$ (+ other assumptions) 

#### Separate Chaining

- Each cell in the hash table holds a list of collided objects
- Most common implementation is to store collided objects as linked lists and each cell holds list head pointers. Can also have objects in each cell that have next pointers to create linked lists of collided objects or even pointers to arrays of collided objects.
- Adds nodes to the head of the linked list when a collision occurs

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/944e9634-74ca-404c-85e3-22c8a580c7f5)

#### Open Addressing

- Collided nodes probe the rest of the array, searching for an empty cell to be placed
- Three probing strategies:
    - Linear: goes to the next cell in the array until it finds an empty cell or it comes back to the original hashed location, in which case the hash table is full and needs resizing, loops back around to the beginning of the hash table when probing at the end
    - Quadratic: uses a quadratic formula to probe to another cell
    - Double hashing: uses two hash functions to probe to another cell

Example of quadratic: 

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/1fee4592-6f19-4c36-b7be-0c03a53c42bc)

Example of double hashing:

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/14226bc4-e72c-4ce2-9c89-f0460a9528b2)

- Limitations of linear probing: a limitation is primary clustering, where a large number of collided objects end up being stored contiguously in the array so that there is a large cluster of objects that were hashed to the same index, lowering the add and search efficieny of objects hashed to these cells
      - Also theoretically suffers from secondary clustering because the probing sequence is the same for a large number of collided objects
- Limitations of quadratic probing: quadratic probing has two limitations
  1. It is not guaranteed to find an empty cell even if one exists in the hash table. It is only guaranteed if
     - Table size is a prime number
     - Table is not more than half-filled
  2. It suffers from secondary clustering, where the probing sequence is the same for a large number of collided objects
 
- Limitations of double hashing: double hashing requires extra time for the second hashing and cannot guarantee an empty cell in general
    - It is also not guaranteed for double hashing to avoid primary or secondary clustering, just avoids them in general but not always
 
- Extra indicators such as an additional array can help probing efficiency by marking how many collisions occur at each cell. Trades space efficiency for time efficiency.
- You need to resize the hash table if it becomes full or half full if using quadratic probing

#### Separate Chaining vs Open Addressing

- Separate chaining can always add objects in without resizing the hash table, trading in space efficiency for flexibility
- Open addressing uses hash table space more efficiently but needs resizing for certain conditions to be met

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/e535a859-891a-43f5-ba1b-c3303a0c6bab)

#### Coalesced Chaining

- A combination of separate chaining and open addressing where collided objects probe through the array searching for an empty cell and point to the index of the next collided object in the hash table

### Hash Functions

- To determine the smallest necessary table size for a given hash function, determine the range of the hash function and set your table size to the upper bound of the range + 1
- The parameter of modulo hashing, which is the divisor, impacts search efficiency, number of collisions, and table size depending on the value of the divisor. If the divisor is large, it requires a larger table size but there are fewer collisions and therefore improves search efficiency. If the divisor is small, it requires a smaller table size but there are more collisions and therefore hinders search efficiency.

## Topic 5: Binary Tree

### Concepts

- Any node that points to other nodes is called a **parent** node and any nodes that are connected from a node higher in the tree are called **child** or **children** nodes. The **root node** does not have any parents.
- Any node that is at a lower level of the tree relative to another node is said to be the **descendant** of that node if there is a path that connects them
- Any node that is at a higher level of the tree relative to another node is said to be the **ancestor** of that node if there is a path that connects them
- Nodes that share the same parent are called **sibling** nodes
- A node can have at most one parent but multiple children
- If a node has no child, it is an **external node** (or **leaf node**)
- If a node has one or two children, it is an **internal node**
- If a node has no parent, it is a **root node**
- An **edge** connects a parent and a child node. This is the line that connects the parent and child nodes in the visualization of the tree
- A **path** is a sequence of nodes such that any two adjacent nodes are connected by an edge
- A **subtree** of T is a tree rooted at X and made of all descendants of X
- The **left subtree** of X is the subtree rooted at X's left child node
- The **right subtree** of X is the subtree rooted at X's right child node
- **Degree of a node** is the number of children it has
- **Degree of a tree** is the maximum degree of all nodes in the tree
- **Depth of a node** is the number of its ancestors (also calculated as the number of edges there are from a node to the root)
- **Height of a tree** is the maximum depth of its leaf nodes
- A **binary tree** is a tree of degree two
- A **complete binary tree** is a binary tree that is completely filled from top to bottom and from left to right per depth. Has to add childern in the leftmost empty spot at the last level.
- A **full binary tree** is a binary tree where each node has either 2 or 0 children

### Traverse

- Inorder Traverse: algorithm that visits nodes in the following order: left subtree, root, right subtree
- Preorder Traverse: algorithm that visits nodes in the following order: root, left subtree, right subtree
- Postorder Traverse: algorithm that visits nodes in the following order: left subtree, right subtree, root
- Breadth-First Traverse: algorithm that visits nodes from top to bottom, left to right. It goes level by level visiting each node from left to right

### Implementation

- Binary trees can be implemented using linked lists or arrays
    - For the linked list implementation, each node has a left and right pointer to point at its left and right children, and a parent pointer to point at the parent
    - For the array-based implementation, nodes are stored in an array. A node at index i has a left child stored in the array at index 2i and a right child stored at index 2i + 1.
 
### Properties

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/e629e12d-ce0f-4f97-a00d-5e8318e3caf8)

#### Property 1

- The upper bound can be proven by observing that each level has $2^h$ nodes in them where h is the height of that node. Summing all nodes up makes $2^0 + 2^1 + ... + 2^h$ where h is the height of the entire tree. We can call this sum S. Multiplying it by 2 and subtracting S from 2S gives $S = 2^{h + 1} - 1$ and that is why the upper bound is $2^{h + 1} - 1$.
- The lower bound can be proven by observing that each level can have a minimum of 1 node each, so at any given height h, the tree can have a minimum of h nodes + the root node so the lower bound for how many nodes there are in the tree, n, is h + 1.

#### Property 4

- The lower bound, which is the height of the shortest binary tree we can build to store n nodes, is $\log{(n + 1)} - 1$. This is because the shortest binary tree is achieved when we have a perfectly full and complete binary tree, that is, every level of the binary tree is filled with nodes. This means that the number of nodes, n, is equal to the maximum number of nodes it can be for a given binary tree with height h, which is $2^{h + 1} - 1$. Adding 1 to both sides, then taking the logarithm of both sides yields $\log{(n + 1)} = h + 1$. Subtracting 1 from both sides gives us the minimum height of a binary tree with the given number of nodes n, which is $h = \log{(n + 1)} - 1$.
- The upper bound is achieved when each node only has 1 child, effectively resulting in a singly linked list of nodes. This happens when the tree has the minimum number of nodes, n, at height h, which is h + 1. Solving for h by subtracting 1 from both sides gives $h \leq n - 1$.

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/731f5677-6169-41ed-9066-dd563fa93f02)

- This property can be proven by observing a simple proper binary tree of 3 nodes. The number of external nodes in this tree would be 2 and the number of internal nodes is 1. Whenever you add two more nodes as children to another node, the external node becomes an internal node, adding 1 to the number of internal nodes and subtracting 1 from the number of external nodes. However, you then add 2 to the number of external nodes because the two newly added nodes are external so in this process, both internal and external nodes only increase by 1, preserving the property.
      - You have to add two nodes per insertion because it has to preserve the full tree property of each node having either 0 or 2 nodes. If you add only 1 node as a child to a leaf node, then it is no longer a full/proper tree and the property doesn't apply.

#### Property 2 and 3

- Since the number of total nodes n, is equal to $n_i + n_e$, where $n_i$ is the number of internal nodes and $n_e$ is the number of external nodes, then you can use Property 1 and the previous property to derive the upper bounds of the Properties 2 and 3 relating the number of internal/external nodes to the height.
- The lower bound for the number of external nodes is simply 1 since in a tree where the minimum number of nodes is h + 1, there is only 1 external node, which is the tail of the linked list.
- The lower bound for the number of internal nodes is h because in the tree where the minimum number of nodes is h, there are h nodes with children, meaning there are h internal nodes. You can also observe that if there is a minimum of 1 external nodes in a tree and the minimum number of total nodes in a tree is h + 1, then you can get the number of internal nodes by doing the following:
- $n = n_e + n_i$
- $h + 1 = 1 + n_i$
- $n_i = h$ 

#### Proof of Parent-Child Index Relationship

- If you have the rth node of a given depth h, you can find its index and its childrens' indices
- First, you can use Property 1 to see how many total nodes there are in the previous levels and this would be the same as the index of the last node in the previous level. This would be $2^{h - 1 + 1} - 1 = 2^h - 1$, where h still represents the depth of the given node. If the given node is the rth node in the level, then you can travel r times after the last node of the previous level to get to the index of the desired node. This means the rth node is at index $2^h - 1 + r$. To find the indices of its children, you can apply Property 1 again, but this time at depth h instead of h - 1 to get to the index of the last node at height h. This would be $2^{h + 1} - 1$. Because the parent is the rth node in its level and there are r - 1 nodes before it in its level and each node has to have 2 children since it is a complete tree, there are $2(r - 1)$ nodes in the next level before the left child. This means that the left child will be at index $2^{h + 1} - 1 + 2(r - 1) + 1 = 2^{h + 1} + 2r - 2 = 2(2^h + r - 1)$. Since the parent node is at index $2^h + r - 1$, we can label that as index i and therefore the left child will be at index 2i. This also means the right child will be at the next index, which is 2i + 1.  

## Topic 6: Binary Search Tree

### Definition

- A binary search tree is a binary tree where all nodes in the left subtree of a node are less than the current node and all nodes in the right subtree are greater than the current node

### Add

- To add a node, you start by implementing search on the BST with the given key until you get to a NIL node where the given key would be placed
- Replace the NIL node at the insertion point with the given node
- Add NIL nodes as children of the new node

### Remove

- There are two cases to consider when removing a node from a BST:
    - The removed node is a leaf node
    - The removed node is an internal node
- If removing a leaf node, you can just replace it with a NIL node
- If removing an internal node, you have to find its inorder successor and replace it with that node, filling in any holes as a result of that process. Its inorder successor can either be the maximum node of the removed node's left subtree or the minimum node of the removed node's right subtree. Both work because no nodes will break the BST property if it replaces the removed node. Any holes that result from replacing nodes in this way can be filled by repeating the same inorder successor process
- An improved algorithm would replace any holes with the subtree of the replacement node if it only had one child. This means that if you replace the removed node and the replacement node only had one child, the resulting hole could be filled directly by replacing it with the subtree rooted at that one child. 

### Connection Between BST and Binary Search

- Binary search has a corresponding BST that would have the same search sequence on the same data set
- Both can search efficiently in the same time because they have the same search sequence (assuming the BST is balanced)
- In general, performing standard search on BST is not as efficient as performing binary search on an array because more often than not, a BST of a given data set will not be balanced
    - Ex: If adding the integers 1, 2, and 3 as a BST, there are 6 permutations for adding them in a particular order
    - 4 out of the 6 permutations are unbalanced because 2 start with 1 and every node after would be in its right subtree and 2 start with 3 and every node after would be in its left subtree. Both of these would be unbalanced because it is a single-branch/single-child tree

### Comparative Efficiency of Different BST Structures

- BST search efficiency depends on the height since you would have to travel down the entire tree in the worst case scenario
- This makes search more efficient on more balanced trees where they are complete and full, meaning that it is at its minimum height
- This also means that search is less efficient on BSTs that are essentially singly linked lists, where there is only one path and the height is equal to the number of nodes - 1

## Time and Space Complexity

- Complexities usually depend on n, or the number of elements in the data structure
- For space complexity, there are two conventions:
    - Including the input space in the space complexity analysis
    - Not including the input space in the space complexity analysis
    - For this study guide, assume we are not including input space
- Three notations for time and space complexity:
    - Big O: upper bound that describes the complexity in the worst-case scenario
    - Big $\Omega$: lower bound that describes the complexity in the best-case scenario
    - Big $\theta$: both bounds that describes a function that can act both as an upper or lower bound for the complexity (usually the same as Big O since you can always scale the Big O function down to where it is a lower bound for the complexity)
 
- How to analyze:
    - List out all operations that take constant time to execute (or all variables/function calls that take space for space complexity)
    - Identify the worst-case scenario
    - Measure the total time/space in the worst-case scenario by identifying each step's dependence on n and gathering like terms
    - Process the total time by identifying the dominant term in the complexity and choosing that as the function for the complexity
 
Ex: 

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/1581641c-825c-4db0-a874-f1cedb4b2034)

### Linked List

#### Time Complexity

- Search
    - Singly: O(n), $\Omega$(1)
    - Doubly: O(n), $\Omega$(1)
 
- Adding to head
    - Singly: O(1), $\Omega$(1)
    - Doubly: O(1), $\Omega$(1)
 
- Adding to tail
    - Singly: O(n) $\Omega$(n) (Could be classified as $\Omega$(1) if you consider the case where the list is either one node or empty as a constant time operation)
    - Doubly: O(1), $\Omega$(1)
 
- Removing from head
    - Singly: O(1), $\Omega$(1)
    - Doubly: O(1), $\Omega$(1)
 
- Removing from tail
    - Singly: O(n), $\Omega$(n) (Same as adding to tail where it could be $\Omega$(1))
    - Doubly: O(1), $\Omega$(1)

#### Space Complexity

- Storing n nodes
    - Singly: O(n), $\Omega$(n)
    - Doubly: O(n), $\Omega$(n)
- Search
    - Singly: O(1), $\Omega$(1) (Only a temp pointer is declared in the algorithm, constant memory)
    - Doubly: O(1), $\Omega$(1)
 
- Adding to head
    - Singly: O(1), $\Omega$(1)
    - Doubly: O(1), $\Omega$(1)
 
- Adding to tail
    - Singly: O(1), $\Omega$(1) (Only a temp pointer to iterate through the list)
    - Doubly: O(1), $\Omega$(1)
 
- Removing from head
    - Singly: O(1), $\Omega$(1) (Only a temp pointer to save the old head before updating the new head so that you can delete it)
    - Doubly: O(1), $\Omega$(1)
 
- Removing from tail
    - Singly: O(1), $\Omega$(1) (Only a temp pointer to iterate through the list)
    - Doubly: O(1), $\Omega$(1)
 
### Stacks and Queues

#### Time Complexity

- Pushing
    - Stack: O(1), $\Omega$(1) (O(n) for array-based implementation due to the possible resize)
    - Queue: O(1), $\Omega$(1) (Same as array-based stack implementation)

- Popping
    - Stack: O(1), $\Omega$(1)
    - Queue: O(1), $\Omega$(1)
 
- Top/Front
    - Stack: O(1), $\Omega$(1)
    - Queue: O(1), $\Omega$(1)

 #### Space Complexity

 - Storing n objects
    - Stack: O(n), $\Omega$(n)
    - Queue: O(n), $\Omega$(n)
  
### Hash Table

#### Time Complexity

- k: largest key
- m: size of the longest chain, often m = O(n)
- h: size of the table (not necessarily dependent on n)

- Search
    - Direct Address Table: O(1), $\Omega$(1) (All keys hashed to the corresponding index of the table)
    - Separate Chaining that holds nodes: O(m), $\Omega$(1) (Have to traverse the entirety of the longest chain in the worst case)
    - Separate Chaining that holds pointers: O(m), $\Omega$(1) (Same as the other separate chaining)
    - Linear probing: O(h), $\Omega$(1) (Have to probe through the entire table in the worst case, even if you encounter an empty cell in the process)

- Adding
    - Direct Address Table: O(1), $\Omega$(1) 
    - Separate Chaining that holds nodes: O(1), $\Omega$(1) (Could be O(m) if you add to the list tail instead of list head)
    - Separate Chaining that holds pointers: O(1), $\Omega$(1) (Same as other separate chaining)
    - Linear probing: O(h), $\Omega$(1) (In the worst case, the only empty cell is the one above where it's initially hashed, meaning you have to check h total cells when probing for an empty cell to add to)
 
- Removing
    - Direct Address Table: O(1), $\Omega$(1)
    - Separate Chaining that holds nodes: O(m), $\Omega$(1) (Have to traverse the longest chain in the worst case)
    - Separate Chaining that holds pointers: O(m), $\Omega$(1) (Same as other separate chaining)
    - Linear probing: O(h), $\Omega$(1) (Have to prove through the entire table in the worst case to search for the desired key to be removed)
 
#### Space Complexity

- Storing n nodes
    - Direct Address Table: O(k), $\Omega$(n) (worst-case is when the largest key is bigger than the number of elements, best-case is when the range of the keys is the same as n)
    - Separate Chaining that holds nodes: O(n), $\Omega$(n) (Have to store n nodes)
    - Separate Chaining that holds pointers: O(h + n), $\Omega$(max(h, n)) (Have to store h pointers and n nodes, have to add them both together in the complexity because it is ambiguous whether h or n will be bigger)
    - Linear Probing: O(h), $\Omega$(h) (Have to allocate space for the entire table, regardless of whether it is full or not)

## Topics on Complexity

### Binary Search Tree

#### Tree Height Complexities

- Tree Height
    - List-based: O(n), $\Omega$($\log{_2}{n}$) (Worst case is when it is a single child/single branch tree, best case is when it is balanced)
    - Array-based: O(n), $\Omega$($\log{_2}{n}$)

- Mathematical Derivation of Tree Height
    - A completely full tree has $n = 2^{h + 1} - 1$. Solving for h (Add 1 to both sides, taking the log of both sides, and then subtracting 1 from both sides), you get $h = \log{_2}{(n + 1)} - 1$

#### Time Complexity

- Search
    - List-based: O(h), $\Omega$(1) (Worst case is when you have to traverse the entire height of the tree, best case is when the target is at the root)
    - Array-based: O(h), $\Omega$(1)

- Adding
    - List-based: O(h), $\Omega$(1) (Worst case is when you have to traverse through the height of the tree, best case is when the root has a missing child and the new node can be added there)
    - Array-based: O(h), $\Omega$(1)

 - Remove
    - List-based: O(h), $\Omega$(h) (Have to travel down to the height of removed node, replace it with its inorder predecessor/successor further down the tree and repeat the process until the replacement is a leaf, meaning you have traveled down the full height)
    - Array-based: O(h), $\Omega$(h)

#### Space Complexity

- Storing n nodes
    - List-based: O(n), $\Omega$(n)
    - Array-based: O($2^n$), $\Omega$(n) (Worst case is when the tree is a single branch tree. The index of the last node in the worst case is $2^n - 1$, which means the array size is $2^n$ because you have to add in the zeroth index
 
### AVL

#### Tree Height Complexity

- Tree Height
    - List-based: O($\log{_2}{n}$), $\Omega$($\log{_2}{n}$) (Heights of left and right subtrees only differ by 1 so it guarantees a balanced tree)
    - Array-based: O($\log{_2}{n}$), $\Omega$($\log{_2}{n}$)

 #### Time Complexity

 - Search
    - List-based: O(h) = O($\log{_2}{n}$), $\Omega$(1) (Traverse through the whole height, which is always $\log{_2}{n}$)
    - Array-based: O(h) = O($\log{_2}{n}$), $\Omega$(1)
  
- Adding
    - List-based: O(h) = O($\log{_2}{n}$), $\Omega$(h) = $\Omega$($\log{_2}{n}$) (Have to traverse the entire height to add, then traverse back up to the root to check violations, even if there are no violations you still have to check all the way back up to the root)
    - Array-based: O(h) = O($\log{_2}{n}$), $\Omega$(h) = $\Omega$($\log{_2}{n}$)

- Removing
    - List-based: O(h) = O($\log{_2}{n}$), $\Omega$(h) = $\Omega$($\log{_2}{n}$)
    - Array-based: O(h) = O($\log{_2}{n}$), $\Omega$(h) = $\Omega$($\log{_2}{n}$)
 
#### Space Complexity

- Storing n nodes
    - List-based: O(n), $\Omega$(n)
    - Array-based: O($n^2$), $\Omega$($n^2$) (Worst case max index is $2^{h + 1} - 1$ where $h < 2 * \log{_2}{n}$. When plugging in $2 * \log{_2}{n}$ into the max index, you get $2n^2 - 1$ which is O(n^2)

### Red-Black Tree

#### Tree Height Complexity

- Tree Height
    - List-based: O($\log{_2}{n}$), $\Omega$($\log{_2}{n}$) 
    - Array-based: O($\log{_2}{n}$), $\Omega$($\log{_2}{n}$)
 
#### Time Complexity

- Search
    - List-based: O(h) = O($\log{_2}{n}$), $\Omega$(1)
    - Array-based: O(h) = O($\log{_2}{n}$), $\Omega$(1)

- Adding
    - List-based: O(h) = O($\log{_2}{n}$), $\Omega$($\log{_2}{n}$)
    - Array-based: O(h) = O($\log{_2}{n}$), $\Omega$($\log{_2}{n}$)

- Removing
    - List-based: O(h) = O($\log{_2}{n}$), $\Omega$($\log{_2}{n}$)
    - Array-based: O(h) = O($\log{_2}{n}$), $\Omega$($\log{_2}{n}$)

 #### Space Complexity
 
- Storing n nodes
    - List-based: O(n), $\Omega$(n) (Similar to AVL tree)
    - Array-based: O($n^2$), $\Omega$($n^2$)
 
### B-Tree

#### Tree Height Complexity

- Tree Height Complexity (with at most b - 1 keys per node)
    - List-based: O($\log{_2}{n}$), $\Omega$($\log{_b}{n}$) (Big O is worst case and the lower the base of a logarithmic function the faster it grows) 
    - Array-based: O($\log{_2}{n}$), $\Omega$($\log{_b}{n}$)

#### Time Complexity

- Search
    - List-based: O(h) = O($\log{_2}{n}$), $\Omega$(1) (Depends on worst case tree structure and worst case key location)
    - Array-based: O(h) = O($\log{_2}{n}$), $\Omega$(1)
 
- Adding
    - List-based: O(h) = O($\log{_2}{n}$), $\Omega$($\log{_b}{n}$)
    - Array-based: O(h) = O($\log{_2}{n}$), $\Omega$($\log{_b}{n}$)
 
- Removing
    - List-based: O(h) = O($\log{_2}{n}$), $\Omega$($\log{_b}{n}$) (Both adding and removing depend on worst case tree structure)
    - Array-based: O(h) = O($\log{_2}{n}$), $\Omega$($\log{_b}{n}$)
 
- Recovery (Split and Merge)
    - List-based: O($\log{_2}{n}$), $\Omega$(1) (In the worst case, you have to split and merge all the way back up to the root, best case is when there is no overflow and you don't need to split and merge)
    - Array-based: O($\log{_2}{n}$), $\Omega$(1)

 #### Space Complexity
 
- Storing n nodes
    - List-based: O(n), $\Omega$(n)
    - Array-based: O(n), $\Omega$(n)
 
### Min Heap

#### Tree Height Complexity

- Tree Height Complexity 
    - List-based: O($\log{_2}{n}$), $\Omega$($\log{_2}{n}$)
    - Array-based: O($\log{_2}{n}$), $\Omega$($\log{_2}{n}$)

#### Time Complexity
 
- Adding
    - List-based: O(h) = O($\log{_2}{n}$), $\Omega$(h) = $\Omega$($\log{_2}{n}$)
    - Array-based: O(h) = O($\log{_2}{n}$), $\Omega$(h) = $\Omega$($\log{_2}{n}$)
 
- Removing
    - List-based: O(h) = O($\log{_2}{n}$), $\Omega$(h) = $\Omega$($\log{_2}{n}$)
    - Array-based: O(h) = O($\log{_2}{n}$), $\Omega$(h) = $\Omega$($\log{_2}{n}$)

 #### Space Complexity
 
- Storing n nodes
    - List-based: O(n), $\Omega$(n)
    - Array-based: O(n), $\Omega$(n)
 
### Graph

- For list-based implementation, n is the number of pointers in the table
- m is the number of node objects (this also equals the number of edges in the graph)

#### Time Complexity

- Finding a Neighbor
    - Matrix-based: O(1), $\Omega$(1) (Given the origin and destination indices and you just go to that cell in the matrix and see if it has a nonzero edge)
    - List-based: O(n), $\Omega$(1)
 
- Depth-First Traverse 
    - Matrix-based: O($n^2$), $\Omega$($n^2$) 
    - List-based: O(n + m), $\Omega$(n + m)
 
- Breadth-First Traverse
    - Matrix-based: O($n^2$), $\Omega$($n^2$) 
    - List-based: O(n + m), $\Omega$(n + m)

 #### Space Complexity

- Depth-First Traverse with Stack based Implementation
    - Matrix-based: O(n), $\Omega$(n) (Storing a stack of size n for the number of nodes as well as a visited array of size n)
    - List-based: O(n), $\Omega$(n)

- Breadth-First Traverse with Queue based Implementation
    - Matrix-based: O(n), $\Omega$(n) (Storing a queue of size n for the number of nodes as well as a visited array of size n)
    - List-based: O(n), $\Omega$(n)

- Storing n nodes and m edges
    - Matrix-based: O($n^2$), $\Omega$($n^2$)
    - List-based: O(n + m), $\Omega$(n + m) (n is the number of pointers in the table and m is the number of nodes)
 
### Complexity of Search and Sorting on Array

#### Time Complexity

- Binary Search
    - O($\log{_2}{n}$)
    - $\Omega$(1)

- Bubble Sort
    - O($n^2$)
    - $\Omega$(n)

- Merge Sort
    - O($n \log{_2}{n}$)
    - $\Omega$($n \log{_2}{n}$)
 
- Counting Sort
    - O(n + m) (m is the largest key in the array, have to construct two array of size m and both count whether the i-th element is in the array for the first m-sized array and how many elements before the i-th cell are in the first m-size array for the second m-sized array)
    - $\Omega$(n + m)

#### Space Complexity

- Bubble Sort
    - O(1)
    - $\Omega$(1)
 
- Merge Sort
    - Operating on Lists: O($\log{_2}{n}$), $\Omega$($\log{_2}{n}$)
    - Operating on Arrays: O(n), $\Omega$(n) (Space complexity of merge phase is O(n) since you create copies of the two halves of the input array that add up to n, the recursive call stack is equal to the height of the decision tree, which is $\log{_2}{n}$, so it is O($\log{_2}{n}$). The total complexity is O(n) + O($\log{_2}{n}$) and O(n) dominates so the final space complexity ends up as O(n))
 
- Counting Sort
    - O(m) (m is the largest key, have to construct two arrays of size m to be able to 1. count how many times the i-th element appears in the input array and 2. count how many elements are in the input array before the i-th cell)
    - $\Omega$(m)

## Topics on Data Structures

### AVL

#### Definition
- AVL tree is a BST with an extra property that, for any node in the tree, the height of its left subtree and the height of its right subtree differ by at most one

#### Key Properties that Guarantee its Big O Height
- Consider a BST with n + 1 nodes and assume each subtree of the root is a single child tree. Without AVL property, all n nodes can go to the right subtree resulting in an "n" height tree. With the AVL property, about n/2 nodes can go to the right (so the heights of both the left subtree and the right subtree are about "n/2") resulting in an "n/2" height tree.

#### Rotations
- Rotations should reduce the height of the taller subtree by 1 while increasing the height of the smaller subtree by 1, thus restoring the AVL property
- Two rotations
    - Clockwise Rotation (used if the left subtree is taller)
    - Counterclockwise Rotation (used if the right subtree is taller)
Ex: 

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/7a744c4d-d3e2-4959-a11c-84a48b519827)

- Clockwise Rotation Pseudocode (Rotating node x)
    - **Creating temp variables**
    - Save x's left child's right child in a temp variable
    - Save x's parent in another temp variable
    - **Rebuilding links between x and its left child**
    - Assign x's left child's right pointer to point at x
    - Assign x's parent pointer to point at its old left child
    - **Rebuilding links between x's old left child and x's old parent**
    - Assign x's left child's parent pointer to x's old parent
    - Assign x's old parent's left/right pointer to x's left child
    - **Reconnect x's old left child's right child**
    - Assign x's left pointer to point at the temp variable that holds x's left child's right child

- Counterclockwise Rotation Pseudocode (Rotating node x)
    - **Creating temp variables**
    - Save x's right child's left child in a temp variable
    - Save x's parent in another temp variable
    - **Rebuilding links between x and its right child**
    - Assign x's right child's left pointer to point at x
    - Assign x's parent pointer to point at its old right child
    - **Rebuilding links between x's old right child and x's old parent**
    - Assign x's right child's parent pointer to x's old parent
    - Assign x's old parent's left/right pointer to x's right child
    - **Reconnect x's old right child's left child**
    - Assign x's right pointer to point at the temp variable that holds x's right child's left child
 
#### Know How to Check Violations
- Check the height of left and right subtrees by calling a function that calculates the height of a given tree on a node's left and right child, then compare their heights
- After a certain operation (adding or removal), check violations starting at the operated node's parent and working your way up to the root (check violations at the operated node's ancestors)
- To check height of a tree, initialize a height variable to -1 (to subtract the root's height contribution) and recursively call the height function on the node's left and right child, saving them in integer variables. Then, compare which is bigger and return the maximum of the two subtree heights + 1.
- The sequence of nodes to check violations is the path of ancestors from where you start all the way up to the root
    - For adding, you start at the added node's parent
    - For removal, you start at the deepest hole's parent (will be a leaf node's parent)

#### Know How to Find Max/Min Nodes
- Max
    - Keep traversing down the right child path until you are at a leaf node
- Min
    - Keep traversing down the left child path until you are at a leaf node
 
#### Know How to Add and Restore
- Perform regular BST adding
- Check for violations starting at the newly added node's parent
- Rotate if a violation is encountered

#### Know How to Remove and Restore
- Perform regular BST removal
- Check for violations starting at the deepest hole's parent
- Rotate if a violation is encountered

#### Violation Scenarios and Restoration Process
Four Scenarios (Violation occurs at node x)
- Left-Left: when x is left-heavy and its left child  is left-heavy, do single rotation (Clockwise rotation at node x)
- Right-Right: when x is right-heavy and its right child is right-heavy, do single rotation (Counterclockwise rotation at node x)
- Left-Right: when x is left-heavy and its left child is right-heavy, do double rotation (Counterclockwise rotation at x's left child, then clockwise rotation at node x)
- Right-Left: when x is right-heavy and its right child is left-heavy, do double rotation (Clockwise rotation at x's right child, then counterclockwise rotation at node x)

### Red-Black Tree

#### Definition
- Red-black tree is a BST with extra properties:
    - A node is colored either red or black
    - Root node is black
    - All leaf nodes are black (NIL)
    - A red node can only have black children
    - At each node, all paths to its descendant leaf nodes contain the same number of black nodes

#### Key Properties that Guarantee its Big O Height
- The property that all paths to any node's descendant leaf nodes contain the same number of black nodes directly encourages a short tree because if we remove all red nodes, it simply requires all leaf nodes to have the same depth (same as B-tree property)
- "Black-depth" of a leaf node (NIL node) is defined as the number of its black ancestors. In relation to the last property, this means that all leaf nodes have the same black depth

#### Know How to Add and Restore (All Cases) 
- Perform standard BST adding
- Color the new node red
- Check for violations

Three Violation Scenarios
1. Added node x is root
- Recolor newly added root as black
2. Parent is red, uncle is also red
- Recolor parent and uncle as black, then grandparent as red
- Check violation at grandparent after recoloring
3. Parent is red, uncle is black
- Rotation plus recoloring
- Rotation depends on four cases: LL, RR, LR, RL
    - Left-Left: Parent is left of grandparent and x is left of parent
    - Right-Right: Parent is right of grandparent and x is right of parent
    - Left-Right: Parent is left of grandparent and x is right of parent
    - Right-Left: Parent is right of grandparent and x is left of parent
- Left-Left: Clockwise rotation of grandparent, then swap colors of grandparent and parent
- Left-Right: Counterclockwise rotation of parent, then apply LL case
- For Right-Right and Right-Left, just mirror the cases for Left-Left and Left-Right respectively

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/705046f0-c6a5-41d5-b7f0-0b0197f19973)

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/92200567-af08-4250-b34f-bebf77ce95d9)

### B-Tree

#### Definition
- A B-tree is a generalization of a BST with the following properties:
    - A node can store up to k keys (a node with k keys is called a "k + 1-node")
    - A node with k keys must have k + 1 children, located between the sorted keys (Nodes between keys a and b are in (a, b))
    - All leaf nodes have the same depth (This encourages a small height)

#### Key Properties that Guarantee its Big O Height
- All leaf nodes having the same depth guarantees the Big O height

#### Know How to Add and Restore (For a 2-3 tree)
1. Each node can hold up to 2 keys, so we can add key to a 2-node or a child of a 3-node
2. Adding always starts from a leaf node found by a regular search algorithm (even if there is a regular 2-node on the search path)
3. If leaf is a 2-node, just add the key to it. If leaf is a 3-node, add the key as its child, which will break the property, and restore the property

Restoration After Adding to a 3-node
1. The 3-node has no parent (it is the root)
2. The 3-node has a 2-node parent
3. The 3-node has a 3-node parent

Case 1: 
1. Add key to the 3-node
2. Turn the middle key into 2-node root
3. Turn other two keys into 2-node children 

Case 2: 
1. Add key standardly
2. Split overflowed node
3. Merge new root into parent

Case 3: 
1. Add key standardly
2. Split overflowed node
3. Merge new root into parent
4. Repeat steps 2-3 until no violation

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/4bb24e9c-a865-4d2f-a76c-6c9673e027bf)

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/2cb64345-4167-4e20-9df9-c2531e058c2c)

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/8dc6a548-f7dc-424e-8312-4f3a56e283c7)

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/fb72777e-f527-442e-b475-8dc496273e7d)

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/56a372be-ef63-4b74-8de6-e1786be7af06)

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/2d0834a7-e592-4014-b377-b3d9b86a2e58)

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/e3996f0d-a2fd-4540-b79f-2d2cc82bcd6c)

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/80c8c646-b0ae-4537-a5e2-090dd61876d7)

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/c091ac60-3d24-493f-ac7f-966c51248706)

#### Know How to Remove and Restore
Strategy: Always delete a key at a leaf node. If it is not there, keep swapping it with its inorder predecessor/successor until it is swapped to a leaf node (then perform deletion)
- An inorder predecessor/successor is the key that is visited immediately before/after during the inorder traversal
Strategy for Deletion at a Leaf Node
- Case 1: Leaf is a 3-node
- Case 2: Leaf is a 2-node and both a sibling and parent are 3-nodes
- Case 3: Leaf is a 2-node and there is no sibling that is a 3-node but parent is

Case 1: Delete the key and the leaf becomes a 2-node

Case 2: Remove the key, fill the hole with the parent key and fill the parent hole with a key in the 3-node sibling

Case 3: Remove the key and merge a key from the parent and a sibling key into the hole

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/337de642-4b69-4912-954b-f5eb94b8e162)

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/9d734350-09d7-4128-8e62-79c4c788e81f)

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/c8e356f7-32b0-46f2-950d-4560c23673b4)

### Splay

#### Definition
- Splay tree is a BST with an extra property that every recently accessed node is moved to the root. The process of moving is called splaying. It is essentially a sequence of rotations that are designed in a principled way to make sure the rotated BST remains efficient for search on average case (amortized time)

#### Common Operations That Trigger Splaying
Three Operations That Trigger Splaying
- Search (Splay the node that you just searched for)
- Add (Splay the node that you just added)
- Remove (Splay the node you want to remove, then delete it, then splay the replacement)

#### Know How Splaying Works
Six scenarios for splaying node x (Dependent on x, parent, and grandparent)
1. X only has parent (left child) but not grandparent (L)
2. X only has parent (right child) but not grandparent (R)
3. X has both parent and grandparent where X is the left child of the parent and the parent is the left child of the grandparent (LL)
4. X has both parent and grandparent where X is the right child of the parent and the parent is the right child of the grandparent (RR)
5. X has both parent and grandparent where X is the left child of the parent and the parent is the right child of the grandparent (LR)
6. X has both parent and grandparent where X is the right child of the parent and the parent is the left child of the grandparent(RL)
- Scenarios 2, 4, and 6 are mirrors of 1, 3, and 5 respectively

Scenario 1: Clockwise rotation at the root

Scenario 3: Two clockwise rotations at the grandparent location

Scenario 6: First perform a counterclockwise rotation at the parent and then perform a clockwise rotation at the grandparent 

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/5c194b1c-10d0-4157-a855-30606e237213)

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/12bcb371-4cef-4a0c-93d1-fd73894a2f68)

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/2973649a-10dc-450f-a090-484b8bfac562)

#### Know That the Amortized Time Complexity of Each Operation is O($\log{_2}{n}$)

![image](https://github.com/TenHam3/CS2413-Study-Guide/assets/109705811/e8403ea1-5a83-4ed2-89c6-54b480348eb5)
