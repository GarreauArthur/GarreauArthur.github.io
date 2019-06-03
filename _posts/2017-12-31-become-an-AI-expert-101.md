---
title: "An (almost) exhaustive list of everything you need to know to become an AI expert"
layout: post
---

cqncpdp previously told that he wasn't going to make an exhaustive list of what
AI can do, so in extent, of what you need to know to build AI agents. So I
decided I was going to give it a try, and make a list of the required knowledge
to become an AI expert. This list will be continuously updated.

I don't consider myself an AI expert, I know most of the elements in the
list, but not everything (marked as unknown `[u]`). My goal is to minimize the
number of unknown subjects.



* Mathematics
	* Logic
	* Calculus
	* Linear algebra
		* Vector spaces
		* Matrix theory
		* linear transformation
		* Subspaces, span
		* Eigenvalues and eigenvectors
	* Set theory
	* Probability
		* Frequentist Probability
		* Bayesian Probability
	* Statistics
		* Estimator
		* Mean Square Error
		* Bias, Variance, Expectation
		* (Maximum) Likelihood
	* Graph theory
		* graph coloring
		* Tree
		* Graph and tree algorithms (cf [here](#gtsa))
	* Markov process & chain
	* `[u]` Game theory
* Information theory
	* entropy
	* cross-entropy
	* joint entropy
	* conditional entropy
	* mutual information
	* Kullback-Leibler divergence
* computer programming
	* Jupyter notebook
	* python
		* IPython
		* Numpy
		* CuPy
		* Pandas
		* Matplotlib
		* Scikit-Learn
    * `[u]` Keras
		* `[u]` PyTorch
		* virtualenv
	* Tensorflow
	* `[u]` R programming
	* `[u]` Go
	* `[u]` Prolog
* Database
	* SQL
	* NoSQL
		* MongoDB
		* `[u]` Neo4j
* computer science
	* Data Structure
		* Array
		* Queue
		* List
		* Stack
		* Graph
		* Trees
	* <span id="gtsa">Graph and tree (search) algorithms</span> 
		* Bellman-Ford algorithm
		* Dijkstra's algorithm
		* British museum
		* Depth-first search
		* Breadth-first search
		* Hill climing
		* Beam search
		* Branch and Bound
		* `A*` search algorithm
 		* Topological sorting
 		* Ford-Fulkerson algorithm
 		* Stepping-stone & Balas-Hammer
 		* Hungarian (or Kuhn–Munkres) algorithm
		* `[u]` Fringe search
		* `[u]` Iterative deepening `A*` (`IDA*`)
		* `[u]` Floyd–Warshall algorithm
		* `[u]` Borůvka's algorithm
		* `[u]` `D*` 
		* `[u]` Edmonds' algorithm or Chu–Liu/Edmonds' algorithm 
		* `[u]` Johnson's algorithm
		* `[u]` Kruskal's algorithm
		* `[u]` Lexicographic breadth-first search
		* `[u]` Prim's algorithm
		* `[u]` `SMA*` or Simplified Memory Bounded `A*`
	* Game search
		* Minimax	
		* Aplha-Beta pruning
		* `[u]` Negamax
	* Recursion
	* Theory of computation
		* Numerical computation
		* Complexity 
	* Dynamic programming
	* Monte Carlo method
	* Knowledge representation and reasoning
* Machine Learning
	* Gradient Descent
	* Mini Batch Gradient Descent
	* Stochastic Gradient Descent
	* Linear Regression
	* Logistic Regression
	* Neural Networks
	* Backpropagation
	* High Bias (Underfitting)
	* High Variance (Overfitting)
	* Support Vector Machines
	* K-Means algorithm
	* Decision Tree & Random Forest
	* Principal Components Analysis
	* Naive Bayesian classification
	* Data Augmentation
	* Early Stopping
	* Normalization
	* Regularization
	* Dropout Regularization
	* RMSprop
	* Momentum
	* Adam Optimization
	* `[u]` Manifold Learning
* Deep Learning
	* Deep Feed Forward
	* Recurrent Neural Network (RNN)
	* Bidirectional RNN
	* Long/Short Term Memory (LSTM)
	* Gated Recurrent Unit networks (GRU)
	* `[u]` Boltzmann machine
	* Deep Convolutional Network
	* `[u]` Generative Adversarial Network (GAN)
	* `[u]` Dynamic neural networks
* Reinforcement Learning
	* Temporal difference
	* `[u]` everything else
* Natural Language Processing
	* hierachical softmax
	* Word vector/Word embedding
		* [skip-grams](https://arxiv.org/pdf/1301.3781.pdf)
		* word2vec
    * [Negative sampling](https://arxiv.org/pdf/1310.4546.pdf)
		* [GloVe](https://nlp.stanford.edu/pubs/glove.pdf)
    * [The problem of bias in word embedding](https://arxiv.org/pdf/1607.06520.pdf)
  * [Bleu score](https://www.aclweb.org/anthology/P02-1040.pdf)
	* `[u]` everything else



