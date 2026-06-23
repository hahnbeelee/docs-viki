# Source: https://docs.developer.yelp.com/docs/api-errors

When there is an error with any of the API calls, the response will have a non-200 HTTP status code and a JSON body describing the error. Besides from the common API errors listed, each API call will have its own errors described in their respective sections.

| Property | Type | Description |
| --- | --- | --- |
| errors | [Error\[\]](https://docs.developer.yelp.com/docs/api-errors#section-error) | see Error resource |

Example:

JSON

`{   "errors": [     {       "error_code": "NOT_AUTHENTICATED",       "error_message": "please authenticate",       "more_info": "[http://www.yelp.com/developers/documentation/v2/overview](http://www.yelp.com/developers/documentation/v2/overview)"     }   ] }`

## 

Error

| Property | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..256) | object type, value: `Error` |
| error\_code | utf8\_string(1..64) | error code |
| error\_message | utf8\_string(1..1024) | error message |
| more\_info | utf8\_string(1..1024) | link to Yelp docs for the error message |

## 

Common API Errors

| Status | error\_code | error\_message (example) |
| --- | --- | --- |
| 400 | FIELD\_REQUIRED | is required |
| 400 | VALIDATION\_ERROR | is invalid: |
| 401 | UNAUTHORIZED | Please authenticate |
| 500 | INTERNAL\_SERVER\_ERROR | Something is wrong with Yelp |

Updated over 7 years ago

---

Did this page help you?

Yes

No

Copy Page