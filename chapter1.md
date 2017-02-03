# **Data collection From Twitter**

Twitter is a popular microblogging platform which gives developers access to tweets using APIs. In this module, we will create a Twitter app and connect with Twitter for collecting our dataset.

### **Creating Twitter app**

We will now create a Twitter app to get authentication details and establish connection with Twitter.

1. Login with your existing \(or create a new\) Twitter account at [twitter.com](https://twitter.com/login)

2. Open the Application Management Portal at [apps.twitter.com](https://apps.twitter.com)

3. Click on “Create new App”

4. Fill in Application Details. Note that the website url in application details should start with http://

5. Click on “Create your Twitter application”. You will be redirected to your new app.

6. Navigate to “Keys and Access Tokens” tab and scroll down to “Access Tokens”

7. Click on “Create my access token

8. Copy paste your Consumer Key \(API Key\), Consumer Secret \(API Secret\), Access Token and Access Token Secret in a txt file, as we will be using these details to connect with Twitter in the next steps.

### **Collecting tweets for specific hashtags or topics**

We’ll now see how to authenticate and connect with Twitter using Tweepy.

* #### **Authentication and Connection with Twitter**

We will use Tweepy - a Twitter-Python Library for authenticating and connecting with Twitter. The tweepy.OAuthHandler authenticates your app and establishes connection using the access token as shown below:

> ```py
> import tweepyauth = tweepy.OAuthHandler(consumer_key, consumer_secret)
> auth.set_access_token(access_key, access_secret)api = tweepy.API(auth)
> ```

_This code snippet is for understanding only._

Using Tweepy API you can create, delete and collect tweets. We’ll see how to search in the history and track live tweets for data collection.

* #### **Search the history**

Using Twitter’s REST API, you can pull data from Twitter, search tweets which are 6-8 days old. A maximum of 180 Requests per 15 mins window for per-user authentication can be made. And a maximum of 18500 tweets/15 mins can only be collected, any number above 18500 will make your connection window to expire.

The below code snippet searches for a set of keywords or a single keyword, with filter as “English”.

> `api.search(‘keywords’,'en', count = 100)`

This returns a response from Twitter in json format with all properties of tweet. We can choose to save a few of properties in any file format.

Finding out what properties we need to save from the Twitter response is very important. Since we are going to perform sentiment analysis on tweets, we will need the tweet text, tweet id \(unique identifier for each tweet\) and the tweet time.

Using the code snippet below, you can receive one tweet response and understand it’s properties. Here we set the tweet count to be 5 on purpose, as our goal is to understand the Twitter json response.

> ```py
> import tweepy
> access_key = "your access key"
> access_secret = "your access secret"
> consumer_key = "your consumer key"
> consumer_secret = "your consumer secret"
>
> #to authenticate
> auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
> auth.set_access_token(access_key, access_secret)
> api = tweepy.API(auth)
> for tweet in api.search('Qatar','en',count = 5):
>     print tweet
>     print "*****end of one tweet*****"
> ```

JSON response for a tweet will look like below. The tweet properties we need such as text, id are highlighted.

```json
Status(contributors=None, truncated=False,text=u'RT @OnlineJobsQatar: Cloud Sales Leader - GNP Job 
https://t.co/6KOyFVLDhG
 @gulf_recruit #doha #jobsavailable #jobsinqatar #qatar', is_quote_status=False, in_reply_to_status_id=None,id=825936244324573184L, favorite_count=0, _api=<tweepy.api.API object at 0x03232B70>, author=User(follow_request_sent=False, has_extended_profile=True, profile_use_background_image=True, _json={u'follow_request_sent': False, u'has_extended_profile': True, u'profile_use_background_image': True, u'default_profile_image': False, u'id': 110190113, u'profile_background_image_url_https': u'
https://pbs.twimg.com/profile\_background\_images/353684821/vinoth\_.JPG
', u'verified': False, u'translator_type': u'none', u'profile_text_color': u'0C3E53', u'profile_image_url_https': u'
https://pbs.twimg.com/profile\_images/745899828052430848/2E5r3JVt\_normal.jpg
', u'profile_sidebar_fill_color': u'FFF7CC', u'entities':...
```

You can parse the json using python or by using [online json parser](http://json.parser.online.fr/) to make it more readable.** **

* #### **Track live tweets**

To track live tweets stream, Twitter Streaming API is used. Stream created using tweepy will be used to create a feed of tweets, as the Streaming API pushes messages to a persistent session. This is the reason why more number of tweets can be downloaded in real time than using the REST API.

We’ll use SEARCH API to pull previous tweets, as it is much faster to get old tweets than tracking live tweets. Tracking live tweets is explained for your understanding and can be explored from [more here](http://docs.tweepy.org/en/v3.4.0/streaming_how_to.html).

* #### **Data Collection**

  **Specific Topic or Event**

As we aim to analyze the sentiment of Gulf Airlines such as Qatar Airways, Emirates and Etihad Airways, a list of relevant hashtags and keywords can be populated. One keyword at a time or a list of keywords can also be used.** **

Find the [hashtag-keywords.txt file here](https://github.com/ArabWICQatar/TwitterSentimentAnalysisVisualization/blob/master/hashtags-keywords.txt) containing a list of keywords.

> _**Create a project folder and copy the hashtag-keywords.txt file**_

* #### **Code**

This python script establishes connection with Twitter and searches for tweets containing keywords and hashtags from keywords.txt file. The function search in python script is written to perform search and gather all tweets in a csv file searchTweets.csv.

> _**Save the script as searchTweets.py in your project folder, edit to add your Twitter app credientials and Run**_

You will see the output searchTweets.csv file saved inside search-data folder.

_You can also find the script file inside your project folder._

```py
'''
To authenticate and connect with Twitter
Use search REST API to gather tweets from a list of keywords
Store tweets as a csv file
'''

import tweepy
import sys
import csv

# to force utf-8 encoding on entire program
reload(sys)
sys.setdefaultencoding('utf8')

alltweets = csv.writer(open("search-data/searchTweets.csv", 'ab'))

def search(keywords):
    access_key = "your app access key here"
    access_secret = "your app access token here"
    consumer_key = "your app consumer key here"
    consumer_secret = "your app consumer secret here"

    #to authenticate
    auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
    auth.set_access_token(access_key, access_secret)
    api = tweepy.API(auth)

    count = 1;
    for tweet in api.search(keywords,'en', count = 100):
        created_at =  tweet.created_at  # accessing tweet time
        tweet_id = tweet.id_str         # accessing tweet id
        tweet_text = tweet.text         # accessing tweet text
        print "gathered tweet ",count
        count = count + 1
        alltweets.writerow([created_at, tweet_id, tweet_text])

#search("Qatar Airways") # to search one keyword at a time

file = open('hashtags-keywords.txt', 'r') # contains a list of keywords
queries = file.readlines()

for q in queries:
    # read one keyword at a time
    print "----"
    print q
    search(q)
```

The collected data will have many duplicates, as a same tweet can be retweeted several times.

_Get started with the _[_Preprocessing_](/preprocessing.md)_._

