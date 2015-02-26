## GetTax

```shell
curl "https://development.avalara.net/1.0/tax/get" --user 1234567890:A1B2C3D4E5F6G7H8 --header "Content-Type: text/json" --data @/Docs/getTaxRequest.json
{
"CustomerCode": "ABC4335",
"DocDate": "2014-01-01",
"CompanyCode": "APITrialCompany",
"Client": "AvaTaxSample",
"DocCode": "INV001",
"DetailLevel": "Tax",
"Commit": "false",
"DocType": "SalesInvoice",
"CustomerUsageType": "G",
"ExemptionNo": "12345",
"Discount": "50",
"TaxOverride": {
"TaxOverrideType": "TaxDate",
"Reason": "Adjustment for return",
"TaxDate": "2013-07-01",
"TaxAmount": "0",
},
"PurchaseOrderNo": "PO123456",
"ReferenceCode": "ref123456",
"PosLaneCode": "09",
"CurrencyCode": "USD",
"Addresses": [
{
"AddressCode": "01",
"Line1": "45 Fremont Street",
"City": "San Francisco",
"Region": "CA"	
},
{
"AddressCode": "02",
"Line1": "118 N Clark St",
"Line2": "Suite 100",
"Line3": "ATTN Accounts Payable",
"City": "Chicago",
"Region": "IL",
"Country": "US",
"PostalCode": "60602"	
},
{
"AddressCode": "03",
"Latitude": "47.627935",
"Longitude": "-122.51702"	
}
],
"Lines": [
{
"LineNo": "01",
"ItemCode": "N543",
"Qty": "1",
"Amount": "10",
"OriginCode": "01",
"DestinationCode": "02",
"Description": "Red Size 7 Widget",
"TaxCode": "NT",
"CustomerUsageType": "L",
"Discounted": "true",
"TaxIncluded": "true",
"Ref1": "ref123",
"Ref2": "ref456"	
},
{
"LineNo": "02",
"ItemCode": "T345",
"Qty": "3",
"Amount": "150",
"OriginCode": "01",
"DestinationCode": "03",
"Description": "Size 10 Green Running Shoe",
"TaxCode": "PC030147"	
},
{
"LineNo": "02-FR",
"ItemCode": "FREIGHT",
"Qty": "1",
"Amount": "15",
"OriginCode": "01",
"DestinationCode": "03",
"Description": "Shipping Charge",
"TaxCode": "FR"	
}
]
}
```

