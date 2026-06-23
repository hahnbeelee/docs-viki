# Source: https://docs.developer.yelp.com/docs/request-a-quote-runbook

> ## 📘
> 
> This feature is currently in **beta** and not yet publicly available.

# 

Yelp AI API - Request a Quote (RAQ)

## 

1\. Overview

The Request a Quote (RAQ) feature enables users to request quotes from businesses through a conversational interface. The system intelligently handles two distinct flows based on whether users specify a particular business or want quotes from multiple providers.

## 

2\. Quote Request Types

### 

2.1 Originating Quote Request with Specific Business

**When it occurs:** User mentions a specific business by name 
**Example:** "I need a quote from Bob's Plumbing for fixing my sink" 
**Key Feature:** System asks if they want competing quotes

### 

2.2 Originating Quote Request without Specific Business

**When it occurs:** User wants a service but doesn't name any business 
**Example:** "I need a plumber to fix my sink" 
**Key Feature:** System finds relevant businesses automatically

### 

2.3 Non-Originating Quote Request

**When it occurs:** User asks for quotes without naming a specific business 
**Example:** "I need quotes for plumbing repair" 
**Key Feature:** No competing quotes question (already getting multiple)

## 

3\. User Experience Flow

### 

3.1 Originating Quote Request with Specific Business

When a user requests a quote from a specific business:

1. User mentions a specific business name
2. System identifies the business and asks for confirmation
3. System presents relevant questions about the job
4. System collects user contact information (email, phone, ZIP code)
5. **System asks: "Would you like to receive competing quotes from nearby businesses as well?"**
 
 > (This is the key differentiator of the originating flow - it allows users who started with 
 > a specific business to still get competitive quotes)
 
6. Based on user's response:
 - **If "Yes":** Quote request sent to the specified business AND qualified nearby businesses
 - **If "No":** Quote request sent only to the specified business
7. User receives confirmation

### 

3.2 Originating Quote Request without Specific Business

When a user requests a quote from a specific business:

1. User expresses need for a service without naming a business
2. System searches for relevant businesses in the user's area
3. System presents a list of businesses and asks user to select ONE
4. User selects a specific business
5. System presents relevant questions about the job
6. System collects user contact information (email, phone, ZIP code)
7. System asks: "Would you like to receive competing quotes from nearby businesses as well?"
8. Based on user's response:
 - **If "Yes":** Quote request sent to the specified business AND qualified nearby businesses
 - **If "No":** Quote request sent only to the specified business
9. User receives confirmation

### 

3.3 Non-Originating Flow

When a user requests quotes without specifying a business:

1. User asks for quotes for a service
2. System identifies the service needed
3. System presents relevant questions about the job
4. System collects user contact information (email, phone, ZIP code)
5. System automatically submits to multiple qualified businesses in the area
6. User receives confirmation

> **Key Difference:** The non-originating flow skips the "competing quotes" question since the user is already requesting quotes from multiple businesses.

## 

4\. Sample Conversations

### 

4.1 Originating Flow Example

**User:** "I need a quote from Joe's Plumbing for fixing a leaky faucet"

**System:** "I found Joe's Plumbing on Main St. Would you like to request a quote from them for plumbing repair?"

**User:** "Yes"

**System:** "Great! I'll help you get a quote from Joe's Plumbing. First, I need to gather some details. What type of faucet needs repair?" 
_Options: Kitchen sink / Bathroom sink / Bathtub / Other_ 
**User:** "Kitchen sink"

**System:** "Is this an emergency" 
_Options: Yes / No_ 
**User:** "No"

**System:** "Please provide your contact information:" 
**System:** "What's your email address?" 
**User:** "[john@example.com](mailto:john@example.com)"

**System:** "What's your phone number?" 
**User:** "555-0123"

**System:** "What's your ZIP code?" 
**User:** "94102"

**System:** "Would you like to receive competing quotes from nearby businesses as well?" 
**User:** "Yes"

**System:** "Great! I've submitted your quote request to Joe's Plumbing and will also send it to other qualified plumbers in your area. You should receive quotes within 24-48 hours."

### 

4.2 Non-Originating Flow Example

**User:** "I need quotes for fixing a leaky kitchen faucet"

**System:** "I'll help you get quotes for fixing your leaky kitchen faucet. I need to collect some information first."

**System:** "What type of faucet needs repair?" 
_Options: Kitchen sink / Bathroom sink / Bathtub / Other_ 
**User:** "Kitchen sink"

**System:** "Is this an emergency" 
_Options: Yes / No_ 
**User:** "No"

**System:** "Please provide your contact information:" 
**System:** "What's your email address?" 
**User:** "[jane@example.com](mailto:jane@example.com)"

