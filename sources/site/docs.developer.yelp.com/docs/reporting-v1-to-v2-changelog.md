# Source: https://docs.developer.yelp.com/docs/reporting-v1-to-v2-changelog

This document highlights the notable changes between Reporting API v1 and v2. The [Reporting API v2 documentation](https://docs.developer.yelp.com/#reporting_api_v2) contains detailed information about the v2 API.

# 

What's Changed

- Requests with a mix of valid and invalid business ids will succeed for the set of valid business ids. Invalid business ids will be listed in the errors dictionary of the response when fetching reports.
- More _Business Metrics_ are now available for reporting. Refer to the [_Business Metrics_](https://docs.developer.yelp.com/docs/reporting-api#reporting_api_business_metrics) section in the API documentation for the full list of supported metrics.
- The maximum number of businesses that can requested in one report has increased from 200 to 500.
- _Advertiser Metrics_ and _Business Metrics_ are no longer requested from separate endpoints. Both type of metrics can be requested through one set of endpoints (daily/monthly).
- Response formats for the GET endpoints have changed. Refer to the [_Endpoints_](https://docs.developer.yelp.com/reference#daily-report-1) documentation for the updated response format.

Updated over 7 years ago

---

Did this page help you?

Yes

No

Copy Page