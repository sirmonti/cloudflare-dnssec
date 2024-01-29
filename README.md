# DNSSEC for Cloudflare SDK v4
***

## Description
Surprisinly, Cloudflare SDK for PHP does not provide functions to manage
DNSSEC, although the REST API provides the webservice.

## Usage

This package provides the class Cloudflare\API\Endpoints\DNSSEC which has
the following methods

|Method|Description|
|---|---|
|get($zoneID)|Get the DNSSEC data for the domain identified by zoneID|
|enable($zoneID)|Enable DNSSEC for the specified domain|
|disable($zoneID)|Disable DNSSEC for the specified domain|
|getStatus($zoneID)|Get the DNSSEC status for the specified domain|
|getDS($zoneID)|Get the data for the DS DNS record|

## Examples

This code snippet show how to enable DNSSEC on a domain and
get the content of the DS record that must be uploaded to your
DNS registry
```php
<?php
  use Cloudflare\API\Adapter\Guzzle;
  use Cloudflare\API\Auth\APIKey;
  use Cloudflare\API\Endpoints\Zones;
  use Cloudflare\API\Endpoints\DNS;
  use Cloudflare\API\Endpoints\DNSSEC;

  $con=new Guzzle(new APIKey(YOURAPIID,YOURAPIKEY));
  $zones=new Zones($con);
  $dns=new DNS($con);
  $dnssec=new DNSSEC($con);

  $domid=$zones->getZoneID(YOURDOMAIN);
  $sec=$dnssec->enable($domid);
  print_r($sec);
  printf("\nRegister DS content: \"%s\"\n\n",$dnssec->getDS(DOMID));
```
This one show how to disable DNSSEC
```php
<?php
  use Cloudflare\API\Adapter\Guzzle;
  use Cloudflare\API\Auth\APIKey;
  use Cloudflare\API\Endpoints\Zones;
  use Cloudflare\API\Endpoints\DNS;
  use Cloudflare\API\Endpoints\DNSSEC;

  $con=new Guzzle(new APIKey(YOURAPIID,YOURAPIKEY));
  $zones=new Zones($con);
  $dns=new DNS($con);
  $dnssec=new DNSSEC($con);

  $domid=$zones->getZoneID(YOURDOMAIN);
  $sec=$dnssec->disable($domid);
  print_r($sec);
```
Of course, in this examples you must replace YOURAPIID and YOURAPIKEY for your
cloudflare API credentials and YOURDOMAIN for one of your domains hosted in
cloudflare
