# Source: https://docs.developer.yelp.com/docs/oauth-authorization

# 

Overview

Access to this feature is reserved for contracted Yelp partners.

To learn more about becoming a partner. Visit one of these pages to explore different partnership types:

- [business.yelp.com/partners](https://business.yelp.com/partners) if you're an advertising agency.
- [Yelp Insights API](https://business.yelp.com/data/products/insights-api/), [Yelp Places API](https://business.yelp.com/data/products/places-api/), or [Yelp AI API](https://business.yelp.com/data/products/ai-api/) if you'd like to license our data.
- [business.yelp.com/partners/listing-management-partners](https://business.yelp.com/partners/listing-management-partners) if you'd like to publish your data on Yelp.

Yelp's OAuth system that uses a client\_id and client\_secret is private and reserved for specific official partnerships. To get set up with access please inquire directly with your Yelp relationship manager. This API enables partners to register their own systems or authorized third-party systems (referred to as “Application Clients” or “clients” in this document) to be able to execute actions on Yelp on a business user’s behalf. Based on the OAuth 2.0 Authorization Framework [RFC 6749](https://tools.ietf.org/html/rfc6749), Yelp grants an access token following a user’s successful login into the site, and in turn uses that token to authorize the user’s review response to be submitted.

## 

APIs using OAuth Authorization:

- [Respond to Reviews API](https://docs.developer.yelp.com/docs/respond-to-reviews-api-v2)
- [Leads API](https://docs.developer.yelp.com/docs/leads-api)

# 

Prerequisites

Before the application client system can initiate a request for an access token, the partner must register with Yelp as a client of our [OAuth Authorization system](https://www.yelp.com/developers/v3/manage_app). Upon registration, the client will be issued a client ID and a client secret to be used in requests.

Updated 10 months ago

---

### What’s Next

- [Authorization Code Workflow](https://docs.developer.yelp.com/docs/authorization-code-workflow)

Did this page help you?

Yes

No

Copy Page