**System:** "What's your phone number?" 
**User:** "555-9876"

**System:** "What's your ZIP code?" 
**User:** "94102"

**System:** "Perfect! I've submitted your quote request to multiple qualified plumbers in your area. You should receive quotes from several providers within 24-48 hours."

## 

5\. API Request/Response Examples

### 

5.1 Originating Flow - Business Identification

**Request:**

JSON

`POST https://api.yelp.com/ai/chat/v2 Authorization: Bearer <Your API Key> Content-Type: application/json  {   "query": "I need a quote from Joe's Plumbing for fixing a leaky faucet",   "locale": "en-US",   "client_id": "abc",   "user_context": {     "locale": "en_US",     "latitude": 37.7749,     "longitude": -122.4194   } }`

**Response:**

JSON

`{     "chat_id": 12345,     "response": {         "text": "To get an accurate quote from Joe's Plumbing, could you clarify if you need faucet repair, sink repair, or another type of plumbing service for your leaky faucet? This will help make sure your request goes to the right specialist.",         "tags": [             {                 "tag_type": "business",                 "start": 30,                 "end": 44,                 "meta": {                     "business_id": "123"                 }             },             {                 "tag_type": "highlight",                 "start": 76,                 "end": 89             },             {                 "tag_type": "highlight",                 "start": 91,                 "end": 102             }         ]     },     "types": [         "request_quote"     ],     "entities": [         {             "businesses": [                 {                     "id": "123",                     "alias": "joes-plumbing",                     "name": "Joe's Plumbing",                     "url": "https://www.yelp.com/biz/joes-plumbing",                     "location": {                         "address1": "2380 Eastman Ln",                         "address2": "",                         "address3": "",                         "city": "Petaluma",                         "zip_code": null,                         "state": "CA",                         "country": "US",                         "formatted_address": "2380 Eastman Ln\nPetaluma, CA 94952"                     },                     "coordinates": {                         "latitude": 38.234500885009766,                         "longitude": -122.69200134277344                     },                     "review_count": 2,                     "price": null,                     "rating": 4.5,                     "categories": [                         {                             "alias": "plumbing",                             "title": "Plumbing"                         }                     ],                     "attributes": {                         "BusinessUrl": null,                         "AboutThisBizBioPhotoDict": null,                         "AboutThisBizBusinessRecommendation": [],                         "BusinessAddressAlternate": null,                         "BusinessCategorySic": null,                         "BusinessMovedFrom": null,                         "BusinessNameAlternate": null,                         "BusinessOpeningDate": null,                         "BusinessTempClosed": null,                         "GroupName": null,                         "StoreCode": null,                         "AboutThisBizBio": null,                         "AboutThisBizBioFirstName": null,                         "AboutThisBizBioLastName": null,                         "AboutThisBizHistory": null,                         "AboutThisBizRole": null,                         "AboutThisBizSpecialties": null,                         "AboutThisBizYearEstablished": null,                         "BusinessAcceptsBitcoin": null,                         "BusinessAcceptsCreditCards": true,                         "BusinessDisplayUrl": null,                         "BusinessMovedTo": null,                         "FlowerDelivery": null,                         "NationalProviderIdentifier": null,                         "OffersMilitaryDiscount": null,                         "OngoingVigilanteEvent": null,                         "OnlineReservations": null,                         "BusinessOpenToAll": null,                         "PlatformDelivery": null,                         "PokestopNearby": null,                         "WaitlistReservation": null,                         "biz_summary": null,                         "biz_summary_long": null                     },                     "phone": "+17077628584",                     "summaries": {                         "short": null,                         "medium": null,                         "long": null                     },                     "contextual_info": {                         "summary": null,                         "review_snippets": [],                         "business_hours": [],                         "photos": [],                         "review_snippet": "Could there be a bigger \"ugh\"?! A friend recommended [[HIGHLIGHT]]Joe's Plumbing[[ENDHIGHLIGHT]], so I looked him up on Yelp and...",                         "accepts_reservations_through_yelp": false,                         "reservation_availability": null                     }                 }             ]         }     ],     "request_a_quote_survey": null }`

### 

5.2 Originating Flow - Starting Job Questions

**Request:**

JSON

`POST https://api.yelp.com/ai/chat/v2 Authorization: Bearer <Your API Key> Content-Type: application/json  {   "chat_id": 12345,   "query": "Faucet repair",   "locale": "en-US",   "client_id": "abc" }`

**Response:**

JSON