```java
GetTaxRequest getTaxRequest = new GetTaxRequest();
// Document Level Elements
getTaxRequest.CustomerCode = "ABC4335";
java.util.Date docDate = new SimpleDateFormat("yyyy-MM-dd", Locale.ENGLISH).parse("2014-01-01");
getTaxRequest.DocDate = new java.sql.Date(docDate.getTime());
getTaxRequest.CompanyCode = "APITrialCompany";
getTaxRequest.Client = "AvaTaxSample";
getTaxRequest.DocCode = "INV001";
getTaxRequest.DetailLevel = TaxSvc.DetailLevel.Tax;
getTaxRequest.Commit = false;
getTaxRequest.DocType = TaxSvc.DocType.SalesInvoice;
// Situational Request Parameters
// getTaxRequest.CustomerUsageType = "G";
// getTaxRequest.ExemptionNo = "12345";
// getTaxRequest.Discount = new BigDecimal(50);
// getTaxRequest.TaxOverride = new TaxOverrideDef();
// getTaxRequest.TaxOverride.TaxOverrideType = "TaxDate";
// getTaxRequest.TaxOverride.Reason = "Adjustment for return";
// getTaxRequest.TaxOverride.TaxDate = "2013-07-01";
// getTaxRequest.TaxOverride.TaxAmount = "0";
getTaxRequest.PurchaseOrderNo="PO123456";
getTaxRequest.ReferenceCode="ref123456";
getTaxRequest.PosLaneCode="09";
getTaxRequest.CurrencyCode="USD";
// Address Data
Address address1 = new Address();
address1.AddressCode = "01";
address1.Line1 = "45 Fremont Street";
address1.City = "San Francisco";
address1.Region = "CA";
Address address2 = new Address();
address2.AddressCode = "02";
address2.Line1 = "118 N Clark St";
address2.Line2 = "Suite 100";
address2.Line3 = "ATTN Accounts Payable";
address2.City = "Chicago";
address2.Region = "IL";
address2.Country = "US";
address2.PostalCode = "60602";
Address address3 = new Address();
address3.AddressCode = "03";
address3.Latitude = new BigDecimal(47.627935);
address3.Longitude = new BigDecimal(-122.51702);
Address[] addresses = { address1, address2, address3 };
getTaxRequest.Addresses = addresses;
// Line Data
Line line1 = new Line();
line1.LineNo = "01";
line1.ItemCode = "N543";
line1.Qty = new BigDecimal(1);
line1.Amount = new BigDecimal(10);
line1.OriginCode = "01";
line1.DestinationCode = "02";
line1.Description = "Red Size 7 Widget";
line1.TaxCode = "NT";
// Situational Request Parameters
// line1.CustomerUsageType = "L";
// line1.Discounted = true;
// line1.TaxIncluded = true;
// line1.TaxOverride = new TaxOverrideDef();
// line1.TaxOverride.TaxOverrideType = "TaxDate";
// line1.TaxOverride.Reason = "Adjustment for return";
// line1.TaxOverride.TaxDate="2013-07-01";
// line1.TaxOverride.TaxAmount = "0";
line1.Ref1 = "ref123";
line1.Ref2 = "ref456";
Line line2 = new Line();
line2.LineNo = "02";
line2.ItemCode = "T345";
line2.Qty = new BigDecimal(3);
line2.Amount = new BigDecimal(150);
line2.OriginCode = "01";
line2.DestinationCode = "03";
line2.Description = "Size 10 Green Running Shoe";
line2.TaxCode = "PC030147";
Line line3 = new Line();
line3.LineNo = "02-FR";
line3.ItemCode = "FREIGHT";
line3.Qty = new BigDecimal(1);
line3.Amount = new BigDecimal(15);
line3.OriginCode = "01";
line3.DestinationCode = "03";
line3.Description = "Shipping Charge";
line3.TaxCode = "FR";
Line[] lines = { line1, line2, line3 };
getTaxRequest.Lines = lines;
//Create URL
String taxget = baseURL+"/1.0/tax/get";
URL url;
HttpURLConnection conn;
//Connect to URL with authorization header, request content.
url = new URL(taxget);
conn = (HttpURLConnection)url.openConnection();
conn.setRequestMethod("POST");
conn.setDoOutput(true);
conn.setDoInput(true);
conn.setUseCaches(false);
conn.setAllowUserInteraction(false);
//Create auth content
String encoded = "Basic " + new String(Base64.encodeBase64((accountNumber + ":" + licenseKey).getBytes())); 
//Add authorization header
conn.setRequestProperty ("Authorization", encoded); 
conn.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");
ObjectMapper mapper = new ObjectMapper();
mapper.setSerializationInclusion(Include.NON_NULL);
//Tells the serializer to only include those parameters that are not null
String content = mapper.writeValueAsString(getTaxRequest);
conn.setRequestProperty("Content-Length", Integer.toString(content.length()));
DataOutputStream wr=new DataOutputStream(conn.getOutputStream());
wr.writeBytes (content);
wr.flush ();
wr.close ();
conn.disconnect();
GetTaxResult res = mapper.readValue(conn.getErrorStream(), GetTaxResult.class);
```

