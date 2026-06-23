# Source: https://docs.developer.yelp.com/reference/get_program_list_all

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

#### URL Expired

The URL for this request expired after 30 days.

offset

integer

Defaults to 0

Pagination offset

limit

integer

1 to 40

Defaults to 20

Pagination limit

program\_status

string

enum

Defaults to CURRENT

Filter by a specific program status

PASTPAUSEDCURRENTFUTUREALL

Allowed:

`PAST``PAUSED``CURRENT``FUTURE``ALL`

# 

200

Successfully fetched a list of advertising programs.

# 

400

Bad Request.

Updated about 2 years ago

---

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

:

xxxxxxxxxx

1

curl \--request GET \\

2

 \--url 'https://partner-api.yelp.com/programs/v1?offset=0&limit=20&program\_status=CURRENT' \\

3

 \--header 'accept: application/json'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400

Updated about 2 years ago

---

Did this page help you?

Yes

No