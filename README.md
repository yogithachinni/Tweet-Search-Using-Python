from tweepy.streaming import StreamListener
from tweepy import OAuthHandler
from tweepy import Stream


access_token = "2283460033-jr1TymWhD35wMTycIaWNh5IaJxkPkTm8UQ9CU8y"
access_token_secret = "Mw1Y37GgkJfnpcK2B6KQjZw2zKhBTWfyuKmRv0lODRGP0"
consumer_key = "dp9znakqTFJv6keVuHg2pi0xJ"     
consumer_secret = "3rQK3PONSqWSspSbmBGAxdV9EvuSwvuSnSUSGmMJnuEkNxBMoY"



class StdOutListener(StreamListener):

    def on_data(self, data):
        print data
        return True

    def on_error(self, status):
        print status


if __name__ == '__main__':

    l = StdOutListener()
    auth = OAuthHandler(consumer_key, consumer_secret)
    auth.set_access_token(access_token, access_token_secret)
    stream = Stream(auth, l)

    #This line filter Twitter Streams to capture data by the keywords: 'python', 'javascript', 'ruby'
    stream.filter(track=['python', 'javascript', 'ruby'])

import json
import pandas as pd
import matplotlib.pyplot as plt
tweets_data_path = '../data/twitter_data.txt'

tweets_data = []
tweets_file = open(tweets_data_path, "r")
for line in tweets_file:
    try:
        tweet = json.loads(line)
        tweets_data.append(tweet)
    except:
        continue 