```php
<?php
$getTaxRequest = new GetTaxRequest();
// Document Level Elements
$getTaxRequest->setCustomerCode("ABC4335");
$getTaxRequest->setDocDate("2014-01-01");
$getTaxRequest->setCompanyCode("APITrialCompany");
$getTaxRequest->setClient("AvaTaxSample");
$getTaxRequest->setDocCode("INV001");
$getTaxRequest->setDetailLevel(DetailLevel::$Tax);
$getTaxRequest->setCommit(FALSE);
$getTaxRequest->setDocType(DocumentType::$SalesInvoice);
// $getTaxRequest->setCustomerUsageType("G");
// $getTaxRequest->setExemptionNo("12345");
// $getTaxRequest->setDiscount(50);
// $taxOverride = new TaxOverride();
// $taxOverride.TaxOverrideType("TaxDate");
// $taxOverride.Reason("Adjustment for return");
// $taxOverride.TaxDate("2013-07-01");
// $taxOverride.TaxAmount("0");
// $getTaxRequest->setTaxOverride($taxOverride);
$getTaxRequest->setPurchaseOrderNo("PO123456");
$getTaxRequest->setReferenceCode("ref123456");
$getTaxRequest->setPosLaneCode("09");
$getTaxRequest->setCurrencyCode("USD");
// Address Data
$addresses = array();
$address1 = new Address();
$address1->setAddressCode("01");
$address1->setLine1("45 Fremont Street");
$address1->setCity("San Francisco");
$address1->setRegion("CA");
$addresses[] = $address1;
$address2 = new Address();
$address2->setAddressCode("02");
$address2->setLine1("118 N Clark St");
$address2->setLine2("Suite 100");
$address2->setLine3("ATTN Accounts Payable");
$address2->setCity("Chicago");
$address2->setRegion("IL");
$address2->setCountry("US");
$address2->setPostalCode("60602");
$addresses[] = $address2;
$address3 = new Address();
$address3->setAddressCode("03");
$address3->setLatitude(47.627935);
$address3->setLongitude(-122.51702);
$addresses[] = $address3;
$getTaxRequest->setAddresses($addresses);
// Line Data
$lines = array();
$line1 = new Line();
$line1->setLineNo("01");
$line1->setItemCode("N543");
$line1->setQty(1);
$line1->setAmount(10);
$line1->setOriginCode("01");
$line1->setDestinationCode("02");
$line1->setDescription("Red Size 7 Widget");
$line1->setTaxCode("NT");
// $line1->setCustomerUsageType("L");
// $line1->setDiscounted(TRUE);
// $line1->setTaxIncluded(TRUE);
// $lineTaxOverride = new TaxOverride();
// $lineTaxOverride.TaxOverrideType("TaxDate");
// $lineTaxOverride.Reason("Adjustment for return");
// $lineTaxOverride.TaxDate("2013-07-01");
// $lineTaxOverride.TaxAmount("0");
// $line1->setTaxOverride($lineTaxOverride);
$line1->setRef1("ref123");
$line1->setRef2("ref456");
$lines[] = $line1;
$line2 = new Line();
$line2->setLineNo("02");
$line2->setItemCode("T345");
$line2->setQty(3);
$line2->setAmount(150);
$line2->setOriginCode("01");
$line2->setDestinationCode("03");
$line2->setDescription("Size 10 Green Running Shoe");
$line2->setTaxCode("PC030147");
$lines[] = $line2;
$line3 = new Line();
$line3->setLineNo("02-FR");
$line3->setItemCode("FREIGHT");
$line3->setQty(1);
$line3->setAmount(15);
$line3->setOriginCode("01");
$line3->setDestinationCode("03");
$line3->setDescription("Shipping Charge");
$line3->setTaxCode("FR");
$lines[] = $line3;
$getTaxRequest->setLines($lines);
$url = $serviceURL."/1.0/tax/get";
$curl = curl_init($url);
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);
curl_setopt($curl, CURLOPT_USERPWD, $accountNumber.":".$licenseKey);
curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
curl_setopt($curl, CURLOPT_POST, true);
curl_setopt($curl, CURLOPT_POSTFIELDS, json_encode($getTaxRequest)); 
$curl_response = curl_exec($curl);
curl_close($curl);
GetTaxResult::parseResult($curl_response);
?>
```

