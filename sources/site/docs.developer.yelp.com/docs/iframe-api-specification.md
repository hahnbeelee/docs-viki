# Source: https://docs.developer.yelp.com/docs/iframe-api-specification

| Event Type | Parameters | Response |
| --- | --- | --- |
| setHeight | `'{"eventType":"setHeight", "height": $body_height }', "https://www.yelp.com"` | None |
| getViewportHeight | `'{"eventType":"getViewportHeight"}', "https://www.yelp.com"` | `{"viewportHeight":724, "viewportTopOffset":385, "iframeHeight":1256, "iframeTopOffset":0}` |
| getPopupPosition | `'{"eventType":"getPopupPosition", "popupHeight": $popup_height }', "https://www.yelp.com"` | `{"top": $top_offset}` |
| scrollTop | `'{"eventType":"scrollTop", "offset":$offset}', "https://www.yelp.com"` | None |
| displayLoading | `'{"eventType":"displayLoading"}',"https://www.yelp.com"` | None |
| hideLoading | `'{"eventType":"hideLoading"}', "https://www.yelp.com"` | None |
| checkoutRedirect | | None |
| displayFixedButton | `'{"eventType":"displayFixedButton", "amount": $amount, "buttonType": $BUTTON_TYPE [2]}', "https://www.yelp.com"` | `{"eventType":"fixedButtonClicked"}` |
| hideFixedButton | `'{"eventType":"hideFixedButton"}', "https://www.yelp.com"` | None |

- The `$body_height` must satisfy `1 <= $body_height < 99999`
- `$BUTTON_TYPE` is one of {CHECKOUT | VIEW\_ORDER | DONE}
- Response sent asynchronously, if and only if the user clicks on the checkout button

## 

Interactions that change HTML body height (Dropdown, Accordion, etc)

