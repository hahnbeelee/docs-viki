# Source: https://docs.developer.yelp.com/docs/yelp-data-quality-guidelines

# 

Introduction

Yelp moderators evaluate the accuracy, eligibility, and formatting of all business information submissions. The accuracy of business information is checked against the primary business website, business presence on social media outlets, and relevant user-generated content (UGC).

# 

What to Watch Out For

1. Incorrect format submissions – Address 1, Address 2, Name
2. Ineligible business submissions – New Business Additions
3. Hours submissions that don’t designate shifts
4. Ineligible websites
5. Invalid “From the Business” content
6. Practitioners vs Practices - ex. avoid pushing Medical Center business data to an already established doctor page
7. Business transition / change of business ownership. (Examples include Apartments, Real Estate Firms, Law Firms, etc.) Please do not override previous business names. Please escalate these cases.

# 

Common Formatting Errors:

**Address 1 & 2**

| Incorrect Format | Correct Format | Comment |
| --- | --- | --- |
| Address1: 123 Main St, Ste 300 | Address1: 123 Main St 
 
Address2: Ste 300 | Suite numbers should be Address2. |
| 123 Main St 
@Harbor Mall | 123 Main St | Address1 should only contain numerical street address. |
| Main Street and High Street | 123 Main St | Cross streets should not be used in any address field – Yelp auto-populates these in many markets. |
| Serving the greater Sacramento area | \[Blank\] | Service areas auto-populate “Serving...area” language. This should not be manually added to the Address field. |

**Name**

| Incorrect Format | Correct Format | Comment |
| --- | --- | --- |
| Clear Pools Co | Clear Pools | Omit corporate abbreviations that consumers wouldn’t use colloquially |
| John Smith, D.M.D | John Smith, DMD | Doctors or dentists should be appended with “MD,” “DDS |
| Dr. Tim Cook | Tim Cook, MD | Doctors or dentists should be appended with “MD,” “DDS” |

# 

Eligibility

**Eligible Businesses**

- **Local Businesses & Services** – businesses with physical locations that users can visit or that offer a service locally
- **Local Places** – landmarks, parks, and other non-business points of interest
- **Businesses without physical locations** - there are service-based businesses that are mobile and do not have a fixed location. For example, personal trainers, yoga instructors, and many local home service providers such as plumbers, electricians, and roof cleaners show up at a customer’s residence to do work - while customers may rarely visit their offices. These businesses should have a service area (which is limited to a 50-mile radius or 100-mile diameter between the two furthest points), rather than using multiple business pages in different geographic areas. Although some of these businesses may work out of their home, we avoid adding a home address to a business page unless the address is public facing and specifically requested by the biz owner.
- **Local Flavor** – unique points of interest, attractions, and city/neighborhood listings (i.e. The 16th Avenue Tiled Steps)
- **Annual Events** – festivals and events that occur every year, such as a marathon race or parade
- **Opening Soon Businesses** - We will accept new businesses that are opening within 45 days. We encourage businesses to also let users know about their date of opening through the From the Business section to avoid consumer confusion.

**Ineligible Businesses:**

- **ATMs** (ex. Bank ATMs).
- **B2B entities serving only corporate/government clients** – B2B is acceptable, as long as the offering is available to a wide range of businesses and is useful to a typical small business owner. For instance, an airbag manufacturer serving only major automobile brands would be ineligible, but a business offering consulting services available to small business owners would be eligible
- **Corporate Offices** - corporate offices or warehouse locations for businesses should not be represented on Yelp as consumer interaction with these businesses occur at storefronts, not the corporate office.
- **E-commerce Products, Direct Sellers and/or Direct Sales** – products and multi-level marketing (MLM) businesses are ineligible for Yelp examples including individual sellers for your local Avon seller.
- **Kiosks/Vending Machines**
- **Online Only or E-commerce Businesses** – businesses that do not provide face-to-face interaction or local services. Professional service businesses that operate remotely (from a home office) are acceptable, but there should be some local interaction. For example, a local travel agent who works primarily via phone and email is acceptable, but an online travel-booking website is not.
- **Online Directories/Referral Services** – online directory websites and lead generation services are not eligible as they are a third party. We want consumers to directly engage with the business providing services, not an intermediary. Third party order-online delivery services are also ineligible.
- **Spam** - We define spammy/fraudulent listings on Yelp as deceptive listings that either resemble fake businesses or multiple listings attempting to represent multiple businesses, when in reality there is only one business. Here are some example biz types in which we commonly see spam: garage door businesses, locksmith service, psychics, towing.
- **Retail store departments & additional services** – retail stores that have different departments and/or services offered should have these denoted in their categories or about the business specialities section of the retail store's page. For example, a clothing store that also offers alterations wouldn't warrant a distinct Yelp page for Alterations.

