---
layout: post
title: "CS: trees, binary trees and tries"
date: 2015-04-01 10:52:38 -0400
comments: true
categories:
---

<i>Note: Most of this information was gained from a basic Google search and is presented here for the sake of distilling some basic concepts of computer science into an easily understandable form. This post concerns Tree data structures.</i>

<b>to do: fill out citations, show code snippets from GA exercises, finish tries section, add a little somethin'-somethin' on graph theory.</b>

<strong>tree/shameless Laruelle plug:</strong>[^1]
<img src="http://rosettacode.org/mw/images/d/d7/Fractal_tree.svg">

<h2>Trees</h2>
<p>A tree is a data structure that consists of a parent or root node which stores a data element and which possesses at least one child or branch. These child nodes in turn possess their own values and may have their own children (note: all nodes have 1 parent except for the root node which has 0).</p>

<p>Trees are particularly useful for storing heirarchically arranged data. They are also very human readable since their visual organization resembles that of an actual tree. Further, for a relatively complex data structure (relative to a stack or queue) they can be traversed or "<a href="http://en.wikipedia.org/wiki/Tree_traversal">walked</a>" through relatively quickly, although this is highly dependent on their depth. Further, in the case of natural language processing, a large corpus of text can be stored as a tree which significantly reduces the query time required to find a sequence of words (as is the case with <a href="http://en.wikipedia.org/wiki/N-gram"><i>n</i>-grams)</a> and the memory requirements for its storage.</p>

Since this terminology can become somewhat convoluted I've provided a list of terms (note: these terms courtesy of the internet).[^2]

<strong>Tree terminology:</strong>
<li>Node: stores a data element</li>
<li>Parent: single node that directly precedes a node</li>
<li>Child: one or more nodes that directly follow a node</li>
<li>Ancestory: any node which precedes a node (itself, its parent, or an ancestory of its parent</li>
<li>Descendent: any node which follows a node (itself, its child, or a descendent of its child</li>
<li>Leaf (external node): node with no children</li>
<li>Internal node: non-leaf node</li>
<li>Siblings: nodes which share some parent</li>
<li>Subtree: a node and all its descendents</li>
<li>Ordered tree: a tree with definied order of children</li>
<li>Binary tree: ordered tree with up to two children per node</li>

<p>Practically, trees are implemented via recursion (where the function that creates the branch is called within the function itself) and a conditional sorting method.</p>

<h2>Two types of trees</h2>

<p>There are a variety of tree types, however, here we will address two simple types: the binary tree, which accordingly is a tree with a left and right branch, and a trie, which unhappily is far more complex (note: evidently the word "trie" comes from the word "retrieval" it can be pronounced either "try" or "tree" but definitively does not have a relationship with the word "tri" as in "tricycle"). For our purposes we will focus on tries for the rest of the article (although binary trees are certainly <a href="http://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees">varied</a> and <a href="http://mathworld.wolfram.com/BinaryTree.html">complicated</a> in their own right).</p>

<div class="picture-column-1">
<strong>Binary tree:</strong>

<img width="330" src="http://upload.wikimedia.org/wikipedia/commons/6/67/Sorted_binary_tree.svg">
</div>
<div class="picture-column-2">
<strong>Trie:</strong>
<img width="355" height="300" src="http://i.stack.imgur.com/KhvoF.png">
</div>
<h2>Tries</h2>

What is immediately distinguishing about a trie vs. a binary tree is that values are not stored at nodes but are rather indicated by the nodes position in the tree: "Unlike a binary search tree, no node in the tree stores the key associated with that node; instead, its position in the tree defines the key with which it is associated. All the descendants of a node have a common prefix of the string associated with that node, and the root is associated with the empty string. Values are normally not associated with every node, only with leaves and some inner nodes that correspond to keys of interest."[^3] Common applications for tries are for autocompletion or for storing predictive text.

More on this later (with code snippets and more!)

[^1]: <a href="http://www.amazon.com/Philosophy-Non-Philosophy-Univocal-Fran%C3%A7ois-Laruelle/dp/1937561127/ref=pd_bxgy_b_img_y">http://www.amazon.com/Philosophy-Non-Philosophy-Univocal-Fran%C3%A7ois-Laruelle/dp/1937561127/ref=pd_bxgy_b_img_y</a>

[^2]: 
[^3]: <a href="http://en.wikipedia.org/wiki/Trie">http://en.wikipedia.org/wiki/Trie</a>
