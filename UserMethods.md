## User Methods

### POST user - Create a new user

POST https://t1.solidi.co/api/v1/user


Create a new user with the supplier details.

#### URL Params
None

#### HTTP POST Params
 - @username - Client chosen username. This must be unique - it could be a database key from your client system.
 - @firstname - Firstname of user
 - @lastname - Lastname of user



#### Return
 - JSON dictionary with:
   - @subuserID - The ID of the user.
 -  E.g.
 
        {
            "subuserID":30019
        }



### GET user - Get a list of all the users

GET https://t1.solidi.co/api/v1/user


Gets a list of all the users created by the client.

#### URL Params
None

#### HTTP POST Params
None


#### Return
 - JSON list of the user objects
   - @id - Unique ID of the user. 
   - @username - Client chosen username.
   - @firstname - Firstname of user
   - @lastname - Lastname of user
 -  E.g.
 
        [
            {
                "firstname":"Jamie",
                "id":30001,
                "lastname":"McNaught",
                "username":"test41"
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
