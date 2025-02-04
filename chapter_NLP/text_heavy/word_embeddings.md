# An Introduction to Word Embeddings

## Why word embeddings matter

Word embeddings are a very useful representation of vocabulary for machine learning purposes. The motive of word embeddings is to capture context, semantic and syntactic similarity, and represent these aspects through a geometric relationship between the embedding vectors. Formulation of these embeddings is often harder as we need to isolate what we actually want to know about the words. Do we want to have embeddings that share a common part of speech appear closer together? Or words with similar meanings appear geometrically closer than those without? How do we derive any of these relationships and how do we represent any of these features? All of these questions are answered in different manners according to the newest models as the field has developed, changing what word embeddings actually do for the down-stream task. The best way to understand why and how word embeddings developed the way they did, is to firstly understand how word embeddings are evaluated and the different aspects which contribute to the success of different methods of embedding.

## Evaluation of word embeddings

The goal of word embeddings is simple: a good embedding will provide a vector representation of a word such that its vector representation when compared with that of another word mirrors the total linguistic relationship between the two words. In the introduction section, we went over the number of linguistic relationships words can have with one another. The variability in expressiveness of these aforementioned characteristics will influence the "performance" of word embeddings.

The paper by Schnabel et al in 2015 provides a standard for evaluation methods with regards to unsupervised word embeddings, that, in a number of ways is still true today. We can break up evaluation of word embeddings into two distinct categories: Intrinsic and Extrinsic evaluation. Extrinsic evaluation refers to "using word embeddings as input features to a downstream task and measuring changes in performance metrics specific to that task" to evaluate the quality of the word embeddings. Examples of such downstream tasks range from part-of-speech (POS) tagging to named-entity recognition (NER) (Pennington et al., 2014). Extrinsic evaluation only provides a single way in specifying the "goodness" of an embedding, and it is relatively unclear how these measurements connect to other measures of "goodness."

Intrinsic evaluations test for syntactic and semantic relationships between specific words (Mikolov et al, 2013a; Baroni et al. 2014). The tasks typically require and involve a pre-selected set of query terms and semantically related target words, which are referred to as the "query inventory." The methods are then evaluated by compiling aggregate scores for each method such that the correlation coefficient serves as an absolute measure of quality. Query inventories were plethoric as psycholinguistics, information retrieval, and image analysis featured similar datasets, but the specificity of the queries led to poorly calibrated corpus statistics. In Schnabel et. al, they provided a newer model to constructing fair query inventories, picking words in an ad hoc fashion and selecting for diversity with respect to frequency, parts-of-speech, and abstractness.

Intrinsic evaluation is further dissected into four main categories: relatedness, analogies, categorization, and selectional preference. Relatedness refers to testing on datasets containing relatedness scores for pairs of words; the cosine similarity of the embeddings of the two words should have high correlation with the human relatedness scores. The second test is analogies, popularized by Mikolov et. al in 2013. The goal was to find the best term x for a given term y such that the relationship between x and y best matches that of the relationship between a and b. The third task is categorization; the goal being to recover a clustering of words into different categories. To do this, the corresponding word vectors of all words in the dataset are clustered and the purity of the returned clusters is computed with respect to the labeled dataset. Selectional preference is the last task; the goal being to determine how typical a noun is for a verb either as a subject or as an object, (e.g. people eat, but we rarely eat people).

To divide evaluations by another metric is


### Distributional vs. Distributed representations

Both of them are based on the distributional hypothesis that words occur in similar context tend to have similar meaning.

Distribution representation is the high-dimensional vector representation obtained from the rows of the word-context co-occurrence matrix, whose dimension size equals to the vocabulary size of the corpus.

Distributed representation is a low-dimensional vector representation, which can be obtained from a neural network based model (such as word2vec, Collobert and Weston embeddings, HLBL embeddings). The matrix factorization based model that perform matrix factorization on the word-context co-occurrence matrix (such as the Glove from Stanford using direct matrix factorization, the Latent Semantic Analysis using SVD factorization). The paper from Levy (Neural Word Embedding as Implicit Matrix Factorization) shows that the matrix factorization method and the neural network based method is somewhat equivalent.

