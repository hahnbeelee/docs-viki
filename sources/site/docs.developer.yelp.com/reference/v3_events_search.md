# Source: https://docs.developer.yelp.com/reference/v3_events_search

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

#### URL Expired

The URL for this request expired after 30 days.

> ## 📘
> 
> This endpoint is part of Yelp Places API, visit [Yelp Places API](https://docs.developer.yelp.com/docs/fusion-intro) to learn more.

locale

string

Locale code in the format of {language code}\_{country code}. See the [list of supported locales](https://docs.developer.yelp.com/docs/resources-supported-locales).

offset

integer

0 to 1000

Offset the list of returned results by this amount.

limit

integer

0 to 50

Defaults to 3

Number of events results to return. By default, it will return 3. Maximum is 50.

sort\_by

string

enum

Defaults to desc

Sort by either descending or ascending order.

ascdesc

Allowed:

`asc``desc`

sort\_on

string

enum

Defaults to popularity

Sort on popularity or time start.

popularitytime\_start

Allowed:

`popularity``time_start`

start\_date

integer

\-2208960000 to 221845420800

Unix timestamp. Will return events that only begin at or after the specified time.

end\_date

integer

\-2208960000 to 221845420800

Unix timestamp. Will return events that only end at or before the specified time.

categories

array of strings

List of category aliases.

categories

ADD string

is\_free

boolean

Filter whether the events are free to attend. By default no filter is applied so both free and paid events will be returned.

truefalse

excluded\_events

array of strings

List of event ids. Events associated with these event ids in this list will not show up in the response.

excluded\_events

ADD string

location

string

length between 1 and 250

Required if either _latitude_ or _longitude_ is not provided. 
This string indicates the geographic area to be used when searching for events. 
Examples: "New York City", "NYC", "350 5th Ave, New York, NY 10118". 
Events returned in the response may not be strictly within the specified location.

latitude

number

\-90 to 90

Required, if _location_ is not provided. Latitude of the location to search from. If latitude is provided, longitude is required too.

longitude

number

\-180 to 180

Required if _location_ is not provided. Longitude of the location to search from. If longitude is provided, latitude is required too.

radius

integer

0 to 40000

Search radius in meters. If the value is too large, a AREA\_TOO\_LARGE error may be returned. The max value is 40000 meters (about 25 miles).

# 

200

One more more events were found.

# 

400

Bad Request. Message varies depending on failure scenario

# 

401

The API key has either expired or doesn't have the required scopes to query this endpoint.

| code | description |
| --- | --- |
| UNAUTHORIZED\_API\_KEY | The API key provided is not currently able to query this endpoint. |
| TOKEN\_INVALID | Invalid API key or authorization header. |

# 

403

The API key provided is not currently able to query this endpoint.

# 

404

Resource Not Found

# 

413

The length of the request exceeded the maximum allowed

# 

429

You have either exceeded your daily quota, or have exceeded the queries-per-second limit for this endpoint. Try reducing the rate at which you make queries.

# 

500

Internal Server Error

# 

503

Service Unavailable

Updated 10 months ago

---

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

xxxxxxxxxx

1

curl \--request GET \\

2

 \--url 'https://api.yelp.com/v3/events?limit=3&sort\_by=desc&sort\_on=popularity' \\

3

 \--header 'accept: application/json'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400 - Invalid Request401 - Unauthorized401 - Invalid Token403 - Authorization Error404 - Resource Not Found413 - Payload Too Large429 - Rate limited500 - Internal Server Error503 - Service Unavailable

Updated 10 months ago

---

Did this page help you?

Yes

No