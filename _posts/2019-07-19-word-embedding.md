---
title: Word Embedding
---

Word Embedding is the vector representation of a particular word.

In word embedding words or phrases from the vocabulary are mapped to vectors of real numbers.

# Word Embedding Software
* Word2Vec
* GloVe
* FastText
* Gensim


# word2vec

Word2vec is a two-layer neural net that processes text. Its input is a text corpus and its output is a set of vectors: feature vectors for words in that corpus. 

Word2vec can utilize either of two model architectures to produce a distributed representation of words:

* [CBOW(Common Bag of Words)](bow.md)
* [Skip-Gram(N-Gram)](ngram.md)

# Word2Vec Model Using Gensim

Gensim’s Word2Vec implementation let’s you train your own word embedding model for a given corpus.
Dependencis: 

* Python(2.7)
* Gensim
            


```python
from gensim.models.word2vec import Word2Vec
from multiprocessing import cpu_count
import gensim.downloader as api

# Download dataset
dataset = api.load("text8")
data = [d for d in dataset]

# Split the data into 2 parts. Part 2 will be used later to update the model
data_part1 = data[:1000]
data_part2 = data[1000:]

# Train Word2Vec model. Defaults result vector size = 100
model = Word2Vec(data_part1, min_count = 0, workers=cpu_count())

# Get the word vector for given word
model['topic']
#> array([ 0.0512,  0.2555,  0.9393, ... ,-0.5669,  0.6737], dtype=float32)

model.most_similar('topic')
#> [('discussion', 0.7590423822402954),
#>  ('consensus', 0.7253159284591675),
#>  ('discussions', 0.7252693176269531),
#>  ('interpretation', 0.7196053266525269),
#>  ('viewpoint', 0.7053568959236145),
#>  ('speculation', 0.7021505832672119),
#>  ('discourse', 0.7001898884773254),
#>  ('opinions', 0.6993060111999512),
#>  ('focus', 0.6959210634231567),
#>  ('scholarly', 0.6884037256240845)]

# Save and Load Model
model.save('newmodel')
model = Word2Vec.load('newmodel')
```


We have trained and saved a Word2Vec model for our document. However, when a new dataset comes, you want to update the model so as to account for new words.

## References
1. [https://en.wikipedia.org/wiki/Word_embedding](https://en.wikipedia.org/wiki/Word_embedding)
2. [https://en.wikipedia.org/wiki/Word2vec](https://en.wikipedia.org/wiki/Word2vec)
3. [https://skymind.ai/wiki/word2vec](https://skymind.ai/wiki/word2vec)
4. [https://towardsdatascience.com/introduction-to-word-embedding-and-word2vec-652d0c2060fa](https://towardsdatascience.com/introduction-to-word-embedding-and-word2vec-652d0c2060fa)
5. [https://www.machinelearningplus.com/nlp/gensim-tutorial/](https://www.machinelearningplus.com/nlp/gensim-tutorial/)