```csharp
GetTaxRequest getTaxRequest = new GetTaxRequest();
// Document Level Elements
getTaxRequest.CustomerCode = "ABC4335";
getTaxRequest.DocDate = "2014-01-01";
getTaxRequest.CompanyCode = "APITrialCompany";
getTaxRequest.Client = "AvaTaxSample";
getTaxRequest.DocCode = "INV001";
getTaxRequest.DetailLevel = DetailLevel.Tax;
getTaxRequest.Commit = false;
getTaxRequest.DocType = DocType.SalesInvoice;
// Situational Request Parameters
// getTaxRequest.CustomerUsageType = "G";
// getTaxRequest.ExemptionNo = "12345";
// getTaxRequest.Discount = 50;
// getTaxRequest.TaxOverride = new TaxOverrideDef();
// getTaxRequest.TaxOverride.TaxOverrideType = "TaxDate";
// getTaxRequest.TaxOverride.Reason = "Adjustment for return";
// getTaxRequest.TaxOverride.TaxDate = "2013-07-01";
// getTaxRequest.TaxOverride.TaxAmount = "0";
getTaxRequest.PurchaseOrderNo = "PO123456";
getTaxRequest.ReferenceCode = "ref123456";
getTaxRequest.PosLaneCode = "09";
getTaxRequest.CurrencyCode = "USD";
// Address Data
Address address1 = new Address();
address1.AddressCode = "01";
address1.Line1 = "45 Fremont Street";
address1.City = "San Francisco";
address1.Region = "CA";
Address address2 = new Address();
address2.AddressCode = "02";
address2.Line1 = "118 N Clark St";
address2.Line2 = "Suite 100";
address2.Line3 = "ATTN Accounts Payable";
address2.City = "Chicago";
address2.Region = "IL";
address2.Country = "US";
address2.PostalCode = "60602";
Address address3 = new Address();
address3.AddressCode = "03";
address3.Latitude = (decimal)47.627935;
address3.Longitude = (decimal)-122.51702;
Address[] addresses = { address1, address2, address3 };
getTaxRequest.Addresses = addresses;
// Line Data
Line line1 = new Line();
line1.LineNo = "01";
line1.ItemCode = "N543";
line1.Qty = 1;
line1.Amount = 10;
line1.OriginCode = "01";
line1.DestinationCode = "02";
line1.Description = "Red Size 7 Widget";
line1.TaxCode = "NT";
// Situational Request Parameters
// line1.CustomerUsageType = "L";
// line1.Discounted = true;
// line1.TaxIncluded = true;
// line1.TaxOverride = new TaxOverrideDef();
// line1.TaxOverride.TaxOverrideType = "TaxDate";
// line1.TaxOverride.Reason = "Adjustment for return";
// line1.TaxOverride.TaxDate = "2013-07-01";
// line1.TaxOverride.TaxAmount = "0";
line1.Ref1 = "ref123";
line1.Ref2 = "ref456";
Line line2 = new Line();
line2.LineNo = "02";
line2.ItemCode = "T345";
line2.Qty = 3;
line2.Amount = 150;
line2.OriginCode = "01";
line2.DestinationCode = "03";
line2.Description = "Size 10 Green Running Shoe";
line2.TaxCode = "PC030147";
Line line3 = new Line();
line3.LineNo = "02-FR";
line3.ItemCode = "FREIGHT";
line3.Qty = 1;
line3.Amount = 15;
line3.OriginCode = "01";
line3.DestinationCode = "03";
line3.Description = "Shipping Charge";
line3.TaxCode = "FR";
Line[] lines = { line1, line2, line3 };
getTaxRequest.Lines = lines;
//Convert the request to XML
XmlSerializerNamespaces namesp = new XmlSerializerNamespaces();
namesp.Add("", "");
XmlWriterSettings settings = new XmlWriterSettings();
settings.OmitXmlDeclaration = true;
XmlSerializer x = new XmlSerializer(getTaxRequest.GetType());
StringBuilder sb = new StringBuilder();
x.Serialize(XmlTextWriter.Create(sb, settings), getTaxRequest, namesp);
XmlDocument doc = new XmlDocument();
doc.LoadXml(sb.ToString());
//Call the service
Uri address = new Uri(serviceURL + "tax/get");
HttpWebRequest request = WebRequest.Create(address) as HttpWebRequest;
//Add Authorization header
request.Headers.Add(HttpRequestHeader.Authorization, 
	"Basic " + Convert.ToBase64String(ASCIIEncoding.ASCII.GetBytes(accountNumber + ":" + licenseKey)));
request.Method = "POST";
request.ContentType = "text/xml";
request.ContentLength = sb.Length;
Stream newStream = request.GetRequestStream();
newStream.Write(ASCIIEncoding.ASCII.GetBytes(sb.ToString()), 0, sb.Length);
WebResponse response = request.GetResponse();
```

