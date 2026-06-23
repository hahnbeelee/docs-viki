# Source: https://docs.developer.yelp.com/docs/reservation

> ## 📘
> 
> This is a Yelp Partner API
> 
> Access is disabled by default. See [Yelp Partner APIs](https://docs.developer.yelp.com/docs/yelp-partner-apis) on how to get access.

The Yelp Reservations API exposes functionality for Yelp Reservations search and native booking flows into partner applications. This will allow users to book reservations through Yelp without ever having to leave the 3rd party application.

Please note that access to this API is reserved for Yelp partners. If you'd like to enable Reservations API access on your account, please apply [here](https://www.yelp.com/fusion/vip/apply).

 

# 

Overview Video

We've recorded a video [here](https://docs.google.com/videos/d/1bcbzM5nySDfTUZLq7UyzWf9NjdsTWM_RP4ltmPHkx6Q/edit?usp=sharing) to cover the basics of the reservations api.

# 

Testing

Yelp will provision your account with access to test business ids that you can book freely on. Testing is done in our production environment and not a distinct sandbox. While testing, please do not book reservations at real Yelp businesses. You'll [query](https://docs.developer.yelp.com/reference/v3_openings) availability for test business ids directly, then complete the booking flow from there.

# 

The Reservation Flow

There are three different parties involved in the flow to book reservations: the end user, the partner, and Yelp. To book a reservation, the flow taken by end users is as follows:

1. End user will search for a reservation by providing a date, time, and number of people attending. The partner will make this request into the existing Search endpoint.
2. Yelp's Search endpoint will return businesses which can accommodate the requested date, time, and number of attendees.
3. Using the Business ID obtained from a given search, the partner will make a request to Yelp's reservation Openings endpoint to get a list of all available reservation dates and times for the restaurant.
4. The end user will select the date and time they want and the partner will place a hold for the time to Yelp's Holds endpoint. This hold lets the partner make sure that the end user does not lose their requested time while they fill out the reservation information.
5. The partner will make a request to the Reservations endpoint, which creates the actual reservation for the end user.

# 

Limitations

At the moment, the API allows you to find businesses which support Yelp Reservations, get open reservation times, place a hold for a reservation, and place a reservation. You **cannot edit reservations or retrieve users' booking histories**, but you will be able to remotely retrieve the reservation status and cancel any confirmed reservation bookings.

Copy Page