# Source: https://docs.developer.yelp.com/docs/leads-api-faqs

## 

General

**What is a lead? What is an interaction event?**

A lead is generated at the start of a conversation between a user and business owner. Every thread between a user and a business owner in Yelp classifies as a single lead. Every interaction in a lead is called an (interaction) event.

**How do I get additional information about the business?**

You can use the [Get business by Id](https://docs.developer.yelp.com/reference/v3_business_info) endpoint to load business information.

**When trying to respond to a Lead I get a 404**

You will get a 404 when the biz user whose oauth token you're using doesn't have access to the business or if the lead doesn't exist. Remember that you're subscribing with your API Key and a biz user's oauth token will only grant you access to the businesses for which this user has access to.

**Why am I not receiving webhooks for all my leads?**

To receive lead webhook notifications, you first need to subscribe to the business ids that you'd like notifications for [here](https://docs.developer.yelp.com/reference/create_business_subscriptions) using event `"subscription_types": ["WEBHOOK"]`. You will only receive webhooks for locations that you're subscribed to. **Syncing your business subscriptions is an ongoing process**: We recommend you do it at _least once every 24 hours_.

## 

Marking as Read

**When should an event be marked as read?**

Once the biz user reads the event in your application. An event should never be marked as read if it wasn't read by a user.

## 

Marking as Replied

**When should a lead be marked as replied?**

You should always reply to a lead. If you respond to a lead by contacting a customer through methods outside of Yelp such as Phone or Emails you should mark the lead as replied with the [Mark Lead as replied](https://docs.developer.yelp.com/reference/mark-lead-as-replied) endpoint. A lead should never be marked as replied if it wasn't replied to outside Yelp.

> ## 📘
> 
> Got more questions?
> 
> [Email us at partner-support@yelp.com](mailto:partner-support@yelp.com)

Updated over 1 year ago

---

Did this page help you?

Yes

No

Copy Page