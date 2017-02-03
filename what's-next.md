# What's Next?

#### Next steps: Challenge Yourself

1. **DATA COLLECTION:** Think of a unique dataset related to Qatar. Research on keywords and hashtags. Collect the data using search REST API script provided to you.

2. Find the popularity for the collected dataset based on the retweets and fav count.

3. Visualize the results using highcharts.

HINT:

Connect with twitter and parse the json response obtained.

Find and extract more tweet properties - such as retweets and fav counts.

```py
retweet = tweet.retweet_count
fav = tweet.favorite_count
alltweets.writerow([created_at, tweet_id, tweet_text, retweet, fav])
```

Add this code to the searchTweets.py for gathering this information while collecting tweets.

### 



