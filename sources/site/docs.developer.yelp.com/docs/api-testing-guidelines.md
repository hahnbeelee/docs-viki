# Source: https://docs.developer.yelp.com/docs/api-testing-guidelines

# 

Introduction

Yelp does not have a sandbox environment that mirrors production environment for developer testing. Therefore, in order to validate code before migrating to the production environment, testing must be done via the live environment via creation of dummy businesses. These steps must be followed in order to avoid any impact on Yelp’s production service.

# 

Parameters for Test Listings

Please follow these parameters when creating test listings:

- Create business with addresses in remote towns/locations so this doesn't affect Yelp users as you're creating these listings in production. Example address:

600 E Tomichi Ave, Ste 200 
Gunnison, CO 81230

- Always include “Ste 200” in Address 2 to help Yelp team further identify this is a test listing.
- You may create up to 3 businesses based on the same business name. For instance, if you create a test listing (e.g. “Cathy’s Chowder”), you can use “Cathy’s Chowder” up to 3 times as the business name using slightly different addresses
- Limit to 25 test listings initially, and notify Yelp if more test listings will need to be created.

# 

Step-By-Step Tutorial

Please follow these steps when testing:

1. Create test listings following the parameters set out above.
2. Immediately submit your test listings via this [form](https://docs.google.com/forms/d/e/1FAIpQLSf9ah3gO5F2715rvpQ_ldgP4iQfMSo6F7ycJUtJa0S4HejnWw/viewform) with each Job ID (required)
3. Once the form is submitted to Yelp, the businesses will be whitelisted and User Operations will be notified so that your provided test listings do not get deleted.
4. Following that, you may check the status of a test listing by using the status endpoint using the same Job ID.

Copy Page