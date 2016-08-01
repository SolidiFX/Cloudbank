# CloudAPI

Access your bank accounts with a simple bank agnostic API.

[TOC]

# Introduction

The Cloudbank Rest API is designed as a completely Restful API making use of HTTP methods GET, POST, PUT, DELETE.

# Methods

There are two sets of methods:

  - Public
    - These methods provide publicly available data such as lists of banks, login requirements.
  - Private
    - These provide access to private information including users transactions. They need to be correctly signed. 


# Prerequisites

You need to have an API key. Contact your Solidi representative for access.

# Signing Private method calls

To call private API methods you need to sign your calls. See the separate documentation on [**HTTP Authentication**](HTTPAuthentication.md "**HTTP Authentication**")

# Methods

## Public Methods

Currently all methods are private. This may change in future.

## Private Methods

### banks - Get a list of the supported Banks

GET https://t1.solidi.co/api/v1/banks


Gets a list of all the supported banks.

#### URL Params
None

#### HTTP POST Params
None


#### Return
 - JSON dictionary of supported banks, keyed on the url of the bank.
   - @name - Full name of the bank.
   - @logo - Logo of the bank which you can use in your application.
 -  E.g.
 
        {
          "rbsdigital.co.uk":{
            "logourl":"https://t1.solidi.co/img/logos/rbs.jpg",
            "name":"Royal Bank Of Scotland"
          }
        }



### loginRequirements

GET https://t1.solidi.co/api/v1/loginRequirements/@bankid


Gets a list of all the supported banks.

#### URL Params
 - @bankid- ID of the bank (dict key from GET banks call)

#### HTTP POST Params
None


#### Return
 - JSON dictionary of login requirements for the specified bank.
   - @type - The type of the question. Either:
     - qa - A single question
     - multiquestion -  User must answer a specified number of questions from a list. See separate documentation.
   - @question - Typical question asked to the user to gather the required information.
   - @answertype- The type of information to be gather. Supported answertypes are:
     - string - Plain text string such as a customer number.
     - password - Password field which must be obscured by platforms default placeholder characters (e.g. asterisks)
     - pin - Numeric field containing only characters 0-9
 -  E.g.
 
        [
          {
            "q1":{
              "answertype":"string",
              "question":"Please enter your customer number.",
              "type":"qa"
            },
            "q2":{
              "answertype":"password",
              "question":"Please enter your password.",
              "type":"qa"
            },
            "q3":{
              "answertype":"pin",
              "question":"Please enter your security number.",
              "type":"qa"
            }
          }
        ]


