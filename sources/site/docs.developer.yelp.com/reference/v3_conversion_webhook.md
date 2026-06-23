# Source: https://docs.developer.yelp.com/reference/v3_conversion_webhook

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

vertical

string

enum

required

Denotes what type of webhook event the request belongs to. 
Required to process and link the event appropriately as more support is implemented.

booking

Allowed:

`booking`

dry\_run

boolean

Defaults to false

Allows for testing the request without enacting any lasting changes. 
The endpoint will respond with an appropriate error response if there are issues with the request, or with success if there were no issues found.

truefalse

Generic partner attribution request body

yelp\_token

string

required

The Base64 encoded string passed by query parameter of linkout URL, and stored by the partner. 
Has to be included in the webhook event associated with the original linkout.

event\_type

string

enum

required

Booking event type

confirmedcanceledrescheduled

Allowed:

`confirmed``canceled``rescheduled`

event\_timestamp

integer

required

Epoch timestamp of event, in milliseconds

external\_id

string

required

External id in the partner domain representing the booking

original\_external\_id

string

For “rescheduled” events, this will be the original booking id if a new one has been created

external\_business\_id

string

For events where a user decided to still go through with the booking, but with a different biz. 
This is the partner encoded biz id, which will be associated with Yelp biz id server-side.

booking\_details\_url

string

Callback URL for Yelp to directly retrieve the details of the booking

booked\_services

array of objects

booked\_services

ADD object

# 

200

Success

# 

400

Bad request

# 

401

Unauthorized - Unauthorized API key

# 

404

Not Found - Query vertical not found

Updated 3 months ago

---

ShellNodeRubyPHPPython

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Success400 - Missing API Key400 - API Key is too short400 - Invalid yelp token400 - Missing yelp token400 - Missing event type400 - Invalid event type400 - Stale Timestamp401 - Unauthorized API Key404 - Invalid request vertical

Updated 3 months ago

---