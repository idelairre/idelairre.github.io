---
layout: post
title: "CS: abstract data types"
date: 2015-04-01 10:52:38 -0400
comments: true
categories:
---

<i>Note: Most of this information was gained from a basic Google search and is presented here for the sake of distilling some basic concepts of computer science into an easily understandable form. This post concerns Abstract Data Types or ADTs.</i>
<h2>Queues</h2>

A queue is a simple data type which functions basically as a line (e.g., a line of cars at a tollbooth or line for a bank teller) where linearly or sequentially ordered elements are added on one end and retrieved at the other (another term for this type of data structure is “sequential collection”).[^1] Operations on the queue are limited to two types: adding elements to the end (called enqueuing) and the removal of elements from the front (dequeuing).[^2] As such, a queue is an example of a “First-In-First-Out (FIFO)” data structure where “the first element added to the queue will be the first element removed.” Queues are useful when only limited computing resources are available or can only handle a limited number of requests. In situations where system resources are scarce, the order of the data must be maintained and timeliness isn’t an issue, queues can be an appropriate way to process something like server requests.[^3]

<!-- more -->

<strong>queue:</strong>

<img src="http://upload.wikimedia.org/wikipedia/commons/5/52/Data_Queue.svg">

<h2>Stacks</h2>

Queues are similar to stacks (they are both sequential collections and linear data structures) with the primary difference being that a stack is a “Last-In-First-Out” (LIFO) as opposed to FIFO data structure. Or rephrased, all the operations on a stack are done at the end or back of the collection whereas in a queue they are performed at the front and back. Again rephrased, in a queue, operations on the first element are processed first whereas, in a stack, operations are performed on the last or most recently added element first. Stacks are also limited to two operations: “pushing” and “popping.” A push adds an element to a collection, whereas a pop removes the last element that was added. Stacks can be implemented when task priority is important (e.g., from a user experience standpoint, the most recent request to a server should be processed first) or the tasks are event-based (where certain event-based operations should be processed immediately rather than queued).

<strong>stack:</strong>

<img src="http://upload.wikimedia.org/wikipedia/commons/2/29/Data_stack.svg">

<h2>Linked List</h2>

A more versatile data type (in the sense that operations can be performed at any place in the collection) is the linked list. Linked lists also possess the benefit that one does not need to specify a fixed size of the list (as is the case with arrays). As such it has more intuitive behavior than an array, i.e., adding elements to the list causes the list to get bigger. Since linked lists are comprised of nodes “linked” together in a sequence insertion and deletion can occur at any part of the collection by using the appropriate node as a reference (e.g., the C functions “insertBefore()” and “insertAfter()” which take a node as a parameter).[^4] Linked lists can also be copied, searched and or merged with other lists into a larger list. Each node (with the exception of the last element) possesses a reference which links it to the next node in the sequence. Linked lists can be linked in a linear (where the last element has “null” for a reference) or circular fashion (where the last element has a reference to the first or header node) and singly and doubly linked. Singly linked lists can only be traversed in one direction (left to right) whereas doubly linked lists can be traversed in any direction. Linked lists are a preferable data type when:

<li>time predictability is crucial since the O of n is constant</li>
<li>you don’t need to index the values of the array
when you don’t know how many items will be in your list</li>
<li>when you need to insert items at any point in the list</li>

<strong>linked list:</strong>

<img src="http://mike-lipman.com/images/linked-list.png">

[^1]: <a href="http://sdmeta.gforge.inria.fr/FreeBooks/Joy/11.pdf">http://sdmeta.gforge.inria.fr/FreeBooks/Joy/11.pdf</a>

[^2]: <a href="http://en.wikipedia.org/wiki/Queue_(abstract_data_type)">http://en.wikipedia.org/wiki/Queue_(abstract_data_type)</a>

[^3]: <a href="http://stackoverflow.com/questions/7431054/when-where-how-should-queues-be-used">http://stackoverflow.com/questions/7431054/when-where-how-should-queues-be-used</a>

[^4]: <a href="https://books.google.com/books?id=NdVS88muul4C&printsec=frontcover#v=onepage&q&f=false">https://books.google.com/books?id=NdVS88muul4C&printsec=frontcover#v=onepage&q&f=false"</a>
