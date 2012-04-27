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

$request = new HTTP_Request2('http://roundtrip.dial800.com/roundtrip');
$request->setMethod(HTTP_Request2::METHOD_POST)
    ->setAuth('user','password', HTTP_Request2::AUTH_BASIC)
    ->setHeader('Content-Type: application/omni')
    ->setBody(
        "<?xml version=\"1.0\" encoding=\"utf-8\"?>\r\n" .
        "<Call xmlns=\"http://www.dial800.com/roundtrip/2011-07-15\r\n" .
        "      xmlns:omni=\"http://www.omnidirect.com/2012-04-01\">\r\n" .
        "   <ANI>tel:3105555555</ANI>\r\n" .
        "   <Target>tel:3109999999</Target>\r\n" . 
        "   <CallStart>2011-07-15T01:02:03-08:00</CallStart>\r\n" .
        "   <omni:MediaSource>AZTCA</omni:MediaSource>\r\n" .
        "   <omni:ProductCode>C612</omni:ProductCode>\r\n" .
        "   <omni:ServicedCall>true</omni:ServicedCall>\r\n" .
        "   <omni:UniqueCall>true</omni:UniqueCall>\r\n" .
        "   <omni:OrderCall>true</omni:OrderCall>\r\n" .
        "   <omni:CustSvcCall>false</omni:CustSvcCall>\r\n" .
        "   <omni:MainOffer>1</omni:MainOffer>\r\n" .
        "   <omni:Counter1>0</omni:Counter1>\r\n" .
        "   <omni:Counter2/>\r\n" .
        "   <omni:Counter3/>\r\n" .
        "   <omni:Counter4/>\r\n" .
        "   <omni:Counter5/>\r\n" .
        "   <omni:Counter6/>\r\n" .
        "   <omni:Counter7>103</omni:Counter7>\r\n" .
        "   <omni:TotalRevenue>269.85</omni:TotalRevenue>" .
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
            const string userName = "USER";
            const string password = "PASSWORD";
            const string contentType = "application/omni";
            const string postMethod = "POST";
            string postData = @"<?xml version='1.0' encoding='utf-8' ?>
                                <Call xmlns='http://www.dial800.com/roundtrip/2011-07-15'
                                     xmlns:omni='http://www.omnidirect.com/2012-04-01'>
                                  <ANI>tel:3105555555</ANI>
                                  <Target>tel:3109999999</Target>
                                  <CallStart>2011-07-15T01:02:03-08:00</CallStart>
                                  <omni:MediaSource>AZTCA</omni:MediaSource>
                                  <omni:ProductCode>C612</omni:ProductCode>
                                  <omni:ServicedCall>true</omni:ServicedCall>
                                  <omni:UniqueCall>true</omni:UniqueCall>
                                  <omni:OrderCall>true</omni:OrderCall>
                                  <omni:CustSvcCall>false</omni:CustSvcCall>
                                  <omni:MainOffer>1</omni:MainOffer>
                                  <omni:Counter1>0</omni:Counter1>
                                  <omni:Counter2/>\r\n<omni:Counter3/>
                                  <omni:Counter4/>\r\n<omni:Counter5/>
                                  <omni:Counter6/>
                                  <omni:Counter7>103</omni:Counter7>
                                  <omni:TotalRevenue>269.85</omni:TotalRevenue>
                                </Call>";

            const string uri = "http://roundtrip.dial800.com/roundtrip";

            var postDataBytes = Encoding.UTF8.GetBytes( postData );

            var urlEndpoint = new Uri(uri);
            var request = WebRequest.Create( urlEndpoint ) as HttpWebRequest;

            request.Headers.Add(HttpRequestHeader.Authorization,
                                "Basic " + Convert.ToBase64String(Encoding.ASCII.GetBytes(userName + ":" + password)));
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
                            "The server returned:\n {2} \nwith the status code {1}: {0}",
                            errorResponse.StatusDescription,
                            errorResponse.StatusCode,
                            new StreamReader(errorResponse.GetResponseStream()).ReadToEnd());
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
      xmlns:omni="http://www.omnidirect.com/2012-04-01">      
    <ANI>tel:3105555555</ANI>
    <Target>tel:3109999999</Target>
    <CallStart>2011-07-15T01:02:03-08:00</CallStart>
    <omni:MediaSource>AZTCA</omni:MediaSource>
    <omni:ProductCode>C612</omni:ProductCode>
    <omni:ServicedCall>true</omni:ServicedCall>
    <omni:UniqueCall>true</omni:UniqueCall>
    <omni:OrderCall>true</omni:OrderCall>
    <omni:CustSvcCall>false</omni:CustSvcCall>
    <omni:MainOffer>1</omni:MainOffer>
    <omni:Counter1>0</omni:Counter1>
    <omni:Counter2/>
    <omni:Counter3/>
    <omni:Counter4/>
    <omni:Counter5/>
    <omni:Counter6/>
    <omni:Counter7>103</omni:Counter7>
    <omni:TotalRevenue>269.85</omni:TotalRevenue>
