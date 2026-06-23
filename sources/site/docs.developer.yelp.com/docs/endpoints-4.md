# Source: https://docs.developer.yelp.com/docs/endpoints-4

# 

Search

`GET https://api.yelp.com/v3/businesses/search`

The endpoint has been upgraded to return businesses which support Yelp Reservations.

The three parameters that must be passed in to find reservations are **reservation\_time**, **reservation\_date**, and **reservation\_covers**.

Sample query that will return Thai Restaurants in San Francisco that accept Yelp reservations: 
[https://api.yelp.com/v3/businesses/search?location=San%20Francisco&term=Thai&attributes=reservation](https://api.yelp.com/v3/businesses/search?location=San%20Francisco&term=Thai&attributes=reservation)

**Parameters**

| parameter name | required | type | description |
| --- | --- | --- | --- |
| reservation\_time | yes | string | The time of the requested reservation, format is HH:MM |
| reservation\_date | yes | string | The date for the reservation, format is YYYY-mm-dd |
| reservation\_covers | yes | number | How many people are attending the reservation (min. value is 1; max value is 10). |
| matches\_party\_size\_param | no | boolean | True (default): This search filters out results which don’t have any openings matching the reservation\_covers params. |
| False: | | | This search returns all results, and disregards the reservation\_covers params. |
| attribute | no | string | submit 'reservation' to return only reservable Yelp businesses. |

**Exceptions**

| code | status code | description |
| --- | --- | --- |
| DATE\_TIME\_VALIDATION\_ERROR | 400 | Invalid format, expected format is %H:%M |
| DATE\_TIME\_VALIDATION\_ERROR | 400 | Invalid format, expected format is %Y-%m-%d |
| TOO\_SMALL\_VALIDATION\_ERROR | 400 | Number too small: {value} |
| TOO\_LARGE\_VALIDATION\_ERROR | 400 | Number too big: {value} |

The response will mostly match our public search response, see [https://www.yelp.com/developers/documentation/v3/business\_search](https://docs.developer.yelp.com/reference/v3_business_search).

Searching for reservations adds an additional field, the "data" field. This will contain additional reservation times that are + or - 30 minutes from the requested reservation time.

**Response**

| parameter name | type | description |
| --- | --- | --- |
| data | object | An object containing additional data on the search query |
| data.reservation\_openings | list | A list of additional reservation opening times. |
| data.reservation\_openings\[x\] | string | The available open reservation time. This is of the format HH:MM and is in a 24-hour clock. |

Sample response of with data field (public data trimmed for brevity):

`# … trimmed 		{ 			"id": "cuisine-of-nepal-san-francisco", 			"name": "Cuisine of Nepal", 			"image_url": ..., 			"is_closed": false, 			"url": ..., 			"review_count": 303, 			"categories": [...], 			"rating": 4.5, 			"coordinates": {...}, 			"transactions": [ 				"delivery", 				"pickup", 				"restaurant_reservation" 			], 			"price": "$$", 			"location": {...}, 			"phone": "+14156472222", 			"display_phone": "(415) 647-2222", 			"distance": 2502.5961202999997, 			"attributes": { 				"gender_neutral_restrooms": true 			}, 			"data": { 				"reservation_openings": [ 					"13:30", 					"13:45", 					"14:00" 				] 			} 		}, # … trimmed`

# 

Openings endpoint

`GET https://api.yelp.com/v3/bookings/{business-id}/openings`

To get the available reservation times for a restaurant, you can give this endpoint the Business ID along with a few parameters. This endpoint will return times around the requested timeslot and across several days to provide the end user with some options.

In general, the openings endpoint will return times across 4 days - the day before, current day and 2 days after the requested date.

Currently, Yelp Reservations API does not support reservations which require a credit card. So, if **"credit\_card\_required": true** is returned, you should NOT proceed to the Holds endpoint. If you do, the Holds endpoint will return a **null** hold\_id.

**Parameters**

| parameter name | required | type | description |
| --- | --- | --- | --- |
| time | yes | string | The time of the requested reservation, format is HH:MM |
| date | yes | string | The date for the reservation, format is YYYY-mm-dd |
| covers | yes | number | How many people are attending the reservation (min. value is 1; max value is 10). |
| get\_covers\_range | no | boolean | If **true**, include the **covers\_range** dict in the response. |

**Exceptions**

| code | status code | description |
| --- | --- | --- |
| DATE\_TIME\_VALIDATION\_ERROR | 400 | Invalid format, expected format is %H:%M |
| DATE\_TIME\_VALIDATION\_ERROR | 400 | Invalid format, expected format is %Y-%m-%d |
| TOO\_SMALL\_VALIDATION\_ERROR | 400 | Number too small: {value} |
| TOO\_LARGE\_VALIDATION\_ERROR | 400 | Number too big: {value} |

**Response**

| parameter name | type | description |
| --- | --- | --- |
| reservation\_times | list | A list of objects that contain available reservation times. |
| reservation\_times\[x\].date | string | The date for possible reservations, format is YYYY-mm-dd |
| reservation\_times\[x\].times | list | A list of possible reservation times for the date provided. |
| reservation\_times\[x\].times\[x\].credit\_card\_required | boolean | Whether or not this reservation requires a credit card. |
| reservation\_times\[x\].times\[x\].time | string | The time of the available reservation, format is HH:MM and is in a 24-hour clock. |
| reservation\_times\[x\].times\[x\].url | string | If the reservation requires a credit card, this URL will let the user book the reservation from our web interface. |
| covers\_range.min\_party\_size | number | The minimum number of people that the business allows to attend a reservation. |
| covers\_range.max\_party\_size | number | The maximum number of people that the business allows to attend a reservation. |

**Sample Request**

`curl -X GET \ 'https://api.yelp.com/v3/bookings/victors-french-bistro-test-listing-san-francisco/openings?covers=2&date=2017-12-30&time=18%3A00' \ -H 'Authorization: Bearer {ACCESS_TOKEN}'`

**Sample Response**

`{   "reservation_times": [     {       "date": "2017-09-22",       "times": [ 	   { 	     "credit_card_required": true, 	     "time": "14:45", 	     "url":     "https://www.devc.yelpreservations.com/r/dorsia/reserve/2017-09-22/1445/3/" 	   }, 	   { 	     "credit_card_required": true, 	     "time": "15:00", 	     "url":     "https://www.devc.yelpreservations.com/r/dorsia/reserve/2017-09-22/1500/3/" 	   }, 	   { 	     "credit_card_required": true, 	     "time": "15:15", 	     "url":    "https://www.devc.yelpreservations.com/r/dorsia/reserve/2017-09-22/1515/3/" 	   },       ]     },     {       "date": "2017-09-23",       "times": [ 	 { 	     "credit_card_required": true, 	     "time": "14:45", 	     "url":    "https://www.devc.yelpreservations.com/r/dorsia/reserve/2017-09-23/1445/3/" 	   }, 	   { 	     "credit_card_required": true, 	     "time": "15:00", 	     "url":    "https://www.devc.yelpreservations.com/r/dorsia/reserve/2017-09-23/1500/3/" 	   }, 	   { 	     "credit_card_required": true, 	     "time": "15:15", 	     "url":    "https://www.devc.yelpreservations.com/r/dorsia/reserve/2017-09-23/1515/3/" 	   },       ]     },   ]   "covers_range": {     "min_party_size": 1,     "max_party_size": 7   } }`

# 

Holds endpoint

`POST https://api.yelp.com/v3/bookings/{business_id}/holds`

This endpoint will place a temporary hold on the requested time slot so that the partner can request all the required reservation information from the user. Holds are only valid for 5 minutes and you must use the hold id returned from this endpoint to place the reservation or you will get a conflict.

**Note:** All parameters being sent into the holds endpoint needs to be sent as form data inside of the request body. They will not work as query parameters.

**Parameters**

| parameter name | required | type | description |
| --- | --- | --- | --- |
| time | yes | string | The time of the requested reservation, format is HH:MM. |
| date | yes | string | The date for the reservation, format is YYYY-mm-dd |
| covers | yes | number | How many people are attending the reservation. |
| unique\_id | yes | string | This should be the user's device id or a unique user id to help tie together actions of the user on the API. Multiple requests to the Holds endpoint by the same user should use the same unique\_id. |

**Exceptions**

| code | status code | description |
| --- | --- | --- |
| COVERS\_VALUE\_OUT\_OF\_RANGE | 400 | This restaurant only accepts online reservations between {min_value} and {max\_value} people. **NOTE:** The {min\_value} and {max\_value} will be dependent on the restaurant's accepted minimum and maximum values for their online reservations._ |
| INVALID\_DATE\_TIME\_RANGE | 400 | The date time range is invalid |
| INVALID\_RESERVATION\_PARAMETER | 400 | Bad request |
| DATE\_TIME\_VALIDATION\_ERROR | 400 | Invalid format, expected format is %H:%M |
| DATE\_TIME\_VALIDATION\_ERROR | 400 | Invalid format, expected format is %Y-%m-%d |
| TOO\_SMALL\_VALIDATION\_ERROR | 400 | Number too small: {value} |
| TOO\_LARGE\_VALIDATION\_ERROR | 400 | Number too big: {value} |
| BUSINESS\_NOT\_FOUND | 404 | The requested business could not be found. |
| DOES\_NOT\_TAKE\_RESERVATIONS | 404 | The given business does not take reservations. |
| HOLD\_SLOT\_NOT\_AVAILABLE | 409 | The requested hold time is not available. Please select a different time. |

**Response**

| parameter name | type | description |
| --- | --- | --- |
| cancellation\_policy | string | The restaurant’s cancellation policy. |
| credit\_card\_hold | boolean | Whether or not a restaurant requires a credit card hold to place a reservation. |
| expires\_at | float | When the hold expires, as a unix timestamp. |
| hold\_id | string | The unique Hold ID to use when placing a reservation. |
| is\_editable | boolean | Whether or not changes can be made to the reservation. |
| last\_cancellation\_date | float | The last cancellable date for the reservation, as a unix timestamp. |
| notes | string | Any reservation notes from the restaurant. |
| reserve\_url | string | The URL at which to place a reservation in case the restaurant requires a credit card hold. |

**Sample Request**

`curl -X POST \ 'https://api.yelp.com/v3/bookings/victors-french-bistro-test-listing-san-francisco/holds' \   -H 'authorization: Bearer {ACCESS_TOKEN}' \   -H 'content-type: application/x-www-form-urlencoded' \   -d 'covers=2&date=2017-12-30&time=18%3A00&unique_id=tmL95Scg93sajOswiIl4kA'`

**Sample Response**

`{ 	"cancellation_policy": "Cancel before it’s too late!", 	"credit_card_hold": false, 	"expires_at": 1506118155.568123, 	"hold_id": "KiXJLFFBnwW6NJbK34uKBQ", 	"is_editable": false, 	"last_cancellation_date": 1506106800.0, 	"notes": "Join us for Happy Hour.", 	"reserve_url": "https://www.yelp.com/reservations/aeJKOHWHK-z9ALQVTZj_Jw/checkout/2017-09-23/1200/3?hold_id=23774490" }`

# 

Reservations endpoint

`POST https://api.yelp.com/v3/bookings/{business_id}/reservations`

With this endpoint, you can place a physical reservation at a restaurant with all the information provided. This endpoint will take an optional hold id if the partner previously placed a hold. If the restaurant requires a credit card hold, you will not be able to place a reservation and the API will return an error.

In this case, you should use the **reserve\_url** provided in the hold endpoint or the opening endpoint to prompt the user for a reservation.

**Note:** All parameters being sent into the reservations endpoint needs to be sent as form data inside of the request body. They will not work as query parameters. Additionally, **you will receive an error** if you don’t pass the exact same reservation **time**, **date** and **covers** values as you supplied to the Holds endpoint.

**Parameters**

| parameter name | required | type | description |
| --- | --- | --- | --- |
| time | yes | string | The time of the requested reservation, format is HH:MM. |
| date | yes | string | The date for the reservation, format is YYYY-mm-dd |
| covers | yes | number | How many people are attending the reservation (min. value is 1; max value is 10). |
| first\_name | yes | string | The first name of the person making the reservation. |
| last\_name | yes | string | The last name of the person making the reservation. |
| phone | yes | string | The phone number to attach to the reservation. |
| email | yes | string | The email to attach to the reservation. |
| unique\_id | yes | string | This should be the user's device id or a unique user id to help tie together actions of the user on the API. Multiple requests to the Holds endpoint by the same user should use the same unique\_id. |
| hold\_id | yes | string | The Hold ID returned from the Holds endpoint. |
| notes | no | string | The additional party notes for the reservation. |

**Exceptions**

| code | status code | description |
| --- | --- | --- |
| INVALID\_RESERVATION\_PARAMETER | 400 | One of the following: 
\- Time must be 0, 15, 30 or 45 
\- date too far out in the future 
\- date is in the past 
\- This restaurant accepts reservations {max\_future\_days} days in the future **NOTE:** The {max\_future\_days} will be dependent on the restaurant's setting 
\- This restaurant only accepts online reservations between {minvalue} and {max\_value} people. **NOTE:** The {min\_value} and {max\_value} will be dependent on the restaurant's accepted minimum and maximum values for their online reservations. 
\- Bad request |
| DATE\_TIME\_VALIDATION\_ERROR | 400 | Invalid format, expected format is %H:%M |
| DATE\_TIME\_VALIDATION\_ERROR | 400 | Invalid format, expected format is %Y-%m-%d |
| TOO\_SMALL\_VALIDATION\_ERROR | 400 | Number too small: {value} |
| TOO\_LARGE\_VALIDATION\_ERROR | 400 | Number too big: {value} |
| INVALID\_HOLD\_ID | 400 | The Hold ID you provided is not valid. |
| RESERVATIONS\_PARAMS\_DONT\_MATCH\_HOLDS\_PARAMS | 400 | Input parameters must match the values provided to the Holds endpoint. |
| BUSINESS\_NOT\_FOUND | 404 | The requested business could not be found. |
| DOES\_NOT\_TAKE\_RESERVATIONS | 404 | The business given does not take reservations. |
| HOLD\_NOT\_FOUND | 404 | No valid hold found corresponding to the hold ID you provided. A hold with this ID may have never existed, or it may have expired. |
| RESERVATION\_SLOT\_NO\_LONGER\_AVAILABLE | 409 | The time you requested to book a reservation for is no longer available. Please try to reserve a different time. |
| CREDIT\_CARD\_REQUIRED | 402 | This reservation requires a credit card hold. Please contact the restaurant or use the reservation URL provided |

**Response**

| parameter name | type | description |
| --- | --- | --- |
| confirmation\_url | string | The confirmation URL for the end user in case they need to change or cancel their reservation. |
| notes | string | Restaurants may optionally provide some notes about the reservation. |
| reservation\_id | string | The unique ID for this reservation. |

**Sample Request**

`curl -X POST \ 'https://api.yelp.com/v3/bookings/victors-french-bistro-test-listing-san-francisco/reservations' \   -H 'authorization: Bearer {ACCESS_TOKEN}' \   -H 'content-type: application/x-www-form-urlencoded' \   -d 'covers=2&date=2017-12-30&time=18%3A00&unique_id={UNIQUE_ID}&hold_id={HOLD_ID}&first_name={FIRST_NAME}&last_name={LAST_NAME}&email={EMAIL}&phone={PHONE}&notes={NOTES}'`

**Sample Response**

`{ 	"confirmation_url": "https://www.yelp.com/reservations/dorsia-san-francisco-6/confirmed/36dbba9e-14a9-43f3-942d-7fdeddda74fc?checkout_success=1&adjust_creative=CPEhJkVcrc5wVgsRVvhEZQ&utm_campaign=yelp_api_v3&utm_medium=api_v3_reservations&utm_source=CPEhJkVcrc5wVgsRVvhEZQ", 	"notes": "reservation password: leprechaun" 	"reservation_id": "e33b40ef-f6b1-4f17-987c-d850892564b", }`

# 

Status endpoint

`GET https://api.yelp.com/v3/bookings/reservation/{reservation_id}/status`

**Parameters**

| parameter name | required | type | description |
| --- | --- | --- | --- |
| reservation\_id | yes | string | The Reservation ID returned from the Reservations endpoint. |

**Exceptions**

| code | status code | description |
| --- | --- | --- |
| INVALID\_RESERVATION\_ID | 400 | The Reservation ID you provided is not valid. |
| RESERVATION\_CANCELED | 400 | This reservation has been canceled. |

**Response**

| parameter name | type | description |
| --- | --- | --- |
| active | boolean | Whether the reservation in active or not. |
| date | string | The date for the reservation, format is YYYY-mm-dd |
| time | string | The time of the requested reservation, format is HH:MM:SS. |
| covers | number | How many people are attending the reservation (min. value is 1; max value is 10). |

**Sample Request**

`curl -X GET \ 'https://api.yelp.com/v3/bookings/reservation/e33b40ef-f6b1-4f17-987c-d850892564b/status \   -H 'authorization: Bearer {ACCESS_TOKEN}'`

**Sample Response**

JSON

`{   "active": true,   "date": "2017-12-30",   "time": "11:00:00",   "covers": 3 }`

# 

Cancel endpoint

`POST https://api.yelp.com/v3/bookings/reservation/{reservation_id}/cancel`

The cancel endpoint allows you to cancel a reservation using a reservation\_id.

**Parameters**

| parameter name | required | type | description |
| --- | --- | --- | --- |
| reservation\_id | yes | string | The Reservation ID returned from the Reservations endpoint. |

**Exceptions**

| code | status code | description |
| --- | --- | --- |
| INVALID\_RESERVATION\_ID | 404 | The Reservation ID you provided is not valid. |
| RESERVATION\_ALREADY\_CANCELED | 409 | This reservation has already been canceled. |
| RESERVATION\_CANCEL\_CONFLICT | 409 | The reservation could not be canceled due to a conflict. |

**Response**

This endpoint returns an empty response.

**Sample Request**

json

`curl -X POST \ 'https://api.yelp.com/v3/bookings/reservation/e33b40ef-f6b1-4f17-987c-d850892564b/cancel \   -H 'authorization: Bearer {ACCESS_TOKEN}'`

**Sample Response**

`{}`

Updated over 1 year ago

---

Did this page help you?

Yes

No

Copy Page