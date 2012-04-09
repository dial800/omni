![Documentation](http://docs.dial800.com/images/roundtrip.png)

We know. You have two days to integrate with us. Don't worry, it's easy. We're here to help.

## How to submit data

* [if I am using PHP](#using-php)?
* [or C Sharp?](#using-c-sharp)
* [or Python?](#using-python)
* [or Ruby?](#using-ruby)

### Using PHP

```php
<?php

# 1. Generate Payload

$request = new HTTP_Request2('http://routing.dial800.com/roundtrip');
$request->setMethod(HTTP_Request2::METHOD_POST)
    ->setAuth('user','password', HTTP_Request2::AUTH_BASIC)
    ->setHeader('Content-type: application/mercury.shortform')
    ->setBody(
        "<?xml version=\"1.0\" encoding=\"utf-8\"?>\r\n" .
        "<Call xmlns=\"http://www.dial800.com/roundtrip/2011-07-15\r\n" .
        "      xmlns:msf=\"http://www.mercurymedia.com/shortform/2011-07-15\">" .
        "   <ANI>tel:3105555555</ANI>\r\n" .
        "   <Target>tel:3109999999</Target>\r\n" . 
        "   <CallStart>2011-07-15T01:02:03-08:00</CallStart>\r\n" .
        "   <msf:ProductCode>PHD4</msf:ProductCode>\r\n" .
        "   <msf:MediaSource>KNBC</msf:MediaSource>\r\n" .
        "   <msf:CallerFirstName>John</msf:CallerFirstName>\r\n" .
        "   <msf:CallerMiddleName>Jerry</msf:CallerMiddleName>\r\n" .
        "   <msf:CallerLastName>Smith</msf:CallerLastName>\r\n" .
        "   <msf:CallerCity>Los Angeles</msf:CallerCity>\r\n" .
        "   <msf:CallerState>CA</msf:CallerState>\r\n" .
        "   <msf:CallerZipCode>90210</msf:CallerZipCode>\r\n" .
        "   <msf:OtherFirstName />\r\n" .
        "   <msf:OtherMiddleInitial />\r\n" .
        "   <msf:OtherLastName />\r\n" .
        "   <msf:OtherCity />\r\n" .
        "   <msf:OtherState />\r\n" .
        "   <msf:OtherZip />\r\n" .
        "   <msf:OtherAreaCode />\r\n" .
        "   <msf:OtherPhone />\r\n" .
        "   <msf:ScriptQ1-1 />\r\n" .
        "   <msf:Gender />\r\n" .
        "   <msf:ScriptQ1-3 />\r\n" .
        "   <msf:ScriptQ1-4 />\r\n" .
        "   <msf:InqReason />\r\n" .
        "   <msf:CallCode>11</msf:CallCode>\r\n" .
        "   <msf:ScriptQ10-2 />\r\n" .
        "   <msf:ScriptQ10-3 />\r\n" .
        "   <msf:ScriptQ10-4 />\r\n" .
        "   <msf:OrderAmount>89.97</msf:OrderAmount>\r\n" .
        "   <msf:ScriptQ30-1 />\r\n" .
        "   <msf:ScriptQ30-2 />\r\n" .
        "   <msf:SequenceID />\r\n" .
        "   <msf:DOB />\r\n" .
        "   <msf:OtherDOB />\r\n" .
        "   <msf:ScriptDate3 />\r\n" .
        "   <msf:Keycode />\r\n" .
        "   <msf:HitScreenDisp />\r\n" .
        "   <msf:MainOfferQty>1</msf:MainOfferQty>\r\n" .
        "   <msf:Upsell1 />\r\n" .
        "   <msf:Upsell2 />\r\n" .
        "   <msf:Upsell3 />\r\n" .
        "   <msf:Upsell4 />\r\n" .
        "   <msf:Upsell5 />\r\n" .
        "   <msf:Upsell6 />\r\n" .
        "   <msf:Upsell7 />\r\n" .
        "   <msf:Upsell8 />\r\n" .
        "   <msf:Upsell9 />\r\n" .
        "   <msf:Upsell10 />\r\n" .
        "   <msf:Upsell11 />\r\n" .
        "   <msf:Upsell12 />\r\n" .
        "   <msf:Upsell13 />\r\n" .
        "   <msf:Upsell14>0</msf:Upsell14>\r\n" .
        "</Call>"
    );

# 2. Submit

echo $request->send()->getBody();
?>
```

### Using C Sharp

```csharp
using System;
using System.IO;
using System.Net;
using System.Text;


namespace Dial800
{
    class Program
    {
        static void Main(string[] args)
        {
            byte[] postDataBytes;
            const string userName    = "user";
            const string password    = "password";
            const string contentType = "application/mercury.shortform";
            const string postMethod  = "POST";
            const string postData    
            = @"<?xml version="1.0" encoding="utf-8" ?>
                <Call xmlns="http://www.dial800.com/roundtrip/2011-07-15"
                      xmlns:msf="http://www.mercurymedia.com/shortform/2011-07-15">      
                    <ANI>tel:3105555555</ANI>
                    <Target>tel:3109999999</Target>
                    <CallStart>2011-07-15T01:02:03-08:00</CallStart>
                    <msf:ProductCode>PHD4</msf:ProductCode>
                    <msf:MediaSource>KNBC</msf:MediaSource>
                    <msf:CallerFirstName>John</msf:CallerFirstName>
                    <msf:CallerMiddleName>Jerry</msf:CallerMiddleName>
                    <msf:CallerLastName>Smith</msf:CallerLastName>
                    <msf:CallerCity>Los Angeles</msf:CallerCity>
                    <msf:CallerState>CA</msf:CallerState>
                    <msf:CallerZipCode>90210</msf:CallerZipCode>
                    <msf:OtherFirstName />
                    <msf:OtherMiddleInitial />
                    <msf:OtherLastName />
                    <msf:OtherCity />
                    <msf:OtherState />
                    <msf:OtherZip />
                    <msf:OtherAreaCode />
                    <msf:OtherPhone />
                    <msf:ScriptQ1-1 />
                    <msf:Gender />
                    <msf:ScriptQ1-3 />
                    <msf:ScriptQ1-4 />
                    <msf:InqReason />
                    <msf:CallCode>11</msf:CallCode>
                    <msf:ScriptQ10-2 />
                    <msf:ScriptQ10-3 />
                    <msf:ScriptQ10-4 />
                    <msf:OrderAmount>89.97</msf:OrderAmount>
                    <msf:ScriptQ30-1 />
                    <msf:ScriptQ30-2 />
                    <msf:SequenceID />
                    <msf:DOB />
                    <msf:OtherDOB />
                    <msf:ScriptDate3 />
                    <msf:Keycode />
                    <msf:HitScreenDisp />
                    <msf:MainOfferQty>1</msf:MainOfferQty>
                    <msf:Upsell1 />
                    <msf:Upsell2 />
                    <msf:Upsell3 />
                    <msf:Upsell4 />
                    <msf:Upsell5 />
                    <msf:Upsell6 />
                    <msf:Upsell7 />
                    <msf:Upsell8 />
                    <msf:Upsell9 />
                    <msf:Upsell10 />
                    <msf:Upsell11 />
                    <msf:Upsell12 />
                    <msf:Upsell13 />
                    <msf:Upsell14>0</msf:Upsell14>
                </Call>";

            const string uri = "http://roundtrip.dial800.com/roundtrip";

            postDataBytes = Encoding.UTF8.GetBytes( postData );

            var urlEndpoint = new Uri(uri);
            var request = WebRequest.Create( urlEndpoint ) as HttpWebRequest;

            request.Credentials   = new NetworkCredential( userName, password );
            request.Method        = postMethod;
            request.ContentType   = contentType;
            request.ContentLength = postDataBytes.Length;

            using(Stream postStream = request.GetRequestStream())
            {
                postStream.Write( postDataBytes, 0, postDataBytes.Length );
            }

            try
            {
                using ( HttpWebResponse response = request.GetResponse() as HttpWebResponse )
                {
                    var reader = new StreamReader( response.GetResponseStream() );
                    Console.WriteLine( reader.ReadToEnd() );
                }
            }
            catch (WebException ex)
            {
                if (ex.Response != null)
                {
                    using (HttpWebResponse errorResponse = (HttpWebResponse)ex.Response)
                    {
                        Console.WriteLine(
                            "The server returned '{0}' with the status code {1} ({2:d}).",
                            errorResponse.StatusDescription, errorResponse.StatusCode,
                            errorResponse.StatusCode);
                    }
                }
            }
            Console.ReadKey();
        }
    }
}
```

### Using Python

```python
from requests.auth import HTTPBasicAuth
payload = '''
<?xml version="1.0" encoding="utf-8" ?>
<Call xmlns="http://www.dial800.com/roundtrip/2011-07-15"
      xmlns:msf="http://www.mercurymedia.com/shortform/2011-07-15">      
    <ANI>tel:3105555555</ANI>
    <Target>tel:3109999999</Target>
    <CallStart>2011-07-15T01:02:03-08:00</CallStart>
    <msf:ProductCode>PHD4</msf:ProductCode>
    <msf:MediaSource>KNBC</msf:MediaSource>
    <msf:CallerFirstName>John</msf:CallerFirstName>
    <msf:CallerMiddleName>Jerry</msf:CallerMiddleName>
    <msf:CallerLastName>Smith</msf:CallerLastName>
    <msf:CallerCity>Los Angeles</msf:CallerCity>
    <msf:CallerState>CA</msf:CallerState>
    <msf:CallerZipCode>90210</msf:CallerZipCode>
    <msf:OtherFirstName />
    <msf:OtherMiddleInitial />
    <msf:OtherLastName />
    <msf:OtherCity />
    <msf:OtherState />
    <msf:OtherZip />
    <msf:OtherAreaCode />
    <msf:OtherPhone />
    <msf:ScriptQ1-1 />
    <msf:Gender />
    <msf:ScriptQ1-3 />
    <msf:ScriptQ1-4 />
    <msf:InqReason />
    <msf:CallCode>11</msf:CallCode>
    <msf:ScriptQ10-2 />
    <msf:ScriptQ10-3 />
    <msf:ScriptQ10-4 />
    <msf:OrderAmount>89.97</msf:OrderAmount>
    <msf:ScriptQ30-1 />
    <msf:ScriptQ30-2 />
    <msf:SequenceID />
    <msf:DOB />
    <msf:OtherDOB />
    <msf:ScriptDate3 />
    <msf:Keycode />
    <msf:HitScreenDisp />
    <msf:MainOfferQty>1</msf:MainOfferQty>
    <msf:Upsell1 />
    <msf:Upsell2 />
    <msf:Upsell3 />
    <msf:Upsell4 />
    <msf:Upsell5 />
    <msf:Upsell6 />
    <msf:Upsell7 />
    <msf:Upsell8 />
    <msf:Upsell9 />
    <msf:Upsell10 />
    <msf:Upsell11 />
    <msf:Upsell12 />
    <msf:Upsell13 />
    <msf:Upsell14>0</msf:Upsell14>
</Call>
'''
r = request.post('http://routing.dial800.com/routing',
                 auth=HTTPBasicAuth('user','password'),
                 headers={'content-type': 'application/mercury.shortform'},
                 data=payload)
```

### Using Ruby

```ruby
require "net/http"
require "uri"

uri = URI.parse("http://routing.dial800.com/routing")

http         = Net::HTTP.new(uri.host, uri.port)
request      = Net::HTTP::Post.new(uri.host,uri.port)
request.body = xml_string
request.basic_auth("user","password")
request.content_type = "application/mercury.shortform"
response     = http.request(request)
```

## Reference

### Authentication

### POST

#### Request

```
POST /calls
Content-Type: application/mercury.shortform
```

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Call xmlns="http://www.dial800.com/roundtrip/2011-07-15"
      xmlns:msf="http://www.mercurymedia.com/shortform/2011-07-15">      
    <ANI>tel:3105555555</ANI>
    <Target>tel:3109999999</Target>
    <CallStart>2011-07-15T01:02:03-08:00</CallStart>
    <msf:ProductCode>PHD4</msf:ProductCode>
    <msf:MediaSource>TV</msf:MediaSource>
    <msf:CallerFirstName>John</msf:CallerFirstName>
    <msf:CallerMiddleName>Jerry</msf:CallerMiddleName>
    <msf:CallerLastName>Smith</msf:CallerLastName>
    <msf:CallerCity>Los Angeles</msf:CallerCity>
    <msf:CallerState>CA</msf:CallerState>
    <msf:CallerZipCode>90210</msf:CallerZipCode>
    <msf:OtherFirstName />
    <msf:OtherMiddleInitial />
    <msf:OtherLastName />
    <msf:OtherCity />
    <msf:OtherState />
    <msf:OtherZip />
    <msf:OtherAreaCode />
    <msf:OtherPhone />
    <msf:ScriptQ1-1 />
    <msf:Gender />
    <msf:ScriptQ1-3 />
    <msf:ScriptQ1-4 />
    <msf:InqReason />
    <msf:CallCode>11</msf:CallCode>
    <msf:ScriptQ10-2 />
    <msf:ScriptQ10-3 />
    <msf:ScriptQ10-4 />
    <msf:OrderAmount>89.97</msf:OrderAmount>
    <msf:ScriptQ30-1 />
    <msf:ScriptQ30-2 />
    <msf:SequenceID />
    <msf:DOB />
    <msf:OtherDOB />
    <msf:ScriptDate3 />
    <msf:Keycode />
    <msf:HitScreenDisp />
    <msf:MainOfferQty>1</msf:MainOfferQty>
    <msf:Upsell1 />
    <msf:Upsell2 />
    <msf:Upsell3 />
    <msf:Upsell4 />
    <msf:Upsell5 />
    <msf:Upsell6 />
    <msf:Upsell7 />
    <msf:Upsell8 />
    <msf:Upsell9 />
    <msf:Upsell10 />
    <msf:Upsell11 />
    <msf:Upsell12 />
    <msf:Upsell13 />
    <msf:Upsell14 />
</Call>
```

#### Response

Call successfully matched.

```xml
200 OK
<ID>XDhshURwv60Q2nRyN4cnGVCmMB1cP</ID>
```

No match for the call.

```
404 Not Found
```

### PUT

```
PUT /calls
Content-Type: application/mercury.shortform
```

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Call xmlns="http://www.dial800.com/roundtrip/2011-07-15"
      xmlns:msf="http://www.mercurymedia.com/shortform/2011-07-15">      
    <ID>12345678990</ID>
    <msf:ProductCode>PHD4</msf:ProductCode>
    <msf:MediaSource>TV</msf:MediaSource>
    <msf:CallerFirstName>John</msf:CallerFirstName>
    <msf:CallerMiddleName>Jerry</msf:CallerMiddleName>
    <msf:CallerLastName>Smith</msf:CallerLastName>
    <msf:CallerCity>Los Angeles</msf:CallerCity>
    <msf:CallerState>CA</msf:CallerState>
    <msf:CallerZipCode>90210</msf:CallerZipCode>
    <msf:OtherFirstName />
    <msf:OtherMiddleInitial />
    <msf:OtherLastName />
    <msf:OtherCity />
    <msf:OtherState />
    <msf:OtherZip />
    <msf:OtherAreaCode />
    <msf:OtherPhone />
    <msf:ScriptQ1-1 />
    <msf:Gender />
    <msf:ScriptQ1-3 />
    <msf:ScriptQ1-4 />
    <msf:InqReason />
    <msf:CallCode>11</msf:CallCode>
    <msf:ScriptQ10-2 />
    <msf:ScriptQ10-3 />
    <msf:ScriptQ10-4 />
    <msf:OrderAmount>89.97</msf:OrderAmount>
    <msf:ScriptQ30-1 />
    <msf:ScriptQ30-2 />
    <msf:SequenceID />
    <msf:DOB />
    <msf:OtherDOB />
    <msf:ScriptDate3 />
    <msf:Keycode />
    <msf:HitScreenDisp />
    <msf:MainOfferQty>1</msf:MainOfferQty>
    <msf:Upsell1 />
    <msf:Upsell2 />
    <msf:Upsell3 />
    <msf:Upsell4 />
    <msf:Upsell5 />
    <msf:Upsell6 />
    <msf:Upsell7 />
    <msf:Upsell8 />
    <msf:Upsell9 />
    <msf:Upsell10 />
    <msf:Upsell11 />
    <msf:Upsell12 />
    <msf:Upsell13 />
    <msf:Upsell14 />
</Call>
```

#### Response

Call successfully matched.

```xml
200 OK
<ID>12345678990</ID>
```

No match for the call.

```
404 Not Found
```

## Glossary
<dl>
    <dt>ID</dt>
    <dd>String value representing the alphanumeric Call ID of the phone call to be matched for the associated Sales data. (The “&lt;ID&gt;” element must always be passed on its own or an error will be issued.) Optional.</dd>
    
    <dt>DNIS</dt>
    <dd>10-Digit string value representing the DNIS (TFN) of the phone call to be matched for the associated Sales data. (The "&lt;DNIS&gt;" element must be passed if the “&lt;ID&gt;” element is absent.) Optional.</dd>
    
    <dt>ANI</dt>
    <dd>10-Digit string value representing the ANI (Caller #) of the phone call to be matched for the associated Sales data. (The "&lt;ANI&gt;" element must be passed if the “&lt;ID&gt;” element is absent.) Optional.</dd>
    
    <dt>Target</dt>
    <dd>10-Digit string value representing the Target (“RingTo”) number of the phone call to be matched for the associated Sales data. (The "&lt;Target&gt;" element must be passed if the “&lt;ID&gt;” element is absent.) Optional.</dd>
    
    <dt>CallStart</dt>
    <dd>The Call Start Time representing when this call was initiated. This value must be expressed using the standard XML DateTime format which includes the timezone offset identifier(i.e. “YYYY-MM-DDThh:mm:ss±HH:MM” or “YYYY-MM-DDThh:mm:ssZ”). (The "&lt;CallStart&gt;" element may optionally be passed if the “&lt;ID&gt;” element is absent.) Optional.</dd>
    
    <dt>ProductCode</dt>
    <dd>Product Code (per Mercury setup sheet) to be associated with the call. Required.</dd>
    
    <dt>MediaSource</dt>
    <dd>Media Source identifying the source of the telephone call. Often a set of call letters (i.e. “KABC”, “KROQ”, etc.) Required.</dd>
    
    <dt>CallerFirstName</dt>
    <dd>The first name of the caller, if known. Optional.</dd>
    
    <dt>CallerMiddleName</dt>
    <dd>The middle name of the caller, if known. Optional.</dd>
    
    <dt>CallerLastName</dt>
    <dd>The last name of the caller, if known. Optional.</dd>
    
    <dt>CallerCity</dt>
    <dd>The City of the caller. Required.</dd>
    
    <dt>CallerState</dt>
    <dd>The State of the caller. Required.</dd>
    
    <dt>CallerZipCode</dt>
    <dd>The ZIP Code of the caller. Required.</dd>
    
    <dt>OtherFirstName</dt>
    <dd>An alernative first name of the caller, if known. (Generally Not Used). Optional.</dd>
    
    <dt>OtherMiddleInitial</dt>
    <dd>An Alternative middle name of the caller, if known. (Generally Not Used). Optional.</dd>
    
    <dt>OtherLastName</dt>
    <dd>An alternative last name of the caller, if known. (Generally Not Used). Optional.</dd>
    
    <dt>OtherCity</dt>
    <dd>An alternative city of the caller, if known. (Generally Not Used). Optional.</dd>
    
    <dt>OtherState</dt>
    <dd>An alternative state of the caller, if known. (Generally Not Used). Optional.</dd>
    
    <dt>OtherZip</dt>
    <dd>An alternative ZIP code of the caller, if known. (Generally Not Used). Optional.</dd>
    
    <dt>OtherAreaCode</dt>
    <dd>An alternative area code of the caller, if known. (Generally Not Used). Optional.</dd>
    
    <dt>OtherPhone</dt>
    <dd>An alternative phone number of the caller, if known. (Generally Not Used). Optional.</dd>
    
    <dt>ScriptQ1-1</dt>
    <dd>An alternative phone number of the caller, if known. (Generally Not Used). Optional.</dd>
    
    <dt>Gender</dt>
    <dd>Gender (M/F) of the caller, if known. (Generally Not Used). Optional.</dd>
    
    <dt>ScriptQ1-3</dt>
    <dd>Response to Script Question #1-3, if captured. (Generally Not Used). Optional.</dd>
    
    <dt>ScriptQ1-4</dt>
    <dd>Response to Script Question #1-4, if captured. (Generally Not Used). Optional.</dd>
    
    <dt>InqReason</dt>
    <dd>Inquiry Reason (per Mercury setup sheet) (Generally Not Used). Optional.</dd>
    
    <dt>CallCode</dt>
    <dd>Call Code (per Mercury setup sheet). Required.</dd>
    
    <dt>ScriptQ10-2</dt>
    <dd>Response to Script Question #10-2, if captured. (Generally Not Used). Optional.</dd>
    
    <dt>ScriptQ10-3</dt>
    <dd>Response to Script Question #10-3, if captured. (Generally Not Used). Optional.</dd>
    
    <dt>ScriptQ10-4</dt>
    <dd>Response to Script Question #10-4, if captured. (Generally Not Used). Optional.</dd>
    
    <dt>OrderAmount</dt>
    <dd>Order Amount, representing the *TOTAL* order value. Required.</dd>
    
    <dt>ScriptQ30-1</dt>
    <dd>Response to Script Question #30-1, if captured. (Generally Not Used). Optional.</dd>
    
    <dt>ScriptQ30-2</dt>
    <dd>Response to Script Question #30-2, if captured. (Generally Not Used). Optional.</dd>
    
    <dt>SequenceID</dt>
    <dd>Sequence ID if known (Generally Not Used). Optional.</dd>
    
    <dt>DOB</dt>
    <dd>Date Of Birth (of caller) if known. (Generally Not Used). Optional.</dd>
    
    <dt>OtherDOB</dt>
    <dd>Alternate Date Of Birth (of caller) if known. (Generally Not Used). Optional.</dd>
    
    <dt>ScriptDate3</dt>
    <dd>Script Date #3 (Generally Not Used). Optional.</dd>
    
    <dt>Keycode</dt>
    <dd>Keycode (Generally Not Used). Optional.</dd>
    
    <dt>HitScreenDisp</dt>
    <dd>Hit Screen/Disposition. (Generally Not Used). Optional.</dd>
    
    <dt>MainOfferQty</dt>
    <dd>Main Offer Quantity Sold. Integer value. Required.</dd>
    
    <dt>Upsell1</dt>
    <dd>Upsell #1 Quantity Sold, if used. Integer value. Optional.</dd>
    
    <dt>Upsell2</dt>
    <dd>Upsell #2 Quantity Sold, if used. Integer value. Optional.</dd>
    
    <dt>Upsell3</dt>
    <dd>Upsell #3 Quantity Sold, if used. Integer value. Optional.</dd>
    
    <dt>Upsell4</dt>
    <dd>Upsell #4 Quantity Sold, if used. Integer value. Optional.</dd>
    
    <dt>Upsell5</dt>
    <dd>Upsell #5 Quantity Sold, if used. Integer value. Optional.</dd>
    
    <dt>Upsell6</dt>
    <dd>Upsell #6 Quantity Sold, if used. Integer value. Optional.</dd>
    
    <dt>Upsell7</dt>
    <dd>Upsell #7 Quantity Sold, if used. Integer value. Optional.</dd>
    
    <dt>Upsell8</dt>
    <dd>Upsell #8 Quantity Sold, if used. Integer value. Optional.</dd>
    
    <dt>Upsell9</dt>
    <dd>Upsell #9 Quantity Sold, if used. Integer value. Optional.</dd>
    
    <dt>Upsell10</dt>
    <dd>Upsell #10 Quantity Sold, if used. Integer value. Optional.</dd>
    
    <dt>Upsell11</dt>
    <dd>Upsell #11 Quantity Sold, if used. Integer value. Optional.</dd>
    
    <dt>Upsell12</dt>
    <dd>Upsell #12 Quantity Sold, if used. Integer value. Optional.</dd>
    
    <dt>Upsell13</dt>
    <dd>Upsell #13 Quantity Sold, if used. Integer value. Optional.</dd>
    
    <dt>Upsell14</dt>
    <dd>Upsell #14 Quantity Sold, if used, or "0". Integer value. Must be populated for transmission integrity check. Required.</dd>

</dl>

## Other Integrations

### Dial800

[Our native interface](http://docs.dial800.com/).

### MercuryMedia

[Mercury Long Form](http://docs.dial800.com/dial800/mlf).

### Euro

Are you using Euro's format? You can find the details [here](http://docs.dial800.com/dial800/euro).