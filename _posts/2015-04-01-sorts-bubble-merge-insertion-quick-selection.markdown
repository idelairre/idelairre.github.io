---
layout: post
title: "CS: bubble, merge, insertion, quick, and selection sorts"
date: 2015-04-01 10:52:38 -0400
comments: true
categories:
---

<i>Note: Most of this information was gained from a basic Google search and is presented here for the sake of distilling some basic concepts of computer science into an easily understandable form. This post concerns the variety of sort types.</i>

<b>to do: shorten bubble sort, finish selection sort (its just citations at the moment), show code snippets from GA exercises, get computer science degree.</b>

<h2>Bubble sort</h2>

The first sorting method we will deal with is the bubble sort. For something like this I immediately want to know why it is called a bubble sort. Fortunately the good folks at wikibooks have an answer: "The bubble sort gets its name because elements tend to move up into the correct order like bubbles rising to the surface."[^1] Interesting, so why does it have this behavior? The scary-smart brogrammer (who like myself could use some decent acne wash) who does the Harvard CS50 course explains: "the right most elements are garaunteed to be in their correct place." He then takes the worst case scenario for sorting an array of numbers (the case that involves the most iterations) to demonstrate.

If we have an array ```[9, 6, 5, 3, 2]``` and we iterate once then we have ```[6, 9, 5, 3, 2]``` on the next pass we have ```[6, 5, 9, 3, 2]```. We can already see the ```9``` being passed to the right on each iteration so that it appears to "bubble" towards the right. 

On the next iteration we have ```[6, 5, 3, 9, 2]``` and finally ```[6, 5, 3, 2, 9]```. On the next iteration it will start with ```6``` thus, ```[5, 6, 3, 2, 9]``` then ```[5, 3, 6, 2, 9]``` and so on. This is clearly a very "expensive" operation (least not indicated because it was very tedious to type all those iterations). As such, its run time O of n is On<sup>2</sup>, checking every element through each iteration.

<strong>Bubble sort in action:</strong>[^2]
<img src="http://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif">

A "naive" or simple sorting algorithm would check all the elements of the array. However, knowing that the right most element is already sorted allows for a slight optimization. One can optimize again with flags and counters. At risk of repeating everything our clever bro says in the movie, I'll allow you to check it out yourself.[^3] Also checkout wikipedia's <a href="http://en.wikipedia.org/wiki/Bubble_sort#Optimizing_bubble_sort">article on optimizing bubble sorts.</a>

<h2>Merge Sort</h2>

A merge sort, as the name suggests, merges two sorted lists. Since there is a major time crunch on this assignment, I'll again stick closely to the CS50 examples (this time featuring a brogrammer in an American Eagle polo his mom probably got for him in high school, but my God is he sexy smart).

Supposing you have two already sorted lists ```[4, 15, 16, 50]``` and ```[8, 23, 42, 108]```, since they are already sorted (with the smallest elements at the left of the list) you can take each first element of the two lists and compare whether one is larger than the other. ```4``` is smaller so it  is entered as the first element of the new sorted list. The next task is to compare whether ```8``` is larger or smaller than ```15```. Since ```8``` is smaller it enters the sorted list as the second element and so forth.

The basic pseudo code for this sorting algorithm is to compare the first two elements of each list and remove the smaller of the two. 

On the first comparison you would have ```[4, 8]``` with the two remaining arrays being ```[15, 16, 50]``` and ```[23, 42, 108]```.  On the second comparison you would have ```[4, 8, 15, 16]``` with the two remaining arrays being ```[50]``` and ```[42, 108]```. On the third comparison you would have ```[4, 8, 15, 16]``` with the two remaining arrays being ```[50]``` and ```[42, 108]``` and so on.

So after iterating through each list our final result would naturally be ```[4, 8, 15, 16, 23, 42, 50, 108]```.

<strong>Merge sort in action:</strong>[^4]
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Merge_sort_animation2.gif/220px-Merge_sort_animation2.gif">

Assuming a less ideal situation where the same numbers are out of order in a single list, we need to adjust the algorithm. Here, our nerdcore brogrammer produces the list ```[108, 15, 50, 4, 8, 42, 23, 16]```.

* First we must split the lists in half until we have <i>n</i> number lists for <i>n</i> number elements: ```[108][15][50][4][8][42][23][16]```

* Step two uses basically the same algorithm as before: the first two elements of two given lists are compared and the smaller one is entered as the first element of a new sorted list until all lists are of size 2: ```[15, 108][4, 50][8, 42][16, 23]```

* Step three is to repeat this process until the lists are of size 4: ```[4, 15, 50, 108][8, 16, 23, 42]```.

* Step four concludes the first pass by producing a single sorted list: ```[4, 8, 15, 16, 23, 42, 50, 108]```

So actually this is rather fast: O(<i>n</i> log <i>n</i>). But  the speed trade off are its memory requirements since it has to make new lists and store them in memory. Further, the use cases for merge sort may be limited since they tend to become inefficient for lists larger than 50 and are not universally faster than other algorithms with all unsorted lists.

If you somehow found this useful than I don't recommend watching the video, however, if you want to watch our brogrammers adorable blooper reel, definitely checkout the <a href="https://www.youtube.com/watch?v=EeQ8pwjQxTM">CS50 video</a>.

