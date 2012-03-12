![Documentation](http://docs.dial800.com/images/roundtrip.png)

We know. You have two days to integrate with us. Don't worry, it's easy. We're here to help.

## How to submit data

* [if I am using PHP](#using-php)?
* [or C Sharp?](#using-c-sharp)
* [or Python?](#using-python)
* [or Ruby?](#using-ruby)

### Using PHP

1. Contact our team for credentials.
2. Generate Payload
3. Submit

### Using C Sharp

1. Contact our team for credentials.
2. Generate Payload
3. Submit

### Using Python

1. Contact our team for credentials.
2. Generate Payload
3. Submit

### Using Ruby

1. Contact our team for credentials.
2. Generate Payload
3. Submit

## Reference

### Authentication

### POST

#### Request

```
POST /calls
Content-Type: application/roundtrip.sales
```

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Call xmlns="http://www.dial800.com/roundtrip/2011-07-15"
      xmlns:rs="http://www.dial800.com/roundtrip-sales/2011-08-04">      
    <ANI>tel:3105555555</ANI>
    <Target>tel:3109999999</Target>
    <CallStart>2011-07-15T01:02:03-08:00</CallStart>
    <rs:Order payment="amex">
        <rs:Item price="100.00">OVEN</rs:Item>
        <rs:Item price="100.00">SPK</rs:Item>
        <rs:Item price="59.72">ERK 3 PAY</rs:Item>
    </rs:Order>
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
Content-Type: application/roundtrip.sales
```

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Call xmlns="http://www.dial800.com/roundtrip/2011-07-15"
      xmlns:rs="http://www.dial800.com/roundtrip-sales/2011-08-04">      
    <ID>12345678990</ID>
    <rs:Order payment="amex">
        <rs:Item price="100.00">OVEN</rs:Item>
        <rs:Item price="100.00">SPK</rs:Item>
        <rs:Item price="59.72">ERK 3 PAY</rs:Item>
    </rs:Order>
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

## Working with Media Agencies

### MercuryMedia

[MercuryMedia](www.mercurymedia.com) uses two slightly different formats, [MLF](http://docs.dial800.com/dial800/mlf) and [MSF](http://docs.dial800.com/dial800/msf).

### Euro

Are you using Euro's format? You can find the details [here](http://docs.dial800.com/dial800/euro).