> The above command returns JSON structured like this:

```json
{
"ResultCode": "Success",
"DocCode": "INV001",
"DocDate": "2014-01-01",
"Timestamp": "2014-03-20T00:19:55.887",
"TotalAmount": "175",
"TotalDiscount": "10",
"TotalExemption": "165",
"TotalTaxable": "0",
"TotalTax": "0",
"TotalTaxCalculated": "0",
"TaxLines": [
{
"LineNo": "01",
"TaxCode": "NT",
"Taxability": "false",
"BoundaryLevel": "Address",
"Exemption": "0",
"Discount": "10",
"Taxable": "0",
"Rate": "0.092500",
"Tax": "0",
"TaxCalculated": "0",
"TaxDetails": [
{
"Country": "US",
"Region": "IL",
"JurisType": "State",
"Taxable": "0",
"Rate": "0.062500",
"Tax": "0",
"JurisName": "ILLINOIS",
"TaxName": "IL STATE TAX"
},
{
"Country": "US",
"Region": "IL",
"JurisType": "County",
"Taxable": "0",
"Rate": "0.007500",
"Tax": "0",
"JurisName": "COOK",
"TaxName": "IL COUNTY TAX"
},
{
"Country": "US",
"Region": "IL",
"JurisType": "City",
"Taxable": "0",
"Rate": "0.012500",
"Tax": "0",
"JurisName": "CHICAGO",
"TaxName": "IL CITY TAX"
},
{
"Country": "US",
"Region": "IL",
"JurisType": "Special",
"Taxable": "0",
"Rate": "0.010000",
"Tax": "0",
"JurisName": "REGIONAL TRANSPORT. 
	AUTHORITY (RTA)",
"TaxName": "IL SPECIAL TAX"
}
]
},
{
"LineNo": "02",
"TaxCode": "PC030147",
"Taxability": "true",
"BoundaryLevel": "Zip5",
"Exemption": "150",
"Discount": "0",
"Taxable": "0",
"Rate": "0.086000",
"Tax": "0",
"TaxCalculated": "0",
"TaxDetails": [
{
"Country": "US",
"Region": "WA",
"JurisType": "State",
"Taxable": "0",
"Rate": "0.065000",
"Tax": "0",
"JurisName": "WASHINGTON",
"TaxName": "WA STATE TAX"
},
{
"Country": "US",
"Region": "WA",
"JurisType": "City",
"Taxable": "0",
"Rate": "0.021000",
"Tax": "0",
"JurisName": "BAINBRIDGE ISLAND",
"TaxName": "WA CITY TAX"}
]
},
{
"LineNo": "02-FR",
"TaxCode": "FR",
"Taxability": "true",
"BoundaryLevel": "Zip5",
"Exemption": "15",
"Discount": "0",
"Taxable": "0",
"Rate": "0.086000",
"Tax": "0",
"TaxCalculated": "0",
"TaxDetails": [
{
"Country": "US",
"Region": "WA",
"JurisType": "State",
"Taxable": "0",
"Rate": "0.065000",
"Tax": "0",
"JurisName": "WASHINGTON",
"TaxName": "WA STATE TAX"
},
{
"Country": "US",
"Region": "WA",
"JurisType": "City",
"Taxable": "0",
"Rate": "0.021000",
"Tax": "0",
"JurisName": "BAINBRIDGE ISLAND",
"TaxName": "WA CITY TAX"
}
]
}
],
"TaxAddresses": [
{
"Address": "45 Fremont St",
"AddressCode": "01",
"City": "San Francisco",
"Country": "US",
"PostalCode": "94105-2204",
"Region": "CA",
"TaxRegionId": "2113460",
"Latitude": "37.791119",
"Longitude": "-122.397366"
},
{
"Address": "45 Fremont St",
"AddressCode": "01",
"City": "San Francisco",
"Country": "US",
"PostalCode": "94105-2204",
"Region": "CA",
"TaxRegionId": "2113460",
"Latitude": "37.791119",
"Longitude": "-122.397366"
},
{
"Address": "45 Fremont St",
"AddressCode": "01",
"City": "San Francisco",
"Country": "US",
"PostalCode": "94105-2204",
"Region": "CA",
"TaxRegionId": "2113460",
"JurisCode": "0607500000",
"Latitude": "37.791119",
"Longitude": "-122.397366"
},
{
"Address": "118 N Clark St Ste 100",
"AddressCode": "02",
"City": "Chicago",
"Country": "US",
"PostalCode": "60602-1304",
"Region": "IL",
"TaxRegionId": "2062953",
"JurisCode": "1703114000",
"Latitude": "41.884132",
"Longitude": "-87.631048"
},
{
"AddressCode": "03",
"Country": "US",
"Region": "WA",
"TaxRegionId": "2109716",
"Latitude": "47.627935",
"Longitude": "-122.51702"
},
{
"AddressCode": "03",
"Country": "US",
"Region": "WA",
"TaxRegionId": "2109716",
"JurisCode": "5303503736",
"Latitude": "47.627935",
"Longitude": "-122.51702"
}
],
"TaxDate": "2013-07-01"
}
```

