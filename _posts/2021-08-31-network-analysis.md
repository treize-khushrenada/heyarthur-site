---
title: "understanding network/ graph analysis"
excerpt_separator: "<!--more-->"
date: 2021-08-31T15:34:30-04:00
categories:
  - Draft
tags:
  - 
header:
  image: /assets/images/carambola-1.png
---

### What to expect:
- 
- 

---

what is a network
representation of connections among a set of items
lines are the edges/ link/ tie, they are the connections
items are called nodes or vertices

small network are still feasible to look at inter relationships and make sense

when it comes to big data, visualization becomes a problem, there are too many nodes and connections

application and questions to ask:
how to identify the subgroups from a network
email communication- rumor spreading?
is a social group likely to split?
where are the centroids in the network?


some networks are more symmetric, some are asym (there's a direction between nodes, no source or destination)
some connections can be attached with a number to indicate the weights (weighted networks), or signed (positive / negative)

mutigraphs (parallel edges) are where multiple connection types applied to the same nodes

path: a seq of nodes connected by an edge

2 properties of connected component:
1. every node in the subset has a path to every other node
2. no other node has a path to any node in the subset (make sure we are grabbing the largest component in the network)

weakly v.s. strongly connected in directed graph
weakly when ignore the directions

distance in a network: use the idea of path to measure the distance, path length is the number of hops between the source and target nodes

BFS algorithm: discover the new nodes in length first, until no new nodes to be discovered. and find the distance from A to B at the end

Average distance: calculate distances between all possible pairs and average out

Diameter: max distance between any pair of nodes (a common practice is to take the large connected component it there are disconnected subgroups)