Because we don't want to show the Iframe scrollbar, the `<iframe>` on the parent page needs to have the same height as the iframe page's body. Every time the body changes height in the iframe page, it should send the new height and the event type `setHeight` in a JSON object to the parent page. The iframe also needs to specify the target origin to be [https://www.yelp.com](https://www.yelp.com).

Following is an example:

JavaScript

`var data = {   "eventType": "setHeight",   "height": 500 };  data = JSON.stringify(data);  window.top.postMessage(data, 'https://www.yelp.com');`

The parent page will be listening to the "message" event and updating the `<iframe>` height in the callback function.

## 

Popup interactions

In order to make the popup interactions smooth and avoid any confusion to the users, the popup should follow these guidelines:

- No overlay in the background
- Not draggable
- Positioned at the center of the viewport

In a typical no-iframe situation, we would need the following two offsets to center the popup:

top offset: `$viewport_height / 2 - $popup_height / 2`

left offset: `$viewport_width / 2 - $popup_width / 2`

In our situation, the popup in the iframe needs to be positioned against the viewport of the parent page, which makes it a bit more complicated. In the iframe page's context, the viewport height and width are always the same as the height and the width of the `<iframe>` on the parent page. The iframe page can just use that width to center the popup horizontally, but in order to vertically center the popup, the iframe page needs the viewport height of the parent page. And there are also situations where we don't want to vertically center the popup.

Following are the diagrams to illustrate the different scenarios:

![726](https://files.readme.io/937b142-Screen_Shot_2018-12-10_at_2.04.15_PM.png)

Parent viewport encompasses no parent header nor footer

**Final top offset needed**:

`($parent_viewport_top_offset - $iframe_top_offset) + ($parent_viewport_height/2 - $popup_height/2)`

![729](https://files.readme.io/948b17a-Screen_Shot_2018-12-10_at_2.06.17_PM.png)

The space between the iframe top and viewport bottom is greater than popup height

**Final top offset needed**:

`((($viewport_height + $viewport_top_offset) - $ifram_top_offset) - $popup_height) / 2`

![718](https://files.readme.io/75e0bf2-Screen_Shot_2018-12-10_at_2.07.03_PM.png)

The space between viewport top and iframe bottom is greater than the popup height

**Final bottom offset needed**:

`(($iframe_bottom_offset - $viewport_top_offset)/2 - $popup_height/2) + $viewport_top_offset - $iframe_top_offset`

![728](https://files.readme.io/08460f0-Screen_Shot_2018-12-10_at_2.07.50_PM.png)

The space between the iframe and viewport bottom is not smaller than the popup height

**Final top offset needed**: 10px. Just below the iframe.

![716](https://files.readme.io/7104e5b-Screen_Shot_2018-12-10_at_2.10.08_PM.png)

Popup height is greater than the space between the viewport top and iframe bottom

**Final top offset needed**: 
`$iframe_height - $popup_height - 10`

![720](https://files.readme.io/9c327c5-Screen_Shot_2018-12-10_at_2.11.19_PM.png)

Popup height is greater than the viewport height and there is enough space in the frame below the viewport to show the remaining popup

**Final top offset needed**:

`$viewport_top_offset - $iframe_top_offset`

![721](https://files.readme.io/8ae20e6-Screen_Shot_2018-12-10_at_2.12.37_PM.png)

Popup height is greater than the viewport height and there is not enough space in the frame below the viewport to show the remaining popup

**Final top offset needed**: `$iframe_height - $popup_height - 10`

The parent page will handle the calculation of the final vertical offset and passes it to the iframe page. When the iframe page needs to display a popup, it should send the popup’s height and the event type `getPopupPosition` in a JSON object to the parent page.

Following is an example:

JavaScript

`var data = {   "eventType": "getPopupPosition",   "popupHeight": $popup_height } data = JSON.stringify(data); window.top.postMessage(data, "https://www.yelp.com");`

At this point, the iframe page should have registered to the message event and be expecting a JSON object containing the top and bottom offsets. The the parent page will use the popup’s dimension to calculate the final offset needed and pass the following to the iframe page:

JSON

`{   "top": $top_offset,   "bottom": $bottom_offset }`

## 

Multi-page flow interactions

In a multi-page flow and the user goes from one page to another inside the iframe, the new iframe page needs to tell the parent page to scroll the viewport to the top. The iframe page should send the event type `scrollTop` and 0 as the offset to the parent page like this:

JavaScript

`var data = {   "eventType": "scrollTop",   "offset": 0 }; data = JSON.stringify(data); window.top.postMessage(data, "https://www.yelp.com");`

## 

Redirection to Yelp checkout page

When a users finishes ordering and clicks the submit button, 2 things should happen:

1. the iframe page should notify the parent page so it will display a Yelp loading/waiting screen:

JavaScript

`var data = {"eventType": "displayLoading"}; data = JSON.stringify(data);  window.top.postMessage(data, "https://www.yelp.com");`

2. Once the partner is done processing the users' order information, the partner will send a `checkoutRedirect` message containing the Yelp orderID in a JSON object to the parent page like this:

JavaScript

`window.top.postMessage(   '{"eventType": "hideLoading"}', "https://www.yelp.com" );  var data = {   "eventType": "checkoutRedirect",   "orderID": $order_id }; data = JSON.stringify(data);  window.top.postMessage(data, "https://www.yelp.com");`

Then the parent page will remove the loading screen and redirect itself to the checkout page.

## 

Display fixed button (mobile specific)

Checkout button is an important call-to-action element that's typically fixed at the bottom of the screen (on mobile). To achieve that fixed positioning Yelp is going to host a fixed button, and partners should send an event when the button needs to be displayed.

Currently three types of buttons are supported: `CHECKOUT`, `VIEW_ORDER` and `DONE`.

`CHECKOUT`, `VIEW_ORDER` both accept a $amount as a parameter. The only difference between them is the text displayed ("Checkout" vs "View Order"). DONE does not require a `$amount`. All three button types will send an event to the partner's iframe when tapped by users.

When a user performs an action requiring a fixed button to be displayed, partners should send an event of type `displayFixedButton`, with the current cart amount as a key in the data passed along.

Example:

JavaScript

`window.top.postMessage(   '{     "eventType": "displayFixedButton",     "buttonType": "CHECKOUT",     "amount": "25.34"   }',   'https://www.yelp.com' );`

If a user clicks on the button, Yelp will send down a message that will be:

JSON

`{"eventType": "fixedButtonClicked"}`

## 

Hide fixed button (mobile specific)

Hides a previously shown checkout button. No data should be sent along.

Example:

JavaScript

`window.top.postMessage(   '{"eventType": "hideFixedButton"}',   'https://www.yelp.com' );`

Copy Page