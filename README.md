TrustedShops PHP SDK
=============

Super-simple, minimum abstraction TrustedShops API v2.x wrapper, in PHP.

I hate complex wrappers. This lets you get from the TrustedShops API docs to the code as directly as possible.

Requires PHP 7.0+. Abstraction is for chimps.

[![Build Status](https://travis-ci.org/antistatique/trustedshops-php-sdk.svg?branch=master)](https://travis-ci.org/antistatique/trustedshops-php-sdk)
[![StyleCI](https://github.styleci.io/repos/207270598/shield?branch=master)](https://github.styleci.io/repos/207270598)
[![Packagist](https://img.shields.io/packagist/dt/antistatique/trustedshops-php-sdk.svg?maxAge=2592000)](https://packagist.org/packages/antistatique/trustedshops-php-sdk)

Getting started
------------

You can install `trustedshops-php-sdk` using Composer:

```
composer require antistatique/trustedshops-php-sdk
```

Examples
--------

Start by `use`-ing the class and creating an instance with your API key

```php
use \Antistatique\TrustedShops\TrustedShops;
```

### List all the shops (with a `public` call via `get` on the `shops/{tsid}` method)

```php
$tsid = 'abc123abc123abc123abc123abc123';
$ts = new TrustedShops();
$response = $ts->get("shops/$tsid");
print_r($result);
```

### Get all reviews (with a `public` call via `get` to the `lists/{listID}/reviews` method)

```php
$tsid = 'abc123abc123abc123abc123abc123';
$ts = new TrustedShops();
$response = $ts->get("shops/$tsid/reviews");
print_r($result);
```

### Read measurement matrix of review complaint indicator for a shop (with a `restricted` authenticated call via `get` on the `shops/{tsid}/quality/complaints` method)

Update a list member with more information (using `patch` to update):

```php
$tsid = 'abc123abc123abc123abc123abc123';
$ts = new TrustedShops('restricted');
$ts->setApiCredentials( 'SECRET_USER', 'SECRET_PASSWORD');
$response = $ts->get("shops/$tsid/quality/complaints");
print_r($result);
```

Troubleshooting
---------------

To get the last error returned by either the HTTP client or by the API, use `getLastError()`:

```php
echo $ts->getLastError();
```

For further debugging, you can inspect the headers and body of the response:

```php
print_r($ts->getLastResponse());
```

If you suspect you're sending data in the wrong format, you can look at what was sent to TrustedShops by the wrapper:

```php
print_r($ts->getLastRequest());
```

If your server's CA root certificates are not up to date you may find that SSL verification fails and you don't get a response. The correction solution for this [is not to disable SSL verification](http://snippets.webaware.com.au/howto/stop-turning-off-curlopt_ssl_verifypeer-and-fix-your-php-config/). The solution is to update your certificates. If you can't do that, there's an option at the top of the class file. Please don't just switch it off without at least attempting to update your certs -- that's lazy and dangerous. You're not a lazy, dangerous developer are you?