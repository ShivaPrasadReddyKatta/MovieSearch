# MovieRecommender
The recommender project is divided into 3 phases of which the first phase is 'Search'. I chose a movie recommendation project and the phase 1 is all about retrieving the movie details when a query(it can be a title or a movie description) is given. The search engine was made possible by utilising concepts such as TF-IDF and Cosine Similarity.</br>

First I imported python libraries like numpy and pandas. The dataset I chose has a total of 24 columns, but out of all of them I
chose only 3 columns which are 'overview', 'tagline', and 'genres'. I combined all these columns into a single column named as text_dump.

    def text_dump(data):
        return data['original_title'] + ' ' + data['overview'] + ' '  + data['tagline'] + ' ' .join(data['genres'])
    df['unprocesses_text_col'] = df.apply(text_dump, axis=1)
    df['unprocesses_text_col'][23455]

Now, I converted the text into lower case and removed punctuation, stopwords from it.

    df.unprocesses_text_col = df.unprocesses_text_col.apply(lambda x: x.lower())
    df['unprocesses_text_col'][23455]
    df['unprocesses_text_col'] = df['unprocesses_text_col'].str.replace('[^\w\s]','')
    df['unprocesses_text_col'][23455]
    cachedStopWords = stopwords.words("english")

    def removeStopWords(text):
        text = ' '.join([word for word in text.split() if word not in cachedStopWords])
        return text

    df['processed_text_col'] = df['unprocesses_text_col'].apply(removeStopWords)
    df['processed_text_col'][23455]
    
 The next step involves stemming and I used Snowball Stemmer which is the version 2 of Porter stemmer.

    stemmer = SnowballStemmer('english')

    def stemmerk(text):
        words = word_tokenize(text)
        return ' '.join([stemmer.stem(w) for w in words])
    df['processed_text_col'] = df['processed_text_col'].apply(stemmerk)
    df['processed_text_col'][23455]
    
Now, I will generate a count matrix for each movie and calculate the TF-IDF.

    count = CountVectorizer()
    count_matrix = count.fit_transform(df['processed_text_col'])
    tfidf_transformer = TfidfTransformer()
    train_tfidf = tfidf_transformer.fit_transform(count_matrix)
    
The following function will take a query as input and return the top 3 results using Cosine Similarity

    def movieList(entry):
        entry = entry.lower()
        entry = re.sub(r'[^\w\s]','',entry)
        entry = removeStopWords(entry)
        entry = stemmerk(entry)
        entry_count_matrix = count.transform([entry])
        entry_tf_idf = tfidf_transformer.transform(entry_count_matrix)
        similarity_score = cosine_similarity(entry_tf_idf, train_tfidf)
        sorted_indexes = np.argsort(similarity_score).tolist()
        return df[['original_title', 'overview']].iloc[sorted_indexes[0][-3:]]
    
    
# Project Report and Video    
You can find my project brochure, project video, and project report under the posts section in my webiste.(https://techno-astrophile.netlify.com)


# REFERENCES

For converting the text into lower case I referred to Chaim Gluck code from his post on Medium: https://medium.com/@chaimgluck1/have-messy-text-data-clean-it-with-simple-lambda-functions-645918fcc2fc

For removing punctuation I referred Bob Haffner’s code from StackOverflow: https://stackoverflow.com/questions/39782418/remove-punctuations-in-pandas

For punctuation I also referred Quora post: https://www.quora.com/How-do-I-remove-punctuation-from-a-Python-string

For removing stop words I referred code provided by Andy Rimmer in StackOverflow: https://stackoverflow.com/questions/19560498/faster-way-to-remove-stop-words-in-python

For tfidf and sorting the results I referred Heet Madhus code : https://github.com/Heetmadhu/Movie-Recommendation/blob/master/MovieSearch.ipynb

For cosine similarity I referred to Emma Giraldi code: https://github.com/emmagrimaldi/Content_based_movie_recommender/blob/master/.ipynb_checkpoints/EG_project5-checkpoint.ipynb

# How to install and use the application
Download the APK file and install it on your Android mobile. The App is named as 'movieREC'. Upon opening the app you can find two options 'Login' and 'Guest User', click on guest user and continue. 


