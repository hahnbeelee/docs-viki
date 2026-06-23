# Source: https://docs.developer.yelp.com/docs/notifications

# 

Overview

The partner must specify a `notification_url` during order creation. Yelp will POST a [OrderStatusChangeNotification](https://docs.developer.yelp.com/docs/resources#section-orderstatuschangenotification) resource to the url whenever there are status changes related to the Order.

Yelp expects the partner to return HTTP 200 for all notifications, indicating the message has been acknowledged. If we receive a non-200 status code in response, we will retransmit the message until a 200 has been received, or the retransmission gives up. Partners should always respond with a 200 upon accepting the notification, with the only exception being server-side issues that require a retransmit to work around.

Yelp guarantees atleast-once delivery for these notifications, so partner MUST support idempotent processing of these notifications, if same notification is delivered more than once.

The notification\_url itself should contain no query parameters (e.g. api.yelp.com/notification?type=food). If the partner wishes to include extra information in the payload, they should encode it as a path parameter in the URL (e.g. api.yelp.com/food/notification).

# 

Notification URL

The `notification_url` must be HTTPS.

Yelp currently takes a url as an argument to order create because there is no central API account management interface for the partner to pre-register and change the url. This gives the Partner flexibility.

# 

Sending Notifications

Yelp will send notifications to the Partner asynchronously after an Order status change and will timeout after 5 seconds with up to 3 retries. Currently all notifications will have object type [OrderStatusChangeNotification](https://docs.developer.yelp.com/docs/resources#section-orderstatuschangenotification), but this is subjected to change in the future.

A notification shall be sent to the partner upon completion of the following events:

| Event | Expected Notification Partner Receives |
| --- | --- |
| User submits order through the yelp site | OrderStatusChangeNotification with order\_status=ready\_for\_fulfillment |
| Partner invokes `/update` | OrderStatusChangeNotification with order\_status=ready\_for\_fulfillment |
| Partner invokes `/cancel` | OrderStatusChangeNotification with order\_status=cancelled |
| User cancels the order through Yelp | OrderStatusChangeNotification with order\_status=cancelled\_by\_user |

If applicable, notifications will also contain transaction\_status\_changes associated with any billing operation that took place with the event. i.e. charging the user's credit card.

The POST request will have [OrderStatusChangeNotification](https://docs.developer.yelp.com/docs/resources#section-orderstatuschangenotification) resource as body.

Copy Page