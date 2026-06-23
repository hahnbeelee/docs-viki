# Source: https://docs.developer.yelp.com/docs/engagement-metrics-api

> ## 📘
> 
> This is a Yelp Partner API
> 
> Access is disabled by default. See [Yelp Partner APIs](https://docs.developer.yelp.com/docs/yelp-partner-apis) on how to get access.

# 

Overview

The Engagement Metrics API returns a business’s consumer engagement score, by week, relative to all other North America-based businesses on Yelp.

# 

Access and Credentials

This API is reserved for Yelp Insights API partners. To inquire about becoming a Yelp Insights API partner please visit [here](https://knowledge.yelp.com/). Upon registration, the client will be permitted access to this endpoint. Credentials can be generated [here](https://www.yelp.com/developers/v3/manage_app).

# 

Authentication

Refer [here](https://docs.developer.yelp.com/docs/fusion-authentication) for more about authentication for this API

# 

Request

To use this endpoint, make the GET request to the following URL with at a minimum the business\_ids parameter.

Text

`GET https://api.yelp.com/v3/businesses/engagement`

Accepted parameters are listed below:

| Parameter name | Description | Example |
| --- | --- | --- |
| business\_ids | Comma separated list of Yelp business id of the locations you'd like metrics for. Maximum of 20 business\_ids per request. | nBvdJyM7TCHp5ppX31SC5Q, 
VImbIWfxODVsiRHebSQePw |
| date\_range\_start | The first week of data you want. | 2018-02-01 |
| date\_range\_end | The last week of data you want | 2018-03-01 |

# 

Sample Request

Text

`GET https://api.yelp.com/v3/businesses/engagement?business_ids=nBvdJyM7TCHp5ppX31SC5Q,WoI1IisL_AgmWdiJLRb-Zw`

# 

Sample Response

Text

`{   "data": [     {       "business_id": "nBvdJyM7TCHp5ppX31SC5Q",       "metrics": [         {           "start_of_week_date": "2018-02-05",           "engagement_metric": 20,           "intent_metric": 10         },         {           "start_of_week_date": "2018-02-12",           "engagement_metric": 20,           "intent_metric": 10         }       ]     },     {       "business_id": "VImbIWfxODVsiRHebSQePw",       "metrics": [         {           "start_of_week_date": "2018-02-05",           "engagement_metric": 20,           "intent_metric": 10         },         {           "start_of_week_date": "2018-02-12",           "engagement_metric": 20,           "intent_metric": 10         }       ]     }   ] }`

# 

Response Attributes

| Name | Type | Description |
| --- | --- | --- |
| business\_id | string | Unique Yelp ID of the business. |
| metrics | object\[\] | List of metrics for the business in the specified week. |
| start\_of\_week\_date | date | The first day of the week for the associated metrics. |
| engagement\_metric | int | Amalgam of page views, website clicks, bookmarks, calls & messages to business, clicks on directions, reviews & photos posted, check-ins. 
Indicative of consumer engagement relative to all other North America-based businesses on Yelp. 
Values range from 1-20 |
| intent\_metric | int | Amalgam of all engagement attributes included in Consumer Engagement Metric except page views. 
Indicative of consumer intent relative to all other North America-based businesses on Yelp. 
Values range from 1-10. |

Updated 10 months ago

---

Did this page help you?

Yes

No

Copy Page