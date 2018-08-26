# Getting Emoji-nal
Applying nlp to emoji

## Background

As of 2016, 92% of the online population use emoji to communicate to each other. I wanted to try and apply NLP techniques to these characters to analyze reddit comments. By doing this, the thought was that the emoji might provide additional meaning and sentiment value to the text beyond just the words. 

## Tools

Using PRAW (Python Reddit API Wrapper), I collected about 12,000 comments with emoji. After cleaning this data using pandas and the python emoji package, I tokenized the text with Sklearn, built a sentiment analyzer using numpy to assign emotion value vectors to each comment and built a naive bayes model with Sklearn to classify the associated emoji.

## Detailed Process