_Yelp reserves the right in its sole discretion to deem any business eligible or ineligible for a listing on Yelp. For any questions on business eligibility, please contact [partner-support@yelp.com](mailto:partner-support@yelp.com)._

# 

Name

- Names should be succinct and reflect how an average person would refer to the business. We want to avoid keyword stuffing or adding information that’s available elsewhere in the listings information, such as neighborhoods or categories. Keep in mind the importance of consistency for chains and multi-location businesses. Avoid keyword stuffing, slogans, or promotional content
- Legal names, like Inc, LLC, Co, etc. are not allowed
- Periods should not be used in abbreviations. DMD is correct, not D.M.D.
- NO ALL CAPS. With few exceptions for short business names who consistently present themselves in all caps across their branding
- Store numbers should not be appended to business name. For example: 7-Eleven #415 is prohibited

**Normalization** 
Yelp admin normalizes certain values in names to comply with our content guidelines. Formatting changes to these values will get automatically corrected by our system.

| Normalized Values |
| --- |
| DDS, D.D.S, etc |
| Inc, INC, Inc., etc. |
| PLLC, Pllc, P.L.L.C., etc. |
| Ltd, LTD, LTD., etc. |

All other professional and legal designations are not normalized. Yelps should take care when sending values that aren’t normalized as these changes will come into our queue and are reviewed by a person.

**Special Naming Convention Rules for Individuals by Category**

| Category | Example Value |
| --- | --- |
| Doctors (with title) | Debbie P Moore, MD. We don’t accept “Dr” preceding the name |
| Lawyers | Debbie P Moore, JD |
| Massage therapist | Debbie P Moore, LMT |
| Accountant | Debbie P Moore, CPA |
| Real Estate Agents | John Smith – State Farm Insurance |

# 

Address

In the US, we generally use USPS Abbreviations **without a period**.

**Normalization** 
Yelp admin normalizes most address designations to comply with USPS standard abbreviations. **Formatting changes to these values will get automatically corrected by our system.**

| Full Name | Normalized Name |
| --- | --- |
| Avenue | Ave |
| Street | St |
| Crescent | Cres |
| Freeway | Fwy |
| Junction | Jct |
| Parade | Pie |
| Square | Sq. |
| Turnpike | Tpke |
| Place | Pl |
| Boulevard | Blvd |
| Center | CT |
| Court | Ct |
| Drive | Dr |
| Road | Rd |
| Route | Rte. |
| Expressway | Espy |
| Parkway | Pkwy |
| Building | Bldg. |
| Suite | Ste. |
| Floor | FL |

Yelp **does not** normalize directionals (North, West, Southeast, etc.) or Highway; partners should take care to send these values as abbreviations per USPS guidelines as any changes to these values will come into the queue and are reviewed by a person.

**Common Address rejections:**

- PO Boxes
- Directionals without abbreviations or with a period (e.g. 123 East Main St, 123 E. Main St)
- Cross-street and neighborhood information: 
 \- Yelp has a separate field for cross-streets that are typically auto generated from the address. 
 \- Yelp has a separate field for Neighborhood & is typically auto generated from the address.

# 

Phone

**Formatting is unimportant**. The system will automatically reformat numbers to standard (212) 555-1212. 
Common rejections:

- Phone number that does not match listed number on business’s primary website, social media, etc.
- Tracking (metered) phone numbers.
- We prefer a local number (vs. Toll Free) when available.

# 

Website

Websites should be business-owner driven and the URLs listed should demonstrate that they belong to the business. **Primary websites** are always preferred, although blogs run by the business owner are acceptable if there is no primary website available.

**Third party transactional websites are prohibited**. We define third party transactional websites as a website created and hosted by a third party company that acts as an online transactional platform between a seller and a buyer.

We also prohibit **third party directory websites**, which we define as websites that specialize in connected consumers with other websites or businesses.

