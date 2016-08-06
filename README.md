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
[User](UserMethods.md) | Responsible for adding a clients "Users" to the platform. You should create a "User" object for each real world user.
[Bank](BankMethods.md) | Manages bank accounts including listing, displaying, getting transactions etc

