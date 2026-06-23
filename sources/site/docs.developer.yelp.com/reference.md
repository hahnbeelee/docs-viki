# Source: https://docs.developer.yelp.com/reference

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

This object captures the user’s request to the Fusion AI Chat endpoint. It includes 
the conversational query, optional user context for more relevant results, and 
an optional chat\_id for session continuity.

query

string

required

length ≤ 1000

• Natural language text for querying Yelp-specific information. 
• Accepts any prompt related to Yelp businesses, such as “Can you find a Thai restaurant near me?” 
• This should be plain text (no special formatting needed).

chat\_id

string

• Uniquely identifies the current conversation (chat session). 
• For the first request, set this to null or omit it; the API will respond with a new chat\_id. 
• Use the returned chat\_id on subsequent requests to continue the same conversation. 
• If omitted on subsequent requests, a new conversation is started. 
• If an invalid chat\_id is provided, the request will fail.

user\_context

object

Contains optional location data (latitude and longitude) that can help the AI 
tailor results to a user’s location. If not provided and a location-based query 
is asked, the system may prompt the user to specify a location.

user\_context object

request\_context

object

Contains optional settings that control how the API processes the request. 
These settings affect the response format and content generation behavior.

request\_context object

# 

200

A successful response

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

Updated 7 months ago

---

ShellNodeRubyPHPPython

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Find Pizza places in Chicago200 - Compare Sumo Sushi and ITs SUSHI in Las Vegas200 - Find me reservation for 2 people at Tuscany Steakhouse for July 12, 2025 at 7:00 PM400 - Invalid Request401 - Unauthorized401 - Invalid Token403 - Authorization Error404 - Resource Not Found413 - Payload Too Large429 - Rate limited500 - Internal Server Error503 - Service Unavailable

Updated 7 months ago

---