Actually, as Yoav Goldberg showed in the presentation "word embeddings what, how and whither" that the distributed representation can be obtained from distributional representation based on matrix factorization.


### Count-based methods vs Prediction-based methods

With the steady growth of textual data, NLP methods are required that are able to process the data efficiently. The focus recently of word embeddings has been on efficient methods that are targeted to compute distributional models that are based on the distributional hypothesis of Harris (1951). This hypothesis claims that words occurring in similar contexts tend to have similar meanings. In order to implement this hypothesis, early approaches (Hindle, 1990; Grefenstette, 1994; Lin, 1997) represented words using count-based vectors of the context. However, such representations are very sparse, require a lot of memory and are not very efficient. In the last decades, methods have been developed that transform such sparse representations into dense representations mainly using matrix factorization. With word2vec (Mikolov et al., 2013), an efficient prediction-based method was introduced, which also represents words with a dense vector. However, also sparse and count-based methods have been proposed that allow an efficient computation, e.g. (Kilgarriff et al., 2004; Biemann and Riedl, 2013). A more detailed overview of semantic representations can be found in (Lund and Burgess, 1996; Turney and Pantel, 2010; Ferrone
and Zanzotto, 2017).

One of the first comparisons between count-based and prediction-based distributional models was performed by Baroni et al. (2014). For this, they consider various tasks and show that prediction-based word embeddings outperform sparse count-based methods and dense count-based methods used for computing distributional semantic models. The evaluation is performed on datasets for relatedness, analogy, concept categorization and selectional preferences. The majority of word pairs considered for the evaluation consists of noun pairs. However, Levy and Goldberg (2014b) showed that dense count-based methods, using PPMI weighted co-occurrences and SVD, approximates neural word embeddings. Levy et al. (2015) showed in an extensive study the impact of various parameters and show the best performing parameters for these methods. The study reports results for various datasets for word similarity and analogy. However, they do not evaluate the performance on local similarity ranking tasks and omit results for pure count-based semantic methods. Claveau and Kijak (2016) performed another comparison of various semantic representation using both intrinsic and extrinsic evaluations. They compare the performance of their count-based method to dense representations and prediction-based methods using a manually crafted lexicon, SimLex and an information retrieval task. They show that their method performs better on the manually crafted lexicon than using word2vec. For this task, they also show that a word2vec model computed on a larger dataset yields inferior results than models computed on a smaller corpus, which is contrary to previous findings, e.g. (Banko and Brill, 2001; Gorman and Curran, 2006; Riedl and Biemann, 2013). Based on the SimLex task and the extrinsic evaluation they show comparable performance to the word2vec model computed on a larger corpus.

### Subword-based and Character-based Embeddings

Learning continuous representations of words has a long history in natural language processing (Rumelhart et al., 1988). These representations are typically derived from large unlabeled corpora using co-occurrence statistics (Deerwester et al., 1990; Schütze, 1992; Lund and Burgess, 1996). A large body of work, known as distributional semantics, has studied the properties of these methods (Turney et al., 2010; Baroni and Lenci, 2010). In the neural network community, Collobert and Weston (2008) proposed to learn word embeddings using a feedforward neural network, by predicting a word based on the two words on the left and two words on the right. More recently, Mikolov et al. (2013b) proposed simple log-bilinear models to learn continuous representations of words on very large corpora efficiently.
Most of these techniques represent each word of the vocabulary by a distinct vector, without parameter sharing. In particular, they ignore the internal structure of words, which is an important limitation for morphologically rich languages, such as Turkish or Finnish. For example, in French or Spanish, most verbs have more than forty different inflected forms, while the Finnish language has fifteen cases for just nouns. These languages contain many word forms that occur rarely (or not at all) in the training corpus, making it difficult to learn good word representations. Because many word formations follow rules, it is possible to improve vector representations for morphologically rich languages by using character level information.

In recent years, many methods have been proposed to incorporate morphological information into word representations. To model rare words better, Alexandrescu and Kirchhoff (2006) introduced factored eural language models, where words are represented as sets of features. These features might include morphological information, and this technique as succesfully applied to morphologically rich languages, such as Turkish (Sak et al., 2010). Recently, several works have proposed different composition functions to derive representations of words from morphemes (Lazaridou et al., 2013; Luong t al., 2013; Botha and Blunsom, 2014; Qiu et l., 2014). These different approaches rely on a morphological decomposition of words.

