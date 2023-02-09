# ZtM-Python-Twitter-Bot
Wrote a customizable twitter bot using the Twitter API

Notes below from the course:

UPDATE: So you know how Elon Musk bought Twitter? Well I have some good news and bad news.



Bad News: Twitter API usage is no longer going to be free.



Good News: This project is still great to learn how to work with APIs. Instead of wasting your money on using the Twitter API (trust me, you don't want to), just watch the next couple of videos to learn how I use the API. You'll still learn lots by watching me use the API without you having to code along :)









Some of the older notes in case you still want to use the API on your own (but really you shouldn't):



Head ups! In the next video we will go over signing up for the Twitter API so we can build a fun Twitter bot. However, Twitter is very cautious when it comes to people creating spam bots, so you will have to apply to get access to their API (it's free). Therefore, I recommend watching the next videos, applying to get access to the API, and you if you have any questions about the process you can see some of the answers of common issues here: https://developer.twitter.com/en/docs/basics/developer-portal/faq



Finally, twitter has 2 versions of their API. v1 and v2. v2 is still brand new and not completely finished. For that reason, I have used version 1 in the coming videos. You can find both versions here: https://developer.twitter.com/en/docs/twitter-api





But.....





IN CASE YOU WANT TO USE TWITTER API v2, we have provided the code below that will work with this version 2 of the API. The principles you will learn in the next videos will be the same with only some minor differences in how we access the API (thanks to Ben Eyal for providing the code!).

# pip install tweepy
import tweepy
 
# config.py : where I keep my keys as constants
import config
 
 
def about_me(client: tweepy.Client) -> None:
    """Print information about the client's user."""
    # The `public_metrics` addition will give me my followers count, among other things
    me = client.get_me(user_fields=["public_metrics"])
    print(f"My name: {me.data.name}")
    print(f"My handle: @{me.data.username}")
    print(f"My followers count: {me.data.public_metrics['followers_count']}")
 
 
def get_ztm_tweets(client: tweepy.Client) -> list[tweepy.Tweet]:
    """Return a list of latest ZTM tweets"""
    ztm = client.get_user(username="zerotomasteryio")
    response = client.get_users_tweets(ztm.data.id)
    return response.data
 
 
if __name__ == "__main__":
    client = tweepy.Client(
        bearer_token=config.BEARER_TOKEN,
        consumer_key=config.API_KEY,
        consumer_secret=config.API_SECRET,
        access_token=config.ACCESS_TOKEN,
        access_token_secret=config.ACCESS_SECRET,
    )
    print("=== About Me ===")
    about_me(client)
    print()
    print("=== ZTM Tweets ===")
    for tweet in get_ztm_tweets(client):
        print(tweet, end="\n\n")




In order to get all the keys, you need to sign up at https://developer.twitter.com/ and create an app. Go to your newly created app, and in the center screen you'll see two tabs: "Settings" and "Keys and tokens". Under "Settings", click "Edit" in the "User authentication settings" box, choose OAuth 1.0a and give https://example.com as a redirect and personal website. In the "Keys and tokens" tab, generate all keys. You need 5 in total: bearer token, API key, API key secret, access token, access token secret. After that you should be good to go.
