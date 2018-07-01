---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - python
 
toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

search: true
---

# API Documentation

Welcome to the Flood Chaser API! This API provides exposure to a database that collects and postprocesses flood related tweets. The database is a part of the deliverables of the UK Space Agency Space for Smarter Government Programme (SSGP) project. You can view code examples in the dark area to the right on how to access this database through the Flood Chaser API.


Base URLs:
https://hydas.co.uk/api/v1/flood/twitter
> Scroll down for code samples, example requests and responses. 

# Flood Tweets
## Get All Tweets

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://hydas.co.uk/api/v1/flood/twitter/all', params={

}, 
headers = headers)

print r.json()
```


> The above command returns JSON structured like this:

```json
[
  {
    "URL": "https://twitter.com/statuses/1011972424135598080", 
    "about_flood": "n", 
    "address_tweet": null, 
    "confidence": null, 
    "created_at": "2018-06-27 14:00:02.000000", 
    "id_str": "1011972424135598080", 
    "index": 0, 
    "lat_nlp": null, 
    "lat_tweet": null, 
    "location": "[]", 
    "lon_nlp": null, 
    "lon_tweet": null, 
    "text": "The latest The significant-events Daily! https://t.co/PEbAo8BBvs Thanks to @arcwinsurance @LegacyPremium @IADCDredging #flood #volcano", 
    "user_id": 30137142
  }, 
  {
    "URL": "https://twitter.com/statuses/1011972425263796224", 
    "about_flood": "n", 
    "address_tweet": null, 
    "confidence": null, 
    "created_at": "2018-06-27 14:00:02.000000", 
    "id_str": "1011972425263796224", 
    "index": 1, 
    "lat_nlp": null, 
    "lat_tweet": null, 
    "location": "[]", 
    "lon_nlp": null, 
    "lon_tweet": null, 
    "text": "With sandbags lined and barriers put up, many Rock Valley residents are having flashbacks to the floods of 2014. https://t.co/1Iz177SwB7", 
    "user_id": 14849086
  }] 
```

This endpoint retrieves all tweets.

### HTTP Request

`GET https://hydas.co.uk/api/v1/flood/twitter/all`

### Response Schema

Name | Type | Description | Example
------- | ----- | -------------|------------
text|string|The text of the tweet.| Just arrived at Victoria Station. It is flooding inside. Oh dear, it is not looking good for my visit to London!
URL | string |The URL of the original tweet.|https://twitter.com/statuses/1011972424135598080
about_flood|string|'y' if the tweet is about a physical flood, 'n' if not.| y 
address_tweet|string|The address where the tweet was sent if the GPS location function was turned on when tweeting. It's nullable.|Buckingham Palace. London SW1A 1AA.
created_at|string|The date and time when the tweet was posted.|2018-06-27 14:00:02.000000
id_str|string|The id of the tweet.|1011972424135598080
index|integer|The index number in the database.|0
lat_tweet|float|The latitude of the tweeting coordinates. It's nullable.|51.212 
lon_tweet|float|The longitude of the tweeting coordinates. It's nullable.|0.001
lat_nlp|float|The latitude of the geocoded coordinates based on location recognition through NLP. It's nullable.|51.212
lon_nlp|float|The longitude of the geocoded coordinates based on location recognition through NLP. It's nullable.|51.212
location|object|A list of locations mentioned in the tweet.|['Victoria Station','London'] 
confidence |integer|The value reflects the confidence of geocoding. The higher the value, the more confident or less ambiguous we are about the address found via location mention in tweets.| 7


## Filter Tweets 


```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://hydas.co.uk/api/v1/flood/
twitter', params={'userid':'30137142'}, headers = headers)

print r.json()

```


> The above command returns JSON structured like this:

```json
'[
  {
    "URL": "https://twitter.com/statuses/1011972424135598080", 
    "about_flood": "n", 
    "address_tweet": null, 
    "confidence": null, 
    "created_at": "2018-06-27 14:00:02.000000", 
    "id_str": "1011972424135598080", 
    "index": 0, 
    "lat_nlp": null, 
    "lat_tweet": null, 
    "location": "[]", 
    "lon_nlp": null, 
    "lon_tweet": null, 
    "text": "The latest The significant-events Daily! https://t.co/PEbAo8BBvs Thanks to @arcwinsurance @LegacyPremium @IADCDredging #flood #volcano", 
    "user_id": 30137142
  }
]'
```

This endpoint filters the database using the following query parameters. All query parameters can be used the same way as shown in the example on the right dark area. 

### HTTP Request

`GET https://hydas.co.uk/api/v1/flood/twitter?parameter=value`

### Query Parameters


Parameter | Type | Description | Example
------- | ----- | -------------|------------
userid | string | The userid of the twitter account. This filters the database to include only tweets sent from this userid|'1009375723855982592'
latest|integer|This parameter can set to return the latest N amount of tweets from the database.| 100 
aboutflood|boolean|This parameter will filter tweets to include only the ones related to physical floods.|y
period | string | The period of interest. By entering the starting datetime and ending datetime, users can filter the database to include tweets sent within the period of interest. Starting and ending datetimes are separated by comma.|'2018-06-27 14:00:00,2018-06-27 18:00:00'
boundingbox|string| Filter tweets that are located in the bounding box. The format would be: SLat,WLon,NLat,Elon. An example to filter tweets for greater London area is shown on the right.|51.279,-0.516,51.698,0.342

