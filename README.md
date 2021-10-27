# tweety
Twitter's API is annoying to work with, and has lots of limitations — luckily their frontend (JavaScript) has it's own API, which I reverse–engineered. No API rate limits. No restrictions. Extremely fast.

## Prerequisites

Before you begin, ensure you have met the following requirements:

* Internet Connection
* Python 3.6+
* BeautifulSoup (Python Module)
* Requests (Python Module)

## All Functions
* get_tweets()
* get_user_info()
* get_trends() (can be used without username)
* search() (can be used without username)
* tweet_detail() (can be used without username)

## Using tweety

### Getting Tweets:
#### Description:
Get 20 Tweets of a Twitter User
#### Required Parameter:
* Username or User profile URL while initiating the Twitter Object
#### Optional Parameter:
* pages : int (default is 1,starts from 2) -> Get the mentioned number of pages of tweets
* include_extras : boolean (default is False) -> Get different extras on the page like Topics etc
* simplify : boolean (default is False) -> get simplifies tweets instead of Twitter's cultured results  
#### Output:
* Type -> dictionary
* Structure
> Not Simplified
```json
    {
      "p-1" : {
        "result": {
            "tweets": []
        }
      },
      "p-2":{
        "result": {
            "tweets": []
        }
      }
    }
```
> Simplified
```json
    {
      "p-1" : {
        "result": {
            "tweets": [
              {
                   "created_on":"Tue Oct 05 17:35:26 +0000 2021",
                   "is_retweet":true,
                   "tweet_id":"1445442518301163521",
                   "tweet_body":"Hello, world. #Windows11 https://t.co/pg3d6EsreQ https://t.co/wh6InmfngF",
                   "language":"en",
                   "likes":"",
                   "retweet_counts":442,
                   "source":"Twitter Web App",
                   "media":[],
                   "user_mentions":[],
                   "urls":[],
                   "hashtags":[],
                   "symbols":""
              },
              {}
            ]
        }
      },
      "p-2":{
        "result": {
            "tweets": []
        }
      }
    }
```
#### Example:
```bash
python
Python 3.7.3 (default, Mar 26 2019, 21:43:19) 
[GCC 8.2.1 20181127] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from tweet import Twitter
>>> all_tweet = Twitter("Username or URL").get_tweets(pages=2)
>>> for i in all_tweet:
...   print(all_tweet[i])
```
### Getting Trends:
#### Description:
Get 20 Locale Trends
#### Output:
* Type -> dictionary
- Structure
```json
  {
    "trends":[
      {
        "name":"<Trend-name>",
        "url":"<Trend-URL>"
      },
      {
        "name":"<Trend-name>",
        "url":"<Trend-URL>"
      }
    ]
  } 
```
#### Example :
```bash
python
Python 3.7.3 (default, Mar 26 2019, 21:43:19) 
[GCC 8.2.1 20181127] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from tweet import Twitter
>>> trends = Twitter().get_trends()
>>> for i in trends['trends']:
...   print(i['name'])
```

### Searching a keyword:
#### Description:
Get 20 Tweets for a specific Keyword or Hashtag
#### Required Parameter:
* keyword : str -> Keyword begin search
#### Optional Parameter:
* latest : boolean (Default is False) -> Get the latest tweets
* simplify : boolean (Default is True) -> Simplify the Results instead of Twitter's cultured results
* pages : int (starts from 2 , default is 1) -> number of pages to get 
#### Output:
* Type -> list
* Structure -> Please check the structure of [get_tweets](#getting-tweets) function
#### Example:
```bash
python
Python 3.7.3 (default, Mar 26 2019, 21:43:19) 
[GCC 8.2.1 20181127] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from tweet import Twitter
>>> trends = Twitter().search("Pakistan")
```

### Getting USER Info:
#### Description:
Get the information about the user
#### Required Parameter:
* Username or User profile URL while initiating the Twitter Object
#### Optional Parameter:
* banner_extensions : boolean (Default is False) -> get more information about user banner image
* image_extensions : boolean (Default is False) -> get more information about user profile image
#### Output:
* Type -> dict

#### Example:
```bash
python
Python 3.7.3 (default, Mar 26 2019, 21:43:19) 
[GCC 8.2.1 20181127] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from tweet import Twitter
>>> trends = Twitter("Username or URL").get_user_info()
```


### Getting a Tweet Detail:
#### Description:
Get the detail of a tweet including its reply
#### Required Parameter:
* Identifier of the Tweet -> Either Tweet URL  OR Tweet ID

#### Output:
* Type -> dict
* Structure
```json
  {
    "conversation_threads":[],
    "tweet": {}
  }
```
#### Example:
```bash
python
Python 3.7.3 (default, Mar 26 2019, 21:43:19) 
[GCC 8.2.1 20181127] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from tweet import Twitter
>>> trends = Twitter().tweet_detail("https://twitter.com/Microsoft/status/1442542812197801985")
```

# Updates:
## Update 0.1:
* Get Multiple Pages of tweets using pages parameter in get_tweets() function
* output of [get_tweets](#getting-tweets) has been reworked.

## Update 0.2:
* Again reworked and simplified tweets in [get_tweets](#getting-tweets) function :stuck_out_tongue_winking_eye:
* Added [tweet_detail function](#getting-a-tweet-detail) for getting details about a tweet including replies to it

## Update 0.2.1:
* Fixed Hashtag Search

## Update 0.2.2:
* Fixed get_tweets() with multiple pages
* Added Simplify Parameter in get_tweets() , to get simplified results instead of Twitter's cluttered results

## Update 0.3:
* Added getting multiple pages while searching keyword
* [searching a keyword](#searching-a-keyword) now supports simplify parameter