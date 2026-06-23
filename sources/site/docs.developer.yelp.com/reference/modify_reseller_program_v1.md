# Source: https://docs.developer.yelp.com/reference/modify_reseller_program_v1

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> This endpoint is part of the Ads API, visit [Ads API](https://docs.developer.yelp.com/docs/ads-api) to learn more.

program\_id

string

required

The program\_id that needs to be modified.

start

date

Start date for the specified program

end

date

End date for the specified program

budget

integer

Monthly budget in cents. For a monthly budget of $50.00, please input “5000”. Value must be greater than or equal to $25 dollars.

max\_bid

integer

Maximum bid value in cents. Can only be changed if program is using max\_bid option. \* The minimum value is $0.50 which is "50"

future\_budget\_date

date

Schedule an upcoming budget change for campaign.

pacing\_method

string

enum

Possible values are: "paced" "unpaced" \* "strict\_paced"

pacedunpaced

Allowed:

`paced``unpaced`

ad\_categories

array of strings

You are able to choose any of the categories of the specified business and run the CPC campaign for only these categories.

You get the categories of a business using the [Get business by ID](https://docs.developer.yelp.com/reference/v3_business_info) endpoint. 
Use the `alias` of the categories (field `categories[].alias`).

Example: If the business has the categories _hvac_ and _plumbing_, you can run two different campaigns for each category with a different budget each.

ad\_categories

ADD string

# 

200

200

# 

400

400

Updated over 2 years ago

---

ShellNodeRubyPHPPython

:

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400 - Result

Updated over 2 years ago

---