## Limitations

## Common types of word embeddings with advantages and disadvantages

The fact of the matter is that machine understanding of language is very construed. By transforming textual data into numerical representations, we are able to train machines over complex variants of mathematical models that pose as intelligent understanding of language.
The process of turning text into numbers is commonly known as “vectorization” or “embedding techniques”. These techniques are functions which map words onto vectors of real numbers. These vectors then combine to form a vector space, an algebraic model where all the rules of vector addition and measures of similarities apply.

Using the word embedding technique word2vec, researchers at Google are able to quantify word relationships in an algebraic model
Such a vector space is a very useful way of understanding language. We can find “similar words” in a vector space by finding inherent clusters of vectors. We can determine word relations using vector addition. We can measure how similar two words by measuring the angles between the vectors or by examining their dot product.
There are more ways of vectorizing text than mapping every word to a vector. We can also map documents, characters or groups of words to vectors as well.
“Document” is a term that gets thrown around a lot in the NLP field. It refers to an unbroken entity of text, usually one that is of interest to the analysis task. For example, if you are trying to create an algorithm to identify spam emails, each email would be its own document.
Vectorizing documents makes it useful to compare text at the document level. It is useful in many applications including topic modeling and text classification. Vectorizing groups of words helps us differentiate between words with more than one semantic meaning. For example, “crash” can refer to a “car crash” or a “stock market crash” or intruding into a party.

The underlying mechanism to creating these vectors is by examining the context in which these words appear. We can examine how often a certain word appears in each document, or how often two words co-occur together.

All of these embedding techniques are reliant on the distributional hypothesis, the assumption that “words which are used and occur in the same contexts tend to purport similar meaning.”

##Bag of Words: the Simplest Embedding Technique

This is one of the simplest methods of embedding words into numerical vectors. It is not often used in practice due to its oversimplification of language, but often the first embedding technique to be taught in the classroom setting.

Let’s consider the following documents. If it helps, you can imagine that they are text messages shared between friends.

- Document 1: High five!
- Document 2: I am old.
- Document 3: She is five.

The *vocabulary* we obtain from this set of documents is (High, five, I, am, old, she, is). We will ignore punctuation for now, although depending on our use case it can also make a lot of sense to incorporate them into our vocabulary.

We can create a matrix representing the relationship between each term from our vocabulary and the document. Each element in the matrix represents how many times that term appears in that particular document.

![Bag Of Words Matrix][images/BOW.png]

Using this matrix, we can obtain the vectors for each word as well as document. We can vectorize “five” as [1,0,1] and “Document 2” as [0,0,1,1,1,0,0].
Bag of words is not a good representation of language, especially when you have a small vocabulary. It ignores word order, word relationships and produces sparse vectors that is largely filled with zeros. We also see here from our small example that the words “I”, “am”, “old” are mapped to the same vector. This implies that these words are similar, something which we know not to be true.

There are many better (and more complicated) alternatives to Bag of words out there, but to keep it simple, we'll stick with Bag of Words for now.

### What now — after I have vectorized my text?

Numerical representations allow us to use numerical classification methods to analyze our text. If we want to build a document classifier, we can obtain document level vectors for each review and use them as feature vectors to predict the class label. We can then plug this data into any type of classifier.

By one hot encoding the classes, we can plug this data into any type of classifier
Textual data is rich and high in dimensions, which makes more complex classifiers such as neural networks ideal for NLP.

Some of the other first iterations of word embeddings were very simple. They were represented as one-hot vectors, the count of unique vocabulary in the corpus as the length of the vector, and the place in which the vocabulary occurred first as the position in the one-hot vector being a 1. For example, if my vocabulary was the following sentence:

> The boy liked the turtles.

