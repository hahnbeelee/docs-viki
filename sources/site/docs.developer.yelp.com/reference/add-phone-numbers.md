# Source: https://docs.developer.yelp.com/reference/add-phone-numbers

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

Request body for adding outbound phone numbers and/or setting an inbound phone number.

phone\_numbers

object

required

Used to configure inbound and outbound phone numbers. At least one of inbound or outbound must be provided.

phone\_numbers object

# 

201

The phone numbers were successfully added

# 

400

This error is returned in any of the following scenarios:

- Required phone numbers are missing from the request
- One of the provided phone numbers is invalid
- One of the provided phone numbers is already stored
- The phone number limit is reached
- The inbound phone number is invalid or already in use
- The inbound phone number is missing during first-time setup

| code | description |
| --- | --- |
| VALIDATION\_ERROR | At least one of inbound or outbound phone numbers must be provided. |
| VALIDATION\_ERROR | `<inbound_phone_number>` is not a valid US phone number. |
| VALIDATION\_ERROR | Inbound number already in use. |
| VALIDATION\_ERROR | Inbound phone number must be provided when setting up for the first time. |
| INVALID\_FORMAT | One or more phone numbers provided are in an invalid format. |
| DUPLICATE\_PHONE\_NUMBER | One or more outbound phone numbers provided are duplicates and can not be added. |
| MAX\_LIMIT\_REACHED | This request would exceed the max amount of outbound phone numbers allowed. |

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

429

You have either exceeded your daily quota, or have exceeded the queries-per-second limit for this endpoint. Try reducing the rate at which you make queries.

# 

500

Internal Server Error

Updated 2 months ago

---

ShellNodeRubyPHPPython

Bearer

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

201 - PhoneNumbers400 - Missing Inbound Or Outbound400 - Invalid Inbound400 - Inbound Already Exists400 - Missing Inbound For New Setup400 - Invalid Format400 - Duplicate Phone Number400 - Max Limit Reached401 - Unauthorized401 - Invalid Token403 - Authorization Error404 - Resource Not Found429 - Rate limited500 - Internal Server Error

Updated 2 months ago

---