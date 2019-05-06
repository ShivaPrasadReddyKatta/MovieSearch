# MovieRecommender
First I imported python libraries like numpy and pandas. The dataset I chose has a total of 24 columns, but out of all of them I
chose only 3 columns which are 'overview', 'tagline', and 'genres'. I combined all these columns into a single column named as text_dump.
Now, I converted the text into lower case and removed stop words from it. Also, I created the count matrix and calculated the tfidf score. 
When the search query is entered it is processed same like the text column by converting it into lowercase, removing stopwords etc., and
also the cosine similarity score is calculated and the results are ranked accordingly.


REFERENCES

For converting the text into lower case I referred to Chaim Gluck code from his post on Medium: https://medium.com/@chaimgluck1/have-messy-text-data-clean-it-with-simple-lambda-functions-645918fcc2fc

For removing punctuation I used Bob Haffner’s code from StackOverflow: https://stackoverflow.com/questions/39782418/remove-punctuations-in-pandas

For punctuation I also referred Quora post: https://www.quora.com/How-do-I-remove-punctuation-from-a-Python-string

For removing stop words I used code provided by Andy Rimmer in StackOverflow: https://stackoverflow.com/questions/19560498/faster-way-to-remove-stop-words-in-python

For tfidf and sorting the results I used Heet Madhus code : https://github.com/Heetmadhu/Movie-Recommendation/blob/master/MovieSearch.ipynb

For cosine similarity I referred to Emma Giraldi code: https://github.com/emmagrimaldi/Content_based_movie_recommender/blob/master/.ipynb_checkpoints/EG_project5-checkpoint.ipynb


