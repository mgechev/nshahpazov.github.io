---
layout: post
title: Linked List in Javascript
author: Nikola Shahpazov
modified:
excerpt:
tags: []
image:
  feature:
date: 2015-06-24T12:46:11+03:00
---

This is my first article, so I wanted it to set the mood for my entire blog and best describe what I'm passionate about, Computer Sciences in a modern web environment. I also wanted it to be an introduction article.

I assume all my readers know what an array is, so I decided to move to something very similar but in the same time describing an entirely different representation of a list.
By definition "linked list is a data structure consisting of a group of nodes which together represent a sequence. Under the simplest form, each node is composed of data and a reference (in other words, a link) to the next node in the sequence; more complex variants add additional links".

So lets start with the first thing. The Node. We want to represent a simple object consisting of data and a reference to another node.

// add a d3 floating node example here
{% highlight javascript %}
function Node(data) {
  this.data = data;
  this.next = null;
}
{% endhighlight %}

It can't get easier than that. A simple function constructor with data and a reference (next) to another node. But what we actually need is a function with which we can attach references.
{% highlight js %}
// our reference setter
Node.prototype.setNext(next) {
  this.next = next;
}
{% endhighlight %}


{% highlight js %}
Node.prototype.setNext(next) {
  this.next = next;
}
{% endhighlight %}

Lets see how it looks.

// Add d3 example here with a button which inserts new references to the last one. with dashed lines (it will be easier to see they are not in a list)

So far so good. The Node is the heart of the Linked List Data Structures which as you can see we are actually missing. So lets write it.

function LinkedList() {
  this.first = null;
  this.last = null;
  this.size = 0;
}

Of course, we'll need some method for adding a record to the list, the array's equivalent Array.prototype.push.

LinkedList.prototype.insert = function (data) {
  // if first is missing, make this first
// else attach it to last and increase size
}
// add button with example adding

// make an introduction to iteration and callback (high order functions)

LinkedList.prototype.forEach = function (callback) {
  var current = this.first;
  while (typeof current !== 'undefined') {
    var doesContinue = callback(current.data, current.index);
    if (!doesContinue) {
      break;
    }
    current = current.next;
  }
}

OK, so far we are able to add and iterate through the elements of the list, but what if we need to remove a record. We'll definitely need a method for removing a record, but by what "forgot the word"? Is it going to be by reference to the data, or by reference to the node?
/*Wouldn't it be best if we try to hide the implementation of the Node entirely in the curtains of the LinkedList class and just show the data? */

// code for removal of a node by reference to the object

// add a d3 example

Why don't we make a generic removal method which removes by a callback function? Lets try.

LinkedList.prototype.remove = function (callback) {

}

// show list of lists

// show insertion sort