The length of the above sentence is five, but there are four unique words in the vocabulary, "the", "boy", "liked", and "turtles." So the length of our embedding vectors for each would be four. For "the," the embedding would look like `[1, 0, 0, 0]`, the embedding for boy would be `[0, 1, 0, 0]`, the embedding for liked would be `[0, 0, 1, 0]`. The embedding for the next "the" would reuse the one-hot vector embedding used previously, and default to `[1, 0, 0, 0]` for every re-occurrence of "the," and lastly, the embedding for turtles would be `[0, 0, 0, 1]`. But according to the questions we posed earlier, these don't represent any of the features of syntactic or semantic similarity; these only represent the most basic feature of whether or not a word occurred or not. In addition, any calculations or computation that one would like to do with these one-hot vectors would be a problem as the inherent sparsity of these vectors makes it increasingly inefficient as the vocabulary size increases.

The weight matrices connecting our word-level inputs to the network's hidden layers would each be $v \times h$,
where $v$ is the size of the vocabulary and $h$ is the size of the hidden layer.
With 100,000 words feeding into an LSTM layer with $1000$ nodes, the model would need to learn
$4$ different weight matrices (one for each of the LSTM gates), each with 100 million weights, and thus 400 million parameters in total.

Fortunately, it turns out that a number of efficient techniques
can quickly discover broadly useful word embeddings in an *unsupervised* manner.

These embeddings map each word onto a low-dimensional vector $w \in R^d$ with $d$ commonly chosen to be roughly $100$.
Intuitively, these embeddings are chosen based on the contexts in which words appear.
Words that appear in similar contexts, like "tennis" and "racquet," should have similar embeddings
while words that are not alike, like "rat" and "gourmet," should have dissimilar embeddings.

Now, we will explore the much more complex set of embeddings created using shallow neural networks by focusing on word2vec models. Trained over large corpora, word2vec uses unsupervised learning to determine semantic and syntactic meaning from word co-occurrence, which is used to construct vector representations for every word in the vocabulary.

Word2vec was developed at Google by a research team led by Tomas Mikolov. The research paper takes a while to read, but is worth the time and effort.
The model uses a two layer shallow neural network to find the vector mappings for each word in the corpus. The neural network is used to predict known co-occurrences in the corpus and the weights of the hidden layer are used to create the word vectors. Somewhat surprisingly, word vectors created using this method preserve many of the linear regularities found in language.

The Efficient Estimation of Word Representations in Vector Space paper shares the following result:
“Using a word offset technique where simple algebraic operations are performed on the word vectors, it was shown for example that vector(”King”) — vector(”Man”) + vector(”Woman”) results in a vector that is closest to the vector representation of the word Queen.”

There are two model architectures used to train word2vec: Continuous Bag of Words and Skip Gram. These models determine how textual data is passed into the neural network. Both of these architectures use a context window to determine contextually similar words. A context window with a fixed size n means that all words within n units from the target word belong to its context.

Consider the following example with a fixed window size of 2:

> "The quick brown fox jumped over the lazy dog."

Fox is our target word and quick, brown, jumped, over belong to the context of fox. The assumption is that with enough examples of contextual similarity, the network is able to learn the correct associations between words.
This assumption is in line with the distributional hypothesis we presented earlier, which states that “words which are used and occur in the same contexts tend to purport similar meaning.”

The implementation of context window in word2vec is dynamic.
A dynamic context window has a maximum window size. Context is sampled from the maximum window size with probability 1/d, where d is the distance between the word to the target.
Consider the target word fox using a dynamic context window with maximum window size of 2. (brown, jumped) have a 1/1 probability of being included in the context since they are one word away from fox. (quick, over) have a 1/2 probability of being included in the context since they are two words away from fox.
Using this concept, the Continuous Bag of Words and the Skip Gram model separates data into observations of target words and their context.

### Continuous Bag of Words
We structure the data such that the context is used to predict the target word. For example, if our context is (quick, brown, jumped, over), we use that as features of the class fox.
### Skip Gram
We structure the data such that the target word is used to predict the context. For example, we use the feature (fox) to predict the context (quick, brown, jumped, over).

### Building the Neural Network
Word2vec trains a shallow neural network over data as structured using either Continuous Bag of Words or Skip Gram architecture. Instead of leveraging the model for predictive purposes, we use the hidden weights from the neural network to generate the word vectors.
Assuming a Continuous Bag of Words architecture with a fixed context window of 1 word, this is what the process would look like. First, the corpus.

