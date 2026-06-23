# Source: https://docs.developer.yelp.com/docs/overview-1

Waitlist Partner API allows restaurant partners to integrate Yelp Guest Manager’s Waitlist functionality into their own mobile / web apps.

The Waitlist Partner API enables partners to:

- Obtain a list of locations owned by the onboarded partner
- Fetch restaurant waitlist status including wait time estimations
- Get restaurant waitlist information including join-radius, seating preferences and max party size
- Join restaurant waitlist queue
- Create an On My Way visit
- Get details about a visit
- Cancel an existing visit

## 

Video Introduction

Check out our quick video introduction [here](https://docs.google.com/videos/d/1LJdYwcgSIcZ47PJAI4zfd5yjFwIPhIqyAj12KQwANx4/edit?usp=sharing).

## 

Getting Started

In order to use Yelp Waitlist Partner API, you need to be a Yelp Partner (see [Yelp Partner APIs](https://docs.developer.yelp.com/docs/yelp-partner-apis) for details, in particular [its Overview](https://docs.developer.yelp.com/docs/overview)). Once you are registered as a Yelp Partner with Fusion API access, please reach out to our Waitlist Partner API support team ([waitlist-api-support@yelp.com](mailto:waitlist-api-support@yelp.com)) and your restaurant customer success contact at Yelp with

- Your Partner ID.
- A CSV file with two columns: Yelp business ids and comments, you can find an example shown in the Q&A section below.

So that we can start the process of enabling and onboarding you for the Waitlist Partner API.

## 

Authentication

The Waitlist Partner API uses your Yelp Fusion API Key for authentication. See [Fusion Authentication](https://docs.developer.yelp.com/docs/fusion-authentication) for details.

## 

Usage

Yelp Partners are able to obtain a list of businesses that are linked to them by calling [GET /v3/partner/restaurants](https://docs.developer.yelp.com/reference/v3_partner_restaurants-1). This endpoint can be used to display the ‘List View’ or ‘Grid View’ of the restaurants that belong to the partner so that users can select from to join the queue or create the OMW visit.

To retrieve the waitlist status for a restaurant/location, partners can call [GET /v3/businesses/{business\_id}/waitlist/status](https://docs.developer.yelp.com/reference/v3_business_waitlist_status-1) with the Yelp business id that was obtained by calling the GET /v3/partner/restaurants. The response contains details including the waitlist state, the closed reason and wait estimates for different party sizes. In addition to above information, partners are able to obtain details about the waitlist of the chosen restaurant by calling [GET /v3/businesses/{business\_id}/waitlist/info](https://docs.developer.yelp.com/reference/v3_business_waitlist_info-1). The response contains details of the waitlist in question such as join radius, maximum party size and seating areas configured for the restaurant.

With the Yelp business id and the required details about the waitlist, depending on what the app users need, partners can utilize [POST /v3/businesses/{business\_id}/waitlist/on-my-way](https://docs.developer.yelp.com/reference/v3_business_waitlist_on-my-way-1) to create an OMW visit and POST [/v3/businesses/{business\_id}/waitlist/visits](https://docs.developer.yelp.com/reference/v3_business_waitlist_visits-1) to join the waitlist. If the request is successful, both endpoints will return a visit identifier that can be used to uniquely identify a visit.

With the visit identifier obtained by creating an OMW visit or joining the waitlist. App users are able to get details about the visit by calling [GET /v3/visits/{visit\_id}](https://docs.developer.yelp.com/reference/v3_visit_get-1) or cancel the visit by calling or [POST /v3/visits/{visit\_id}/cancel](https://docs.developer.yelp.com/reference/v3_visit_cancel-1).

## 

Q&A

1. What if I want to add newly opened / remove recently closed businesses to my restaurant list?

Please write an email to [waitlist-api-support@yelp.com](mailto:waitlist-api-support@yelp.com) and include your restaurant customer success contact at Yelp with the client ID of your OAuth client you created by following [Fusion Authentication](https://docs.developer.yelp.com/docs/fusion-authentication) and the Yelp business ids associated with the businesses so that we can help to add them to / remove them from your list.

2. What do we need to submit if we want to onboard a list of businesses to our Yelp Partner profile? 
 You can submit a list of businesses using CSV format, you can find the example as shown below:

csv

`biz_id,comment(optional) c6HT44PKCaXqzN_BdgKPCw,Restaurant_1 zT0PuDsIV-S7M-W_NaX9vw,Restaurant_2 fFGPBtsutYpn3A155Sf75Q,Restaurant_3`

3. I don't want to develop my application using a real Yelp Business, what should I do?

We can create / assign a test location to you for your development usage. After the onboarding process, please write an email to [waitlist-api-support@yelp.com](mailto:waitlist-api-support@yelp.com) and include your restaurant customer success contact at Yelp with the client ID of your OAuth client you created by following [Fusion Authentication](https://docs.developer.yelp.com/docs/fusion-authentication) . We will add the test location to your restaurant list and you will be able to see it by calling [GET /v3/partner/restaurants](https://docs.developer.yelp.com/reference/v3_partner_restaurants-1).

Copy Page