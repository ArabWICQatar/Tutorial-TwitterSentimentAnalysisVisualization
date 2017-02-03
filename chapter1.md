# **Data collection From Twitter**

Twitter is a popular microblogging platform which gives developers access to tweets using APIs. In this module, we will create a Twitter app and connect with Twitter for collecting our dataset.

### **Creating Twitter app**

We will now create a Twitter app to get authentication details and establish connection with Twitter.

1. Login with your existing \(or create a new\) Twitter account at [twitter.com](https://twitter.com/login)

2. Open the Application Management Portal at [apps.twitter.com](https://apps.twitter.com)

3. Click on “Create new App”

4.  Fill in Application Details. Note that website url should start with http://

5. Click on “Create your Twitter application”. You will be redirected to your new app.

6. Navigate to “Keys and Access Tokens” tab and scroll down to “Access Tokens”

7. Click on “Create my access token

8. Copy paste your Consumer Key \(API Key\), Consumer Secret \(API Secret\), Access Token and Access Token Secret in a txt file, as we will be using these details to connect with Twitter in the next steps.

For more details - View the following image.

### **Collecting tweets for specific hashtags or topics**

We’ll now see how to authenticate and connect with Twitter using Tweepy.

* #### **Authentication and Connection with Twitter**

We will use Tweepy - a Twitter-Python Library for authenticating and connecting with Twitter. The tweepy.OAuthHandler authenticates your app and establishes connection using the access token as shown below:

> `import tweepyauth = tweepy.OAuthHandler(consumer_key, consumer_secret)`
>
> `auth.set_access_token(access_key, access_secret)api = tweepy.API(auth)`

_This code snippet is for understanding only._



Using Tweepy API you can create, delete and collect tweets. We’ll see how to search in the history and track live tweets for data collection.

* #### **Search the history**

Using Twitter’s REST API, you can pull data from Twitter, search tweets which are 6-8 days old. A maximum of 180 Requests per 15 mins window for per-user authentication can be made. And a maximum of 18500 tweets/15 mins can only be collected, any number above 18500 will make your connection window to expire.

The below code snippet searches for a set of keywords or a single keyword, with filter as “English”.

> `api.search(‘keywords’,'en', count = 100)`

  
This returns a response from Twitter in json format with all properties of tweet. We can choose to save a few of properties in any file format. 

Finding out what properties we need to save from the Twitter response is very important. Since we are going to perform sentiment analysis on tweets, we will need the tweet text, tweet id \(unique identifier for each tweet\) and the tweet time.

Using the code snippet below, you can receive one tweet response and understand it’s properties. Here we set the tweet count to be 5 on purpose, as our goal is to understand the Twitter json response.  


```
import tweepy
access_key = "your access key"
access_secret = "your access secret"
consumer_key = "your consumer key"
consumer_secret = "your consumer secret"

#to authenticate
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_key, access_secret)api = tweepy.API(auth)
for tweet in api.search('Qatar','en',count = 5):
    print tweetprint "*****end of one tweet*****"
```

JSON response for a tweet will look like below. The tweet properties we need such as text, id are highlighted.  


| Status\(contributors=None, truncated=False,text=u'RT @OnlineJobsQatar: Cloud Sales Leader - GNP Job https://t.co/6KOyFVLDhG @gulf\_recruit \#doha \#jobsavailable \#jobsinqatar \#qatar', is\_quote\_status=False, in\_reply\_to\_status\_id=None,id=825936244324573184L, favorite\_count=0, \_api=&lt;tweepy.api.API object at 0x03232B70&gt;, author=User\(follow\_request\_sent=False, has\_extended\_profile=True, profile\_use\_background\_image=True, \_json={u'follow\_request\_sent': False, u'has\_extended\_profile': True, u'profile\_use\_background\_image': True, u'default\_profile\_image': False, u'id': 110190113, u'profile\_background\_image\_url\_https': u'https://pbs.twimg.com/profile\_background\_images/353684821/vinoth\_.JPG', u'verified': False, u'translator\_type': u'none', u'profile\_text\_color': u'0C3E53', u'profile\_image\_url\_https': u'https://pbs.twimg.com/profile\_images/745899828052430848/2E5r3JVt\_normal.jpg', u'profile\_sidebar\_fill\_color': u'FFF7CC', u'entities':  |
| :--- |


You can parse the json using python or by using[online json parser](http://json.parser.online.fr/)to make it more readable.

**  
**

1. 1. 1. 1. 1. ### **Track live tweets**

1. 1. 1. 1. 1. **To track live tweets stream, Twitter Streaming API is used. Stream created using tweepy will be used to create a feed of tweets, as the Streaming API pushes messages to a persistent session. This is the reason why more number of tweets can be downloaded in real time than using the REST API.**

**We’ll use SEARCH API to pull previous tweets, as it is much faster to get old tweets than tracking live tweets. Tracking live tweets is explained for your understanding and can be explored from**[**more here**](http://docs.tweepy.org/en/v3.4.0/streaming_how_to.html)**.**

* * * * ### **Data Collection**
      * 1. ### **Specific Topic or Event**

**As we aim to analyze the sentiment of Gulf Airlines such as Qatar Airways, Emirates and Etihad Airways, a list of relevant hashtags and keywords can be populated. One keyword at a time or a list of keywords can also be used.**

**  
**

**Find the**[**hashtag-keywords.txt file here**](https://github.com/ArabWICQatar/TwitterSentimentAnalysisVisualization/blob/master/hashtags-keywords.txt)**containing a list of keywords.**

**Create a project folder and copy the hashtag-keywords.txt file**

1. 1. 1. 1. 1. ### **Code**

**This python script establishes connection with Twitter and searches for tweets containing keywords and hashtags from keywords.txt file. The function search in python script is written to perform search and gather all tweets in a csv file searchTweets.csv.**

**Save the below script as searchTweets.py in your project folder, edit to add your Twitter app credientials and**[**Run**](https://docs.google.com/document/d/1U63W24otRRT0Q5AM0xfFJ5DDCXkOHb-B8oN52eB94NQ/edit#heading=h.46m4p15kgy05)

**  
**

**You will see the output searchTweets.csv file saved inside search-data folder.**

| **import tweepyimport sysimport csv \# to force utf-8 encoding on entire programreload\(sys\)sys.setdefaultencoding\('utf8'\) \# to write all tweets in a csv filealltweets = csv.writer\(open\("search-data/searchTweets.csv", 'ab'\)\) def search\(keywords\):access\_key = "your app access key here"access\_secret = "your app access token here"consumer\_key = "your app consumer key here"consumer\_secret = "your app consumer secret here"\#to authenticateauth = tweepy.OAuthHandler\(consumer\_key, consumer\_secret\)auth.set\_access\_token\(access\_key, access\_secret\)api = tweepy.API\(auth\)  count = 1;for tweet in api.search\(keywords,'en', count = 100\):created\_at = tweet.created\_attweet\_id = tweet.id\_strtweet\_text = tweet.textprint "gathered tweet ",countcount = count + 1alltweets.writerow\(\[created\_at, tweet\_id, tweet\_text\]\) \#search\("Qatar Airways"\) \# to search one keyword at a time file = open\('keywords.txt', 'r'\) \# contains a list of keywordsqueries = file.readlines\(\) for q in queries:\# read one keyword at a timeprint "----"print qsearch\(q\)** |
| :--- |


**  
**

