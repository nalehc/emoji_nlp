# Getting Emoji-nal
Applying nlp to emoji

## Background

As of 2016, 92% of the online population use emoji to communicate to each other. I wanted to try and apply NLP techniques to these characters to analyze reddit comments. By doing this, the thought was that the emoji might provide additional meaning and sentiment value to the text beyond just the words. 

## Tools

Using PRAW (Python Reddit API Wrapper), I collected about 12,000 comments with emoji. After cleaning this data using pandas and the python emoji package, I tokenized the text with NLTK, built a sentiment analyzer using numpy to assign emotion value vectors to each comment and built a naive bayes model with Sklearn to classify the associated emoji.

## Detailed Process
To tokenize comments, I used the word Tokenize function from SkLearn to seperate words and used a standard regex to seperate emoji tokens. From here, I used a lexicon I found [here].(http://sentiment.nrc.ca/lexicons-for-research/) The lexicon pairs words with positive and negative sentiment as well as 8 emotional affects. For example, the word "abandon" is associated with the emotions anger, fear, and sadness, so it scores a one for each of those values. For sentiment, it's a negative word, so it scores 1 there as well. Some words do not have emotional value or sentiment (such as "bifurcation"). The summed total of the words in the comment are assigned as a new column in my data. Tokenized emoji were then td-idf vectorized.


I then performed DBSCAN with SkLearn to cluster the emotional vectors. The results were not ideal, but I did end up with 4 recognizable clusters, 3 with generally positive emotional values and/or positive sentiment and one with neutral (0 value) average emotion vector values. 

By assigning a cluster label to each comment, I was able to build a Naive Bayes Classifier to classify my td-idf emoji vectors based on cluster label. 

## Conclusions and Improvements

I believe the results my classifier provides is useful in certain contexts, such as providing an idea whether the comment writer is attempting to convey a positive message (e.g. a joke, heartfelt encouragement). However, I believe the model can and should be improved. First, there should be some attempt to include more modern evolutions of word emotion (a good example is "dying" which in the data generally was always positive (dying of laughter or affection for someone/something), but in the dictionary had a value of fearful affect and negative sentiment). We could do this by analyzing emoji sentiment and word sentiment seperatly to determine if there were strong neg/pos combinations which might indicate slang or sarcasm. We might also combine Emoji2Vec to embed word meanings to emoji or use sense embeddings of the emotion dictionary to improve results.  
