# CloudAPI

Access your bank accounts with a simple bank agnostic API.

# Introduction

The Cloudbank Rest API is designed as a completely Restful API making use of HTTP methods GET, POST, PUT, DELETE.

# Prerequisites

You need to have an API key. Contact your Solidi representative for access.

# Beta Warning

This API is in Beta and may change with little notice. Currently known defects which will definitely change are listed below.


# Signing Private method calls

To call private API methods you need to sign your calls. See the separate documentation on [**HTTP Authentication**](HTTPAuthentication.md "**HTTP Authentication**")

# Methods

There are two sets of methods:

  - Public
    - These methods provide publicly available data such as lists of banks, login requirements.
  - Private
    - These provide access to private information including users transactions. They need to be correctly signed. 


## Public Methods

Currently all methods are private. This may change in future.

## Private Methods


Module | Description
----|---
[User](UserMethods) | Responsible for adding a clients "Users" to the platform. You should create a "User" object for each real world user.
[Bank](BankMethods) | Manages bank accounts including listing, displaying, getting transactions etc


 

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


Gets the login details which must be gathered from a user in order to be able to login to the banking service.

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


### bankLogin

POST https://t1.solidi.co/api/v1/loginRequirements/@bankid


Adds a new bank login to your account. This will test logging into the bank account.

#### URL Params
 - @bankid- ID of the bank (dict key from GET banks call)

#### HTTP POST Params
 - @loginDetails - JSON dictionary of the answers to the questions returned by loginRequirements.
 - e.g. For rbsdigital.co.uk

        {
          "q1":{"answer": "01234567"},
          "q2":{"answer": "1234"},
          "q3":{"answer": "mypassword"},
        }


#### Return
 - JSON dictionary with result of operation
   - @result - Either:
     - "Login Added" (Success)
     - an error message


### account

GET https://t1.solidi.co/api/v1/account


Gets a list of all the bank accounts that have been found.
WARNING - Currently this works at the level of the API client. This will be updated shortly to work at the user level.

#### URL Params
None

#### HTTP POST Params
None


#### Return
 - JSON list of bank accounts
   - @id - Unique ID of the account
   - @sortcode - 6 digit UK bank sortcode
   - @accno - 8 digit account number
   - @description - Description of the account as supplied by the bank
 -  E.g.
 
        [
          {
            "accno":"01234567",
            "description":"MR JOE BLOGGS",
            "id":1014,
            "sortcode":"010203"
          },
          {
            "accno":"76543210",
            "description":"MR & MRS BLOGGS",
            "id":2011,
            "sortcode":"010203"
          }
        ]

### transactions

GET https://t1.solidi.co/api/v1/transactions/@accountid


Gets a list of all the transactions in the account.

#### URL Params
 - @accountid- ID of the bank account as returned in the call to GET account

#### HTTP POST Params
None


#### Return
 - JSON list of bank accounts
   - @amt- Amount of the txn in GBP
   - @date- Date of the transaction
   - @desc1- Description field 1
   - @desc2- Description field 2
   - @id - Unique ID of the transaction
 -  E.g.
 
        [
            {
                "amt":5.5,
                "date":"2016-07-30T23:00:00.000Z",
                "desc1":"CJT2L7L",
                "desc2":"",
                "id":9878
            }
        ]
