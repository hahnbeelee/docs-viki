# Source: https://docs.developer.yelp.com/docs/resources

> ## 📘
> 
> Type Notation
> 
> - primitive/simple types like (strings, ints) are in lowercase.
> - decimal types have exact precision and are encoded as strings
> - Objects or resources are in camel-case.
> - for string types, utf8\_string(n) means string must have exactly n characters, not bytes
> - for string types, utf8\_string(i..j) means string must have at least i characters and at most j characters
> - for integers, we will use uint32 (for unsigned 32 bit ints)
> - arrays of Objects or primitives are denoted with \[\] after the type
> - timestamp type is an ISO8601 with timezone offset relative to UTC utf8\_string encoding
> - uuid\_hex is a UUID in hex encoding (32 characters)

## 

Order

| Property | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..256) | object type, value: `Order` |
| yelp\_order\_id | uuid\_hex | (may be null if creating an Order) unique identifier for Order that’s assigned when Order is created |
| order\_lines | [OrderLine\[\]](https://docs.developer.yelp.com/docs/resources#section-orderline) | order lines |
| service | [Service](https://docs.developer.yelp.com/docs/resources#section-service) | polymorphic service resource |
| billing\_type | [BillingType](https://docs.developer.yelp.com/docs/resources#section-billingtype-enum) | `partner` or `yelp`. Describes who collects the money and affects crediting. |
| _collection\_type_ | [CollectionType](https://docs.developer.yelp.com/docs/resources#section-collectiontype-enum) | `prepaid` or `postpaid`. Describes whether money will be collected upfront or on explicit `/complete` call from partner. CURRENTLY ONLY prepaid is SUPPORTED. |
| partner\_business\_id | utf8\_string(1..100) | partner’s id of business that is “fulfilling” the order |
| partner\_order\_id | utf8\_string(1..64) | an order id provided by partner for this order for partner’s tracking purposes |
| customer\_address | [Address](https://docs.developer.yelp.com/docs/resources#section-address) | address of customer, may be `null` |
| merchant\_commission\_rate | float (0.0 - 1.0) | sets the proportion of the total cost of goods which is given to the merchant. If this is not provided, it will default to the value in the partner contract. On updates, if this is missing, the existing merchant\_commission\_rate will be used. This field is only used as part of order create and update requests. |

## 

Validation

- `order_lines` must have at least one OrderLineItem or OrderLineBooking or OrderLineMedicalCompliant.
- `order_lines` must have at least one OrderLineTax ($0 amount is okay for states, cities, etc. with no tax). We are requiring tax lines (even for $0) to be explicit that Yelp doesn't handle tax (yet), and the partner is responsible for specifying it.
- `order_lines` must total to $0 or greater
- `partner_business_id` must map to a `yelp_business_id`, which we determined when they uploaded their business feed to us via [Data Ingestion API](https://docs.developer.yelp.com/docs/data-ingestion-api)
- `merchant_commission_rate` is enabled on a per partner basis at this time.

## 

Service

| Property | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..256) | object type, value: `Service` |
| type | [ServiceType](https://docs.developer.yelp.com/docs/resources#section-servicetype-enum) | the ServiceType enum (e.g. `food`) |
| option | [OptionType](https://docs.developer.yelp.com/docs/resources#section-optiontype-enum) | the OptionType enum (e.g. `at_customer`) |

## 

ServiceType enum

| Type Value (utf8\_string) | Description |
| --- | --- |
| food | Orders for food-related goods (food delivery, takeout) |
| booking | Orders that are reserving appointments (e.g. spas) or requesting a service at a future date (e.g. plumber, repairs) |
| hotel\_reservation | Orders that reserve hotel rooms |
| restaurant\_reservation | Orders that reserve tables at restaurants |
| goods | Orders for physical non-food items |
| club\_service | Orders for club service (table booking and bottles) |
| medical\_compliant | Orders that are reserving medical appointments (e.g. dentist, doctor) |

## 

OptionType enum

| Type Value (utf8\_string) | Description |
| --- | --- |
| at\_customer | Service will be at customer’s address or food will be delivered to customer’s address |
| at\_business | Service will be at business’ address or food will be picked up at business’ address |

## 

BillingType enum

| Type Value (utf8\_string) | Description |
| --- | --- |
| partner | Partner will collect payment from the business, which will in turn collect it directly from the customer. Yelp will debit Partner’s account for revenue sharing purposes. |
| yelp | Yelp will collect payment from the customer (via credit card). Yelp will credit Partner’s account for revenue sharing purposes. |

## 

CollectionType enum

| Type Value (utf8\_string) | Description |
| --- | --- |
| prepaid | Yelp will collect payment from the user as soon as order is submitted, without any explicit action from partner. |
| postpaid | **NOT SUPPORTED.** |

## 

OrderLine

OrderLine is polymorphic on the object field. The resources below describe the different types of OrderLines and what fields are required per type.

## 

OrderLine object types

| Type Value (utf8\_string) | Description |
| --- | --- |
| [OrderLineItem](https://docs.developer.yelp.com/docs/resources#section-orderlineitem) | A regular line describing a good being purchased, or a service |
| [OrderLineBooking](https://docs.developer.yelp.com/docs/resources#section-orderlinebooking) | A line describing a reservation booking |
| [OrderLineTip](https://docs.developer.yelp.com/docs/resources#section-orderlinetax-orderlineadjustment-orderlinetip) | A line for specifying a tip amount |
| [OrderLineTax](https://docs.developer.yelp.com/docs/resources#section-orderlinetax-orderlineadjustment-orderlinetip) | A line for specifying a tax amount |
| [OrderLineMedicalCompliant](https://docs.developer.yelp.com/docs/resources#section-orderlinemedicalcompliant) | A line for specifying a medical compliant reservation |
| [OrderLineAdjustment](https://docs.developer.yelp.com/docs/resources#section-orderlinetax-orderlineadjustment-orderlinetip) | A line for specifying misc adjustments e.g. discounts, delivery fee, etc. |

> ## 📘
> 
> Notes
> 
> - OrderLine is polymorphic instead of Order
> - OrderLine loosely corresponds to lines you would see on customer receipt or invoice and its structure depends on the partner. More information can be placed in description or can be split out into another OrderLine.

## 

OrderLineTax, OrderLineAdjustment, OrderLineTip

If **OrderLineAdjustment** is used for specifying service fee, Please prefix while specifying `name` property. For example, "Yelp Test" partner would provide name as "Yelp Test Service Fee".

| Property | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..256) | one of `OrderLineTax`, `OrderLineAdjustment`, `OrderLineTip` |
| name | utf8\_string(2..256) | name of item/service |
| quantity | uint32 | number of units being purchased |
| price | [Currency](https://docs.developer.yelp.com/docs/resources#section-currency) | price per unit (could be negative) |

## 

OrderLineItem

| Property | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..256) | object type, value: `OrderLineItem` |
| name | utf8\_string(2..256) | name of item/service |
| _description_ | utf8\_string(0..1024) | (optional) plaintext details about or customizations for item/service. newline-delimited (`\n`) |
| quantity | uint32 | number of units being purchased |
| price | [Currency](https://docs.developer.yelp.com/docs/resources#section-currency) | price per unit (could be negative) |
| partner\_item\_id | utf8\_string(0..64) | partner’s unique id for what’s being purchased with this OrderLine |

## 

OrderLineMedicalCompliant

| Property | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..256) | object type, value: `OrderLineMedicalCompliant` |
| name | utf8\_string(2..256) | name of item/service |
| description | utf8\_string(0..1024) | plaintext details about or customizations for item/service. newline-delimited (`\n`) |
| quantity | uint32 | number of units being purchased |
| price | [Currency](https://docs.developer.yelp.com/docs/resources#section-currency) | price per unit (could be negative) |
| partner\_item\_id | utf8\_string(0..64) | partner’s unique id for what’s being purchased with this OrderLine |
| _cancellation\_policy_ | CancellationPolicy | (optional) polymorphic object |

## 

OrderLineBooking

| Property | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..256) | object type, value: `OrderLineBooking` |
| name | utf8\_string(2..256) | name of item/service being reserved |
| _description_ | utf8\_string(0..1024) | (optional) plaintext details about or customizations for item/service. newline-delimited (`\n`) |
| price | [Currency](https://docs.developer.yelp.com/docs/resources#section-currency) | price for reservation (could be negative). This is total value of the service. At the service time, the customer is expected to pay (price - upfront\_price) |
| partner\_item\_id | utf8\_string(0..64) | partner’s unique id for what’s being purchased with this OrderLine |
| start\_time | timestamp | start datetime of reservation |
| _end\_time_ | timestamp | (optional) end datetime of reservation |
| _cancellation\_policy_ | CancellationPolicy | (optional) polymorphic object |
| quantity | uint32 | number of items being reserved |

## 

Validation

- quantity must be >= 1 for all types
- price is required for all types but may be 0
- In cases where cancellation\_policy object is missing, Yelp assumes that there is no cancellation policy to enforce, and the user can cancel an appointment without any penalty up to the start of the appointment.

## 

Address

| Property | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..255) | object type, value: `Address` |
| address1 | utf8\_string(0..255) | address line 1 |
| address2 | utf8\_string(0..255) | (optional) address line 2 |
| address3 | utf8\_string(0..255) | (optional) address line 3 |
| city | utf8\_string(1..255) | city / district / town / village |
| region | utf8\_string(1..64) | state (US) or region |
| postal\_code | utf8\_string(1..64) | postal code |
| _county_ | utf8\_string(0..255) | (optional) county |
| country | utf8\_string(2) | country code (ISO 3166-1 alpha 2) |

## 

Currency

| Property | Type | Description |
| --- | --- | --- |
| amount | decimal(10, 3) | currency amount with exact precision; number of decimal places should follow ISO 4217 |
| currency\_code | utf8\_string(3) | 3-char code ISO 4217 |

## 

Validation

- `amount` must be above -10,000,000 and below 10,000,000.

## 

CustomerAddressConstraint

This is provided as an `availablity_constraint` of Opportunity

| Property | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..128) | the object type, value: `CustomerAddressConstraint` |
| customer\_address\_str | utf8\_string(1..256) | original user-inputted address string |
| customer\_address | [Address](https://docs.developer.yelp.com/docs/resources#section-address) | address of customer, may be null |

## 

FulfillmentUserInfo

| Property | Type | Description |
| --- | --- | --- |
| first\_name | utf8\_string(1..256) | first name |
| last\_name | utf8\_string(1..256) | last name |
| email | utf8\_string(1..256) | email |
| phone | utf8\_string(7..32) | phone number |
| _availability\_constraints_ | polymorphic availability\_constraints\[\] | (optional) This is a list of constraints entered by the user. At the moment, it may be [CustomerAddressConstraint](https://docs.developer.yelp.com/docs/resources#section-customeraddressconstraint) |

## 

CancellationPolicy

A polymorphic object that describes when a particular cancellation action (e.g. it's ok to cancel, the user must contact business, etc). The following object types are supported.

| Object type | Description |
| --- | --- |
| [AlwaysCancellationPolicy](https://docs.developer.yelp.com/docs/resources#section-alwayscancellationpolicy) | an action that applies unconditionally |
| [MinutesBeforeCancellationPolicy](https://docs.developer.yelp.com/docs/resources#section-minutesbeforecancellationpolicy) | an action that applied specified period of time before the appointment begins. |

## 

AlwaysCancellationPolicy

Indicates that the cancellation action applies unconditionally of time.

| Property | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..256) | object type, value: `AlwaysCancellationPolicy` |
| _flat\_fee_ | [Currency](https://docs.developer.yelp.com/docs/resources#section-currency) | (optional): a flat cancellation fee that applies to cancellation (e.g. $10 fee independent of the value of the service). |
| violation\_action | [ViolationActionEnum](https://docs.developer.yelp.com/docs/resources#section-violationactionenum) | indicates who should enforce the cancellation policy and how, in cases when User wants to cancel within cancellation policy window |

## 

MinutesBeforeCancellationPolicy

| Property | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..256) | object type, value: `MinutesBeforeCancellationPolicy` |
| minutes\_before | integer | describes a cancellation policy that is in effect if current time is within this many minutes before the appointment start time (E.g. 24 hours would be minutes\_before=24\*60) |
| violation\_action | [ViolationActionEnum](https://docs.developer.yelp.com/docs/resources#section-violationactionenum) | indicates who should enforce the cancellation policy and how, in cases when User wants to cancel within cancellation policy window |

## 

ViolationActionEnum

Describes who should enforce the cancellation fee and how

| Type Value (utf8\_string) | Description |
| --- | --- |
| contact\_business | Yelp will show user a message to call/contact the business for cancellation. Whether a cancellation fee is waived, or partially or fully applied is up to the discretion of the business/partner. |

## 

Opportunity

This resource represents a user's request to enter the ordering flow.

| Property | Type | Description |
| --- | --- | --- |
| opportunity\_id | uuid\_hex | unique identifier for this Opportunity |
| partner\_business\_id | utf8\_string(1..100) | partner’s business id to check availability against. Partner provided this to Yelp via Data Ingestion. |
| request\_time | timestamp | ISO8601 UTC, time user requested |
| service\_type | [ServiceType](https://docs.developer.yelp.com/docs/resources#section-servicetype-enum) | service type enum |
| selected\_option | [OptionType](https://docs.developer.yelp.com/docs/resources#section-optiontype-enum) | option selected by user |
| availability\_constraints | polymorphic availability\_constraints\[\] | This is a list of constraints entered by the user. At the moment, it may be [CustomerAddressConstraint](https://docs.developer.yelp.com/docs/resources#section-customeraddressconstraint) |

## 

CouponInfo

| Property | Type | Description |
| --- | --- | --- |
| code | utf8\_string(1..256) | coupon code that was applied to Order. This could be null if no coupon was applied to this Order. |
| discount | [Currency](https://docs.developer.yelp.com/docs/resources#section-currency) | discount amount for the applied coupon |

## 

OrderStatus

| Property | Type | Description |
| --- | --- | --- |
| yelp\_order\_id | uuid\_hex | unique identifier of Order |
| order\_status | [OrderStatusCode](https://docs.developer.yelp.com/docs/resources#section-orderstatuscode-enum) | status of Order (see status codes below) |
| time\_created | timestamp | time Order was created |
| time\_updated | timestamp | time Order was last updated |

## 

OrderStatusCode enum

| Type Value (utf8\_string) | Description |
| --- | --- |
| pending\_user\_submit | waiting for user to provide billing/required information and to confirm purchase or reservation |
| charge\_pending | waiting for the billing to charge user |
| update\_pending | Yelp is processing an `/update` call |
| cancel\_pending | Yelp is processing a `/cancels` call |
| ready\_for\_fulfillment | Order is in a completed state and Yelp is not waiting on the Partner to call any other API endpoint. Partner/business could fulfill orders in this state. |
| cancelled | order was cancelled by partner |
| cancelled\_by\_yelp | order was cancelled by Yelp because there has been no action on it after a while or for other reasons like security |
| cancelled\_by\_user | order was cancelled by user |
| cancel\_by\_user\_pending | Yelp is processing a cancel by user request. |

## 

OperationType enum

| Type Value (utf8\_string) | Description |
| --- | --- |
| charge | user submitted purchase on the Yelp checkout page |
| update | update operation requested by partner |
| cancel | cancel operation requested by partner. |

## 

OperationStatus enum

| Type Value (utf8\_string) | Description |
| --- | --- |
| success | operation specified from OperationType is successful |
| failed | operation specified from OperationType failed |
| pending | operation specified from OperationType is pending |

## 

TransactionStatusChange

| Property | Type | Description |
| --- | --- | --- |
| operation\_type | [OperationType](https://docs.developer.yelp.com/docs/resources#section-operationtype-enum) | operation as requested by partner or user |
| amount | [Currency](https://docs.developer.yelp.com/docs/resources#section-currency) | depending on the operation\_type, this is charged or refunded amount. |
| time\_updated | timestamp | UTC time notification was created |
| operation\_status | [OperationStatus](https://docs.developer.yelp.com/docs/resources#section-operationstatus-enum) | status of the above operation request |

## 

OrderStatusChangeNotification

| Property | Type | Description |
| --- | --- | --- |
| notification\_id | uuid\_hex | uuid identifying this notification |
| yelp\_order\_id | uuid\_hex | uuid identifying order |
| _order\_request\_id_ | utf8\_string(0..32) | (optional) present for notifications corresponding to `/update` and `/cancel` partner requests |
| time\_created | timestamp | UTC time notification was created |
| order\_status | [OrderStatusCode](https://docs.developer.yelp.com/docs/resources#section-orderstatuscode-enum) | the most current order status regardless of when the notification was created |
| _coupon_ | [CouponInfo](https://docs.developer.yelp.com/docs/resources#section-couponinfo) | (optional) includes discount information if Yelp coupon was applied for this order |
| _user\_info_ | [FulfillmentUserInfo](https://docs.developer.yelp.com/docs/resources#section-fulfillmentuserinfo) | (optional) user information required for fulfilling this order, will only be present for charge operation\_type |
| transaction\_status\_change | [TransactionStatusChange](https://docs.developer.yelp.com/docs/resources#section-transactionstatuschange) | Transaction operation requested by partner and status of the operation |
| billing\_type | [BillingType](https://docs.developer.yelp.com/docs/resources#section-billingtype-enum) | Corresponds to the billing type of the order |

## 

ConfirmationType enum

| Type Value (utf8\_string) | Description |
| --- | --- |
| order\_confirmed | The order is confirmed |
| delivery\_in\_progress | The delivery is in progress |

## 

CheckoutConfirmationStatusBody

| Property | Type | Description |
| --- | --- | --- |
| confirmation\_type | [ConfirmationType](https://docs.developer.yelp.com/docs/resources#section-orderstatuschangenotification) | The state the order is being updated to |
| eta\_in\_minutes | integer | The estimated time of arrival |

## 

CancellationScenario enum

| Type Value (utf8\_string) | Description |
| --- | --- |
| cancelled\_by\_user\_via\_yelp | This /cancel call would be in response to AWAITING\_CANCEL\_POLICY\_RESOLUTION, which the case where a user initiated a cancel on the yelp, yelp notified the partner of user’s intent, and now yelp is waiting for the partner to call /cancels with an appropriate cancellation\_fee and bring the order to one of the cancelled states. Yelp Platform Action: fully refund the order and set it to CANCELLED or CANCELLED\_WITH\_FEE state. |
| cancelled\_by\_partner | Administrative cancelled by partner. In this case, cancellation\_fee should not be present in the POST request body. Yelp Platform Action: fully refund the order and set it to CANCELLED state. |
| customer\_no\_show | Business has reported to the partner that the customer was not at the appointment. cancellation\_fee contains the penalty that business wishes to charge the customer. YTP Action: charge the user the cancellation\_fee, and set the order to CANCELLED or CANCELLED\_WITH\_FEE as appropriate. |
| customer\_contacted\_business\_to\_cancel | Customer contacted the business and cancelled the appointment. cancellation\_fee contains the penalty that business wishes to charge the customer. If customer cancels in time when and no penalty applies, cancellation\_fee should be $0. YTP Action: charge the user the cancellation\_fee, and set the order to CANCELLED or CANCELLED\_WITH\_FEE as appropriate. |
| customer\_cancelled\_through\_yelp | This is an order cancelled by Yelp, most likely because a customer contacted Yelp requesting a cancel / disputing an order. |

Updated about 7 years ago

---

Did this page help you?

Yes

No

Copy Page