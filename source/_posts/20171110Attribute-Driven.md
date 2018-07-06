---
layout: '[default_layout]'   
title: Attribute-Driven Community Search           
date: 2017-11-10 14:47:41  
toc: true                  
tags:                        
- Social Network
- Search

categories:                  
- Social Network

---
十九大心得体会：“雄关漫道真如铁，而今漫步从头越”。不忘初心，牢记使命。新的时代、新的思想、新的征程，更需要新的作为。不忘初心，方得始终。“空谈误国、实干兴邦”，比实绩不比态度。敢于担当、勇于担当、善于担当，在工作学习当中做出实绩，成为一名老师放心、同学信任、组织满意的中国共产党人。
<!--more-->

# ABSTRACT
- analysis of protein-protein interaction (PPI) networks,
- citation graphs
- collaboration networks

 finding attributed truss communities (ATC), i.e., finding connected and close k-truss subgraphs containing Vq, with the largest attribute relevance score. 

we develop an efficient greedy algorithmic framework to iteratively remove nodes with the least popular attributes, and shrink the graph into an ATC. In addition, we also build an elegant index to maintain k-truss structure and attribute information, and propose effi-cient query processing algorithms. 

# 1. INTRODUCTION

a collaboration network. The nodes qi, vj , ... represent authors. Node attributes (e.g., DB, ML) represent authors’topics of expertise. 

Previous community search methods include those based on k-core [32, 26, 10], k-truss [19], and 1.0-quasi-k-clique-l-adjacent community [9]. A k-core [26] is a subgraph in which each vertex has at least k neighbors within the subgraph. A k-truss [19] is a subgraph in which each edge is contained in at least (k−2) triangles within the subgraph. The 1.0-quasi-k-clique- l-adjacent community model [9] allows two k-cliques overlapping in ` vertices to be merged into one community. 

an attributed truss community (ATC) model. Given a query Q = (Vq, Wq) consisting of a set of query nodes Vq and a set of query attributes Wq, a good community H must be a dense subgraph which contains all query nodes and attributes Wq must be contained in numerous nodes of the community. 

This algorithm first generates a Steiner tree connecting all query nodes.

# 2. PRELIMINARIES AND DESIDERATA
## 2.1 Preliminaries
- an undirected, unweighted simple graph G = (V, E) with n = |V (G)| vertices and m = |E(G)| edges. 
- the set of neighbors of a vertex v by N(v).
- the degree of v by d(v) = |N(v)|. 
- d_{max} = max_{v∈V} d(v) denote the maximum vertex degree in G.
-  the set of all attributes in a graph by A.
- Each node v ∈ V contains a set of zero or more attributes, denoted by attr(v) ⊆ A.
- We use V_w ⊆ V to denote the set of nodes having attribute w, i.e., Vw = {v ∈ V | w ∈ attr(v)}.

## 2.2 Desiderata of a good community
the attributed community search (ACS) problem is to find a subgraph H ⊆ G containing all query nodes Vq, where the vertices are densely inter-connected, cover as many query attributes Wq as possible and share numerous attributes.

the commonly accepted desiderata of a good attributed community.
an attributed community is a connected subgraph H = (V (H), E(H)) ⊆ G

1. (Participation) H contains all query nodes as Vq ⊆ V (H);
2. (Cohesiveness) A cohesiveness function coh(H) that measures the cohesive structure of H is high.
3. (Attribute Coverage and Correlation) An attribute score function f(H, Wq) that measures the coverage and correlation of query attributes in vertices of H is high.
4. (Communication Cost) A communication cost function com(H) that measures the distance of vertices in H is low.

# 3. RELATED WORK
- Community Search
- Keyword Search
- Team Formation
- Community Detection in Attributed Graphs.

未完不待续。。。