<h2>Insertion sort: the most phallogocentric sorting method</h2>

An insertion sort iterates through an unsorted list one element at a time, grabbing it and determining its correct position in the sorted array. This is done by determing if it is larger or smaller than the first element in the sorted list. If it larger, it compares itself against the next element in the list until it finds an element larger than itself, in this case, it inserts itself in front of that element.[^5]

As such it is hardly an efficient algorithm. However, it can be faster than more advanced algorithms with very small data sets. Further, it is an incredibly simple program to write. Wikipedia notes that there is a three-line C version (which must be nothing short of a miracle).[^6] Another advantage is that the sorted list is always sorted since it always puts the new element in the right order.

<strong>insertion sort in action:</strong>[^7]
<img src="http://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif">

So much for insertion sort.

<h2>Quick sort</h2>

<i>Note: this sort method is really difficult to explain so I feel it is best to start with its terms. In this instance I find it useful to "bruteforce" my understanding with a lot of different examples. <a href="https://www.youtube.com/watch?v=3OLTJlwyIqQ">This video</a> was particularly helpful.</i>

<strong>quick sort terms:</strong>

* pivot: the element being sorted
* wall: the end of the list
* current element: leftmost element

Firstly, it is important to note that all elements to the right of the wall are bigger than then the the elements to the left.

Quick sort takes the "pivot" element and compares its size against the element against the "wall" to see if it is larger than it. If it isn't than it counts up the list until it finds such an element. When it finds it, it takes that element and puts it against the wall and takes the element previously against the wall and places it in the index of the swapped number, the wall then moves up to the next position in the list.

If no other elements on the right side of the wall are larger then the algorithm takes the pivot element and swaps it with the first item to the right of the wall and the wall moves up accordingly.


This algorithm is has the potential to be somewhat expensive in the worst, worst case scenario. Thus to increase the efficiency of this sort, one can use an inexpensive search to find the median value of the elements of the array to use as the pivot.[^8]

Definitely check out this <a href="http://cs.stackexchange.com/questions/3/why-is-quicksort-better-than-other-sorting-algorithms-in-practice">stack exchange post</a> if runtime and efficiency interests you.

<strong>quick sort:</strong>[^9]
<img src="http://www.lisdn.com/attachments/2013/07/1_2013070813412612CE8.gif">

<h2>Selection Sort</h2>

"Selection sort is one way to sort an array of numbers. Data is divided into sorted and unsorted portions. One by one, the smallest values remaining in the unsorted portion are selected and swapped over to the sorted portion of the array."[^10]

* First, scan the unsorted portion of the array to find the smallest value.

* Swap that value with the first unsorted value -- it is now part of the sorted subarray.

* Repeat until there are no more values in the unsorted portion of the array.

"In both the best and worst cases, we'd have to compare each element to every other element in the unsorted subarray to ensure that the smallest value is selected on each iteration. As such, the selection sort algorithm takes n2 in the best and worst cases."[^11]


Since the best and worst case runtimes of selection sort are equivalent, the expected runtime is Θ(n2)

<strong>selection sort in action:</strong>[^12]
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/b/b0/Selection_sort_animation.gif/250px-Selection_sort_animation.gif">

[^1]: <a href="http://en.wikibooks.org/wiki/Algorithm_Implementation/Sorting/Bubble_sort">http://en.wikibooks.org/wiki/Algorithm_Implementation/Sorting/Bubble_sort</a>

[^2]: <a href="http://en.wikipedia.org/wiki/Bubble_sort#Analysis">http://en.wikipedia.org/wiki/Bubble_sort#Analysis</a>

[^3]: <a href="https://www.youtube.com/watch?v=8Kp-8OGwphY">https://www.youtube.com/watch?v=8Kp-8OGwphY</a>. See also: <a href="https://study.cs50.net/bubble_sort">https://study.cs50.net/bubble_sort</a>.

[^4]: <a href="http://en.wikipedia.org/wiki/Merge_sort">http://en.wikipedia.org/wiki/Merge_sort</a>

[^5]: for the wonderful ambiguity of the term "ahead" or "behind" and some excellent intellectual penis jokes checkout Derrida's <a href="http://www.scribd.com/doc/39065838/Derrida-The-Postcard#scribd"><i>Postcard</i></a>

[^6]: <a href="http://en.wikipedia.org/wiki/Insertion_sort">http://en.wikipedia.org/wiki/Insertion_sort</a>

[^7]: <a href="http://en.wikipedia.org/wiki/Insertion_sort#Algorithm">http://en.wikipedia.org/wiki/Insertion_sort#Algorithm</a>

[^8]: <a href="https://www.youtube.com/watch?v=aQiWF4E8flQ">https://www.youtube.com/watch?v=aQiWF4E8flQ</a>

[^9]: Note: the website I got this from is in Chinese <a href="http://www.lisdn.com/">http://www.lisdn.com/</a>

[^10]: <a href="https://study.cs50.net/selection_sort">https://study.cs50.net/selection_sort</a>

[^11]: ibid.

[^12]: <a href="http://en.wikipedia.org/wiki/Selection_sort">http://en.wikipedia.org/wiki/Selection_sort</a>