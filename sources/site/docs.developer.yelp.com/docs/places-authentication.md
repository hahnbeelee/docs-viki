# Source: https://docs.developer.yelp.com/docs/places-authentication

Yelp Places API uses private API Keys to authenticate requests. To authenticate the call to an endpoint, there are only 2 steps:

1. Create an app to obtain your private API Key.
2. Authenticate API calls with the API Key.

### 

Create an app on Yelp's Developers site

In order to set up your access to Yelp Places API, you need to create an app with Yelp. This app represents the application you'll build using our API and includes the credentials you'll need to gain access. Here are the steps for creating an app:

1. Choose a plan that fits your needs [here](https://business.yelp.com/data/products/places-api/).
2. In the create new app form, enter information about your app, then agree to Yelp API Terms of Use and Display Requirements. Then click the Submit button.
3. You will now have an API Key.

> ## 🚧
> 
> **Please keep the API Key to yourself** since it is the credential for your call to Yelp's API.

### 

Authenticate API calls with the API Key

To authenticate API calls with the API Key, set the `Authorization` HTTP header value as `Bearer API_KEY`.

cURL

`curl --request GET \      --url https://api.yelp.com/v3/events/awesome-event \      --header 'Authorization: Bearer API_KEY' \      --header 'accept: application/json'`

### 

Refreshing your API Key

If your API Key has become compromised, you can disable it and receive a new one. Here are the steps for refreshing your API Key:

1. Go to [Manage App](https://www.yelp.com/developers/v3/manage_app)
2. Find the "Refresh My API Key" section, and click the "Refresh My API Key" button.
3. Your new API Key will be displayed in place of the old one on the Manage App page.

Updated 9 months ago

---

### What’s Next

- [Daily Access Limiting](https://docs.developer.yelp.com/docs/fusion-daily-access-limiting)

Did this page help you?

Yes

No

Copy Page