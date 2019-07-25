# Text Preprocessing
It's important to preprocess text to make it machine understandable. 

Like image after obtaining text we need to normalize it. 

## Text Normalization

Text Normalization includes:

* **Converting all letters to lower or upper case**
* **Converting number into words or removing numbers**
* **Removing punctuation mark, accent mark**
* **Removing whitespaces**
* **Expanding  abbreviations**
* **Removing stop words, sparse terms, and particular words**

### converting to lowercase

```py
>>>text = "The 5 biggest countries by population in 2017 are China, India, United States, Indonesia, and Brazil."
>>>text.lower()
'the 5 biggest countries by population in 2017 are china, india, united states, indonesia, and brazil.'

```

### Removing Numbers

```py
>>>import re
>>> text = 'Box A contains 3 red and 5 white balls.'
>>> result = re.sub(r'\d+', '',text)
>>> result
 'Box A contains  red and  white balls.'

```

### Removing Punctuations

```py
import re
text = 'hello!, this is what?'
regex = re.compile('[%s]' % re.escape(string.punctuation))
result = regex.sub('', text)
result
# output: 'hello this is what'

```

### Removing Whitespace

```py
input_str = " \t a string example\t "
input_str = input_str.strip()
input_str
```

### Removing stop words

```py
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize

input_str = "NLTK is a leading platform for building Python programs to work with human language data."
stop_words = set(stopwords.words(‘english’))
tokens = word_tokenize(input_str)
result = [i for i in tokens if not i in stop_words]
print (result)
# output: ['NLTK', 'leading','platform', 'building', 'Python', 'programs', 'work','human', 'language', 'data', '.']

```

### Stemming

```py
from nltk.stem import PorterStemmer
from nltk.tokenize import word_tokenize
stemmer= PorterStemmer()
input_str="There are several types of stemming algorithms."
input_str=word_tokenize(input_str)
for word in input_str:
    print(stemmer.stem(word))
    
# output: there are sever type of stem algorithm.
```

### Lemmatization

```py
from nltk.stem import WordNetLemmatizer
from nltk.tokenize import word_tokenize
lemmatizer=WordNetLemmatizer()
input_str="been had done languages cities mice"
input_str=word_tokenize(input_str)
for word in input_str:
    print(lemmatizer.lemmatize(word))

# output: be have do language city mouse
```


## References
1. [https://medium.com/@datamonsters/text-preprocessing-in-python-steps-tools-and-examples-bf025f872908](https://medium.com/@datamonsters/text-preprocessing-in-python-steps-tools-and-examples-bf025f872908)
2. [https://stackoverflow.com/questions/265960/best-way-to-strip-punctuation-from-a-string-in-python](https://stackoverflow.com/questions/265960/best-way-to-strip-punctuation-from-a-string-in-python)
