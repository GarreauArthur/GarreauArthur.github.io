---
title: "A bunch of tree and graph search algorithms"
layout: post

---

Just trying to make a cheat sheet of some Tree and graph search algorithms

## Dijkstra

Algorithm for finding the shortest paths between nodes in a graph.

## Bellman-Ford

The Bellman-Ford or Bellman-Ford-Moore or Ford algorithm computes shortest
paths from a single source vertex to all of the other vertices in a weighted 
digraph (direct graph).

It's slower than Dijkstra's algorithm but is capable of handling graphs with
negative edge weigths.

* Worst-case performance : O(|V||E|)
* Worst-case space complexity : O(|V|)


Algo

	Data
		vertices
		edges
		vertex source
		distance
		predecessor
	Initialization of the graph
		for each vertex v in vertices do
			distance[v] := infinity
			predecessor[v] := null
		end_for
		distance[source] := 0
	ALGO
		for i from 1 to size(vertices) do
			for each edge(u,v) with weight w do
				if(distance[u] + w) < distance[v] then
					distance[v] := distance[u] + w
					predecessor[v] := u
				end_if
			end_for_each
		end_for
		// check for negative-weight cycles
		for each edge(u, v) with weight w do
			if (distance[u] + w) < distance[v] then
				error "Graph ccontains a negative-weight cycle"
			end_if
		end_for_each
	END_ALGO

Recherche des plus courts chemins entre un sommet donnée, appelé source et tous
les autres sommets

a chaque sommet si est associé un poids pi variable

-sommet de départ est numéroté 1
-les autres sont numérotés dans un ordre quelconque

cas d'une minimisation :

	p1 = 0
	pi = +infinity pour tout i >1

	tant que existe arc(i,j) tel que pj > pi+vij faire
		pj <- pi+vij
	fin tant que
	//pi: valeur minimale d'un chemin du sommet 1 au sommet i
	//vij: poid arc de i vers j

	// trouver le plus petit chemin
	si pj = + infini alors // cas d'une minimisation
		pas de chemin de i à j
	sinon
		reculer à partir de j en utilisant à chaque recul un arc (k,l) tel que
		pk + vkl = pl
	fin si

algo :

	i <- 0
	tant que i < nbSommets faire
		j <- 0
		revenirSommetEnArriere <- faux
		tant que ( j<nbSommets) && !revenirSommetEnArriere faire
			si M[i][j] > 0 //arc existe
			   && pj > pi + M[i][j] alors
				pj <- pi + M[i][j]
				Si i>j alors // si pas de circuit absorbant
					i<-j-1
					revenirSommetEnArriere <- vrai
				fin si
			fin si
			j++
		fin tant que
		i++
	fin tant que

Cas d'une maximisation, même chose sauf :

	p1 <- 0; pi <- -infinity pour tout i>1

	tant que existe arc(i,j) tel que pj < pi + vij faire

## Floyd–Warshall algorithm

* Find the lengths (summed weights) of the shortest paths between all pairs of
vertices
* Versions of the algorithm can also be used for finding the transitive closure
of a relation {\displaystyle R} R,
* Or (in connection with the Schulze voting system) widest paths between all pairs of vertices in a weighted graph