**Common rejections**:

- Tracking URLs
- Third party transactional websites
- Third party directories
- Menu URLs in the Web Address field
- Social media links
- Irregular capitalization (WWW.YeLP.com)

# 

Display Website

Display websites should be used to display a clean, shorter version of the URL. This field should only be used if the desired website display is different from the web address. Most businesses will NOT need to use this field. 
Example: 
**Website**: [http://www.timhortons.com/us/en/locations/get-directions.php?id=910878](http://www.timhortons.com/us/en/locations/get-directions.php?id=910878) 
**Display Website**: [www.timhortons.com](http://www.timhortons.com)

Common Rejections:

- Display Websites that are the same as Website

# 

Categories

Categories should represent the specific, primary offerings of a business. A business may be in no more than three categories and keep in mind, we prefer listing the more specific Child category. For example, an attempt to replace “Chinese” with “Restaurants” will be rejected.

- See the Yelp Yelps Category Description to find definitions of US categories, and a list of Discouraged Pairings. Full list of categories [here](https://www.yelp.com/developers/documentation/v3/all_category_list) spreadsheet format [here](https://docs.google.com/spreadsheets/d/1bMNYTPXLlHR63ZQ-YafmzjK_LjFwBa5jHzQjq68LXEU/edit#gid=0).
- In order to be eligible for a specific category, a business must provide the full offering of that category 
 For example: a bar that has a live music performance once a week should not be listed under music venues.
- A Child category will always supplant its Parent category 
 For example: a submission of both “Dentists” and “General Dentistry” will result in the business being categorized as “General Dentistry.” The Parent category collapses when added in conjunction with the Child category.

# 

“About the Business” Section

This section provides users with some relevant color; a personal, prose description of a business’s History and Specialties. 
**“About The Business” sections**:

- **Specialties** – This should be a summary of a few things the business does best, not everything the business has to offer. Character limit (1500)
- **History** – The story of the business. Who founded it, and when? Why? Note that there’s a specific field for them to enter the year the business began operation. Character limit (1000)
- **Bio** - A little bit of information about the owner(s). This does not need to line up with the name of the business owner’s account. Could cover things like where they’re from, how they got into the business, etc. Character limit (1000)

**Guidelines used by Yelp agents when Accepting/Rejecting Content**:

- Submissions should have proper formatting, such as spacing, correct capitalization (no ALL CAPS), and use of punctuation for the most part.
- Grammar and spelling do not need to be perfect but content should be comprehensible to the average user.
- We don’t offer formatting tools such as bold, italics, etc. on listings, and efforts to recreate the effect **\***with weird punctuation**\*\*\*** or a lot of exclamation points!!!!!!!! Should be rejected. Same with text-speak (lol!)

**Common rejections:**

- Contact information, such as websites, phone numbers, and email addresses
- Keyword stuffing: excessive use of keywords, which Yelp loosely defines as 15+ keywords or phrases in list form, is not permitted

# 

Business Transitions

Business transitions occur when a business undergoes a major change, including:

- Location Moves
- Renovation
- New Name
- New Ownership

When a business undergoes a transition, Yelp User Ops will evaluate the scale of the change and take one of two actions:

- Update the existing listing: This is done if the transition is relatively minor or if it’s for a service-based business
- Close the old listing and create a new listing: This is done if the transition is major or if location/ambience are an integral part of the user experience

**Common rejections:**

- Unverifiable changes
- Changes to an old listing when a new listing has been created.

# 

How Many Listings Does a Business Get?

In general, a business should have a single page per location. However there are some other scenarios where 
multiple pages may be warranted. Please email [partner-support@Yelp.com](mailto:partner-support@Yelp.com) for any questions.

- **Discrete service offerings**: Businesses offering a variety of services in which users will have distinctly different experiences may require separate pages. One example is a car sales/repair business - a user can have a 5-star experience buying their car but may have a 3-star experience getting their car serviced. These separate service departments also typically have different operating hours and phone numbers as well, therefore it makes sense to keep them separate.
- **Businesses within another location**: Businesses located inside another location should have separate pages. For example, a restaurant located in a hotel should maintain a separate page. Certain departments within larger businesses, such as a pharmacy within a department store, may also warrant separate pages, particularly if hours or contact information are different.
- **Individual providers vs. group practices**: Some individual service providers, whose work tends to be evaluated separately from their shared practice group, have their own business pages. For example, individual doctors will typically have their own business pages, which are separate from any business pages for the hospitals, medical offices, or group practices where they may perform their services. Not every situation is the same, so submit a report if you think we need to merge two pages or create a new one.

# 

Spammy/Fraudulent Listings

We define spammy/fraudulent listings on Yelp as deceptive listings that either resemble fake businesses or multiple listings attempting to represent multiple businesses, when in reality there is only one business. These can include, but are not limited to, lead generation companies, impersonating a valid business, and multiple fake accounts that represent one actual business. Such listings will be rejected at the NBA level or removed from search if a listing already exists.

Locksmiths and movers, in particular, are common offenders. All new locksmith and mover listings must be verifiable from a credible online source. They may have either one listing per physical location **that users can visit**, or one listing per metro area in which they have a verifiable local presence.

# 

Hours

Hours should represent operating hours during which users can visit/interact with a business.

Open 24 hours

- There is no “open 24” hours attribute feature
- The same effect can be obtained by setting both Open and Closed hours to 12:00am

Multiple hours (shifts) for the same day can and should be submitted where applicable

- This is most common in restaurant and similar business type

Yelp currently is unable to display multiple sets of hours for different 
offerings (e.g. separate bar and restaurant hours) on the same listing.

![259](https://files.readme.io/e95183b-hours.png)

**Common Rejections**:

- Hours that are not verifiable on a credible source (e.g. primary website, business-run Facebook page).
- Hours submissions that don’t designate shifts

# 

Virtual Kitchens & Ghost Restaurants

**Background** 
There are 3 business models within this biz vector - please note that sometimes the vocabulary is often used interchangeably within this industry.

- **Virtual Restaurants**: Different cuisines are produced out of real-life restaurants specifically for delivery. Usually, the parent restaurant also owns and controls the delivery sub-brands.
 
- **Ghost Kitchens**: Commercial kitchens that serve as a meal preparation hub for delivery orders, typically with no retail presence except for possible takeout. These commercial kitchens usually represent a handful of brands either owned or partnered with by a single entity that owns & manages the kitchen - for instance, [Reef Kitchens](http://reefkitchens.com/) owns and operates mobile kitchens, with offerings from multiple individual vendors. A consumer typically orders from one of those vendors without necessarily knowing there are other options at that facility.
 
- **Virtual Food Courts**: An emerging model, where a commercial kitchen aggregates offerings from a spectrum of brands and affords consumers a single place to order from many vendors. [Kitchen United](https://www.kitchenunited.com/) is the best current example of this - a user can order from several brands at once.
 

**Biz Page Setup 
** 
Businesses are eligible for one biz page per kitchen location where the food is prepared. Service areas should be added rather than additional pages if one kitchen serves multiple areas. (e.g. If a facility is located in the Mission District of San Francisco, the VR biz should only have one biz page on Yelp. This page should display a service area of the neighborhoods they serve.

**Formatting Guidelines 
**

**Category**

- Food Delivery Service (Mandatory)
- At least 1 restaurant category to describe type of cuisine (e.g. American Traditional, Mexican, etc.)

**Attributes**

- Virtual Restaurants marked as Yes (Mandatory)
- Delivery OR Delivery-Only (Mandatory)
- Dine-In \[sit\_down\_dining\] marked as No

**Optional Attributes**

- Takeout
- Delivery-Only (use only for businesses that do not offer takeout/pick-up)
- Online Ordering-Only (use only for businesses that do not offer phone orders)

**Address 1**

- For delivery-only, no address should be included.
- Only list Address 1 if business accepts takeout orders that a consumer would pick up from that address.

**Service Area**

- We recommend virtual restaurants establish service areas to demonstrate how far away from their kitchen they’ll deliver. Note: If a virtual restaurant has multiple kitchens within a city, service areas shouldn’t overlap.

**Name**

- Should be the name of the entity, same as any other restaurant.
- Do not add “Delivery Only,” Takeout Only,” or similar appendages to the ‘Name’ field.

**Phone and Website**

- Should go to primary contacts for those businesses; third-party delivery counterparts are prohibited.

Updated 7 months ago

---

Did this page help you?

Yes

No

Copy Page