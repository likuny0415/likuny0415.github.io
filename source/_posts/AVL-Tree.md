---
title: AVL Tree
date: 2021-04-26 11:26:56
tags: Data Structure
---

# Binary Tree

What **search algorithm** depends?
- Depends on the height of the tree

What is **height** range?
- Min logN
- Max n

What is the **problem** of Binary Tree?
- It is highly flexible
E.g
30 40 10 50 20 5 35 -- Time->logN   
50 40 35 30 20 10 5 -- Time->N

# AVL Tree
**Definition** of AVL Tree
- Balance factor = height of left subtree - height of right subtree
- Balance factor in [-1, 0 , 1] is a balanced tree

**Rotation** in AVL
- Four types
    - LL
        - Single rotation
    - LR
        - Double rotation
    - RR
        - Single rotation
    - RL
        - Double rotation

# Huffman coding
What it used for?
- For compressing message and reduce the cost of tranmission

How to use it?
- If a message contains 5 characters, than we use 3 bits(can have 7 different representation) to represent it instead of 8 bits(ASCII)

How to build a **Huffman coding**?
- Lettere with least number of count on the right
- combining characters count with minimum
- Build a tree
- Left subtree labled 0 and right subtree labled 1
- Each character has a unique bit representation (bit reduce)
- Send the table and message to the receiver
