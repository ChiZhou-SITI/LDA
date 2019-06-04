# LDA
Topic modeling with latent Dirichlet allocation using variational inference and Gibbs sampling

## Introduction of Latent Dirichlet Allocation
Suppose you have the following set of sentences:

* I like to eat broccoli and bananas.
* I ate a banana and spinach smoothie for breakfast.
* Chinchillas and kittens are cute.
* My sister adopted a kitten yesterday.
* Look at this cute hamster munching on a piece of broccoli.

What is latent Dirichlet allocation? It’s a way of automatically discovering topics that these sentences contain. For example, given these sentences and asked for 2 topics, LDA might produce something like

* Sentences 1 and 2: 100% Topic A
* Sentences 3 and 4: 100% Topic B
* Sentence 5: 60% Topic A, 40% Topic B
* Topic A: 30% broccoli, 15% bananas, 10% breakfast, 10% munching, … (at which point, you could interpret topic A to be about food)
* Topic B: 20% chinchillas, 20% kittens, 20% cute, 15% hamster, … (at which point, you could interpret topic B to be about cute animals)

The question, of course, is: how does LDA perform this discovery?

### LDA Model
In more detail, LDA represents documents as mixtures of topics that spit out words with certain probabilities. It assumes that documents are produced in the following fashion: when writing each document, you 
* Decide on the number of words N the document will have (say, according to a Poisson distribution).
* Choose a topic mixture for the document (according to a Dirichlet distribution over a fixed set of K topics). For example, assuming that we have the two food and cute animal topics above, you might choose the document to consist of 1/3 food and 2/3 cute animals.
* Generate each word w_i in the document by:
	* First picking a topic (according to the multinomial distribution that you sampled above; for example, you might pick the food topic with 1/3 probability and the cute animals topic with 2/3 probability).
	* Using the topic to generate the word itself (according to the topic’s multinomial distribution). For example, if we selected the food topic, we might generate the word “broccoli” with 30% probability, “bananas” with 15% probability, and so on.

Assuming this generative model for a collection of documents, LDA then tries to backtrack from the documents to find a set of topics that are likely to have generated the collection.

## Implementations
There are two kinds of implementations based on variational inference and gibbs sampling

* [Online variational inference](/doc/Online_Learning_for_Latent_Dirichlet_Allocation.pdf)
* [Gibbs sampling](http://www.pnas.org/content/101/suppl_1/5228.abstract)

## Examples

Implementation example using online variational inference

	* [example_1](/examples/example_sklearn_variational_inference/LDA_example_1.ipynb)
	* [example_2](/examples/example_sklearn_variational_inference/LDA_exmaple_2.ipynb)

Implementation using gibbs sampling

	* [example_3](/examples/example_gibbs_sampling/LDA_example_3.ipynb)