Calculates taxes on a document such as a sales order, sales invoice, purchase order, purchase invoice, or credit memo.

### URL and Method

URL: /1.0/tax/get POST

For development, 
	https://development.avalara.net
	/1.0/tax/get
    
For production, 
	https://avatax.avalara.net
	/1.0/tax/get
    
Note that xml-encoded requests should use /1.0/tax/get.xml

### Headers

**Authorization:** header, *required*

In the format "Basic[ account number]:[license key]" encoded to <a href="http://en.wikipedia.org/wiki/Base64">Base64</a>, as per <a href="http://en.wikipedia.org/wiki/Basic_access_authentication">basic access authentication</a>.

Sample: Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=

**Content Type:** header, *required*

Standard content type header, indicating the content type of the request content.

**Content Length:** header, *required*

Standard content length header, indicating the size of the request content.

### GetTaxRequest

Input for GetTax describing the document on which tax should be calculated.

#### Properties 

**BusinessIdentificationNo:** string [25], *optional, unless the user needs VAT calculated*

The buyer's VAT id. Using this value will force VAT rules to be considered for the transaction. This may be set on the document or the line.

**Commit:** bool, *optional*

Default is false. Setting this value to true will prevent further document status changes, except voiding with CancelTax.

**Client:** string [50], *optional*

An identifier of software client generating the API call.

**CompanyCode:** string [25], *optional*

The code that identifies the company in the AvaTax account in which the document should be posted. This code is declared during the company setup in the <a href="https://admin-development.avalara.net/" target="_blank">AvaTax Admin Console</a>. If no value is passed, the document will be assigned to the default company.

**CustomerCode:** string [50], *required*

The client application customer reference code. This is required since it is the key to the Exemption Certificate Management Service in the Admin Console.

**CurrencyCode:** string [3], *optional*

3 character ISO 4217 compliant currency code.

**CustomerUsageType:** string [25], *optional*

The client application customer or usage type.

The standard values for the CustomerUsageType are:

 - A - Federal Government
 - B - State/Local Govt.
 - C - Tribal Government
 - D - Foreign Diplomat
 - E - Charitable Organization
 - F - Religious/Education
 - G - Resale
 - H - Agricultural Production
 - I - Industrial Prod/Mfg.
 - J - Direct Pay Permit
 - K - Direct Mail
 - L - Other
 - N - Local Government
 - P - Commercial Aquaculture (Canada)
 - Q - Commercial Fishery (Canada)
 - R - Non-resident (Canada)
 - MED1 - US MDET with exempt sales tax
 - MED2 - US MDET with taxable sales tax

**DetailLevel:** DetailLevel, *optional*

Specifies the level of detail to return.

 - Summary - summarizes document and jurisdiction detail with no line breakout
 - Document - only document detail
 - Line - document and line detail
 - Tax - document, line and jurisdiction detail
 
 **Discount:** decimal, *optional*

The discount amount to apply to the document. This may be used along with the line attribute Discounted in order to distribute a set discount amount proportionally across the applicable document lines.

**DocCode:** string [50], *optional*

