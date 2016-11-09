---
title: Sentence Split
---

There are multiple way to split sentence into a list of text.
Some papers said they use `nltk` and some said `Stanford NLP`. Here are
example of how to use it.

**using nltk**

```python
from nltk.tokenize import word_tokenize, sent_tokenize
def sent_split(documents):
    words = [word_tokenize(sent) for sent in sent_tokenize(text)]
    return words

text = 'Hello all. My name is Titipat, the best LoL player.'
sent_split(text)
```

**using stanford core nlp**

```python
import re
from pycorenlp import StanfordCoreNLP
nlp = StanfordCoreNLP('http://localhost:9000')

properties={
  'annotators': 'ssplit',
  'outputFormat': 'json'
  }

def sentence_split(text, properties={'annotators': 'ssplit', 'outputFormat': 'json'}):
    """Split sentence using Stanford NLP"""
    annotated = nlp.annotate(text, properties)
    sentence_split = list()
    for sentence in annotated['sentences']:
        s = [t['word'] for t in sentence['tokens']]
        sentence_split.append(s)
    return sentence_split

text = 'Hello all. My name is Titipat, the best LoL player.'
sentence_split(text, properties)
```
