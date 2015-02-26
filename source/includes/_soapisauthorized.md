## IsAuthorized

```shell
curl -X POST --header "Content-Type: text/xml" \
--header "SOAPAction: \"http://avatax.avalara.com/services/IsAuthorized\"" \
--data-binary @isAuthorizedRequest.xml https://development.avalara.net/tax/taxsvc.asmx

<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://avatax.avalara.com/services">
<SOAP-ENV:Header>
<wsse:Security xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" SOAP-ENV:mustUnderstand="1">
<wsse:UsernameToken>
<wsse:Username>1234567890</wsse:Username>
<wsse:Password Type="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-username-token-profile-1.0#PasswordText">A1B2C3D4E5F6G7H8</wsse:Password>
</wsse:UsernameToken>
</wsse:Security>
<Profile xmlns="http://avatax.avalara.com/services" SOAP-ENV:actor="http://schemas.xmlsoap.org/soap/actor/next" SOAP-ENV:mustUnderstand="0">
<Client>AvaTaxSample</Client>
<Adapter>customAdapter</Adapter>
<Name>Development</Name>
</Profile>
</SOAP-ENV:Header>
<SOAP-ENV:Body>
<ns1:IsAuthorized>
<ns1:Operations>Ping, IsAuthorized, GetTax,PostTax, GetTaxHistory, CommitTax,CancelTax, AdjustTax</ns1:Operations>
</ns1:IsAuthorized>
</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

```csharp
TaxSvc taxSvc = new TaxSvc();

taxSvc.Configuration.Security.Account ="1234567890";
taxSvc.Configuration.Security.License = "A1B2C3D4E5F6G7H8";
taxSvc.Configuration.Url = "https://development.avalara.net";
taxSvc.Configuration.ViaUrl = "https://development.avalara.net";
taxSvc.Profile.Client = "AvaTaxSample";
taxSvc.Profile.Name = "Development";

IsAuthorizedResult isAuthorizedResult = taxSvc.IsAuthorized("Ping, IsAuthorized, GetTax,PostTax, GetTaxHistory, CommitTax,CancelTax, AdjustTax");
```

```php
<?php
require('../../AvaTax4PHP/AvaTax.php');

new ATConfig('Development', array(
    'url' => 'https://development.avalara.net',
    'account' => '1234567890',
    'license' => 'A1B2C3D4E5F6G7H8')
);

$taxSvc = new TaxServiceSoap('Development');

$isAuthorizedResult = $taxSvc->isAuthorized("Ping,IsAuthorized,GetTax,PostTax,GetTaxHistory,CommitTax,CancelTax,AdjustTax");	
?>
```

```java
TaxSvcLocator taxSvcLocator = new TaxSvcLocator();
String url = "https://development.avalara.net";
TaxSvcSoap taxSvc = taxSvcLocator.getTaxSvcSoap(new URL(url));
Profile profile = new Profile();
profile.setClient("AvaTaxSample");
taxSvc.setProfile(profile);
Security security = new Security();
security.setAccount("1234567890");
security.setLicense("A1B2C3D4E5F6G7H8");
taxSvc.setSecurity(security);

IsAuthorizedResult isAuthorizedResult = taxSvc.isAuthorized("Ping, IsAuthorized,GetTax, PostTax, GetTaxHistory, CommitTax, CancelTax, AdjustTax");

```

> The above command returns XML structured like this:

```xml
<IsAuthorizedResult>
<TransactionId>0</TransactionId>
<ResultCode>Success</ResultCode>
<Expires>2024-01-01</Expires>
<Operations>Ping,IsAuthorized,GetTax,PostTax,GetTaxHistory,CommitTax,CancelTax,AdjustTax</Operations>
</IsAuthorizedResult>
```

IsAuthorized allows you to send a user's credentials along with a list of AvaTax methods to check which methods that user is authorized to use. You can also get your account expiration date via this method. There is technically no request to build - just a string to pass in the method call when you instantiate the result object.

### IsAuthorized Result

Result data returned from IsAuthorized.

#### Properties

**Expires:** DateTime

The date and time at which your AvaTax account will expire.

**Operations:** string [255]

The operations that the current user is authorized to use. Determined from the list provided in the IsAuthorized call.

**Messages:** Message[]

If ResultCode is Success, Messages is null. Otherwise, it describes any warnings, errors, or exceptions encountered while processing the request. Properties defined in <a title="Common Response Format" href="/api-docs/soap/shared-formats-and-methods#CommonResponseFormat">Common Response Format</a>

**ResultCode:** SeverityLevel

Indicates success or failure. One of:

* Success
* Warning
* Error
* Exception

**TransactionId:** bigint as string

The unique transaction ID assigned by AvaTax to this request/response set. This value need only be retained for troubleshooting.
