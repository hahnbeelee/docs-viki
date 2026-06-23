# Source: https://docs.developer.yelp.com/reference/get_business_migration_info

⚠️

This reference guide is currently experiencing difficulties and will be back online shortly. Please contact [support@readme.io](mailto:support@readme.io?subject=API Explorer Error [ERR-YR5GEB]) with your error code.

`ERR-YR5GEB`

business\_ids

string

required

Comma-delimited list of yelp business ids (up to 200).

# 

200

Successfully fetched the business migration infos for the given businesses.

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

 \--url https://partner-api.yelp.com/v1/business\_migration\_info/business\_ids \\

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