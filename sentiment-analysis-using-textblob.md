# Sentiment Analysis using TextBlob

TextBlob is a python API which is well known for different applications like Parts-of-Speech, Tokenization, Noun-phrase extraction, Sentiment analysis etc. We will use TextBlob for sentiment analysis, by feeding the unique tweets and obtaining the sentiment polarity as output. More on sentiment analysis using TextBlob can be found[here](http://textblob.readthedocs.io/en/dev/quickstart.html#sentiment-analysis).

On executing the below python script: the sentimentUniqueTweets.csv will have the sentiment polarity score and the corresponding sentiment, as the polarity value ranges between \[-1, 1\]. So a tweet has Positive sentiment when it’s polarity is greater than 0 and negative sentiment when it’s polarity is lesser than 0. When the sentiment polarity is exactly 0 the tweet is said to have neutral polarity.

> _**Save the below script as sentiment.py in your project folder and Run the script**_

You will see the output sentimentUniqueTweets.csv file with sentiment polarity inside search-data folder.

```py
'''
uses TextBlob to obtain sentiment for unique tweets
'''

import csv
from textblob import TextBlob
import sys

# to force utf-8 encoding on entire program
reload(sys)
sys.setdefaultencoding('utf8')

alltweets = csv.reader(open("search-data/uniqueSearchTweets.csv", 'rb'))
sntTweets = csv.writer(open("search-data/sentimentUniqueTweets.csv", "wb"))

for row in alltweets:
    blob = TextBlob(row[2])
    print blob.sentiment.polarity
    if blob.sentiment.polarity > 0:
        sntTweets.writerow([row[0], row[1], row[2], blob.sentiment.polarity, "positive"])
    elif blob.sentiment.polarity < 0:
        sntTweets.writerow([row[0], row[1], row[2], blob.sentiment.polarity, "negative"])
    elif blob.sentiment.polarity == 0.0:
        sntTweets.writerow([row[0], row[1], row[2], blob.sentiment.polarity, "neutral"])
```

We now have sentiment generated for all unique tweets. 

_Let's get started with the _[_Visualizing_](/visualization-using-highcharts.md)_ the results._