While this is an optional field, serious consideration should be given to using it. If no value is sent, AvaTax assigns a GUID value to keep the document unique. This can make reconciliation a challenge.

**DocDate:** DateTime, *required*

The date on the invoice, purchase order, etc. Format YYYY-MM-DD.

**DocType:** DocumentType

The document type specifies the category of the document and affects how the document is treated after a tax calculation.

 - SalesOrder: This is a temporary document type and is not saved in tax history. GetTaxResult will return with a DocStatus of Temporary.
 - SalesInvoice: The document is a permanent invoice; document and tax calculation results are saved in the tax history. GetTaxResult will return with a DocStatus of Saved.
 - PurchaseOrder: This is a temporary document type and is not saved in tax history. GetTaxResult will return with a DocStatus of Temporary.
 - PurchaseInvoice : The document is a permanent invoice; document and tax calculation results are saved in the tax history. GetTaxResult will return with a DocStatus of Saved.
 - ReturnOrder: This is a temporary document type and is not saved in tax history. GetTaxResult will return with a DocStatus of Temporary.
 - ReturnInvoice: The document is a permanent sales return invoice; document and tax calculation results are saved in the tax history GetTaxResult will return with a DocStatus of Saved.


**ExemptionNo:** string [25], *optional*

Any string value will cause the sale to be exempt. This should only be used if your finance team is manually verifying and tracking exemption certificates.

**PosLaneCode:** string [50], *optional*

Permits a Point of Sale application to record the unique code / ID / number associated with the terminal processing a sale.

**PurchaseOrderNo:** string [50], *optional*

Your customer's purchase order number.

**ReferenceCode:** string [50], *optional*

For returns, refers to the DocCode of the original invoice.

**TaxOverride:** TaxOverride, *optional*

TaxOverride for the document - can be used to manually override components of the tax calculation. See TaxOverride for more information.

**Addresses:** Address, at least one required

Document address array. Should represent all origin and destination addresses which will be associated with individual lines.

**Lines:** Line, at least one required

Document line array. There is a limit of 1000 lines per document.

#### TaxOverride

Nested object describing any tax override applied to the document. TaxOverride only needs to be included when there is need to override our tax calculation. Most commonly on ReturnInvoices. For each document, this may be done at either the document or line level, but not both on the same document. 

This will probably be handled within some conditional statement like:

 - if(getTaxRequest.DocType == DocumentType.ReturnInvoice)
 - do TaxOverride


**Reason:** string [255], *required*

This provides the reason for a tax override for audit purposes. Typical reasons include: "Return", "Layaway", "Imported".

**TaxOverrideType:** string, *required*

 - None: Default

 - TaxAmount: The TaxAmount overrides the total tax for the document. This is used for imported documents, returns, and layaways where the tax has already been calculated either by AvaTax or another means.


 - Exemption: Exemption certificates are overridden making the document taxable. This may be used for situations where a normally exempt entity needs to be treated as not exempt.


 - TaxDate: The TaxDate overrides the DocDate as the effective date used for tax calculation. This may effect rates, rules and other factors.

**TaxDate:** string, *must be valid date, required if TaxOverrideType is TaxDate*

The override tax date to use. This is used when the tax has been previously calculated as in the case of a layaway, return or other reason indicated by the Reason element. If the date is not overridden, then it should be set to the same as the DocDate.

**TaxAmount:** string, *must be numeric, required if TaxOverrideType is TaxAmount*

The overriding amount of tax to apply. This is distributed across all taxable rows.

#### Line
Input property of the GetTaxRequest describing item lines.

**LineNo:** string [50], *required*

Line item identifier. LineId uniquely identifies the line item row.

**DestinationCode:** string, *required*

Destination (ship-to) address code.DestinationCode references an address from the Addresses collection.

**OriginCode:** string, *required*

Origination (ship-from) address code. OriginCode references an address from the Addresses collection.

**ItemCode:** string [50], *optional*

Your item identifier, SKU, or UPC. Strongly recommended. 

**TaxCode:** string [25], *optional*

Product taxability code of the line item. Can be an AvaTax system tax code, or a custom-defined tax code.

**CustomerUsageType:** string [25], *optional*

