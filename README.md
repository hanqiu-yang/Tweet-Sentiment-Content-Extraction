# Tweet-Sentiment-Content-Extraction

*This is group project created for a Kaggle competition: Tweet Sentiment Extraction - https://www.kaggle.com/c/tweet-sentiment-extraction*


Project content:

Capturing tweets sentiments is essential in today’s online community since the comments may have significant business or personal impacts. This dataset includes 27481 unique tweets and provides the sentiment for each tweet accordingly.
The training csv file contains four columns: “textID”, “text”, “selected_text”, “sentiment”. The testing csv file contains three columns: “textID”, “text”, “sentiment”.The sentiment includes “neutral”, “positive” and “negative” tones. 

What we need is to develop a method to pick out the part of the tweet (word or phrase) that reflects the sentiment (sentiment is given) - Which means we need to create the "selected_text" column in the test dataset.

Methodology:
- Step 1 - Create ngram from original text;
- Step 2 - Create features: "
