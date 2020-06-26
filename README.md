# Tweet-Sentiment-Content-Extraction

*This is group project created for a Kaggle competition: Tweet Sentiment Extraction - https://www.kaggle.com/c/tweet-sentiment-extraction*


Project content:

Capturing tweets sentiments is essential in today’s online community since the comments may have significant business or personal impacts. This dataset includes 27481 unique tweets and provides the sentiment for each tweet accordingly.
The training csv file contains four columns: “textID”, “text”, “selected_text”, “sentiment”. The testing csv file contains three columns: “textID”, “text”, “sentiment”.The sentiment includes “neutral”, “positive” and “negative” tones. 

What we need is to develop a method to pick out the part of the tweet (word or phrase) that reflects the sentiment (sentiment is given) - Which means we need to create the "selected_text" column in the test dataset.

Methodology:
- Step 1 - Preprocessing:
  - Drop missing value (row 314) from train set;
  - Remove texts with neutral sentiment from train set and test set;
  - Remove URL from train set and test set;
  - Create n-grams subsets for train set and test set from original texts for only the row with subsets Len(ngrams) / Len(original text) <= 0.5.
  
- Step 2 - Create features: 
  Create part of general features without using n-grams to save time. Then create other features for texts after creating train subsets and test subsets with n-grams： 
  - Text_n_words: Number of words in original text
  - Text_n_str: Number of strings in original text
  - Text_n_uq_chars: Number of unique characters in original text
  - Sel_text_n_words: Number of words in ngram
  - Prop_sel_text_len: Length of selected words / Length of original texts
  - Sentiment: positive/ negative/ neutral
  - Dif_text_sent_blob: sentiment score difference between ngram and original text based on Blob sentiment analysis package
  - Sel_text_n_str: Number of strings of texts in ngram
  - Prop_sel_text_n_str: Number of strings of ngram / Number of strings of texts
  - Sel_text_n_uq_words: Number of unique words of ngram
  - Prop_sel_text_n_uq_words: Number of unique words in ngram / Number of unique words in the original text
  - Prop_sel_text_n_uq_chars: Number of unique characters in ngram / Number of unique characters in original text
  - Prop_sel_text_n_prepositions: Number of prepositions in ngram / Number of prepositions in original text
- Step 3 - Create Dependent Variable:
  - Jaccard: Jaccard score between n-grams and selected text
- Step 4 - Train model and make predictions
  - Train XgBoost regression model on created train subsets with n-grams;
  - Used trained model to predict jaccard score on test subsets with n-grams;
  - Select rows of texts with unique ‘textID’ with the highest jaccard score;
  - Use ‘ngram’ in each of the rows as predictions for texts with positive/negative sentiment;
  - Use original text to represent predictions for texts with neutral sentiment.