The client application customer or usage type. CustomerUsageType determines the exempt status of the transaction based on the exemption tax rules for the jurisdictions involved. Can also be referred to as Entity/Use Code.

**Description:** string [255], *optional*

Item description. Required for customers using our filing service.

**Qty:** decimal, *required*

Item quantity. The tax engine does NOT use this as a multiplier with price to get the Amount.

**Amount:** decimal, *required*

Total amount of item (extended amount, qty * unit price)

**Discounted:** bool, *optional*

Should be set to true if the document level discount is applied to this line item. Defaults to false.

**TaxIncluded:** bool, *optional*

Should be set to true if the tax is already included, and sale amount and tax should be back-calculated from the provided Line.Amount. Defaults to false.

**Ref1:** string [250], *optional*

Value stored with SalesInvoice DocType that is submitter dependent.

**Ref2:** string [250], *optional*

Value stored with SalesInvoice DocType that is submitter dependent.

**TaxOverride** TaxOverride, *optional*

Same as document-level TaxOverride. Use this if you only need to override individual lines.


#### Address
Input property of GetTaxRequest representing addresses needed for tax calculations.

**AddressCode:** string, *required*

Reference code uniquely identifying this address instance.

**Line1:** string [50], *required*

Address line 1, required if Latitude and Longitude are not provided.

**Line2:** string [50], *optional*

Address line 2

**Line3:** string [50], *optional*

Address line 3

**City:** string [50], *optional*

City name, required unless PostalCode is specified and/or Latitude and Longitude are provided.

**Region:** string [3], *optional*

State, province, or region name. Required unless City is specified and/or Latitude and Longitude are provided.

**Country:** string [2], *optional*

Country code. If not provided, will default to "US".

**PostalCode:** string [11], *optional unless City and Region are not specified*

Postal or ZIP code, Required unless City and Region are specified, and/or Latitude and Longitude are provided.

**Latitude:** decimal, *optional*

Geographic latitude. If Latitude is defined, it is expected that the longitude field will also be provided. Failure to do so will result in operation error.

**Longitude:** decimal, *optional*

Geographic longitude. If Longitude is defined, it is expected that the latitude field will also be provided. Fail to do so will result in operation error.

**TaxRegionId:** int, *optional*

AvaTax tax region identifier. If a non-zero value is entered into TaxRegionId, other fields will be ignored.


### GetTaxResult

#### Properties
Document-level tax calculation information.

**DocCode:** string [50]

The document code, if not supplied in the request the returned value is a GUID.

**DocDate:** date

Date of invoice, sales order, purchase order, etc.

**TimeStamp:** DateTime

Server timestamp of request.

**TotalAmount:** decimal

Sum of all line Amount values.

**TotalDiscount:** decimal

Sum of all TaxLine discount amounts.

**TotalExemption:** decimal

Total exemption amount.

**TotalTaxable:** decimal

Total taxable amount.

**TotalTax:** decimal

Sum of all TaxLine tax amounts.

**TotalTaxCalculated:** decimal

TotalTaxCalculated indicates the total tax calculated by AvaTax. This is usually the same as the TotalTax, except when a tax override amount is specified. 
This is for informational purposes. The TotalTax will still be used for reporting.

**TaxDate:** date

Date used to assess tax rates and jurisdictions.

**TaxLines:** TaxLine[]

Tax calculation details for each item line (returned for detail levels Line and Tax).

**TaxSummary:** TaxDetail[]

Summary of the jurisdiction details for all item lines (returned for detail levels Summary and Line).

**TaxDetails:** TaxDetail[]

Tax calculation details for each jurisdiction per line (returned for detail level Tax).

**TaxAddresses:** TaxAddress[]

Addresses used in tax calculations (returned for detail levels Line and Tax).

**ResultCode:** SeverityLevel

Severity as per <a title="Common Response Format" href="/api-docs/soap/shared-formats-and-methods#CommonResponseFormat">Common Response Format</a>

**Messages:** Message[]

As per <a title="Common Response Format" href="/api-docs/soap/shared-formats-and-methods#CommonResponseFormat">Common Response Format</a>

#### TaxLine

#### TaxDetail
#### TaxAddress