`{     "chat_id": 12345,     "response": {         "text": "Is this an emergency repair?",         "tags": []     },     "types": [         "request_quote"     ],     "entities": [         {             "businesses": [                 {                     "id": "123",                     "alias": "joes-plumbing",                     "name": "Joe's Plumbing",                     "url": "https://www.yelp.com/biz/joes-plumbing",                     "location": {                         "address1": "2380 Eastman Ln",                         "address2": "",                         "address3": "",                         "city": "Petaluma",                         "zip_code": null,                         "state": "CA",                         "country": "US",                         "formatted_address": "2380 Eastman Ln\nPetaluma, CA 94952"                     },                     "coordinates": {                         "latitude": 38.234500885009766,                         "longitude": -122.69200134277344                     },                     "review_count": 2,                     "price": null,                     "rating": 4.5,                     "categories": [                         {                             "alias": "plumbing",                             "title": "Plumbing"                         }                     ],                     "attributes": {                         "BusinessUrl": null,                         "AboutThisBizBioPhotoDict": null,                         "AboutThisBizBusinessRecommendation": [],                         "BusinessAddressAlternate": null,                         "BusinessCategorySic": null,                         "BusinessMovedFrom": null,                         "BusinessNameAlternate": null,                         "BusinessOpeningDate": null,                         "BusinessTempClosed": null,                         "GroupName": null,                         "StoreCode": null,                         "AboutThisBizBio": null,                         "AboutThisBizBioFirstName": null,                         "AboutThisBizBioLastName": null,                         "AboutThisBizHistory": null,                         "AboutThisBizRole": null,                         "AboutThisBizSpecialties": null,                         "AboutThisBizYearEstablished": null,                         "BusinessAcceptsBitcoin": null,                         "BusinessAcceptsCreditCards": true,                         "BusinessDisplayUrl": null,                         "BusinessMovedTo": null,                         "FlowerDelivery": null,                         "NationalProviderIdentifier": null,                         "OffersMilitaryDiscount": null,                         "OngoingVigilanteEvent": null,                         "OnlineReservations": null,                         "BusinessOpenToAll": null,                         "PlatformDelivery": null,                         "PokestopNearby": null,                         "WaitlistReservation": null,                         "biz_summary": null,                         "biz_summary_long": null                     },                     "phone": "+17077628584",                     "summaries": {                         "short": null,                         "medium": null,                         "long": null                     },                     "contextual_info": {                         "summary": null,                         "review_snippets": [],                         "business_hours": [],                         "photos": [],                         "review_snippet": "Could there be a bigger \"ugh\"?! A friend recommended [[HIGHLIGHT]]Joe's Plumbing[[ENDHIGHLIGHT]], so I looked him up on Yelp and...",                         "accepts_reservations_through_yelp": false,                         "reservation_availability": null                     }                 }             ]         }     ],     "request_a_quote_survey": {         "job_display_name": "Faucet repair",         "status": "in_progress",         "questions": [             {                 "text": "Is this an emergency repair?",                 "available_choices": [                     "Yes",                     "No"                 ],                 "only_accepts_choices": true,                 "is_multi_select": false,                 "required": false,                 "user_response": null             },             {                 "text": "How many faucets need repair?",                 "available_choices": [                     "1",                     "2",                     "3",                     "4",                     "5 or more"                 ],                 "only_accepts_choices": false,                 "is_multi_select": false,                 "required": false,                 "user_response": null             },             {                 "text": "What's wrong with your faucet? Select all that apply.",                 "available_choices": [                     "Difficult to operate",                     "Leaking",                     "Low water pressure",                     "Noisy",                     "Spraying"                 ],                 "only_accepts_choices": false,                 "is_multi_select": true,                 "required": false,                 "user_response": [                     "Leaking"                 ]             },             {                 "text": "Please add any additional details that can help service providers",                 "available_choices": null,                 "only_accepts_choices": false,                 "is_multi_select": false,                 "required": false,                 "user_response": null             }         ],         "user_info": {             "first_name": null,             "last_name": null,             "email": null,             "phone": null,             "zip_code": null         },         "requested_biz_ids": [             "123"         ],         "num_matched_businesses": 0,         "submit_to_nearby_businesses": false     } }`

 

### 

5.3 Originating Flow - Collecting Contact Information

**Request:**

JSON

`POST https://api.yelp.com/ai/chat/v2 Authorization: Bearer <Your API Key> Content-Type: application/json  {   "chat_id": 12345,   "query": "The leak is constant",   "locale": "en-US",   "client_id": "abc" }`

**Response:**

JSON

