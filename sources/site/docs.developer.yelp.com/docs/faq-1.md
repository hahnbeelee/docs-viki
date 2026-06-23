# Source: https://docs.developer.yelp.com/docs/faq-1

# 

Endpoints

**What should I do if I receive zero restaurant results (open at desired time, with availability for the desired time, or in the desired location)?**

1. Query the Business Search endpoint with all reservations parameters.
2. If the response is an empty list of businesses, query the business search endpoint again without the reservations params but keep **attributes = reservations** and set **open\_at = < time\_specified\_in\_first\_query >**
 - if the response has businesses in it, then Yelp Reservations restaurants are in the area, but there is no availability in the initially selected time
3. If the response from Step 2 has zero businesses in it, query the Business Search endpoint again without the reservations parameters, keeping **attributes=reservations** but remove the **open\_at** param
 - if the response has businesses in it, then Yelp Reservations restaurants are in the area, but they’re not open right now
 - if the response has zero businesses in it, then you’re likely in an isolated region far away from any available Yelp Reservations restaurants

**Which businesses can I test in the developer sandbox?**

You have access to the below test businesses.

**Note:** you can still book reservations for the **Bento Burger**, **La Tre Vietnamese Restaurant**, **Tracie's Taqueria** and others in production.

- Victor's French Bistro **_(sandbox-only)_**
 - [https://www.yelp.com/biz/victors-french-bistro-test-listing-san-francisco](https://www.yelp.com/biz/victors-french-bistro-test-listing-san-francisco)
- Bento Burger
 - [https://www.yelp.com/biz/bento-burger-test-listing-kake](https://www.yelp.com/biz/bento-burger-test-listing-kake)
- La Tre Vietnamese Restaurant
 - [https://www.yelp.com/reservations/la-tre-vietnamese-restaurant-test-listing-kake](https://www.yelp.com/reservations/la-tre-vietnamese-restaurant-test-listing-kake)
- Tracie's Taqueria
 - [https://www.yelp.com/biz/tracies-taqueria-test-listing-kake](https://www.yelp.com/biz/tracies-taqueria-test-listing-kake)
- Truffle Gal
 - [https://www.yelp.com/biz/truffle-gal-test-listing-kake](https://www.yelp.com/biz/truffle-gal-test-listing-kake)
- Dhruv's Dal
 - [https://www.yelp.com/biz/dhruvs-dal-test-listing-kake](https://www.yelp.com/biz/dhruvs-dal-test-listing-kake)
- Delicious Fried Chicken
 - [https://www.yelp.com/biz/delicious-fried-chicken-test-listing-kake](https://www.yelp.com/biz/delicious-fried-chicken-test-listing-kake)
- Halal Siblings
 - [https://www.yelp.com/biz/halal-siblings-test-listing-kake](https://www.yelp.com/biz/halal-siblings-test-listing-kake)
- Cake in Kake
 - [https://www.yelp.com/biz/cake-in-kake-test-listing-kake](https://www.yelp.com/biz/cake-in-kake-test-listing-kake)
- Swanky Restaurant
 - [https://www.yelp.com/biz/swanky-restaurant-test-listing-kake](https://www.yelp.com/biz/swanky-restaurant-test-listing-kake)

**How do I search for businesses which are reservable?**

You can set the attributes parameter to 'reservation' in the Business Search endpoint to restrict results to restaurants that only offer Yelp Reservations.

For example, a call to look for restaurants that offer Yelp Reservations in San Francisco would look like:

`https://api.yelp.com/v3/businesses/search?location=San Francisco, CA&attributes=reservation&term=restaurants`

**What is the difference between the “Takes Reservations” attribute on Yelp and “restaurant\_reservation” Search or Business Lookup API response?**

"Takes Reservations” means that this business offers reservations in general (via phone call or visit) but may not offer bookings as a Yelp Reservations customer. If you see "restaurant\_reservation" in the transactions field, this means that you can book reservations on Yelp with this restaurant.

**The business/search endpoint returns reservation\_openings while the /bookings/{id}/openings endpoint returns reservation\_times. Why do these differ**

The intent of each of these endpoints is a little different. The business/search endpoint is focused around a specific time on a date while the /openings endpoint is more broad and returns openings across multiple days.

**Are business/search endpoint reservation\_openings only returned when we make a specific inquiry or are they always present? If they are always present, can we assume current day? Otherwise should we always inquire for them? What’s a good default?**

The _reservation\_openings_ will only appear if you make a specific query using _reservation\_time_, _reservation\_date_ and _reservation\_covers_. Yes, you should always inquire for them if you want to get _reservation\_openings_.

**Do I need client-side logic to select a subset of the openings, or can we trust that in production we can simply display all the openings returned by the server?**

(bookings/{id}/openings returns openings every 15 minutes for the entire day)

In production, you can trust that we’ll simply display all openings returned by the server. We have 15 min slots so you have more slots to test with. No need for client-side logic to select a subset of the openings – you will see the same slots that you see on yelp.com today when you try searching for reservations.

**Can I book multiple reservations for a given user across many restaurants? What's the limit?**

No timeline for this functionality yet.

**Can I book multiple reservations for a given user on the same day for 1 restaurant?**

Same day reservations can't be made if you're trying to book a reservation for a user (based on unique\_id) that is 3 hours before or 3 hours after a reservation that's already booked by the user at a given restaurant.

**How far in advance can a reservation be made?**

Restaurants individually configure how far in advance they accept reservations, up to a maximum of 1 year. The most common is to accept reservations up to 90 days in advance. Time slots can only be searched for and reserved up to that date.

**Is there a 'minimum advance reservation' time? Or: can a reservation be made that starts 1 second from now?**

Yes, this is configured per-restaurant. Some restaurants may want a minimum amount of advance notice for new reservations, so they require reservations be made a certain amount of time in advance. Other restaurants accept any new reservation and have no minimum advance reservation time. It is always impossible to book a reservation in the past. Any time slots that it is too late to book will not be searchable and it is impossible to reserve that slot.

# 

Credit Cards

**How can I test for reservations that require credit card hold while I'm testing in sandbox mode?**

The sandboxed test restaurant requires credit card holds for reservations of 8 people or more. So, if you want credit card hold time slots, then reserve for 8 people or more. If you don't want time slot with credit card required, then reserve for 7 people or fewer.

**Note:** live production bookings, regardless of party size, may also require credit cards in certain scenarios. These may be tied to high-demand periods such as Valentine’s Day or other major holidays.

**Can I search for restaurants which don’t require credit card holds?**

No timeline for this functionality yet.

**What percentage of restaurants require a credit card hold?**

About 25% of restaurants require credit card hold, but some restaurants only require CC holds at peak times and days of the week.

**Can we pass through user CC data from our database?**

We don’t have API support to pass in CC values at this time. Consuming credit cards is hard to do safely and we want make sure we can ensure the security of our partners and their users before we expose this.

Currently, Yelp Reservations API does not support reservations which require a credit card. So, if you use Holds endpoint to reserve restaurants/openings that require credit card, the Holds endpoint will return a null hold\_id.

**Note:** you will receive a Reservation URL in each Reservations API response for completed bookings.

# 

Hold IDs

**Why do I receive null hold\_id sometimes?**

**How can I update phone number for a confirmed reservation?**

We don’t currently offer this functionality for guest bookings via API, Yelp.com or our mobile apps.

**Can we release a hold? Otherwise if a user switches context or changes their mind back and forth, they will have to wait 5 min for the spot to release itself.**

Releasing holds is automatic if you try to create a new hold using the same unique\_id. For example, if a user goes back and changes their party size, date and/or time, Yelp will automatically delete the old hold for that unique\_id and create a new one.

# 

Reservation Status, Cancellation and History

**When can I retrieve reservation status or history?**

Please refer to our Status and Cancel endpoints, which respectively let you retrieve a confirmed reservation booking and remotely cancel a booking. Alternatively, users can always call the business and edit or cancel via phone.

For reservation history, you should store all successful reservations on your servers so you can show history to your users.

**Can I authenticate a Yelp account to access user data?**

No timeline for this functionality.

# 

Time Zones and Boundaries

**What is the time zone for date and time?**

Time zone is localized by default to the specified Yelp Reservations business.

**What is the recommended future date to allow a user to make a reservation?**

The future date should be set based on your main use case but should be set to no more than 90 days from today to mirror the date constraints that are set on Yelp.com.

# 

Production Requirements

**Which businesses should I book during production testing?**

Please limit live production Yelp Reservations bookings to the following guidelines:

- for **_same day reservations_**
 - physically **go to the restaurant and not cancel** the reservation
 - since these reservations are legitimate, there isn't a limit here
- for **_advance reservations_**
 - these must be made **at least 2 weeks in advance**
 - cancel them by end of the business day
 - please limit advance advance reservations to 3 per restaurant 
 please limit to a total of **15 reservations total per day** across **all** restaurants

**What is an acceptable booking volume so I don’t impact restaurant operations?**

Please limit daily live bookings per business to 3, and aggregate daily bookings to 15.

\*the above limits only apply for testing, integrations in production do not need to throttle requests since production reservations are expected to be honored by the consumer that booked them.

Updated about 2 years ago

---

Did this page help you?

Yes

No

Copy Page