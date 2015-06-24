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

.btn {
  border-radius: 12px;
  background-color: #336699;
  cursor: pointer;
}

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
    {"name": "1", "group": 1}
  ],
  "links":[
    // {"source":1,"target":0,"value": 100},
    ]
  }

  function Canvas(id, width, height) {
    this.data = {
      nodes: [],
      links: []
    };
    this.size = 0;

    this.force = d3.layout.force()
      .charge(-200)
      .linkDistance(40)
      .size([width, height]);

    this.svg = d3.select(id).append("svg")
        .attr("width", width)
        .attr("height", height);
  }

  // static color for all
  Canvas.color = d3.scale.category20();

  Canvas.prototype.redraw = function () {

    this.node = this.node.data(this.data.nodes);
    this.node.enter().insert("circle")
      .attr("class", "node")
      .attr("r", 15)
      .style("fill", function (d) {
        return Canvas.color(d.group);
      })
      .call(this.force.drag);

    this.link = this.link.data(this.data.links);
    this.link.enter().insert("line", ".node")
      .attr("class", "link");

    this.force.start();
  }

  Canvas.prototype.addNode = function (node) {
    this.data.nodes.push(node);
    // this.redraw();
    // this.start();
    this.size++;
  };

  Canvas.prototype.addEdge = function (edge) {
    this.data.links.push(edge);
    // return this.redraw();
    // this.start();
  };

  Canvas.prototype.start = function () {
    var self = this;
    this.force.nodes(this.data.nodes)
      .links(this.data.links)
      .start();

    this.link = this.svg.selectAll(".link")
    .data(this.data.links)
    .enter().append("line")
      .attr("class", "link")
      .style("stroke-width", function (d) {
        return Math.sqrt(d.value);
      });

      this.node = this.svg.selectAll(".node")
        .data(this.data.nodes)
        .enter().append("circle")
          .attr("class", "node")
          .attr("r", 15)
          .style("fill", function (d) { return Canvas.color(d.group); })
          .call(this.force.drag);

      // node.append("title")
      //     .text(function (d) { return d.name; });

      this.force.on("tick", function() {
        self.link.attr("x1", function (d) { return d.source.x; })
            .attr("y1", function (d) { return d.source.y; })
            .attr("x2", function (d) { return d.target.x; })
            .attr("y2", function (d) { return d.target.y; });

        self.node.attr("cx", function(d) { return d.x; })
            .attr("cy", function(d) { return d.y; });
      });
  };

  document.addEventListener("DOMContentLoaded", function (event) {
    var secondCanvas = new Canvas("#second-canvas", 678, 300);
    secondCanvas.data.nodes.push({name: 'sss', group: 1});
    secondCanvas.start();
    // secondCanvas.addNode({"name": "1" + Math.random() * 130, "group": 1});

    document.querySelector('#second-btn')
    .addEventListener('click', function (event) {
      // secondCanvas.data.nodes.push({name: "ala", group: 1});
      var group = parseInt(Math.random() * 356);
      secondCanvas.addNode({name: "ala", group: group});
      secondCanvas.addEdge({source: secondCanvas.size - 1, target: secondCanvas.size});
      secondCanvas.redraw();
    });

    var width = 678,
        height = 200,
        color = d3.scale.category20();

    var force = d3.layout.force()
        .charge(-800)
        .linkDistance(400)
        .size([width, height]);

    var svg = d3.select(".node-canvas").append("svg")
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
          .style("stroke-width", function (d) {
            return Math.sqrt(d.value);
          });

      var node = svg.selectAll(".node")
          .data(graph.nodes)
        .enter().append("circle")
          .attr("class", "node")
          .attr("r", 15)
           // .attr("transform", function(d) {
           //    return "translate(" + d.x + "," + d.y + ")";
           //  })
          .style("fill", function (d) { return color(d.group); })
          .call(force.drag);

      node.append("title")
          .text(function(d) { return d.name; });

      force.on("tick", function() {
        link.attr("x1", function (d) { return d.source.x; })
            .attr("y1", function (d) { return d.source.y; })
            .attr("x2", function (d) { return d.target.x; })
            .attr("y2", function (d) { return d.target.y; });

        node.attr("cx", function(d) { return d.x; })
            .attr("cy", function(d) { return d.y; });
      });

      function redraw() {
        node = node.data(graph.nodes);
        node.enter().insert("circle")
          .attr("class", "node")
          .attr("r", 1)
          .transition()
          .duration(4000)
          .ease("elastic")
          .style("fill", function (d) { return color(d.group); })
          .attr("r", 15);

        // node.exit().transition()
        //   .attr("r", 0)
        //   .remove();

        force.start();
      }

      // ** Update data section (Called from the onclick)
    var btn = document.querySelectorAll("#add-new-node-btn")[0];
      btn.addEventListener('click', function (ev) {
      var group = parseInt(Math.random() * 356);
      console.log(group);
      graph.nodes.push({name: '' + group, group: group});
      redraw();
    });
  });
</script>

This is my first article, so I wanted it to set the mood for my entire blog and best describe what I'm passionate about, Computer Sciences in a modern web environment. I also wanted it to be an introduction article.<br/>


I assume all of my readers know what an array is, so I decided to move to something very similar but in the same time describing an entirely different representation of a list.
By definition "linked list is a data structure consisting of a group of nodes which together represent a sequence. Under the simplest form, each node is composed of data and a reference (in other words, a link) to the next node in the sequence; more complex variants add additional links". So lets start with the first thing.

###The Node.

We want to represent a simple object consisting of data and a reference to another node.

// add a d3 floating node example here
{% highlight javascript %}
function Node(data) {
  this.data = data;
  this.next = null;
}
{% endhighlight %}

<div id="single-node-canvas" class="node-canvas"></div>
<a class="btn" id="add-new-node-btn">Add New One</a>
<br>

It can't get easier than that. A simple function constructor with data and a reference (next) to another node. But what we actually need is a function with which we can attach references.

{% highlight js %}
// our reference setter
Node.prototype.setNext(next) {
  this.next = next;
}
{% endhighlight %}

Lets see how it looks when we use it.
<div id="second-canvas" class="node-canvas"></div>
<a id="second-btn" class="btn">Add New One</a>

The Node is the heart of the linked list data structure and as you can see we are only inserting at the end of the last inserted node.
OK. Lets wrap what we have so far in a LinkedList class constructor.

{% highlight js %}
function LinkedList() {
  this.first = null;
  this.last = null;
  this.size = 0;
}
{% endhighlight %}

At this point you are probably thinking. "Wait a minute! This thing starts to look a lot like an array!! What is the point of all of this?!?"<br/>
<p><br></p>

I am showing you all this because there's a fundamental concept in the Linked List. And that is the reference. In an array we have cells with data where we can query whichever element of the array as long as we know it's index. Here we have a reference connected to a reference, connected to a reference and so on. It's an entirely different view on the matter of connection of objects.



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