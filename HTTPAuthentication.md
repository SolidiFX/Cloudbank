# HTTP API Authentication

The Cloudbank Restful API requires private methods to be signed using the API Secret supplied by your Solidi representative.

When calling the API you should use the following HTTP headers:

 - API-Key - The public key form the Settings page. 
 - API-Sign - The signature for the call (see below) 

And also store the nonce as a HTTP param.

### Signing Method calls

You can generate a signature to use as the API-Sign HTTP header using the following method (Python code):

	import time
	import urllib

	import hashlib
	import hmac
	import base64

	url = "https://t1.solidi.co/api/v1/order"
	api_secret = "8+RHStFQsBmiFi==" // Shortened for clarity, real
	                                // API secret is longer.
	params = {}
	params['nonce'] = int(time.time()*1000)
	postdata = urllib.urlencode(params)
	message = url+postdata
	b64secret = base64.b64encode(api_secret)
	sig = hmac.new(b64secret, message, hashlib.sha256)


### Disabling HTTP Authentication

As part of a short development phase in your project - for example to aid with meeting a demo deadline - Solidi may turn off the requirement to sign your API calls.

This is done on a case by case basis and will have restrictions placed on the number of users who can use the API.