# MovieRecommender
First I imported python libraries like numpy and pandas. The dataset I chose has a total of 24 columns, but out of all of them I
chose only 3 columns which are 'overview', 'tagline', and 'genres'. I combined all these columns into a single column named as text_dump.
Now, I converted the text into lower case and removed stop words from it. Also, I created the count matrix and calculated the tfidf score. 
When the search query is entered it is processed same like the text column by converting it into lowercase, removing stopwords etc., and
also the cosine similarity score is calculated and the results are ranked accordingly.
