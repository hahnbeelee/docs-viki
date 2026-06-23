# Source: https://docs.developer.yelp.com/reference/get_program_list

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

business\_ids

string

required

Comma-delimited list of yelp business ids (up to 200).

start

integer

≥ 0

Defaults to 0

Pagination offset for programs within each business.

limit

integer

0 to 40

Defaults to 20

Pagination limit for programs within each business.

# 

200

Successfully fetched the advertising program information for the given businesses.

# 

400

Bad Request.

Updated about 2 years ago

---

ShellNodeRubyPHPPython

:

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400

Updated about 2 years ago

---