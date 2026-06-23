# Source: https://docs.developer.yelp.com/docs/iframe-style-developer-guidelines

## 

Overview

The partner is expected to deliver:

- A web iframe
- A mobile version of the iframe

We have style requirements for these 2 pages. The goal of this style guide is

- Enabled the bare-minimum consistency across multiple apps on the platform
- Help partner understand design choices that will allow the user experience to flow smoothly from Yelp to Partner and back to Yelp

## 

Iframe Style Guide Requirements

![1400](https://files.readme.io/0efd155-image1.png)

## 

Look and Feel

1. Design and layout can resemble partners look and feel
2. Attribution, logo as shown in the above diagram (for mobile, this can be at the bottom of the menu page on one or more views)
 - Powered by
 - Attribution can be text or a logo of your company. We’ve found that 40PX in height is a good size unless partner needs something bigger.
3. Terminology for Food Delivery
 - Use Checkout or View Order as the action verb for transferring cart to Yelp for food delivery
 - Use Delivery for all Delivery options
 - Use Takeout for all Pickup options
4. Terminology for Appointments
 - Use Appointments instead of Reservations
 - Use Book instead of Reserve or anything else
 - Action button (if one exists and is explicitly named) should be “Continue Booking” or “Continue”
5. Action button
 - We’d like the action button to be as shown on the screen above.
 - For mobile, we need you to use our fixed button if you have any intermediate cart buttons

![640](https://files.readme.io/c4c6ffb-image4.png)

## 

Features

1. Conflicting features
 - Partner removes conflicting features such as reviews, notes etc
 - Don’t solicit reviews from users through emails or any other promotional material
2. Partner specific features
 - Remove promotions features such as your loyalty programs, links to sign-up for deals/offers etc
3. Links
 - Outbound links to your legal/privacy statement unless required & signed off by Yelp
 - Outbound links to other places on your site that break the flow

## 

Navigation

The user will be able to navigate back from our checkout pages and into the iframes. We will re-load the iframe with the same URL (with the opportunity token). Partner should re-initiate the iframe with the right context (cart filled, form fields filled up).

## 

Data

1. Partner Responsibility - We need you to collect fulfillment related information (special instructions, tip amount, anything custom like party size, or anything unique to your vertical). In the case of food delivery, you are allowed to enable the user to change their delivery address at any point. We have a requirement for you to send that information back to us when you create order (via the Checkout API)
2. Yelp Responsibility - We’ll manage all payment and identity. We do provide partner with an API to query for user information needed to complete an order (email, delivery address, phone number, first name, last name). You are not allowed to collect any piece of user identity from the user.

## 

Email Style Guide Requirements

Yelp typically sends all emails. Partners are not allowed to email users unless there exists a use case that’s signed-off by Yelp Business development team and then must include the Yelp Logo on top.

In particular, emails should never:

- Include promotional upsell material
- Call to actions that involve downloading an app, signing up for an account etc
- Solicit writing a review

An example of EatStreet email (notice logo attribution, clear and simple introduction that sets context, lack of promotional material)

![829](https://files.readme.io/6bac51e-image3.png)

## 

Developer Guidelines for Iframes

## 

Overflow:auto

For your mobile iframes, we require you avoid using `overflow: auto` anywhere on your page. This causes the fixed button feature to not work correctly.

### 

Background material

Fixed elements on a page can be made to move if the page contains an iframe meeting certain conditions.

Given the following code.

index.html

`<html>     <head>         <meta name="viewport" content="initial-scale=1, maximum-scale=1, user-scalable=no">         <style type="text/css">             .fixed {                 position: fixed;                 bottom: 0;             }         </style>     </head>     <body>         <iframe src="internal.html"></iframe>         <div class="fixed">             Fixed Content         </div>     </body> </html>`

internal.html

`<html>     <head> 	    <style type="text/css">             #container {                 overflow: auto;                 -webkit-overflow-scrolling: touch;             }         </style>     </head>     <body>         <div id="container">             <a href="#">Drag me down, the fixed content will move.</a>         </div>         <script>             document.addEventListener('touchstart', function() {}, true);         </script>     </body> </html>`

Load `index.html` (which will contain `internal.html` in an iframe). If you drag directly on the link the fixed content will incorrectly scroll with the page. If you drag anywhere else on the page the fixed content will remain stationary as it should.

### 

Conditions to Reproduce

The following conditions must be met on the page with fixed content:

- There must be some fixed content.
- There must be an iframe containing a page meeting the conditions below.

The following conditions must be met by the page inside the iframe:

- There must be an element with the CSS properties `overflow: auto` and `-webkit-overflow-scrolling: touch`.
- The previous element must contain an element with some active property, such as a hyperlink.
- There must be a `touchstart` listener added to the document.

### 

Variations

The element with the `overflow` and `-webkit-overflow-scrolling` properties can itself have some active state instead of containing an element that does. 
The `touchstart` listener can be added to either page.

## 

Performance

- Make sure your js & css is minified
- Make sure your js & css is concatenated

Copy Page