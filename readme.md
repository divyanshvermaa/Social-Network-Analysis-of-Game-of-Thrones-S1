
# Social Network Analysis of Game of Thrones: Season 1
<div align="right"><i>Year: 2021</i></div>
<img src="https://i.imgur.com/QDW5DIH.png">
Performed social network analysis of Game of Thrones: Season 1, one of the most popular fantasy drama television series of all time. The results obtained were observed to be coherent with the actual plot to a great extent.

## Data
The dataset for performing analysis was obtained from [here](https://github.com/mathbeveridge/gameofthrones/tree/master/data); and is based on interactions between characters: whether it is through them appearing in a scene or direction, or exchanging a dialogue, or mentioning other characters/ being mentioned by other characters. 

These interactions are seen as links between the characters. They have been extracted from fan-authored scripts. The fact that the links depend directly on the script, and hence verbal interaction between the characters, gives more importance to communication than battle scenes with no dialogues.

## Analysis

### Nodes, Edges, Subgraphs, Neighbors, and Paths
The nodes would be the unique characters for our network, including both Source and Target. In the case of Season 1, there are 126 nodes or 126 characters among whom the interactions are recorded. The edges are these interactions between the characters, represented from Source to Target. 

There are a total of 549 edges for our network, which is unsurprisingly large, given that the series has several characters with interweaving plots. Finally, weights represent the number of interactions between the two characters under consideration. For instance, a weight of 192 for source being Ned and target being Robert denotes there were 192 interactions between the two. 

If we were to plot the network as-is, without the character names, or the labels for the nodes, it would appear as below:

![enter image description here](https://user-images.githubusercontent.com/32619706/157382025-9376b2b3-f6a5-4050-abc0-ac045826cf3e.png)

Expectedly, there are a lot of interactions between the characters, owing to the reasons stated previously: multiple plots being interweaved throughout the season. To understand which characters were most often the source or target, without former knowledge of the show, in- and out-degrees can be used:

<img src=https://user-images.githubusercontent.com/32619706/157382572-6b2c87ab-38a8-4bbf-805f-55fb1cdbc404.png>

This matches with what one would have expected – Tyrion was indeed one of the most important characters. Further, Catelyn’s role also becomes prominent in episodes 3-5.

Having looked at some of the characters that had the most interactions: to and from, it can be observed that ‘Ned’ appeared in the top five lists for both. Once again, this is expected, as Ned was indeed the most prominent character till the end of the first season. Let’s look at his part of the network:

<img src=https://user-images.githubusercontent.com/32619706/157384816-993e9c79-0148-4f38-b7c1-a4572e739351.png>

Tyrion Lannister’s subgraph also depicts something similar, while Cersei Lannister’s subgraph – given her involvement was not as much – suggests limited interaction; these can be seen in the notebook. For each of these characters, the predecessors (source characters), and successors (target characters) were extracted. Finally, the interactions between the characters based on the path traversed in moving through the nodes were also derived.

### Node Importance

**Degree Centrality:**
Node importance based on number of connections, higher the more.

 <img src=https://user-images.githubusercontent.com/32619706/157383780-66e24cef-a452-4b97-9d40-27392ae36ab0.png width="300">

This makes sense as Ned and Tyrion were indeed the most prominent characters for the season. Ned, who was beheaded eventually, had a lot of the story revolving around him and thus shows up at the top. The result can be visualized as:

**Betweenness Centrality:**
Importance of nodes based on how often they lie between the shortest paths among other nodes.

 <img src=https://user-images.githubusercontent.com/32619706/157383797-cd983745-c6dd-4245-9d26-4512155e9030.png width="300">

Though Ned remains at the top, being central to the plot, Catelyn moves up to being second as she is often in involved between interactions.

**Closeness Centrality:**
Node importance based on how close the node is located to the actions.

 <img src=https://user-images.githubusercontent.com/32619706/157383812-9ede6617-c11d-4b8c-a673-a12c0410c5f5.png width="300">

Understandably, Varys comes up for this metric as he is responsible for the spread of information on the war that was to ensue mid-season.

**PageRank:**
Importance of nodes based on the quality of those nodes that are connected to it.

 <img src=https://user-images.githubusercontent.com/32619706/157383823-63f9806a-ace6-40ea-b8e2-abfd18676c31.png width="300">

Tyrion being key interaction among most prominent characters shows up first.

Next, we assess if there is a correlation between metrics for node importance. 

<img src=https://user-images.githubusercontent.com/32619706/157385579-1df068e6-e775-4821-b833-b3670d3db898.png> 

It appears that Degree Centrality and Betweenness Centrality are highly correlated.

### Community Detection

Finally, we try to identify self-contained subsets of the network. In plain terms, this would imply the existence of a higher number of edges within the communities and fewer outside of them. This can be measured through modularity. For our network, we see that the modularity index is highest when there are five sub-networks (levels+1):

<img src=https://user-images.githubusercontent.com/32619706/157385802-86406417-1888-4369-b4b6-f8e58eaba3ea.png> 

This, again, is as expected, as the first season has five prominent communities: Lannisters, Dothraki, King’s Landing, Starks and Night’s Watch. 

The network as well as the communities identified (represented by different colors) by Louvain Modularity are as below:

<img src=https://user-images.githubusercontent.com/32619706/157386234-94adc759-867b-4515-88c8-7090044b1b5f.png>

These are a bit more coherent than those identified by Girvan & Newmann Clustering and InfoMap, the results of which are available in the notebook.

**Comparison**
Given the set of clusters that have been identified, the three algorithms can be compared through the run using cluster evaluation metrics such as: 
1.	Internal Edge Density (number of edges between the community)
2.	Expansion or External Connectivity (nodes with edges outside the community)
3.	Conductance (ratio of expansion over the sum of Internal Edge Density and Expansion)

<img src=https://user-images.githubusercontent.com/32619706/157387239-2c2a903f-c0fa-45d9-b6f1-6e82108d5eb8.png>

Girvan & Newman resulted in some communities with very low internal edge density and very high expansion, which are not desired. On the contrary, Louvain and InfoMap created some communities with decent size and low conductance.
