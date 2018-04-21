# GP Webpay PHP SDK
[![Build Status](https://travis-ci.org/newPOPE/gp-webpay-php-sdk.svg?branch=master)](https://travis-ci.org/newPOPE/gp-webpay-php-sdk)

Full featured PHP SDK for [GP Webpay payments](http://www.gpwebpay.cz).

## Installation

The best way to install GP Webpay PHP SDK is using  [Composer](http://getcomposer.org/):

```sh
$ composer require vitexus/webpay-php5 dev-php56

## Setup

```php
$signer = new \AdamStipak\Webpay\Signer(
  $privateKeyFilepath,    // Path of private key.
  $privateKeyPassword,    // Password for private key.
  $publicKeyFilepath      // Path of public key.
);
    
$api = new \AdamStipak\Webpay\Api(
  $merchantNumber,    // Merchant number.
  $webpayUrl,         // URL of webpay.
  $signer             // instance of \AdamStipak\Webpay\Signer.
);

```

## Create payment

### Create payment url

 ```php
 use \AdamStipak\Webpay\PaymentRequest;
 
 $request = new PaymentRequest(...);
 
 $url = $api->createPaymentRequestUrl($request); // $api instance of \AdamStipak\Webpay\Api
 
 // use $url as you want. In most cases for redirecting to GP Webpay.
 
 ```
 
### Verify payment response
 
```php
use \AdamStipak\Webpay\PaymentResponse;
use \AdamStipak\Webpay\Exception;
 
$response = new PaymentResponse(...); // fill response with response parameters (from request).
 
try {
  $api->verifyPaymentResponse($response);
} 
catch (PaymentResponseException $e) {
  // PaymentResponseException has $prCode, $srCode for properties for logging GP Webpay response error codes.
}
catch (Exception $e) {
  // Digest is not correct.
}

```
 
##Development

GP Webpay PHP SDK is developed in [Docker](https://docker.com) container via `docker-compose` command.

Example:  
```sh
$ docker-compose run --rm default install  # install deps via composer
$ docker-compose run --rm default  # runs tests in container
```

Attach to container:  
```sh
$ docker-compose run --rm default bash # runs bash in container and attach tty
```
 
 
 
