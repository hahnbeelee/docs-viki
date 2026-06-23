# Source: https://docs.developer.yelp.com/reference/v3_business_search

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> This endpoint is part of Yelp Places API, visit [Yelp Places API](https://docs.developer.yelp.com/docs/fusion-intro) to learn more.

location

string

length between 1 and 250

Required if either _latitude_ or _longitude_ is not provided. 
This string indicates the geographic area to be used when searching for businesses. 
Examples: "New York City", "NYC", "350 5th Ave, New York, NY 10118". 
Businesses returned in the response may not be strictly within the specified location.

latitude

number

\-90 to 90

Required, if _location_ is not provided. Latitude of the location to search from. If latitude is provided, longitude is required too.

longitude

number

\-180 to 180

Required if _location_ is not provided. Longitude of the location to search from. If longitude is provided, latitude is required too.

term

string

length ≤ 300

Search term, e.g. "food" or "restaurants". 
The term may also be the business's name, such as "Starbucks". If term is not included the endpoint will default to searching across businesses from a small number of popular categories.

radius

integer

0 to 40000

A suggested search radius in meters. This field is used as a suggestion to the search. The actual search radius may be lower than the suggested radius in dense urban areas, and higher in regions of less business density. 
If the specified value is too large, a AREA\_TOO\_LARGE error may be returned. The max value is 40,000 meters (about 25 miles).

categories

array of strings

Categories to filter the search results with. See the list of supported categories. The category filter can be a list of comma delimited categories. 
e.g., "bars,french" will filter by Bars OR French. 
The category alias should be used (e.g. "discgolf", not "Disc Golf").

categories

ADD string

locale

string

Locale code in the format of {language code}\_{country code}. See the [list of supported locales](https://docs.developer.yelp.com/docs/resources-supported-locales).

price

array of integers

length ≤ 4

Pricing levels to filter the search result with: 1 = $, 2 = $$, 3 = $$$, 4 = $$$$. The price filter can be a list of comma delimited pricing levels. 
e.g., "1, 2, 3" will filter the results to show the ones that are $, $$, or $$$.

price

ADD integer

open\_now

boolean

When set to true, only return the businesses that are open now. 
Notice that _open\_at_ and _open\_now_ cannot be used together.

truefalse

open\_at

integer

An integer representing the Unix time in the timezone of the search location. If specified, it will return businesses open at the given time. 
Notice that _open\_at_ and _open\_now_ cannot be used together.

attributes

array of strings

Try these additional filters to return specific search results!

- _hot\_and\_new_ - popular businesses which recently joined Yelp
- _request\_a\_quote_ - businesses which actively reply to Request a Quote inquiries
- _reservation_ - businesses with Yelp Reservations bookings enabled on their profile page
- _waitlist\_reservation_ - businesses with Yelp _Wait List_ bookings enabled on their profile screen (iOS/Android)
- _gender\_neutral\_restrooms_ - businesses which provide gender neutral restrooms
- _open\_to\_all_ - businesses which are Open To All
- _wheelchair\_accessible_ - businesses which are Wheelchair Accessible

\*\*Premium Search Filters, available to users with a [Yelp Places Premium Plan](https://business.yelp.com/data/products/fusion/):

- _accepts\_credit\_cards_ - businesses which accepts credit cards
- Ambience
 - _ambience_ - ambience of the business
 - _ambience\_casual_ - is the ambience at the business casual
 - _ambience\_classy_ - is the ambience at the business classy
 - _ambience\_divey_ - is the ambience at the business divey
 - _ambience\_hipster_ - is the ambience at the business hippy
 - _ambience\_intimate_ - is the ambience at the business intimate
 - _ambience\_romantic_ - is the ambience at the business romantic
 - _ambience\_touristy_ - is the ambience at the business touristy
 - _ambience\_trendy_ - is the ambience at the business trendy
 - _ambience\_upscale_ - is the ambience at the business upscale
- _dogs\_allowed_ - dog-friendly businesses
- _good\_for\_dancing_ - businesses which are good for dancing
- _happy\_hour_ - businesses which have happy hour specials
- Liked by
 - _liked\_by\_beer_ - businesses liked by people who drink beer
 - _liked\_by\_dates_ - businesses liked by people who are on a date
 - _liked\_by\_fifties_ - businesses liked by people who are in their fiftees
 - _liked\_by\_forties_ - businesses liked by people who are in their forties
 - _liked\_by\_genx_ - businesses liked by people who belong to Generation X
 - _liked\_by\_thirties_ - businesses liked by people who are in their thirties
 - _liked\_by\_twenties_ - businesses liked by people who are in their twenties
 - _liked\_by\_men_ - businesses liked by men
 - _liked\_by\_students_ - businesses liked by Students
 - _liked\_by\_travelers_ - businesses liked by people who are travelling
 - _liked\_by\_vegetarians_ - businesses which are liked by vegetarians
 - _liked\_by\_wine_ - businesses liked by people who drink wine
 - _liked\_by\_women_ - businesses liked by women
 - _liked\_by\_young\_professionals_ - businesses liked by young prefessionals
- Noise level
 - _noise\_level_ - noise level at the business
 - _noise\_level\_average_ - is the noise level average
 - _noise\_level\_loud_ - is the noise level loud
 - _noise\_level\_quiet_ - is the noise level quiet
 - _noise\_level\_very\_loud_ - is the noise level very loud
- _outdoor\_seating_ - businesses with outdoor seating areas
- Parking
 - _parking_ - businesses with parking
 - _parking\_garage_ - businesses which itself has a garage or there is a parking garage nearby
 - _parking\_lot_ - businesses which have a parking lot
 - _parking\_street_ - businesses with street parking available nearby
 - _parking\_valet_ - businesses which offer a valet parking
 - _parking\_validated_ - businesses which can validate a parking ticket from an external parking
 - _parking\_bike_ - businesses with bike parking type
- _restaurants\_delivery_ - restaurants which offer delivery service
- _restaurants\_takeout_ - restaurants with take-out option
- WiFi
 - _wifi_ - businesses with WiFi
 - _wifi\_free_ - businesses with free WiFi
 - _wifi\_paid_ - businesses with paid WiFi

You can combine multiple attributes by providing a comma separated like "attribute1,attribute2". 
If multiple attributes are used, only businesses that satisfy all the attributes will be returned in search results. 
e.g., the attributes "_hot\_and\_new_,_request\_a\_quote_" will return businesses that are 'Hot and New', and offer 'Request a Quote'.

attributes

ADD string

sort\_by

string

enum

Defaults to best\_match

Suggestion to the search algorithm that the results be sorted by one of the these modes: _best\_match_, _rating_, _review\_count_ or _distance_. 
The default is _best\_match_. Note that specifying the sort\_by is a suggestion (not strictly enforced) to Yelp's search, which considers multiple input parameters to return the most relevant results.

e.g., the _rating_ sort is not strictly sorted by the rating value, but by an adjusted rating value that takes into account the number of ratings, 
similar to a Bayesian average. This is to prevent skewing results to businesses with a single review.

best\_matchratingreview\_countdistance

Allowed:

`best_match``rating``review_count``distance`

device\_platform

string

enum

Determines the platform for mobile\_link

androidiosmobile-generic

Allowed:

`android``ios``mobile-generic`

reservation\_date

string

The date for the reservation, format is YYYY-mm-dd

reservation\_time

string

The time of the requested reservation, format is HH:MM

reservation\_covers

integer

1 to 10

How many people are attending the reservation

matches\_party\_size\_param

boolean

Whether to filter out results that don't have openings matching the params

truefalse

job\_alias

string

Return only businesses that service this job type (e.g. plumbing, HVAC repair). 
Acceptable job aliases can be found via the [Get Jobs](https://docs.developer.yelp.com/reference/v3_get_jobs) endpoint. If you need access to [Get Jobs](https://docs.developer.yelp.com/reference/v3_get_jobs), please [contact us](https://business.yelp.com/data/products/places-api/#form).

limit

integer

0 to 50

Defaults to 20

Number of results to return.

offset

integer

0 to 1000

Offset the list of returned results by this amount.

# 

200

One more more businesses were found.

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

Authorization Error

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

ShellNodeRubyPHPPython

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400 - Invalid Request401 - Unauthorized401 - Invalid Token403 - Authorization Error404 - Resource Not Found413 - Payload Too Large429 - Rate limited500 - Internal Server Error503 - Service Unavailable

Updated 10 months ago

---