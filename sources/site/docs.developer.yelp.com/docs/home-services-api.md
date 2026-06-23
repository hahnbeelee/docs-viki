# Source: https://docs.developer.yelp.com/docs/home-services-api

> ## 📘
> 
> Access is disabled by default. To have access, please [contact us](https://business.yelp.com/data/products/places-api/#form).

The Yelp Home Services API allows partners to enable their users to request quotes for a wide range of home services (like plumbing, painting, bathtub installation, etc.). Through this integration, partners can help users to identify the type of service they need, collect detailed information about the service, and submit quote requests to the best suited home services professionals.

# 

The Home Services Flow

There are three participants in this flow: the end user, the partner, and Yelp. The typical flow for requesting home services is as follows:

1. [Get Jobs](https://docs.developer.yelp.com/reference/v3_get_jobs) Endpoint: 
 The end user or partner describes the task or project they need help with, in natural language (example: “fix a leaking faucet”) or as keywords (example: “Faucet repair”). The partner application submits this information to the Get Jobs endpoint, which returns a list of possible job aliases that match the user’s input.
2. [Get Survey](https://docs.developer.yelp.com/reference/v3_job_survey) Endpoint: 
 From the list of job aliases, the most appropriate job alias is selected based on the user's needs and the application’s logic. The partner then calls the Get Survey endpoint with the selected job alias, which returns a set of tailored questions. Collecting answers to these questions ensures all necessary information is captured for project submission, which enables Yelp to find the best service provider for the user’s needs.
3. [Business Search](https://docs.developer.yelp.com/reference/v3_business_search) Endpoint: 
 Using the job alias, the partner application can call the Business Search endpoint. By passing the job alias as a parameter and including _request\_a\_quote_ in the `attributes` parameter, the search results will return only businesses that both offer the selected service and are enabled to accept online quote requests. This ensures that any businesses returned from this search are eligible to receive quote requests through the Request a Quote feature.
4. [Request a Quote](https://docs.developer.yelp.com/reference/v3_raq_submit_project) Endpoint: 
 Once the partner has collected all the answers to the survey and the user’s contact information, the partner application submits all the required data to the Request a Quote endpoint. This action creates a new project and returns a unique project ID. Yelp will then begin matching the request to qualified businesses and invite them to provide quotes to the user.

# 

Testing

Yelp can provision your account with access to submit quote requests to test businesses only. This allows you to test freely with various job aliases without impacting real businesses.

Updated 3 months ago

---

Did this page help you?

Yes

No

Copy Page