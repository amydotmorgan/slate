## Validate

Normalizes a single US or Canadian address, providing a non-ambiguous address match.

### URL and Method

URL: /1.0/address/validate GET

For development, 
	https://development.avalara.net
	/1.0/address/validate
    
For production, 
	https://avatax.avalara.net
	/1.0/address/validate
    
Note that xml-encoded requests should use /1.0/address/validate.xml

### Headers

**Request Method:** HTTP POST

**Authorization:** header, *required*

In the format "Basic[account number]:[license key]" encoded to <a href="http://en.wikipedia.org/wiki/Base64">Base64</a>, as per <a href="http://en.wikipedia.org/wiki/Basic_access_authentication">basic access authentication</a>.

Sample: Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=

**Content Type:** header, *required*

Standard content type header, indicating the content type of the request content.

**Content Length:** header, *required*

Standard content length header, indicating the size of the request content.


### Validate Request

Input to normalize a single US or Canadian address, providing a non-ambiguous address match.

#### Properties

**Line1:** string [50], *required*

Address line 1

**Line2:** string [50], *optional*

Address line 2

**Line3:** string [50], *optional*

Address line 3

**City:** string [50], *optional unless PostalCode is not specified*

City name

**Region:** string [3], *optional unless PostalCode is not specified*

State, province, or region name

**Country:** string [50], *optional*

Country code

**PostalCode:** string [11], *optional unless City and Region are not specified*

Postal or ZIP code

### ValidateResult

Output for address/validate showing the validated address match or address validation errors.

#### Properties

**Line1:** string [50]

Address line 1

**Line2:** string [50]

Address line 2

**Line3:** string [50]

Address line 3

**City:** string [50]

City name

**Region:** string [3]

State, province or region name

**Country:** string [2]

Country code as ISO 3166-1 (Alpha-2) country code (e.g. “US”)

**AddressType:** string [1]

Address type code.


* F - Firm or company address
* G - General Delivery address
* H - High-rise or business complex
* P - PO Box address
* R - Rural route address
* S - Street or residential address

**PostalCode:** string [11]

Postal or ZIP code

**County:** string [50]

County name

**FipsCode:** string [10]

FIPSCode is a unique 10-digit code representing each geographic combination of state, county, and city. The code is made up of the Federal Information Processing Code (FIPS) that uniquely identifies each state, county, and city in the U.S. Returned for US addresses only.

Digits represent jurisdiction codes:

* 1-2 State code
* 3-5 County code
* 6-10 City code

**CarrierRoute:** string [4]

CarrierRoute is a four-character string representing a US postal carrier route. The first character of this property, the term, is always alphabetic, and the last three numeric. For example, "R001" or "C027" would be typical carrier routes. The alphabetic letter indicates the type of delivery associated with this address. Returned for US addresses only.

* B - PO Box
* C - City delivery
* G - General delivery
* H - Highway contract
* R - Rural route

**TaxRegionId:** string

AvaTax tax region identifier

**PostNet:** string [12]

POSTNet is a 12-digit barcode containing the ZIP Code, ZIP+4 Code, and the delivery point code, used by the USPS to direct mail. Returned for US addresses only digits represent delivery information:

* 1-5 ZIP code
* 6-9 Plus4 code
* 10-11 Delivery point
* 12 Check digit

**ResultCode:** SeverityLevel

SeverityLevel as per <a title="Common Response Format" href="/api-docs/soap/shared-formats-and-methods#CommonResponseFormat">Common Response Format</a>

**Messages:** Message[]

As per <a title="Common Response Format" href="/api-docs/soap/shared-formats-and-methods#CommonResponseFormat">Common Response Format</a>