`{     "chat_id": 12345,     "response": {         "text": "I'll need your contact information to send your quote request to Joe's Plumbing. What's your name, email, phone number, and zip code?",         "tags": [             {                 "tag_type": "business",                 "start": 65,                 "end": 79,                 "meta": {                     "business_id": "123"                 }             }         ]     },     "types": [         "request_quote"     ],     "entities": [         {             "businesses": [                 {                     "id": "123",                     "alias": "joes-plumbing”,                     "name": "Joe's Plumbing",                     "url": "https://www.yelp.com/biz/joes-plumbing",                     "location": {                         "address1": "2380 Eastman Ln",                         "address2": "",                         "address3": "",                         "city": "Petaluma",                         "zip_code": null,                         "state": "CA",                         "country": "US",                         "formatted_address": "2380 Eastman Ln\nPetaluma, CA 94952"                     },                     "coordinates": {                         "latitude": 38.234500885009766,                         "longitude": -122.69200134277344                     },                     "review_count": 2,                     "price": null,                     "rating": 4.5,                     "categories": [                         {                             "alias": "plumbing",                             "title": "Plumbing"                         }                     ],                     "attributes": {                         "BusinessUrl": null,                         "AboutThisBizBioPhotoDict": null,                         "AboutThisBizBusinessRecommendation": [],                         "BusinessAddressAlternate": null,                         "BusinessCategorySic": null,                         "BusinessMovedFrom": null,                         "BusinessNameAlternate": null,                         "BusinessOpeningDate": null,                         "BusinessTempClosed": null,                         "GroupName": null,                         "StoreCode": null,                         "AboutThisBizBio": null,                         "AboutThisBizBioFirstName": null,                         "AboutThisBizBioLastName": null,                         "AboutThisBizHistory": null,                         "AboutThisBizRole": null,                         "AboutThisBizSpecialties": null,                         "AboutThisBizYearEstablished": null,                         "BusinessAcceptsBitcoin": null,                         "BusinessAcceptsCreditCards": true,                         "BusinessDisplayUrl": null,                         "BusinessMovedTo": null,                         "FlowerDelivery": null,                         "NationalProviderIdentifier": null,                         "OffersMilitaryDiscount": null,                         "OngoingVigilanteEvent": null,                         "OnlineReservations": null,                         "BusinessOpenToAll": null,                         "PlatformDelivery": null,                         "PokestopNearby": null,                         "WaitlistReservation": null,                         "biz_summary": null,                         "biz_summary_long": null                     },                     "phone": "+17077628584",                     "summaries": {                         "short": null,                         "medium": null,                         "long": null                     },                     "contextual_info": {                         "summary": null,                         "review_snippets": [],                         "business_hours": [],                         "photos": [],                         "review_snippet": "Could there be a bigger \"ugh\"?! A friend recommended [[HIGHLIGHT]]Joe's Plumbing[[ENDHIGHLIGHT]], so I looked him up on Yelp and...",                         "accepts_reservations_through_yelp": false,                         "reservation_availability": null                     }                 }             ]         }     ],     "request_a_quote_survey": {         "job_display_name": "Faucet repair",         "status": "awaiting_user_info",         "questions": [             {                 "text": "Is this an emergency repair?",                 "available_choices": [                     "Yes",                     "No"                 ],                 "only_accepts_choices": true,                 "is_multi_select": false,                 "required": false,                 "user_response": [                     "Yes"                 ]             },             {                 "text": "How many faucets need repair?",                 "available_choices": [                     "1",                     "2",                     "3",                     "4",                     "5 or more"                 ],                 "only_accepts_choices": false,                 "is_multi_select": false,                 "required": false,                 "user_response": [                     "1"                 ]             },             {                 "text": "What's wrong with your faucet? Select all that apply.",                 "available_choices": [                     "Difficult to operate",                     "Leaking",                     "Low water pressure",                     "Noisy",                     "Spraying"                 ],                 "only_accepts_choices": false,                 "is_multi_select": true,                 "required": false,                 "user_response": [                     "Leaking"                 ]             },             {                 "text": "Please add any additional details that can help service providers",                 "available_choices": null,                 "only_accepts_choices": false,                 "is_multi_select": false,                 "required": false,                 "user_response": [                     "The leak is constant"                 ]             }         ],         "user_info": {             "first_name": null,             "last_name": null,             "email": null,             "phone": null,             "zip_code": null         },         "requested_biz_ids": [             "123"         ],         "num_matched_businesses": 0,         "submit_to_nearby_businesses": false     } }`

 

### 

5.4 Originating Flow - Competing Quotes Question

**Request:**

JSON

`POST https://api.yelp.com/ai/chat/v2 Authorization: Bearer <Your API Key> Content-Type: application/json  {   "chat_id": 12345,   "query": "94102",   "locale": "en-US",   "client_id": "abc" }`

**Response:**

JSON

