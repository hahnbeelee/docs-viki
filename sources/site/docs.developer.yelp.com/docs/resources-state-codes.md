# Source: https://docs.developer.yelp.com/docs/resources-state-codes

The API uses [ISO 3166-2](https://en.wikipedia.org/wiki/ISO_3166-2#Current_codes) subdivision codes (without country code) for the "state" field in our API requests and responses. This page clarifies edge cases and exceptions to that rule.

In several countries where there are several levels of subdivisions the API may support some but not all of them.

### 

Subdivisions in countries with multiple layers

In countries with multiple layers of subdivisions with ISO 3166-2 codes, we may support some but not all.

| Country Code | Country Name | Description |
| --- | --- | --- |
| CZ | Czech Republic | [Regions](https://en.wikipedia.org/wiki/ISO_3166-2:CZ#Regions) are supported. 
[Districts](https://en.wikipedia.org/wiki/ISO_3166-2:CZ#Districts) are not supported. |
| ES | Spain | [Provinces and](https://en.wikipedia.org/wiki/ISO_3166-2:ES#Provinces) [autonomous cities](https://en.wikipedia.org/wiki/ISO_3166-2:ES#Autonomous_communities.3B_autonomous_cities_in_North_Africa) are supported. 
[Autonomous communities](https://en.wikipedia.org/wiki/ISO_3166-2:ES#Autonomous_communities.3B_autonomous_cities_in_North_Africa) are not supported. |
| FR | France | [Metropolitan departments](https://en.wikipedia.org/wiki/ISO_3166-2:FR#Metropolitan_departments) are supported. 
[Metropolitan Regions](https://en.wikipedia.org/wiki/ISO_3166-2:FR#Metropolitan_regions), [Overseas Departments](https://en.wikipedia.org/wiki/ISO_3166-2:FR#Overseas_departments), and [Dependency and overseas territorial collectivities](https://en.wikipedia.org/wiki/ISO_3166-2:FR#Dependency_and_overseas_territorial_collectivities) are not supported. |
| GB | United Kingdom | [Two-tier counties](https://en.wikipedia.org/wiki/ISO_3166-2:GB#List_of_subdivisions) are supported. 
[Unitary authorities](https://en.wikipedia.org/wiki/ISO_3166-2:GB#List_of_subdivisions) are supported. 
One custom state "XGL" (Greater London) covers the City of London and the 32 London boroughs. 
[Metropolitan counties](https://en.wikipedia.org/wiki/Metropolitan_county) are supported, with the following custom codes: 
 
| XGM | Greater Manchester |
| --- | --- |
| XMS | Merseyside |
| XSY | South Yorkshire |
| XTW | Tyne and Wear |
| XWM | West Midlands |
| XWY | West Yorkshire |

 
[London Boroughs](https://en.wikipedia.org/wiki/ISO_3166-2:GB#List_of_subdivisions) are not supported. 
[Metropolitan Districts](https://en.wikipedia.org/wiki/ISO_3166-2:GB#List_of_subdivisions) are not supported. 
[Countries](https://en.wikipedia.org/wiki/ISO_3166-2:GB#Three_countries_and_one_province) are not supported. |
| IE | Ireland | [Counties](https://en.wikipedia.org/wiki/ISO_3166-2:IE#Counties) are supported. 
[Provinces](https://en.wikipedia.org/wiki/ISO_3166-2:IE#Provinces) are not supported. |
| IT | Italy | [Provinces](https://en.wikipedia.org/wiki/ISO_3166-2:IT#Provinces) are supported. 
[Regions](https://en.wikipedia.org/wiki/ISO_3166-2:IT#Regions) are not supported. |
| NL | Netherlands | [Provinces](https://en.wikipedia.org/wiki/ISO_3166-2:NL#Provinces) are supported. 
[Countries and Special Municipalities](https://en.wikipedia.org/wiki/ISO_3166-2:NL#Countries_and_special_municipalities) are not supported. |
| PH | Philippines | [Provinces are supported. One custom province "NCR" covers Metro Manila.](https://en.wikipedia.org/wiki/ISO_3166-2:PH#Provinces) 
 
[Regions](https://en.wikipedia.org/wiki/ISO_3166-2:PH#Regions) are not supported. |
| SG | Singapore | One custom state "SG" is supported. 
[Districts](https://en.wikipedia.org/wiki/ISO_3166-2:SG#Current_codes) are not supported. |
| TW | Taiwan | [Districts](https://en.wikipedia.org/wiki/ISO_3166-2:TW#Current_codes) are supported, with the exception of: 
 

| KHQ | (see KHH) |
| --- | --- |
| TXQ | (see TXG) |
| TNQ | (see TNN) |

 
Note that TPQ refers to New Taipei City. 
 
[Municipalities](https://en.wikipedia.org/wiki/ISO_3166-2:TW#Current_codes) are supported. 
All currently assigned [special municipalities](https://en.wikipedia.org/wiki/ISO_3166-2:TW#Current_codes) are supported. 
 
Two custom codes cover additional counties: 
 

| LCH | Lienchiang County (incl. Lienchiang and Matsu Islands) |
| --- | --- |
| KNM | Kinmen County (incl. Kinmen and Quemoy) |

 |

### 

Subdivisions included in ISO 3166-1

Some country subdivisions also have a dedicated ISO 3166-1 country code. In this case, the same code is used as both the country and state code.

#### 

United States Outlying Areas

| Country Code | Country Name | State Code |
| --- | --- | --- |
| AS | American Samoa | AS |
| GU | Guam | GU |
| MP | Northern Mariana Islands | MP |
| PR | Puerto Rico | PR |
| UM | United States Minor Outlying Islands | UM |
| VI | US Virgin Islands | VI |

#### 

United Kingdom Crown Dependencies

| Country Code | Country Name | State Code |
| --- | --- | --- |
| GG | Guernsey | GG |
| IM | Isle of Man | IM |
| JE | Jersey | JE |

Updated over 3 years ago

---

Did this page help you?

Yes

No

Copy Page