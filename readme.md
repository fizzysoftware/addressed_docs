# Business API documentation for [Addresses](http://addressed.me) API v1.0.

1. To communicate addressed API first step is authenticate your application.
2. Addressed uses [Http basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) for providing API access to other application. Addressed will generate api_key and api_token for other application to provide API access.


## Poll application for addresses:-
* Url for accessing API is:- `http://api.addressed.me/api/v1/get_addresses.json`. Request type is 'POST'
* Addressed will respond with Addresses of the app user's addresses.
* Polling for addresses requires either phone_number or email of the user.

Sample call with email of user:-

```json
{
  email: "johndoe@example.com"
}
```
Sample call with phone_number of user:-

```json
{
  phone_number: "+01234567890"
}
```

* If user record associated with the email or phone_number exists in Addressed it will give response with the addresses of that user:-

Sample response:-

```json
[
  -{
    -address: {
      address_line_1: "500 South Main Street"
      address_line_2: "Downtown"
      city:  "Bishop"
      pincode: "90012"
      state: "CA"
      country: "United States"
      address_type: "shipping_address"
    }
  }
  -{
    -address: {
      address_line_1: "SUITE 5A-1204"
      address_line_2: "799 E DRAGRAM"
      city:  "TUCSON"
      pincode: "10019"
      state: "AZ"
      country: "U.S.A"
      address_type: "billing_address"
    }
  }
]
```
* If there is no record associated with the email or phone number the response will be no record found:-

```json
{
  error: "Record doesn't exist"
}
```

* Addressed will keep track of time when any business polled the API for every user.
* If the user addresses haven't updated from the time when last time polled, it will simply return no update else whole address response will be given.

Sample response if no update:-

```json
{
  message: "No update in address"
}
```