</Call>
'''
r = request.post('http://roundtrip.dial800.com/roundtrip',
                 auth=HTTPBasicAuth('user','password'),
                 headers={'Content-Type': 'application/omni'},
                 data=payload)
```

### Using Ruby

```ruby
require "net/http"
require "uri"

uri = URI.parse("http://roundtrip.dial800.com/roundtrip")

http         = Net::HTTP.new(uri.host, uri.port)
request      = Net::HTTP::Post.new(uri.host,uri.port)
request.body = xml_string
request.basic_auth("user","password")
request.content_type = "application/omni"
response     = http.request(request)
```

## Reference

The Reference documentation can be found [here](http://docs.dial800.com/dial800/reference).

### POST

#### Request

```
POST /calls
Content-Type: application/omni
```

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Call xmlns="http://www.dial800.com/roundtrip/2011-07-15"
      xmlns:omni="http://www.omnidirect.com/2012-04-01">      
    <ANI>tel:3105555555</ANI>
    <Target>tel:3109999999</Target>
    <CallStart>2011-07-15T01:02:03-08:00</CallStart>
    <omni:MediaSource>AZTCA</omni:MediaSource>
    <omni:ProductCode>C612</omni:ProductCode>
    <omni:ServicedCall>true</omni:ServicedCall>
    <omni:UniqueCall>true</omni:UniqueCall>
    <omni:OrderCall>true</omni:OrderCall>
    <omni:CustSvcCall>false</omni:CustSvcCall>
    <omni:MainOffer>1</omni:MainOffer>
    <omni:Counter1>0</omni:Counter1>
    <omni:Counter2/>
    <omni:Counter3/>
    <omni:Counter4/>
    <omni:Counter5/>
    <omni:Counter6/>
    <omni:Counter7>103</omni:Counter7>
    <omni:TotalRevenue>269.85</omni:TotalRevenue>
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
Content-Type: application/omni
```

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Call xmlns="http://www.dial800.com/roundtrip/2011-07-15"
      xmlns:msf="http://www.omnidirect.com/2012-04-01">      
    <ID>12345678990</ID>
    <omni:MediaSource>AZTCA</omni:MediaSource>
    <omni:ProductCode>C612</omni:ProductCode>
    <omni:ServicedCall>true</omni:ServicedCall>
    <omni:UniqueCall>true</omni:UniqueCall>
    <omni:OrderCall>true</omni:OrderCall>
    <omni:CustSvcCall>false</omni:CustSvcCall>
    <omni:MainOffer>1</omni:MainOffer>
    <omni:Counter1>0</omni:Counter1>
    <omni:Counter2/>
    <omni:Counter3/>
    <omni:Counter4/>
    <omni:Counter5/>
    <omni:Counter6/>
    <omni:Counter7>103</omni:Counter7>
    <omni:TotalRevenue>269.85</omni:TotalRevenue>
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

### Core Fields
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
</dl>

### Required Fields
<dl>
    <dt>MediaSource</dt>
    <dd>The Media Source (Station Call Letters) associated with this call. Required.</dd>
    
    <dt>ProductCode</dt>
    <dd>Product Code (per campaign setup sheet) to be associated with the call. Required.</dd>
    
    <dt>ServicedCall</dt>
    <dd>Serviced Call Indicator/Flag. Required.</dd>
    
    <dt>UniqueCall</dt>
    <dd>Unique Call Indicator/Flag. Required.</dd>
    
    <dt>OrderCall</dt>
    <dd>Order Call Indicator/Flag. Required.</dd>
    
    <dt>CustSvcCall</dt>
    <dd>Customer Service Call Indicator/Flag. Required.</dd>
    
    <dt>MainOffer</dt>
    <dd>Main Offer Counter (numeric). Required.</dd>
</dl>

### Optional Fields
<dl>
    
    <dt>Counter1</dt>
    <dd>Upsell Counter #1 (numeric) to be associated with the call. Optional.</dd>
    
    <dt>Counter2</dt>
    <dd>Upsell Counter #2 (numeric) to be associated with the call. Optional.</dd>
    
    <dt>Counter3</dt>
    <dd>Upsell Counter #3 (numeric) to be associated with the call. Optional.</dd>
    
    <dt>Counter4</dt>
    <dd>Upsell Counter #4 (numeric) to be associated with the call. Optional.</dd>
    
    <dt>Counter5</dt>
    <dd>Upsell Counter #5 (numeric) to be associated with the call. Optional.</dd>
    
    <dt>Counter6</dt>
    <dd>Upsell Counter #6 (numeric) to be associated with the call. Optional.</dd>
    
    <dt>Counter7</dt>
    <dd>Upsell Counter #7 (numeric) to be associated with the call. If this counter is not otherwise allocated, may be used for Script ID. Optional.</dd>
    
    <dt>TotalRevenue</dt>
    <dd>Total Revenue reported for this call. Optional.</dd>
</dl>

## Other Integrations

### Dial800

[Our native interface](http://docs.dial800.com/).

### MercuryMedia

[Mercury Long Form](http://docs.dial800.com/dial800/mlf).

### Euro

Are you using Euro's format? You can find the details [here](http://docs.dial800.com/dial800/euro).