`{     "chat_id": 12345,     "response": {         "text": "Would you like to receive competing quotes from nearby businesses as well, or just from Joe's Plumbing?",         "tags": []     },     "types": [         "request_quote"     ],     "entities": [         {             "businesses": [                 {                     "id": "123",                     "alias": "joes-plumbing",                     "name": "Joe's Plumbing",                     "url": "https://www.yelp.com/biz/joes-plumbing",                     "location": {                         "address1": "2380 Eastman Ln",                         "address2": "",                         "address3": "",                         "city": "Petaluma",                         "zip_code": null,                         "state": "CA",                         "country": "US",                         "formatted_address": "2380 Eastman Ln\nPetaluma, CA 94952"                     },                     "coordinates": {                         "latitude": 38.234500885009766,                         "longitude": -122.69200134277344                     },                     "review_count": 2,                     "price": null,                     "rating": 4.5,                     "categories": [                         {                             "alias": "plumbing",                             "title": "Plumbing"                         }                     ],                     "attributes": {                         "BusinessUrl": null,                         "AboutThisBizBioPhotoDict": null,                         "AboutThisBizBusinessRecommendation": [],                         "BusinessAddressAlternate": null,                         "BusinessCategorySic": null,                         "BusinessMovedFrom": null,                         "BusinessNameAlternate": null,                         "BusinessOpeningDate": null,                         "BusinessTempClosed": null,                         "GroupName": null,                         "StoreCode": null,                         "AboutThisBizBio": null,                         "AboutThisBizBioFirstName": null,                         "AboutThisBizBioLastName": null,                         "AboutThisBizHistory": null,                         "AboutThisBizRole": null,                         "AboutThisBizSpecialties": null,                         "AboutThisBizYearEstablished": null,                         "BusinessAcceptsBitcoin": null,                         "BusinessAcceptsCreditCards": true,                         "BusinessDisplayUrl": null,                         "BusinessMovedTo": null,                         "FlowerDelivery": null,                         "NationalProviderIdentifier": null,                         "OffersMilitaryDiscount": null,                         "OngoingVigilanteEvent": null,                         "OnlineReservations": null,                         "BusinessOpenToAll": null,                         "PlatformDelivery": null,                         "PokestopNearby": null,                         "WaitlistReservation": null,                         "biz_summary": null,                         "biz_summary_long": null                     },                     "phone": "+17077628584",                     "summaries": {                         "short": null,                         "medium": null,                         "long": null                     },                     "contextual_info": {                         "summary": null,                         "review_snippets": [],                         "business_hours": [],                         "photos": [],                         "review_snippet": "A friend recommended [[HIGHLIGHT]]Joe's Plumbing[[ENDHIGHLIGHT]], so I looked him up on Yelp and checked out his website.",                         "accepts_reservations_through_yelp": false,                         "reservation_availability": null                     }                 }             ]         }     ],     "request_a_quote_survey": {         "job_display_name": "Faucet repair",         "status": "awaiting_submit_to_nearby",         "questions": [             {                 "text": "Is this an emergency repair?",                 "available_choices": [                     "Yes",                     "No"                 ],                 "only_accepts_choices": true,                 "is_multi_select": false,                 "required": false,                 "user_response": [                     "No"                 ]             },             {                 "text": "How many faucets need repair?",                 "available_choices": [                     "1",                     "2",                     "3",                     "4",                     "5 or more"                 ],                 "only_accepts_choices": false,                 "is_multi_select": false,                 "required": false,                 "user_response": null             },             {                 "text": "What's wrong with your faucet? Select all that apply.",                 "available_choices": [                     "Difficult to operate",                     "Leaking",                     "Low water pressure",                     "Noisy",                     "Spraying"                 ],                 "only_accepts_choices": false,                 "is_multi_select": true,                 "required": false,                 "user_response": [                     "Leaking"                 ]             },             {                 "text": "Please add any additional details that can help service providers",                 "available_choices": null,                 "only_accepts_choices": false,                 "is_multi_select": false,                 "required": false,                 "user_response": null             },             {                 "text": "Would you like to receive competing quotes from nearby businesses as well?",                 "available_choices": [                     "Yes",                     "No"                 ],                 "only_accepts_choices": true,                 "is_multi_select": false,                 "required": true,                 "user_response": null             }         ],         "user_info": {             "first_name": "John",             "last_name": "Doe",             "email": "john.doe@gmail.com",             "phone": null,             "zip_code": "94103"         },         "requested_biz_ids": [             "123"         ],         "num_matched_businesses": 1,         "submit_to_nearby_businesses": false     } }`

 

### 

5.5 Originating Flow - Final Submission

**Request:**

JSON

