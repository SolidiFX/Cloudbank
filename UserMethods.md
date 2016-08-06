## User Methods

[TOC]

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


### GET user/@userid - Get user

GET https://t1.solidi.co/api/v1/user/@userid


Get a specific user account.

#### URL Params
 - @userid - ID of the user to get.

#### HTTP POST Params
None

#### Return
 - JSON list of the user objects (only 1)
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


### DELTE user/@userid - Delete user

DELETE https://t1.solidi.co/api/v1/user/@userid


Delete a specific user account.

#### URL Params
 - @userid - ID of the user to delete.

#### HTTP POST Params
None

#### Return
 - JSON dictionary containing result
   - @result - Test description of result. 
 -  E.g.
 
        {
            "result":"User deleted"
        }

### PUT user/@userid - Update a user

PUT https://t1.solidi.co/api/v1/user/@userid


Update an existing user account.

#### URL Params
 - @userid - ID of the user to update.

#### HTTP POST Params
 - @username - Client chosen username. This must be unique - it could be a database key from your client system.
 - @firstname - Firstname of user
 - @lastname - Lastname of user

#### Return
 - JSON dictionary containing result
   - @result - Test description of result. 
 -  E.g.
 
        {
            "result":"User updated"
        }
