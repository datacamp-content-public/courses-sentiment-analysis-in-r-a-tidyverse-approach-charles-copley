---
title: Insert title here
key: 106a7c5fade7e64b6db58bda3e72ec16

---
## Lesson  2.1 Pre-processing: Tokenization

```yaml
type: "TitleSlide"
key: "e7c4963d25"
```

`@lower_third`

name: Charles Copley
title: Head of Data Science


`@script`
Previously we learned about sentiment analysis, and specifically how it fits well with the tidyverse way of implementing data processing pipelines. In this video we will be teaching you about the very first step in a standard natural language processing pipeline: tokenization


---
## What is a token?

```yaml
type: "FullSlide"
key: "1d28895992"
```

`@part1`
A _unit_ after breaking up text into pieces
1. Words
2. Phrases
3. Sentences


`@script`
To start with, let us refresh what a token is, so that we can better understand the process of tokenization. A token is what you get after breaking up a piece of text into smaller pieces, and usually involves discarding punctuation The smaller piecse are usually words, but can also be other units of language such as phrases or sentences. We will see how this concept is useful through the rest of this Course


---
## Tidyverse tokenization?

```yaml
type: "FullSlide"
key: "7517a871b3"
```

`@part1`
Reminder of what Tidy Data should look like:
- Each variable forms a column
- Each observation forms a row
- Each type of observation forms a table
 
Let us start with the book _Treasure Island_ by Robert Louis Stevenson
```
treasure_island <- gutenberg_download(c(120))
```


`@citations`
Wickham, H, Journal of Statistical Software, August 2014


`@script`
Ok, so we understand tokenization... But how would tokenization be implemented in tidyverse? In the 2014 paper, Hadley Wickham described Tidy data is based on the following principles: Each variable is a column, each observation is a row and each type of observational unit is a table. So we can expect that tokenized text will conform to this when implemented in tidyverse...To illustrate this we will be using the text from Treasure Island by Robert Louis Stevenson


---
## The unnest_tokens() function

```yaml
type: "TwoRows"
key: "7a0a5314b3"
disable_transition: false
```

`@part1`
```
treasure_island %>% unnest_tokens(tokens, text, token = 'words')
	%>% count(tokens) 
    %>% with(wordcloud(tokens, n, max.words =100,
    colors=pal_col))  
```


`@part2`
![](https://assets.datacamp.com/production/repositories/5077/datasets/2c5a3ad0308ce02b917066cf0ee7991071f29895/wordcloud.png = 35)


`@script`
In R tidytext, tokenization is carried out by the unnest_tokens() function. 

Running the code below uses this function and pipes the output into the count() function and finishes with a wordcloud depiction of the word counts in the book. The size of a word depicts the relative frequency of occurrence of the word in the book 

You can see from this that there is a problem- there are a large number of occurrences of uninteresting words- we call these stopwords and we will be dealing with those in a subsequent lesson.


---
## What does unnest_tokens() do?

```yaml
type: "FullSlide"
key: "8a81a6d5f2"
```

`@part1`
So... what does unnest_tokens() actually do?

```
treasure_island 
	%>% unnest_tokens(tokens, text, token = 'words')
```

![](https://assets.datacamp.com/production/repositories/5077/datasets/88b7db9de3aa2e4bf27b8b7ed10fa1dfc55f4585/tokens_r.png = 50)


`@script`
In tidy text we expect that each variable should be a column and each observation a row. For the tokenizer we then expect that each row should represented a token, looking at the output table this is what we see together with the gutenberg_id identifier of the book on Project Gutenberg.


---
## Options for the tokenizer?

```yaml
type: "FullSlide"
key: "a188af3d9f"
```

`@part1`
```
treasure_island 
  %>% unnest_tokens(tokens, text, token = 'ngrams',n = 2)
  %>% count(tokens) 
  %>% with(wordcloud(tokens, n, max.words = 100,
      colors=pal_col)) 
```
![](https://assets.datacamp.com/production/repositories/5077/datasets/398a6bd3e1a47c897cb17cedff611b7f46428ec2/datacamp%20wordclouds.png = 35)


`@script`
We mentioned earlier that tokens can be different 'pieces' of text like words, sentences, phrases and other sections. The unnest_token() function gives the following options:
"words" (default), "characters", "character_shingles", "ngrams", "skip_ngrams", "sentences", "lines", "paragraphs", "regex",and even "tweets"! 

In the above example we have used n-grams with n=2 to show how two-word combinations exist in the Treasure Island example...


---
## Let's practice!

```yaml
type: "FinalSlide"
key: "598027f497"
```

`@script`
It is time to put this into practice- let's try out some tokenization!