`POST https://api.yelp.com/ai/chat/v2 Authorization: Bearer <Your API Key> Content-Type: application/json  {   "chat_id": 12345,   "query": "Yes",   "locale": "en-US",   "client_id": "abc", }`

**Response:**

JSON

`{     "chat_id": 7744,     "response": {         "text": "Your quote request for Joe's Plumbing has been submitted successfully. They and other nearby businesses will review your request and contact you soon. If you have any updates or need further help, just let me know.",         "tags": []     },     "types": [         "request_quote"     ],     "entities": [         {             "businesses": [                 {                     "id": "123",                     "alias": "joes-plumbing",                     "name": "Joe's Plumbing",                     "url": "https://www.yelp.com/biz/joes-plumbing",                     "location": {                         "address1": "2380 Eastman Ln",                         "address2": "",                         "address3": "",                         "city": "Petaluma",                         "zip_code": null,                         "state": "CA",                         "country": "US",                         "formatted_address": "2380 Eastman Ln\nPetaluma, CA 94952"                     },                     "coordinates": {                         "latitude": 38.234500885009766,                         "longitude": -122.69200134277344                     },                     "review_count": 2,                     "price": null,                     "rating": 4.5,                     "categories": [                         {                             "alias": "plumbing",                             "title": "Plumbing"                         }                     ],                     "attributes": {                         "BusinessUrl": null,                         "AboutThisBizBioPhotoDict": null,                         "AboutThisBizBusinessRecommendation": [],                         "BusinessAddressAlternate": null,                         "BusinessCategorySic": null,                         "BusinessMovedFrom": null,                         "BusinessNameAlternate": null,                         "BusinessOpeningDate": null,                         "BusinessTempClosed": null,                         "GroupName": null,                         "StoreCode": null,                         "AboutThisBizBio": null,                         "AboutThisBizBioFirstName": null,                         "AboutThisBizBioLastName": null,                         "AboutThisBizHistory": null,                         "AboutThisBizRole": null,                         "AboutThisBizSpecialties": null,                         "AboutThisBizYearEstablished": null,                         "BusinessAcceptsBitcoin": null,                         "BusinessAcceptsCreditCards": true,                         "BusinessDisplayUrl": null,                         "BusinessMovedTo": null,                         "FlowerDelivery": null,                         "NationalProviderIdentifier": null,                         "OffersMilitaryDiscount": null,                         "OngoingVigilanteEvent": null,                         "OnlineReservations": null,                         "BusinessOpenToAll": null,                         "PlatformDelivery": null,                         "PokestopNearby": null,                         "WaitlistReservation": null,                         "biz_summary": null,                         "biz_summary_long": null                     },                     "phone": "+17077628584",                     "summaries": {                         "short": null,                         "medium": null,                         "long": null                     },                     "contextual_info": {                         "summary": null,                         "review_snippets": [],                         "business_hours": [],                         "photos": [],                         "review_snippet": "A friend recommended [[HIGHLIGHT]]Joe's Plumbing[[ENDHIGHLIGHT]], so I looked him up on Yelp and checked out his website.",                         "accepts_reservations_through_yelp": false,                         "reservation_availability": null                     }                 }             ]         }     ],     "request_a_quote_survey": {         "job_display_name": "Faucet repair",         "status": "submitted",         "questions": [             {                 "text": "Is this an emergency repair?",                 "available_choices": [                     "Yes",                     "No"                 ],                 "only_accepts_choices": true,                 "is_multi_select": false,                 "required": false,                 "user_response": [                     "No"                 ]             },             {                 "text": "How many faucets need repair?",                 "available_choices": [                     "1",                     "2",                     "3",                     "4",                     "5 or more"                 ],                 "only_accepts_choices": false,                 "is_multi_select": false,                 "required": false,                 "user_response": null             },             {                 "text": "What's wrong with your faucet? Select all that apply.",                 "available_choices": [                     "Difficult to operate",                     "Leaking",                     "Low water pressure",                     "Noisy",                     "Spraying"                 ],                 "only_accepts_choices": false,                 "is_multi_select": true,                 "required": false,                 "user_response": [                     "Leaking"                 ]             },             {                 "text": "Please add any additional details that can help service providers",                 "available_choices": null,                 "only_accepts_choices": false,                 "is_multi_select": false,                 "required": false,                 "user_response": null             },             {                 "text": "Would you like to receive competing quotes from nearby businesses as well?",                 "available_choices": [                     "Yes",                     "No"                 ],                 "only_accepts_choices": true,                 "is_multi_select": false,                 "required": true,                 "user_response": [                     "Yes"                 ]             }         ],         "user_info": {             "first_name": "John",             "last_name": "Doe",             "email": "john.doe@gmail.com",             "phone": null,             "zip_code": "94103"         },         "requested_biz_ids": null,         "num_matched_businesses": 10,         "submit_to_nearby_businesses": true     } }`

 

