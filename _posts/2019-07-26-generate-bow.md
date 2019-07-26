
---
title: Generate Bag of Word(Step by Step)
---

We know **Neural Network** or **Machine Learning Algorithm** need features to train. 
**Bag of Words(BOW)** is a method to extract features from text. 

**STEPS:**

**Document**>>**Clean Text**>>**Tokenize**>>**Build Vocabulary**>>**Generate Vectors**

## Cleaning Text


```python
import re

document = "Joe waited for the train. The train was late. Mary and Samantha took the bus. I looked for Mary and Samantha at the bus station. Mary and Samantha arrived at the bus station early but waited until noon for the bus."

# removing punctuation and separating sentence with comma(,)
remove_punc_text = re.sub(r'[^\w\s]',',',document)
print(remove_punc_text)
```

    Joe waited for the train, The train was late, Mary and Samantha took the bus, I looked for Mary and Samantha at the bus station, Mary and Samantha arrived at the bus station early but waited until noon for the bus,
    


```python
clean_text = remove_punc_text.split(", ")
print(clean_text)
```

    ['Joe waited for the train', 'The train was late', 'Mary and Samantha took the bus', 'I looked for Mary and Samantha at the bus station', 'Mary and Samantha arrived at the bus station early but waited until noon for the bus,']
    

## Tokenize


```python
"""
word_extraction function will split sentence into words and ignore stopwords.
Here we give a small stopwords set('a', 'the', 'is')

"""

def word_extraction(sentence):
    ignore = ["a", "the", "is"]
    words = re.sub("[^\w]", " ",  sentence).split()
    cleaned_text = [w.lower() for w in words if w not in ignore]
    return cleaned_text
```


```python
# applying tokenization to our all sentences
def tokenize(sentences):
    words = []
    for sentence in sentences:
        w = word_extraction(sentence)
        words.extend(w)
        
    words = sorted(list(set(words)))
    return words

tokens = tokenize(clean_text)
print(tokens)
```

    ['and', 'arrived', 'at', 'bus', 'but', 'early', 'for', 'i', 'joe', 'late', 'looked', 'mary', 'noon', 'samantha', 'station', 'the', 'took', 'train', 'until', 'waited', 'was']
    

## Build Vocabulary


```python
vocab = tokens
print("Word List for Document \n{0} \n".format(vocab));
print("Length of our vocabulary is:", len(vocab))
```

    Word List for Document 
    ['and', 'arrived', 'at', 'bus', 'but', 'early', 'for', 'i', 'joe', 'late', 'looked', 'mary', 'noon', 'samantha', 'station', 'the', 'took', 'train', 'until', 'waited', 'was'] 
    
    Length of our vocabulary is: 21
    

## Generating Vectors


```python

import numpy as np

for sentence in clean_text:
        words = word_extraction(sentence)
        bag_vector = np.zeros(len(vocab))
        for w in words:
            for i,word in enumerate(vocab):
                if word == w: 
                    bag_vector[i] += 1
                    
        print("{0}\n{1}\n".format(sentence,np.array(bag_vector)))
        

```

    Joe waited for the train
    [0. 0. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0.]
    
    The train was late
    [0. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 0. 0. 0. 0. 1. 0. 1. 0. 0. 1.]
    
    Mary and Samantha took the bus
    [1. 0. 0. 1. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0. 0. 1. 0. 0. 0. 0.]
    
    I looked for Mary and Samantha at the bus station
    [1. 0. 1. 1. 0. 0. 1. 1. 0. 0. 1. 1. 0. 1. 1. 0. 0. 0. 0. 0. 0.]
    
    Mary and Samantha arrived at the bus station early but waited until noon for the bus,
    [1. 1. 1. 2. 1. 1. 1. 0. 0. 0. 0. 1. 1. 1. 1. 0. 0. 0. 1. 1. 0.]
    
    

## Explanation

How it works:

*step 1:* Initiaze a zero vector array with len(vocab)

our here: `[0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]`

*step 2:* enumerate the vocabulary

Our here: 

`0 : and, 1 : arrived, 2 : at, 3 : bus, 4 : but, 5 : early, 6 : for,
7 : i, 8 : joe, 9 : late, 10 : looked, 11 : mary, 12 : noon, 13 : samantha, 
14 : station, 15 : the, 16 : took, 17 : train, 18 : until, 19 : waited, 20 : was`

*step 3:* Compare each word with this enumeration list and increament vector element value

such as: 

for sentence:

`Joe waited for the train`

`[0. 0. 0. 0. 0. 0. 1. 0. 1. 0. 0. 0. 0. 0. 0. 0. 0. 1. 0. 1. 0.]`


word `joe` position is 8. so we increament vector value to 1 at position 8.
same for other words.

**Now use these feature vectors for you Machine Learning Model.**

