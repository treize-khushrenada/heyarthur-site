---
title: "Dealing with Network Data- Understanding Network/ Graph Analysis"
excerpt_separator: "<!--more-->"
date: 2021-09-15T15:34:30-04:00
categories:
  - Blog
tags:
  - 
header:
  image: /assets/images/spider-man-analyzing-the-web.png
---

### What to expect:
- Understand basic concepts and key components in network/ graph data models
- How to simulate network diffusion 
- How to detect network and create clusters based on algorithms

---

What is a network?
- representation of connections among a set of items
- lines are the edges/ link/ tie, they are the connections
- items are called nodes or vertices

- small network are still feasible to look at inter relationships and make sense

when it comes to big data, visualization becomes a problem, there are too many nodes and connections

application and questions to ask:
how to identify the subgroups from a network
email communication- rumor spreading?
is a social group likely to split?
where are the centroids in the network?

some networks are more symmetric, some are async (there's a direction between nodes, no source or destination)
some connections can be attached with a number to indicate the weights (weighted networks), or signed (positive / negative)

mutigraphs (parallel edges) are where multiple connection types applied to the same nodes

path: a seq of nodes connected by an edge

2 properties of connected component:
1. every node in the subset has a path to every other node
2. no other node has a path to any node in the subset (make sure we are grabbing the largest component in the network)

weakly v.s. strongly connected in directed graph
weakly when ignore the directions

Generally, removing nodes will tend to increase the number of connected components as the graph begins to fragment. However, not all nodes will have the same effect. Removing some highly central nodes is more likely to fragment the graph (and increase the number of connected components) than removing some nodes with low centrality. 

distance in a network: use the idea of path to measure the distance, path length is the number of hops between the source and target nodes

BFS algorithm: discover the new nodes in length first, until no new nodes to be discovered. and find the distance from A to B at the end

Average distance: calculate distances between all possible pairs and average out

Diameter: max distance between any pair of nodes (a common practice is to take the large connected component it there are disconnected subgroups)

clustering coefficient is a measure of the degree to which nodes in a graph tend to cluster together.

How to calculate local clustering coefficient?
- Compute the local clustering coefficient for every node C:
number of pairs (nodes connected) among C's connected nodes (#pairs of C's friends who are friends)
divided by number of possible pairs of C's connected nodes, i.e. combinations variations: (degree*(degree -1))/2 (if zero -> the result is zero)

Global Clustering Coefficient, known as transitivity (percentage of open triads that are triangles in a network): 3* number of closed triads, divided by number of open triads. High transitivity means that the network contains communities or groups of nodes that are densely connected internally.
* one triangle has 3 open triads

Avg LCC for connected subgroups, and

How to define node importance? it depends on different cases, such as number of connected nodes, proximity, etc. This extends to different approaches for calculating the centrality of networks. (e.g. google page rank)

Degree centrality: degree of node v (number of connected nodes. it can be in/ out degree for directed graph) divided by N(total number of nodes) - 1

Closeness centrality: N -1, divided by the sum of lengths of shortest path from any node u to main node v.

assume important nodes are close to other nodes, and penalize the nodes that can not reach the main node v

Between-ness centrality: there are multiple shortest paths between 2 nodes. in this case we have to average out the paths- sum of (num of shortest paths that passes between the 2 nodes s and t through the main node/ number of shortest paths between the two nodes). s and t to be only the nodes that reach each other. normalization is needed for large networks, divide by number of pairs of nodes. computationally expensive with it comes to different pairs. we can do sampling to make it more efficient.

PageRank (k from 1 to infinity until value converges):
1. example- k = 1, all node have 1/N 
2. Update rule: each node gives an equal share of its current pagerank to all the nodes it links to. the new pagerank of each node is the sum of all the pagerank it received from other nodes. continue til k = infinity

the problem of pagerank- the random walk approach-> it will get stuck on some nodes, while other nodes gets 0 pagerank. Damping parameter (alpha, between 0.8 and 0.9), it will try to jump out and go anywhere in the network. This is called scaled pagerank

Hubs and Authorities focus on relevance to the query in search engine. good authorities get pointed by good hubs

HITS algorithm
1. A and H score = 1
2. a update rule: each node's a score is the sum of h score of each node that points to it (= in degree if k = 1)
3. h update rule: each nodes h score is the sum of a scores of each node that it points to (= out degree if k = 1)
4. normalize a and h scores (/(added up the corresponding score))
5. repeat k times

assumptions for creating synthetic network:
rich get richer (Preferential attachment)
small world (surprisingly short paths between any nodes)

scoring measurements for link prediction (how likely the 2 nodes would form an edge):
the quality of common nodes, whether they are in the same community, degree, the meaningfulness of the common nodes etc.

number of triadic closures determines the level of clustering coefficient (connected nodes of node v form edges among themselves too)

Nodes also tend to be connected by short paths in preferential attachment model