### 

5.6 Non-Originating Flow - Initial Request

**Request:**

JSON

`POST https://api.yelp.com/ai/chat/v2 Authorization: Bearer <Your API Key> Content-Type: application/json  {   "query": "I need quotes for fixing a leaky kitchen faucet",   "locale": "en-US",   "client_id": "abc",   "user_context": {     "locale": "en_US",     "latitude": 37.7749,     "longitude": -122.4194   } }`

**Response:**

JSON

`{     "chat_id": 12345,     "response": {         "text": "To help you get the right quote, can you tell me a bit more about the issue—are you looking for a repair to your existing kitchen faucet, or do you need a new faucet installed?",         "tags": []     },     "types": [         "request_quote"     ],     "entities": [         {             "businesses": []         }     ],     "request_a_quote_survey": null }`

 

### 

5.7 Non-Originating Flow - Contact Information

**Request:**

JSON

`POST https://api.yelp.com/ai/chat/v2 Authorization: Bearer <Your API Key> Content-Type: application/json  {   "chat_id": 12345,   "message": "No",   "client_id": "123" }`

**Response:**

JSON

`{     "chat_id": 12345,     "response": {         "text": "I'll need your contact information to send your quote request. Can you provide your name, email, phone number, and zip code?",         "tags": []     },     "types": [         "request_quote"     ],     "entities": [         {             "businesses": []         }     ],     "request_a_quote_survey": {         "job_display_name": "Faucet repair",         "status": "awaiting_user_info",         "questions": [             {                 "text": "Is this an emergency repair?",                 "available_choices": [                     "Yes",                     "No"                 ],                 "only_accepts_choices": true,                 "is_multi_select": false,                 "required": false,                 "user_response": [                     "No"                 ]             },             {                 "text": "How many faucets need repair?",                 "available_choices": [                     "1",                     "2",                     "3",                     "4",                     "5 or more"                 ],                 "only_accepts_choices": false,                 "is_multi_select": false,                 "required": false,                 "user_response": [                     "1"                 ]             },             {                 "text": "What's wrong with your faucet? Select all that apply.",                 "available_choices": [                     "Difficult to operate",                     "Leaking",                     "Low water pressure",                     "Noisy",                     "Spraying"                 ],                 "only_accepts_choices": false,                 "is_multi_select": true,                 "required": false,                 "user_response": [                     "Leaking"                 ]             },             {                 "text": "Please add any additional details that can help service providers",                 "available_choices": null,                 "only_accepts_choices": false,                 "is_multi_select": false,                 "required": false,                 "user_response": null             }         ],         "user_info": {             "first_name": null,             "last_name": null,             "email": null,             "phone": null,             "zip_code": null         },         "requested_biz_ids": null,         "num_matched_businesses": null,         "submit_to_nearby_businesses": false     } }`

### 

5.8 Non-Originating Flow - Final Submission

**Request:**

JSON

`POST https://api.yelp.com/ai/chat/v2 Authorization: Bearer <Your API Key> Content-Type: application/json  {   "chat_id": 12345,   "message": "yes",   "client_id": "abc" }`

**Response:**

JSON

`{     "chat_id": 12345,     "response": {         "text": "Your quote request for faucet repair has been sent. Local service providers will review your details and contact you soon. If you have any updates or questions, just let me know.",         "tags": []     },     "types": [         "request_quote"     ],     "entities": [         {             "businesses": []         }     ],     "request_a_quote_survey": {         "job_display_name": "Faucet repair",         "status": "submitted",         "questions": [             {                 "text": "Is this an emergency repair?",                 "available_choices": [                     "Yes",                     "No"                 ],                 "only_accepts_choices": true,                 "is_multi_select": false,                 "required": false,                 "user_response": [                     "No"                 ]             },             {                 "text": "How many faucets need repair?",                 "available_choices": [                     "1",                     "2",                     "3",                     "4",                     "5 or more"                 ],                 "only_accepts_choices": false,                 "is_multi_select": false,                 "required": false,                 "user_response": [                     "1"                 ]             },             {                 "text": "What's wrong with your faucet? Select all that apply.",                 "available_choices": [                     "Difficult to operate",                     "Leaking",                     "Low water pressure",                     "Noisy",                     "Spraying"                 ],                 "only_accepts_choices": false,                 "is_multi_select": true,                 "required": false,                 "user_response": [                     "Leaking"                 ]             },             {                 "text": "Please add any additional details that can help service providers",                 "available_choices": null,                 "only_accepts_choices": false,                 "is_multi_select": false,                 "required": false,                 "user_response": null             }         ],         "user_info": {             "first_name": "Jogn",             "last_name": "Doe",             "email": "john.doe@gmail.com",             "phone": null,             "zip_code": "94103"         },         "requested_biz_ids": null,         "num_matched_businesses": 10,         "submit_to_nearby_businesses": false     } }`

