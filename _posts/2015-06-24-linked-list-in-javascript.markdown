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
<style>

.node {
  stroke: #fff;
  stroke-width: 1.5px;
}

.link {
  stroke: #999;
  stroke-opacity: .6;
}

</style>
<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.5/d3.min.js" charset="utf-8"></script>
<script>
  var graph = {
  "nodes":[
    {"name":"1","group":1},
    {"name":"2","group":4},
    {"name":"3","group":5},
    {"name":"4","group":7},
  ],
  "links":[
    {"source":1,"target":0,"value": 100},
    {"source":1,"target":2,"value": 100},
    {"source":2,"target":3,"value": 100}
  ]
}
  document.addEventListener("DOMContentLoaded", function(event) {
    console.log("DOM fully loaded and parsed");
    var x = document.querySelectorAll("#canvas");
    debugger;

  var width = 960,
    height = 500;

var color = d3.scale.category20();

var force = d3.layout.force()
    .charge(-800)
    .linkDistance(400)
    .size([width, height]);

var svg = d3.select("#canvas").append("svg")
    .attr("width", width)
    .attr("height", height);

  force
      .nodes(graph.nodes)
      .links(graph.links)
      .start();

  var link = svg.selectAll(".link")
      .data(graph.links)
    .enter().append("line")
      .attr("class", "link")
      .style("stroke-width", function(d) { return Math.sqrt(d.value); });

  var node = svg.selectAll(".node")
      .data(graph.nodes)
    .enter().append("circle")
      .attr("class", "node")
      .attr("r", 30)
      .style("fill", function (d) { return color(d.group); })
      .call(force.drag);

  node.append("title")
      .text(function(d) { return d.name; });

  force.on("tick", function() {
    link.attr("x1", function(d) { return d.source.x; })
        .attr("y1", function(d) { return d.source.y; })
        .attr("x2", function(d) { return d.target.x; })
        .attr("y2", function(d) { return d.target.y; });

    node.attr("cx", function(d) { return d.x; })
        .attr("cy", function(d) { return d.y; });
  });
});
</script>

This is my first article, so I wanted it to set the mood for my entire blog and best describe what I'm passionate about, Computer Sciences in a modern web environment. I also wanted it to be an introduction article.<br/>


I assume all of my readers know what an array is, so I decided to move to something very similar but in the same time describing an entirely different representation of a list.
By definition "linked list is a data structure consisting of a group of nodes which together represent a sequence. Under the simplest form, each node is composed of data and a reference (in other words, a link) to the next node in the sequence; more complex variants add additional links". So lets start with the first thing.

###The Node.

We want to represent a simple object consisting of data and a reference to another node.
<div id="canvas"></div>
// add a d3 floating node example here
{% highlight javascript %}
function Node(data) {
  this.data = data;
  this.next = null;
}
{% endhighlight %}

<h1>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Excepturi harum cum, maiores vel expedita praesentium quos officiis, nisi cupiditate esse, natus vitae itaque nam sunt accusantium est aut sed voluptatibus.</h1>

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

So far so good. The Node is the heart of the Linked List Data Structures which as you can see we are actually missing.

##Linked List

{% highlight js %}
function LinkedList() {
  this.first = null;
  this.last = null;
  this.size = 0;
}
{% endhighlight %}


Of course, we'll need some method for adding a record to the list, the array's equivalent Array.prototype.push.

{% highlight js %}
LinkedList.prototype.insert = function (data) {
  // if first is missing, make this first
// else attach it to last and increase size
}
{% endhighlight %}

// add button with example adding

// make an introduction to iteration and callback (high order functions)

{% highlight js %}
LinkedList.prototype.forEach = function (callback) {
  var current = this.first,
      doesContinue;
  while (current) {
    doesContinue = callback(current.data, current.index);
    if (doesContinue === false) {
      break;
    }
    current = current.next;
  }
}
{% endhighlight %}


OK, so far we are able to add and iterate through the elements of the list, but what if we need to remove a record. We'll definitely need a method for removing a record, but by what "forgot the word"? Is it going to be by reference to the data, or by reference to the node?
/*Wouldn't it be best if we try to hide the implementation of the Node entirely in the curtains of the LinkedList class and just show the data? */

// code for removal of a node by reference to the object
// add a d3 example

Why don't we make a generic removal method which removes by a callback function? Lets try.

{% highlight js %}
LinkedList.prototype.remove = function (callback) {

}
{% endhighlight %}

// show list of lists

// show insertion sort