For network diffusions:
SI model 
Susceptible -> infected
p = successful infection probability for seed/infected nodes' neighbors

SIS model
Susceptible -> infected -> Susceptible
p = successful infection probability for seed node's neighbors
s = probability of infected node becomes susceptible (not infected) again
there's a chance that all nodes become not infected, then infected nodes would stay 0.

SIR model
Susceptible -> infected -> removed
p = successful infection probability for seed node's neighbors
s = probability of infected node becomes removed (dead)

Independent Cascade Model
Relax the assumption that different edges share same Ps
-> different edges have different Ps, or the Ps can even change over time.
-> a threshold is specified for edges and represents the probability of diffusion along each edge.
every node has one chance to affect other nodes, can be generalized to be more than one shot

Complex Contagion-> linear threshold model
- e.g. people have to adopt only after hearing something a number of times
- a directed graph, edge is an 'influence score' from node u to node v
- in the network, all scores added up pointed to any node cannot be larger than  1
- each node itself has a threshold theta, representing how "susceptible" node u is
- at the time step that node v becomes "the target", if the total of influence scores from the influencer nodes  is larger than or equal to theta, influencing node v will be successful


influence maximization problem
expected number of nodes to be infected `sigma`, given budget of k nodes, set the right seed node set `A0` so that sigma can be maximized. cascade varies based of seed nodes set A0 (monotonic). when we consider having only subsets of A0 as seed nodes, when we add elements in the subset, the submodular monotonic functions f() will have 'diminishing returns' when we add the element to a larger set, i.e. the smaller subset we choose, the gained utility (delta) is larger (diminishing returns). 

- decide the live the dead edges first
- set seed(s)
- simulate the transmission process based on seed(s) going through the live edges for n time steps, and having the final infected set, `sigma x of A0`

how to choose the seed nodes? the greedy algorithm provides approximation (63%, proven in paper) in the problem for the independent cascade model. assume there's an empty set, first, find the seed node that will generate the largest average cascade, then add it in the empty set as seed node `s1`. then continue simulating by putting nodes (one at a time) that would help the set to generate largest possible cascade, until k nodes are chosen. it does a pretty good job. there are other tactics in finding good seed nodes for this problem, including finding seed nodes by their degree centrality and closeness centrality. their performance can be close to the greedy algorithm. 

nomination strategy
if we don't know the edges in a network, but we know the nodes. we can pick random nodes, ask them to refer a friend, by doing this, its is very likely to find the very influential nodes, because based on the preferential attachment model, we can "copy the edge" and find the nodes tend to highly central nodes.

Community detection
- useful in biology
- predict how group is going to split
- find sets of nodes that are many edges within the set but few edges between the sets, and score the partitions (modularity):

Let i, j be 2 nodes
m be the number of edges

I = 1/2m * (sigma- for every i, j: (Aij- Adjacency matrix- 1 if i j connected or 0 if i j not connected )(1 if i j in same community or 0 if i j not in the same community))

provided that edges are placed at random-
I exp = 1/2m * (sigma- for every i, j: (degree of node i- ki)*(the chance that node j is on the other side of this edge- kj/2m)*(1 if i j in same community or 0 if i j not in the same community))

 Q = I (fraction of edges within communities) - I exp (expected I under random edge assignment, while controlling for degrees )

 Girvan-Newman Algorithm
 - remove edges that lie between communities, and the the results (connected components) are the communities, based on the edge betweenness of all edges, starting from the highest betweenness, until all components are broken down, then look back and evaluate partitions throughout the process.

- when looking back the partitions, we pick the splits and calculate their modularity, find the highest ones.

Agglomerative hierarchical clustering
- the bottom-up approach: assume all the single nodes are communities in the network, get its modularity score, then try to merge communities such that modularity score increases.
- repeat the merging process until communities no longer leads to modularity increase.

Label propagation
similar to agglomerative hierarchical clustering, but with labels assigned to each node. given an order, nodes to choose which label to follow based on their neighbors' choices. when there are ties, choose random.
- async approach: random order for each node to update, each node to update one by one, once the first node is updated, the next node has to decide based on the new label assignments
- async approach's problem: unstable- output different partitions based on random order
- sync approach: for each iteration in the network set, each node to update one by one, once the first node is updated, the next node still looks to the original label assignments. until all nodes in the iteration have done updating, all new labels will be updated at once and be assigned as the "new setting".
- sync approach's problem: in some cases the updating will not converge. nodes go from label A<->B forever.
- semi-sync approach: break nodes into partitions without connections with partition, it applies async updating one partition as a time.

Quality of a partition
Coverage: ratio of the number of intra community edges to the total number of edges in the graph
Performance: total intra-community edges + inter-community non-edges / total number of possible edges
Separability: for each community, get ratio of intra-community edges to inter community edges, then average over all communities
Density: for each community, get fraction intra community edges out of all possible edges within community. then average over all communities. 