# Source: https://docs.developer.yelp.com/docs/fusion-rate-limiting

## 

Queries-Per-Second (QPS) Rate Limiting

If you make queries against the API too quickly, you may get HTTP 429 errors with the json body:

JSON

`{     "error": {         "code": "TOO_MANY_REQUESTS_PER_SECOND",         "description": "You have exceeded the queries-per-second limit for this endpoint.                         Try reducing the rate at which you make queries."     } }`

If you are seeing these regularly, please slow down the rate at which you are making calls to the API.

## 

Daily Rate Limiting

In addition to QPS rate limiting, there is also a limit to the number of Yelp Places API requests that can be made per day and optionally a limit for specific endpoints.

Depending on the selected trial plan during signup, a client is limited to 300 (Starter Plan) API calls per 24 hours, resetting every midnight UTC. Your remaining calls, along with your maximum and the time at which your limit will reset are returned in the header of each response.

Bash

`HTTP/1.1 200 OK Content-Type: application/json Content-Length: 26 RateLimit-DailyLimit: 500 RateLimit-Remaining: 499 RateLimit-ResourceDailyLimit: 100 RateLimit-ResourceRemaining: 99 RateLimit-ResetTime: 2024-03-28T00:00:00+00:00`

| | |
| --- | --- |
| RateLimit-DailyLimit | The maximum number of calls you can make per day |
| RateLimit-Remaining | The number of calls remaining within the current day |
| RateLimit-ResourceDailyLimit | The maximum number of calls you can make per day to the current endpoint (Optional) |
| RateLimit-ResourceRemaining | The number of calls remaining within the current day to the current endpoint (Optional) |
| RateLimit-ResetTime | The time at which the current rate limiting window will expire as an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) timestamp |

Your maximum and remaining calls can also be viewed on the [Manage App](https://www.yelp.com/developers/v3/manage_app) page.

Any request sent after hitting the daily rate limit will return a HTTP 429 with JSON body:

JSON

`{     "error": {         "code": "ACCESS_LIMIT_REACHED",         "description": "You've reached the access limit for this client.           See instructions for requesting a higher access limit at            https://docs.developer.yelp.com/docs/fusion-rate-limiting"     } }`

### 

How do I get more API calls?

Additional API calls are granted based on actual user traffic, typically after a product has launched. During your development stage, please minimize API calls by caching Yelp data for up to 24 hours and storing business IDs which may be used solely for back-end matching purposes. Using the contact email associated with your Places client, email [data-licensing@yelp.com](mailto:data-licensing@yelp.com) with your Client ID and tell us about your product/integration and the number of daily requests you are hoping to have. Please also include mock-ups, screenshots, websites, etc. of your integration so we can make sure it abides by our [API Terms of Use](https://www.yelp.com/developers/api_terms) and [Display Requirements](https://www.yelp.com/developers/display_requirements).

Copy Page