## 

6\. Relevant Fields for RAQ Responses

### 

Core Response Fields

- **response.text**: Natural language response providing information about the quote request process, next steps, and user instructions
- **response.tags**: Array of text annotations for highlighting entities (businesses, locations) with position and metadata
- **chat\_id**: Persistent conversation identifier maintaining state across API calls

### 

Response Type Indicators

- **types**: Array indicating the current response type:
 - `"business_search"` - Business search results (when searching for a specific business)
 - `"business_question"` - General business question (non-RAQ queries)
 - `"request_quote"` - Quote request interaction

### 

RAQ Survey Object

- **request\_a\_quote\_survey**: Contains complete RAQ state and questionnaire data:
 - **job\_display\_name**: Human-readable job type (e.g., "Plumbing", "Electrical", "Landscaping")
 - **status**: Current quote request status:
 - `"in_progress"` - Collecting job details via questionnaire
 - `"awaiting_user_info"` - Collecting contact information
 - `"awaiting_confirmation"` - Waiting for competing quotes decision (originating only)
 - `"submitted"` - Request successfully sent to businesses
 - `"failed"` - Request failed due to validation or system error

### 

Questions Array

- **questions**: Dynamic array of job-specific questions:
 - **text**: The question being asked
 - **available\_choices**: List of predefined answer options (null for free text)
 - **only\_accepts\_choices**: Boolean indicating if only predefined choices are accepted
 - **is\_multi\_select**: Boolean indicating if multiple selections are allowed
 - **required**: Boolean indicating if answer is mandatory
 - **user\_response**: Array containing user's answer(s) or null if not yet answered

### 

User Information

- **user\_info**: Contact details object:
 - **first\_name**: User's first name (optional)
 - **last\_name**: User's last name (optional)
 - **email**: User's email address (required)
 - **phone**: User's phone number (required)
 - **zip\_code**: Service location ZIP code (required)

### 

Business Matching Fields

- **requested\_biz\_ids**:
 - For originating flow: Array containing specific business ID(s)
 - For non-originating flow: `null`
- **num\_matched\_businesses**: Total count of businesses that received the request
- **submit\_to\_nearby\_businesses**:
 - `true`: Send to additional businesses beyond requested one
 - `false`: Send only to specifically requested business

### 

Entities and Business Data

- **entities.businesses\[\]**: Array of relevant businesses:
 - **id**: Unique business identifier
 - **name**: Business name
 - **url**: Yelp business page URL
 - **location**: Complete address information including:
 - address1, address2, address3
 - city, state, zip\_code, country
 - display\_address (formatted array)
 - **coordinates**: Latitude and longitude
 - **phone**: Business phone number
 - **rating**: Average star rating (1-5)
 - - **attributes**: Business attributes (accepts credit cards, by appointment, etc.)
 - **contextual\_info**: Additional context when relevant:
 - **summary**: Business description
 - **business\_hours**: Array of daily hours
 - **review\_snippets**: Sample reviews with rating
 - **photos**: Related business photos

## 

7\. RAQ Capabilities

### 

Current Capabilities:

- **Service Coverage:** Supports wide range of home and business services including:
 - Plumbing, electrical, HVAC, roofing
 - Landscaping, painting, cleaning, moving
 - Home improvement and repair services
- **Intelligent Flow Detection:** Automatically determines originating vs non-originating based on business name mention
- **Dynamic Questionnaires:** Job-specific questions tailored to each service type
- **Flexible Data Collection:** Supports single-select, multi-select, and free-text responses
- **Business Validation:** Ensures mentioned businesses offer the requested service
- **Contact Information Validation:** Validates email, phone, and ZIP code formats
- **Conversation Context:** Maintains state across multiple API calls using chat\_id

### 

Current Limitations:

- **No Request Modification:** Cannot edit submitted quote requests
- **No Cancellation:** Cannot cancel requests after submission
- **No Direct Messaging:** No in-API communication with businesses after submission
- **No Price Information:** Actual quotes are provided directly by businesses outside the API
- **No Scheduling:** Cannot book appointments directly through the API
- **No Status Tracking:** Cannot check the status of submitted requests
- **Business Contact Only:** Businesses contact users directly via provided email/phone
- **Geographic Limits:** Service availability depends on business coverage in the area

Copy Page