> I like math
> I like programming
> Today is Friday
> Today is a good day

To make things even easier, we can require our context window to only include words which proceeds the target. We can assume that the context of words at the end of a sentence is the first word of the next sentence. Under such rules:

- like is the context of target I
- math is the context of target like
- programming is also the context of target like

Even with such a simple corpus, we can begin to recognize some patterns. “Math” and “programming” are both context to “like”. While this might not be picked up by the model, both of these words can be understood as things that I like.

#### Step 1
The first step is to one hot encode our classes like we did above with the 'I like turtles' example (the words in our vocabulary): I, like, math, programming, today, is, Friday, a, good, day

#### Step 2
Create a feed forward neural network with one hidden layer and an output layer using the softmax activation function. The data set used to train the network uses the one hot encoded context vector to predict the one hot encoded target vector.
The number of neurons in the hidden layer corresponds to the number of dimensions in the final word vectors.

#### Step 3
Obtain the weights of the hidden network. Each row in the weight matrix corresponds to the vector of each word in the vocabulary.

Realistically, this is not something that we do very often. Good word2vec models require a very large corpus in the billions of words. Fortunately, pre-trained models are easy to use and find. You can download the word2vec model trained over the 100 billion word Google News corpus on their website, or you can use GluonNLP to load a set of pre-trained word embedding.

Practitioners of deep learning for NLP typically initialize their models
using *pre-trained* word embeddings, bringing in outside information, and reducing the number of parameters that their neural network needs to learn from scratch.

To begin, let's first import a few packages that we'll need for this example:

```{.python .input}
import warnings
warnings.filterwarnings('ignore')

from mxnet import gluon
from mxnet import nd
import gluonnlp as nlp
import re
```
Now we'll demonstrate how to index words,
attach pre-trained word embeddings for them,
and use such embeddings in Gluon.
First, let's assign a unique ID and word vector to each word in the vocabulary
in just a few lines of code.

To begin, suppose that we have a simple text data set consisting of newline-separated strings.

```{.python .input}
text = " hello world \n hello nice world \n hi world \n"
```

To start, let's implement a simple tokenizer to separate the words and then count the frequency of each word in the data set. We can use our defined tokenizer to count word frequency in the data set.

```{.python .input}
def simple_tokenize(source_str, token_delim=' ', seq_delim='\n'):
    return filter(None, re.split(token_delim + '|' + seq_delim, source_str))

counter = nlp.data.count_tokens(simple_tokenize(text))
```

The obtained `counter` behaves like a Python dictionary whose key-value pairs consist of words and their frequencies, respectively.
We can then instantiate a `Vocab` object with a counter.

Because `counter` tracks word frequencies, we are able to specify arguments
such as `max_size` (maximum size) and `min_freq` (minimum frequency) to the `Vocab` constructor to restrict the size of the resulting vocabulary.

Suppose that we want to build indices for all the keys in counter.
If we simply want to construct a  `Vocab` containing every word, then we can supply `counter`  the only argument.

```{.python .input}
vocab = nlp.Vocab(counter)
```

A `Vocab` object associates each word with an index. We can easily access words by their indices using the `vocab.idx_to_token` attribute.

```{.python .input}
for word in vocab.idx_to_token:
    print(word)
```

Contrarily, we can also grab an index given a token using `vocab.token_to_idx`.

```{.python .input}
print(vocab.token_to_idx["<unk>"])
print(vocab.token_to_idx["world"])
```

In GluonNLP, for each word, there are three representations: the index of where it occurred in the original input (idx), the embedding (or vector/vec), and the token (the actual word). At any point, we may use any of the following methods to switch between the three representations: `idx_to_vec`, `idx_to_token`, `token_to_idx`.

Our next step will be to attach word embeddings to the words indexed by `vocab`.
In this example, we'll use *fastText* embeddings trained on the *wiki.simple* dataset.
First, we'll want to create a word embedding instance by calling `nlp.embedding.create`,
specifying the embedding type `word2vec` (an unnamed argument) and the source `source='freebase-vectors-skipgram1000'` (the named argument).

