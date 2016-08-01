# CloudAPI

Access your bank accounts with a simple bank agnostic API.

## Introduction

The Cloudbank Rest API is designed as a completely Restful API making use of HTTP methods GET, POST, PUT, DELETE.

## Methods

There are two sets of methods:

  - Public
    - These methods provide publicly available data such as lists of banks, login requirements.
  - Private
    - These provide access to private information including users transactions. They need to be correctly signed. 


## Prerequisites

You need to have an API key. Contact your Solidi representative for access.

## Signing Private method calls

To call private API methods you need to sign your calls. See the separate documentation on [**HTTP Authentication**](HTTPAuthentication.md "**HTTP Authentication**")

## Methods

### Public Methods

Currently all methods are private. This may change in future.

### Private Methods

### banks - Get a list of the supported Banks

GET https://t1.solidi.co/api/v1/banks


Gets a list of all the supported banks.

#### URL Params
None

#### HTTP POST Params
None


##### Return #####
 - JSON dictionary of banks
   - @amount - Amount in units of base currency.
   - @datetime - Order timestamp in milliseconds since unix epoch.
   - @id - Unique order identifier
   - @multiplier - Multiplier vs the base price. 
   - @type - 0 (buy) / 1 (sell)
   - @price - Price per unit of base currency
 - 
        {
    "rbsdigital.co.uk":{
        "logourl":"https://t1.solidi.co/img/logos/rbs.jpg",
        "name":"Royal Bank Of Scotland"
    }
}

