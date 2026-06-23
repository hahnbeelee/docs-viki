# Source: https://docs.developer.yelp.com/reference/update_portfolio_project

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

name

string

Name of the project.

call\_to\_action

string

enum

Action of the button that shows on the project.

MTBWEBSITEPHONENONE

Allowed:

`MTB``WEBSITE``PHONE``NONE`

description

string

A description of the project.

service\_offerings

array of strings

List of service offerings

service\_offerings

ADD string

cost

string

enum

The cost of the project.

LESS\_THAN\_100100\_TO\_300300\_TO\_1K1K\_TO\_5K5K\_TO\_10K10K\_TO\_20K20K\_TO\_35KMORE\_THAN\_35K

Show 8 enum values

duration

string

enum

The duration of the project.

LESS\_THAN\_1\_DAY1\_TO\_7\_DAYS1\_TO\_2\_WEEKS2\_TO\_4\_WEEKS1\_TO\_2\_MONTHS2\_TO\_3\_MONTHSMORE\_THAN\_3\_MONTHS

Allowed:

`LESS_THAN_1_DAY``1_TO_7_DAYS``1_TO_2_WEEKS``2_TO_4_WEEKS``1_TO_2_MONTHS``2_TO_3_MONTHS``MORE_THAN_3_MONTHS`

completion\_year

integer

The year of completion of the project.

completion\_month

integer

The month of completion of the project \[1,12\].

# 

200

Successfully updated the given portfolio project.

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

curl \--request PUT \\

2

 \--url https://partner-api.yelp.com/program/program\_id/portfolio/project\_id/v1 \\

3

 \--header 'accept: application/json' \\

4

 \--header 'content-type: application/json'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400

Updated over 2 years ago

---

Did this page help you?

Yes

No