```{.python .input}
w2v = nlp.embedding.create('word2vec', source='freebase-vectors-skipgram1000')
```

To attach the newly loaded word embeddings `w2v` to indexed words in `vocab`, we can simply call vocab's `set_embedding` method:

```{.python .input}
vocab.set_embedding(w2v)
```

To see other available sources of pre-trained word embeddings using the *fastText* algorithm,
we can call `text.embedding.list_sources`.

```{.python .input}
nlp.embedding.list_sources('word2vec')
```

The created vocabulary `vocab` includes four different words and a special
unknown token. Let us check the size of `vocab`.

```{.python .input}
len(vocab)
```

By default, the vector of any token that is unknown to `vocab` is a zero vector.
Its length is equal to the vector dimensions of the word2vec word embeddings:
(300,).

```{.python .input}
vocab.embedding['beautiful'].shape
```

The first five elements of the vector of any unknown token are zeros.

```{.python .input}
vocab.embedding['beautiful'][:5]
```

Let us check the shape of the embedding of the words 'hello' and 'world' from `vocab`.

```{.python .input}
vocab.embedding['hello', 'world'].shape
```

We can access the first five elements of the embedding of 'hello' and 'world' and see that they are non-zero.

```{.python .input}
vocab.embedding['hello', 'world'][:, :5]
```

To demonstrate how to use pre-
trained word embeddings in Gluon, let us first obtain the indices of the words
'hello' and 'world'.

```{.python .input}
vocab['hello', 'world']
```

We can obtain the vectors for the words 'hello' and 'world' by specifying their
indices (5 and 4) and the weight or embedding matrix, which we get from calling `vocab.embedding.idx_to_vec` in
`gluon.nn.Embedding`. We initialize a new layer and set the weights using the layer.weight.set_data method. Subsequently, we pull out the indices 5 and 4 from the weight vector and check their first five entries.

```{.python .input}
input_dim, output_dim = vocab.embedding.idx_to_vec.shape
layer = gluon.nn.Embedding(input_dim, output_dim)
layer.initialize()
layer.weight.set_data(vocab.embedding.idx_to_vec)
layer(nd.array([5, 4]))[:, :5]
```

We can also create
vocabulary by using vocabulary of pre-trained word embeddings, such as GloVe.
Below are a few pre-trained file names under the GloVe word embedding.

```{.python .input}
nlp.embedding.list_sources('glove')[:5]
```

For simplicity of demonstration, we use a smaller word embedding file, such as
the 50-dimensional one.

```{.python .input}
glove_6b50d = nlp.embedding.create('glove', source='glove.6B.50d')
```

Now we create vocabulary by using all the tokens from `glove_6b50d`.

```{.python .input}
vocab = nlp.Vocab(nlp.data.Counter(glove_6b50d.idx_to_token))
vocab.set_embedding(glove_6b50d)
```

Below shows the size of `vocab` including a special unknown token.

```{.python .input}
len(vocab.idx_to_token)
```

We can access attributes of `vocab`.

```{.python .input}
print(vocab['beautiful'])
print(vocab.idx_to_token[71424])
```

To apply word embeddings, we need to define
cosine similarity. Cosine similarity determines the similarity between two vectors.

```{.python .input}
from mxnet import nd
def cos_sim(x, y):
    return nd.dot(x, y) / (nd.norm(x) * nd.norm(y))
```

The range of cosine similarity between two vectors can be between -1 and 1. The
larger the value, the larger the similarity between the two vectors.

```{.python .input}
x = nd.array([1, 2])
y = nd.array([10, 20])
z = nd.array([-1, -2])

print(cos_sim(x, y))
print(cos_sim(x, z))
```

### Word Similarity

Given an input word, we can find the nearest $k$ words from
the vocabulary (400,000 words excluding the unknown token) by similarity. The
similarity between any given pair of words can be represented by the cosine similarity
of their vectors.

We first must normalize each row, followed by taking the dot product of the entire
vocabulary embedding matrix and the single word embedding (`dot_prod`).
We can then find the indices for which the dot product is greatest (`topk`), which happens to be the indices of the most similar words.

