<https://www.youtube.com/watch?v=sDMJr0h5_xw>

"GeoRanging tweets"

* Based on a set of local influencers ( schools, museums, politicians, local celebrities ), discover if an account is used by someone linked to a geo
K-means

LDA

* Assume a topic is a distribution of words
* Assume a document is a distribution of topics
* Update every word assignment according to our terrible model
* Repeat until convergence

The combination gives you a way to model a corpus.

Non-Negative Matrix Factorization

* ?
  
Community Detection

* Louvain ?
  * Modularity
  * How many of the edges reside in the comunities
  * How unique are these communities to this graph
  * -> Very Fast. Allows tuning K on the fly.
"""

* Define word co-occurrence ( two words in the same tweet)
* COnstruct graph where words are nodes and edges are co-occurrence relationship
* Filter out low information words by high frequency and low pairings
* Pick Heaviest edges
* Run Community detection

How to find representative tweets?
"Summarization techniques"

* for each cluster, look for the closest tweets: Cosine similarity between

Future

* Overlapping communities
* Conductance ( Modularity suffers from a tendency to ignore very small clusters )
* Optimization Metrics
* Reducing Word Noise ( co-occurrence distribution )
* Better sentence segmentation
* Bi-Partite Graphs
  * Tweets on the left, words on the right, look for words
* User-Defined sensitivity
