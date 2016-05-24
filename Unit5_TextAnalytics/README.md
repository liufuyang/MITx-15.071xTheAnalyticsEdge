# Text Analysis

## Bag of words
### Text cleaning up before apply bag of words:
* change all words to either lower-case or upper-case
    * Apple, aPPLE, APPLE -> apple:3
* remove all punctuations 
    * @apple, Apple!!!, --apple-- -> apple:3
* remove unhelpful terms (stop words)
    * Examples: the, is, at, which...
    * Words unlikely to improve machine learning prediction quality
    * Remove to reduce size of data
    * Becareful of some exceptions
* Stemming
    * argue, argued, argues, arguing
    * stem argu
    * Algorithmic process of performing this reduction is called stemming
    * Many ways to approach the problem
        * One approch: build a database of words and their stems
            * Pro: handles exceptions
            * Con: won't handle new words, bad for the Internet!
        * Another approch: can write a rule-based algorithm
            * e.g. if words ends in "ed", "ing", or "ly", remove it
            * Pro: handles new/unknown words well
            * Con: many exceptions, missed words like child and chilren, mouse and mice
        * Another better option:
            * "Porter Stremmer" by Martin Porter in 1980
            * Stemmers have been written for many languages
        * Other options include machine learning (train algorithms to recognize the roots of the words) and combinations of the above.

### R examples:
```
corpus = Corpus(VectorSource(tweets$Tweet))
corpus = tm_map(corpus, tolower)
corpus = tm_map(corpus, PlainTextDocument)

corpus = tm_map(corpus, removePunctuation)

corpus = tm_map(corpus, removeWords, c("apple", stopwords("english")))

corpus = tm_map(corpus, stemDocument)
```

And works like 

`'I have to say, Apple has by far the best customer care service I have ever received! @Apple @AppStore'`
will become:
`say far best custom care servic ever receiv appstor`