```{.python .input}
def norm_vecs_by_row(x):
    return x / nd.sqrt(nd.sum(x * x, axis=1) + 1E-10).reshape((-1,1))

def get_knn(vocab, k, word):
    word_vec = vocab.embedding[word].reshape((-1, 1))
    vocab_vecs = norm_vecs_by_row(vocab.embedding.idx_to_vec)
    dot_prod = nd.dot(vocab_vecs, word_vec)
    indices = nd.topk(dot_prod.reshape((len(vocab), )), k=k+1, ret_typ='indices')
    indices = [int(i.asscalar()) for i in indices]
    # Remove unknown and input tokens.
    return vocab.to_tokens(indices[1:])
```

Let us find the 5 most similar words to 'baby' from the vocabulary (size:
400,000 words).

```{.python .input}
get_knn(vocab, 5, 'baby')
```

We can verify the cosine similarity of the vectors of 'baby' and 'babies'.

```{.python .input}
cos_sim(vocab.embedding['baby'], vocab.embedding['babies'])
```

Let us find the 5 most similar words to 'computers' from the vocabulary.

```{.python .input}
get_knn(vocab, 5, 'computers')
```

Let us find the 5 most similar words to 'run' from the given vocabulary.

```{.python .input}
get_knn(vocab, 5, 'run')
```

Let us find the 5 most similar words to 'beautiful' from the vocabulary.

```{.python .input}
get_knn(vocab, 5, 'beautiful')
```

### Word Analogies

We can also apply pre-trained word embeddings to the word
analogy problem. For example, "man : woman :: son : daughter" is an analogy.
This sentence can also be read as "A man is to a woman as a son is to a daughter."

The word analogy completion problem is defined concretely as: for analogy 'a : b :: c : d',
given the first three words 'a', 'b', 'c', find 'd'. The idea is to find the
most similar word vector for vec('c') + (vec('b')-vec('a')).

In this example,
we will find words that are analogous from the 400,000 indexed words in `vocab`.
dkl

```{.python .input}
def get_top_k_by_analogy(vocab, k, word1, word2, word3):
    word_vecs = vocab.embedding[word1, word2, word3]
    word_diff = (word_vecs[1] - word_vecs[0] + word_vecs[2]).reshape((-1, 1))
    vocab_vecs = norm_vecs_by_row(vocab.embedding.idx_to_vec)
    dot_prod = nd.dot(vocab_vecs, word_diff)
    indices = nd.topk(dot_prod.reshape((len(vocab), )), k=k, ret_typ='indices')
    indices = [int(i.asscalar()) for i in indices]
    return vocab.to_tokens(indices)
```

We leverage this method to find the word to complete the analogy 'man : woman :: son :'.

```{.python .input}
get_top_k_by_analogy(vocab, 1, 'man', 'woman', 'son')
```

Let us verify the cosine similarity between vec('son')+vec('woman')-vec('man')
and vec('daughter').

```{.python .input}
def cos_sim_word_analogy(vocab, word1, word2, word3, word4):
    words = [word1, word2, word3, word4]
    vecs = vocab.embedding[words]
    return cos_sim(vecs[1] - vecs[0] + vecs[2], vecs[3])

cos_sim_word_analogy(vocab, 'man', 'woman', 'son', 'daughter')
```

And to perform some more tests, let's try the following analogy: 'beijing : china :: tokyo : '.

```{.python .input}
get_top_k_by_analogy(vocab, 1, 'beijing', 'china', 'tokyo')
```

And another word analogy: 'bad : worst :: big : '.

```{.python .input}
get_top_k_by_analogy(vocab, 1, 'bad', 'worst', 'big')
```

And the last analogy: 'do : did :: go :'.

```{.python .input}
get_top_k_by_analogy(vocab, 1, 'do', 'did', 'go')
```

## Exercises
1. Rewrite the sentiment analysis notebook's code to deal with a different embedding type you personally implemented.
2.

## References

- https://medium.com/analytics-vidhya/introduction-to-natural-language-processing-part-1-777f972cc7b3
- https://gluon-nlp.mxnet.io/examples/word_embedding/word_embedding.html
-
