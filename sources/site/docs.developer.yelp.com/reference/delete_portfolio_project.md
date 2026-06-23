# Source: https://docs.developer.yelp.com/reference/delete_portfolio_project

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
> This endpoint is part of the Program Feature API, visit [Program Feature API](https://docs.developer.yelp.com/docs/program-feature-api) to learn more.

program\_id

string

required

project\_id

string

required

The project identifier

# 

204

Successfully deleted the given portfolio project.

# 

400

Bad Request.

Updated over 2 years ago

---

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

:

xxxxxxxxxx

1

curl \--request DELETE \\

2

 \--url https://partner-api.yelp.com/program/program\_id/portfolio/project\_id/v1 \\

3

 \--header 'accept: application/json'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

204400

Updated over 2 years ago

---

Did this page help you?

Yes

No