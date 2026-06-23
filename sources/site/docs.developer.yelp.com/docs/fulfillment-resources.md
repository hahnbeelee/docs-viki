# Source: https://docs.developer.yelp.com/docs/fulfillment-resources

## 

ServiceType enum

| Type Value (utf8\_string) | Description |
| --- | --- |
| food | Orders for food-related goods (food delivery, pickup) |
| booking | Orders that are reserving appointments (e.g. spas, dentist, doctor) or requesting a service at a future date (e.g. plumber, repairs) |
| hotel\_reservation | Orders that reserve hotel rooms |
| restaurant\_reservation | Orders that reserve tables at restaurants |

## 

OptionType enum

This specifies where the service or goods will be rendered.

| Type Value (utf8\_string) | Description |
| --- | --- |
| at\_customer | Service will be at customer’s address or food will be delivered to customer’s address |
| at\_business | Service will be at business’ address or food will be picked up at business’ address |

## 

CustomerAddressConstraint

his is provided as an availablity\_constraint of Opportunity

| Name | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..128) | the object type, value: `CustomerAddressConstraint` |
| customer\_address\_str | utf8\_string(1..256) | original user-inputted address string |
| customer\_address | [Address](https://docs.developer.yelp.com/docs/fulfillment-resources#section-address) | address of customer, may be null |

## 

RepeatOrderConstraint

This is provided as an availablity\_constraint of Opportunity

| Name | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..128) | the object type, value: `RepeatOrderConstraint` |
| reorder\_yelp\_order\_id | uuid\_hex | The yelp\_order\_id for an order in the past for re-order. |

## 

Expectations from the partner iframe when showing a re-order

- The items that can be fulfilled will already be selected in the basket.
- For items that are no longer offered, there is a message stating that the items are not available, and that the customer should try something else.
- In some cases, there may be a price change to the item(s) in the new order. If previously ordered item is different in price than the currently re-ordered item, then put the item in the basket, but tell the customer that prices have changed.

## 

Opportunity

This resource represents a user's request to enter the ordering flow.

| Name | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..128) | the object type, value: `Opportunity` |
| opportunity\_token | uuid\_hex | unique identifier for this Opportunity |
| partner\_business\_id | utf8\_string(1..100) | partner’s business id to check availability against. Partner provided this to Yelp via Data Ingestion. |
| request\_time | timestamp | ISO8601 UTC, time user requested |
| service\_type | [ServiceType](https://docs.developer.yelp.com/docs/fulfillment-resources#section-servicetype-enum) | service type enum |
| selected\_option | [OptionType](https://docs.developer.yelp.com/docs/fulfillment-resources#section-optiontype-enum) | option selected by user |
| availability\_constraints | polymorphic availability\_constraints\[\] | This is a list of constraints entered by the user. At the moment, it may be [CustomerAddressConstraint](https://docs.developer.yelp.com/docs/fulfillment-resources#section-customeraddressconstraint) |

## 

Address

| Property | Type | Description |
| --- | --- | --- |
| object | utf8\_string(1..256) | object type, value: `Address` |
| address1 | utf8\_string(0..256) | address line 1 |
| address2 | utf8\_string(0..256) | address line 2 |
| address3 | utf8\_string(0..256) | address line 3 |
| city | utf8\_string(1..256) | city / district / town / village |
| region | utf8\_string(1..64) | state (US) or region |
| postal\_code | utf8\_string(1..64) | postal code |
| county | utf8\_string(0..256) | county |
| country | utf8\_string(2) | country code (ISO 3166-1 alpha 2) |

## 

AvailabilityStatus enum

| Type Value (utf8\_string) | Description |
| --- | --- |
| available | Business can fulfill the order (i.e. deliver to the User’s delivery address) |
| available\_can\_fulfill\_reorder\* | In case a RepeatOrderConstraint was specified and the partner can service the re-order to their best ability, this value is passed back. |
| unsupported | This service\_type and/or selected\_option is not supported by the Partner |
| unsupported\_by\_business | This service\_type and/or selected\_option is not supported by the Business |
| not\_available\_outside\_of\_hours | Business does not fulfill orders of this type at the given request\_time |
| not\_available\_outside\_of\_area | For selected\_option = `at_customer` only: customer address is outside of business’ service area |
| not\_available\_invalid\_address | For selected\_option = `at_customer` only: customer address is invalid or has bad format |
| not\_available\_ambiguous\_address | For selected\_option = `at_customer` only: customer address is ambiguous and has multiple similar locations |
| not\_available\_cannot\_fulfill\_reorder | In case a RepeatOrderConstraint was specified and the partner cannot service the re-order, this value is passed back (for eg. if the partner cannot find the order specified by the repeat order constraint) |
| not\_available\_other | Service not available for any other reason |
| no\_inventory\_available | For selected\_option = `at_business` only: the business does not have any available inventory at the time |

> ## 📘
> 
> available\_can\_fulfill\_reorder
> 
> Note that if the partner can only partially satisfy the reorder, then they should still send this status. However, they are expected to show errors on the iframe with items that are removed / not enough inventory etc. (see [Expectations from the partner iframe when showing a re-order](https://docs.developer.yelp.com/docs/fulfillment-resources#section-expectations-from-the-partner-iframe-when-showing-a-re-order))

Copy Page