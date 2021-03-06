---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Carnot API! You can use our API to access Carnot API endpoints, which can get information on various users, cars, devices and trips in our database.

You can view code examples to access the API in the dark area to the right.

This API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> Make sure to replace `<api_key>` with your API key and `<auth_token>` with your Auth Token

Carnot uses API keys to allow access to the API. You can get a new API key by writing to us at prathamesh1729@gmail.com

The API key must be included in all API requests to the server in a header that looks like the following:

`Apikey: <api_key>`

Apart from the API key all the endpoints that require user authentication require a Token. The token must be supplied in a header that looks as follows:

`Authorization: Token <auth_token>`

<aside class="notice">
You must replace <code>&lt;api_key&gt;</code> with your personal API key. You must replace <code>&lt;auth_token&gt;</code> with the user's auth token.
</aside>


# Users

## Emergency contact details

```shell

Get emergency contacts

curl "http://<BASE_URL>/users/<ID>/econtacts/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":{
    "contacts":[
      {
      "em":"hello1@openxcell.com",
      "ph":8899773322,
      "nm":"John"
      },
      {
      "em":"hello2@openxcell.com",
      "ph":9933224455,
      "nm":"Bruce"
      }
    ],
    "n":2
  }
}
```

```shell

Set emergency contacts

curl "http://<BASE_URL>/users/<ID>/econtacts/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"contacts":[{"em": "hello4@openxcell.com", "ph": 8899773321, "nm": "Johny"},
              {"em": "hello5@openxcell.com", "ph": 8899773323, "nm": "Johnathan"}]}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "Success"
}
```

This endpoint sets and retrieves a user's emergency contact details.

### HTTP Request (Get contacts)

`GET http://<BASE_URL>/users/<ID>/econtacts/`

### HTTP Request (Set contacts)

`POST http://<BASE_URL>/users/<ID>/econtacts/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user whose data is to be retrieved

## Rider Profile

```shell

Get Rider Profile

curl "https://<BASE_URL>/users/<ID>/settings/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "success",
  "data": {
    "nm": "<full name>",
    "gd": "<gender>",
    "ag": "<rider age>",
    "photo": "<profile pic link>"
  }
}
```

```shell

Set Rider Profile details

curl "https://<BASE_URL>/users/<ID>/settings/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"nm": "<rider name>", "ag": <age>, "gd": "<gender>", "content_type": "image/<extension>",
      "file": "<base64 encoded image byte string>"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "success",
  "imgUrl": "<uploaded image url>"
}
```

The endpoint is used to set and retrive Rider profile info.

### HTTP Request (Get profile)

`GET https://<BASE URL>/users/<ID>/settings/`

### HTTP Request (Set profile)

`POST https://<BASE URL>/users/<ID>/settings/`

### URL Parameters

Parameter | Description
----------|------------
ID | ID of the user

## Users car status (User garage)

```shell
curl "http://<BASE_URL>/users/<ID>/garage/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
```
> The above command returns JSON structured like this:

```json
{
  "message":"Success",
  "status":true,
  "data":[
    {
      "flag":0,
      "id":9,
      "lat":19.1287833333,
      "isOnTrip":false,
      "lock":0,
      "lon":72.8886133333,
      "name":"My i201",
      "lut":"2016-07-15T17:05:44Z",
      "latest_trip":57,
      "speed":5
    },
    {
      "flag":0,
      "id":3,
      "lat":23.007577,
      "isOnTrip":false,
      "lock":0,
      "lon":77.810271,
      "name":"My Swift Dzire",
      "lut":0,
      "latest_trip":0,
      "speed":0
    }
  ]
}
```
This method is used for getting user related cars and their status information.

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/garage/`

### URL Parameters

Parameter|Description
---------|-----------
ID| User ID

### Response Parameters

Parameter|Description
---------|------------
id| Car ID
lat,lon|Current location of car
speed|speed in kmph
latest_trip | ID of recent trip made by the car
flag | 1 if data sync is pending, 0 if all data synced.
lut | Last update time for car data
lock | Location info


### Location Info

Parameter | Description
----------|------------
1 | GPS Lock
2 | GSM Lock
0 | No Location


## Get User Information and Stats

```shell
curl "http://<BASE_URL>/users/<ID>/fullprofile/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token"
```
> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":
    [
      {
        "mileage":20,
        "photo":"http://carnotimgs.s3.amazonaws.com/pictures/img_73_profile.png",
        "recentBadges":{},
        "hardAcc":20,
        "isOnTrip":false,
        "speed":0,
        "driverscore":50,
        "hardBreak":20,
        "name":"PSJ",
        "distance":0,
        "gender":"M",
        "age":23,
        "idlingTime":20,
        "time":60,
        "nTrips":0,
        "badge":{},
        "tips":{}
      }
    ]
}
```

The API is used to get Users overall driving stats and profile info.

### HTTP Request

`GET http://<BASE_URL>/users/<ID>/fullprofile/`

### URL Parameters

Parameter|Description
---------|-----------
ID|User ID


# Cars

## Get car brands

```shell
curl "http://<BASE_URL>/cars/brands/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":{
    "brands":[
      "Aston Martin",
      "Audi",
      "Bentley",
      "Caterham",
      "Chevrolet",
      "Conquest",
      "Datsun",
      "DC",
      "BMW",
      "Bugatti",
      "Ferrari",
      "Fiat",
      "Force",
      "Ford",
      "Honda",
      "Hyundai",
      ...
    ]
  }
}
```
The endpoint is used during car setup to get list of car brands.

### HTTP Request

`GET http://<BASE_URL>/cars/brands/`

### URL Parameters

None

## Get car models

```shell
curl "http://<BASE_URL>/cars/<brand>/models/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"success",
  "data":{
    "models":[
      "1 Series",
      "3 Series",
      "X1",
      "5 Series",
      "X3",
      "X5",
      "Z4",
      "7 Series",
      "6 Series",
      "X6",
      "M Series",
      "i8"
    ]
  }
}
```
The endpoint retrives car models when a brand name is provided. This is useful during car setup.

### HTTP Request

`GET http://<BASE_URL>/cars/<brand>/models/`

### URL Parameters

Parameter|Description
--------|------------
brand| Brand name for which models are to be retrieved

## Get Plug-in adapter Links

```shell
curl "http://<BASE_URL>/cars/save/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"brand":"<brand>", "model":"<model>"}'
```

> The above command returns JSON strctured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":{
    "imageUrl":"<image_link>",
    "videoUrl":"<video_link>"
  }
}
```

This method is used for displaying OBD port reference video for a selected brand and model.

### HTTP Request

`POST http://<BASE_URL>/cars/getlinks/`

### URL Parameters

Parameter|Description
---------|-----------
brand | Car brand
model | Car model


## Save car info

```shell
Add new car details:

curl "http://<BASE_URL>/cars/save/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"brand":"<brand>", "model":"<model>",
    "name": "<car nickname>", "ln":"<license number>",
    "ft": "<Fuel type>", "userid":<user_id>,
    "printedPasscode":"<16-digit passcode>"}'
```

> The above method returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":{
    "carId":21,
    "device_pk": 42,
    "nrfid": "123456",
    "stmid": "C0001",
    "key": "5634",
    "fuel": "Petrol"
  }
}
```

```shell

Update existing car details

curl "http://<BASE_URL>/cars/save/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"brand":"<brand>", "model":"<model>",
    "name": "<car nickname>", "ln":"<license number>",
    "userid":<user_id>, "carid": <ID of car to be updated>}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "success"
}
```

This method is used to save car and it's associated device or update car info when car setup is complete.

### HTTP Request

`POST http://<BASE_URL>/cars/save/`

### URL Parameters

Parameter|Description
---------|-----------
brand | Selected brand of car
model | Selected car model
name | Car nickname given
ln | license number of car
ft | Fuel type of the car
userid | ID of user to which the car belongs
carid | ID of car to be updated
printedPasscode | 16-digit passcode printed on device

### Response Parameters

Parameter|Description
---------|-----------
carId | ID of the saved car, to be used for any subsequent Car APi's
nfrid | NFR ID of the device
stmid | STM ID of the device
key | The key to be sent be to device over Bluetooth for authentication
device_pk | Device ID to be used for any subsequent device specific API's


<aside class="note">
  Send <i> carid </i> in POST data only when car details are to be updated
</aside>


## Get car info

```shell
Add new car details:

curl "http://<BASE_URL>/cars/<ID>/overview/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above method returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":{
    "name":21,
    "ln":"MH01HN3002",
    "brand":"Honda",
    "model": "Jazz",
    "fuel": "Diesel"
  }
}
```

This method is used to get car info when car setup is complete.

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/overview/`

### URL Parameters

Parameter|Description
---------|-----------
brand | Selected brand of car
model | Selected car model
name | Car nickname given
ln | license number of car
ID | ID of car to be retrieved
fuel | Fuel type of the car

## Car Diagnostics

```shell
curl "http://<BASE_URL>/cars/<ID>/diagnostics/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
```
> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":{
    "car_errors":{},
    "engine_oil":true,
    "tyre_pressure_front_right":0,
    "tyre_pressure_front_left":0,
    "cabin_temperature":80,
    "battery_health":100,
    "tyre_pressure_bottom_left":0,
    "coolant_temperature":90,
    "tyre_pressure_bottom_right":0
  }
}
```
The API is used to get diagnostics details for a car. The diagnostics data contains list of error info, oil, tyre, cabin and coolant temperature information.

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/diagnostics/`

### URL Parameters

Parameter|Description
---------|-----------
ID| Car ID


## Speed Limit Settings

```shell
Set Speed Limit

curl "http://<BASE_URL>/cars/<ID>/speedlimit/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"sl":<limit>}'
```

> THe above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "success"
}

```

```shell
Get Speed Limit

curl "http://<BASE_URL>/cars/<ID>/speedlimit/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X GET
```

> The above command returns JSON structured like this

```json
{
  "status": true,
  "message": "success",
  "data": {
    "speed_limit": 40
  }
}
```
This endpoint sets and retrieves speed limit for a car.  

### HTTP Request (Get Speed Limit)

`GET http://<BASE_URL>/cars/<ID>/speedlimit/`


### HTTP Request (Set Speed Limit)

`POST http://<BASE_URL>/cars/<ID>/speedlimit/`


### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be set/retrieved


## Car Passport


```shell
Car Document Upload

curl "http://<BASE_URL>/cars/<car_id>/upload/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"data": {"dtype": "<document type>", "dinfo":"<document info>",
     "content_type": "image/<extension>", "file": "<base64 encoded image byte string>",
     "meta": "<optional placeholder for meta info of document>"}}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "success",
  "imgUrl": "uploaded image url"
}
```


```shell
Car Document Download

curl "http://<BASE_URL>/cars/<car_id>/download/<dtype>"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X GET
```

> The above command returns JSON structured like this

> 1. Car Profile Download
> 2. Car Document (PUC/DL/Insurance/Service) Download

```json

{
  "status": true,
  "message": "Success",
  "data": {
    "np": "MH01CD007",
    "nm": "My Celerio",
    "img": "http://carnotimgs.s3.amazonaws.com/pictures/img_20_profile.jpg?Signature=Llyb%2BY9ASg4JJXqKGx%2FDAxGZsag%3D&Expires=1494583772&AWSAccessKeyId=AKIAJCDK5W4ISB6FL7RA"
  }
}


{
  "status": true,
  "message": "Success",
  "data": {
    "info": "car registration details",
    "meta": {
      "date": "2015-03-23"
    },
    "img": "http://carnotimgs.s3.amazonaws.com/pictures/img_20_registration.jpg?Signature=R86aQe0sGnpBpV44Utcsixih6gg%3D&Expires=1494587758&AWSAccessKeyId=AKIAJCDK5W4ISB6FL7RA",
    "type": "registration"
  }
}

```

This endpoint sets and retrieves document details of a specific car. This is useful for displaying a car's passport view.

The Document type here:

Parameter|Description
---------|-------------
profile| Car Profile
reg| Registration Document
puc| Car PUC Document
ins| Insurance Document
dl| Driver's License
ser| Car Service Document

### HTTP Request (Upload Documents)

`POST http://<BASE_URL>/cars/<ID>/upload/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved

### HTTP Request (Download Documents)

`GET http://<BASE_URL>/cars/<ID>/download/<doc type>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved
doc type | Document type

For more info on base64 encoded image byte strings, see:
<br/><br/>[1] Encode image: https://www.base64-image.de/
<br/>[2] Decode image: http://codebeautify.org/base64-to-image-converter

# Devices

## Get Device Info

```shell
curl "http://<BASE_URL>/devices/<ID>/info/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "Success",
  "data": {
    "fwID": "309-33-44",
    "devID": "23456123"
  }
}
```

This endpoint retrieves the info of a particular device.
Useful for the Device Info screen on the app.

### HTTP Request

`GET http://<BASE_URL>/devices/<ID>/info/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the device, the info of which is to be retrieved

## Log a production device

```shell
curl "http://<BASE_URL>/devices/log/"
  -H "ApiKey: <api_key>"
  -X POST
  -d '{
      "lb":<label_id>,
      "pc":"<passcode>",
      "flg":<device status>,
      "stm":"<STM ID>",
      "stmv":<STM version>,
      "nrf":"<NRF ID>",
      "nrfv":<NRF version>,
      "simcc":"<sim ccid>",
      "stms_st":"<STM status string",
      "stms_i":<STM status Int>,
      "nrfs_st":"<NRF status string>",
      "nrfs_i":<NRF status Int>,
      "gsmv":"<GSM version string>",
      "pwr":<power voltage supply: Float>,
      "update": <1 to update existing entries, 0 otherwise>
    }'
```
> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "Device logged into system"
}
```
The endpoint is used to log devices that are in production when labelling is to be done.

### HTTP Request

`POST http://<BASE_URL>/devices/log/`

### URL Parameters

Parameter | Description
----------|-------------
lb| Label ID
pc| 16-digit passcode
flg| Device status 1 for Good 0 Otherwise
stm|STM ID
stmv|STM version
nrf|NRF ID
nrfv|NRF version
simcc|SIM CCID
stms_st|STM Status string
stms_i|STM Status Integer (first 5 bits converted to number)
nrfs_st|NRF Status string
nrfs_i|NRF Status Integer (first 4 bits converted to number)
gsmv|GSM Version
pwr| Power voltage supply float field
update | Flag to notify if update should be done. (1-> update, 0->otherwise)


## Reset Device

<aside class="note">
  Before calling this API, all data on app, for the device (car) should be deleted.
</aside>


```shell
curl "http://<BASE_URL>/devices/<ID>/reset/"
  -H "Authorization: Token <auth_token>"
  -H "ApiKey: <api_key>"
```
> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "Device reset successful"
}
```
The endpoint is used to reset device.

### HTTP Request

`GET http://<BASE_URL>/devices/<ID>/reset/`

### URL Parameters

Parameter | Description
----------|-------------
ID | Device ID

# Accounts

## Send OTP to Phone

This API is used as pre-registration, to send OTP to input phone number.

```shell
curl "http://<BASE_URL>/users/getotp/"
  -H "Apikey: <api_key>"
  -X POST
  -d '{"phone":<phone>}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "OTP Sent",
  "data":
    {
      "otp": "119745",
      "phone": 9922883311
    }
}
```

### HTTP Request

`POST https://<BASE_URL>/users/getotp/`

### URL Parameters

Parameter | Description
----------|------------
phone | phone number of the user

### Response Parameters

Parameter | Description
----------|------------
status | OTP send status, true when success, false otherwise
message | success on OTP sent, on failure re-verify
otp | OTP sent to the number
phone | Number on which the otp is sent



## Register

This endpoint registers a new user to the Carnot backend.

```shell
curl "http://<BASE_URL>/users/register/"
  -H "Content-Type: application/json"
  -H "Apikey: <api_key>"
  -X POST
  -d '{"email":"abc@xyz.com","password":"xyz","name":"John Doe", "phone": 9988776655}'
```

> The above command returns JSON structured like this:

```json
{
    "status": true,
    "message": "success",
    "data":
    {
        "token": "ae4e00bf6a08cf9cd56a37b99d0162e69db4fd74",
        "id": 43,
        "email": "abc@xyz.com",
        "phone": 9988776655,
        "name" : "App Dev",
        "cars": []
    }
}

```

### HTTP Request

`POST http://<BASE_URL>/users/register/`

### URL Parameters

Parameter | Description
--------- | -----------
email | Email address of the registering user. This eventually becomes the unique username required for login
password | Password of the registering user
name | Name of the registering user
phone | 10-digit phone number

### Response Parameters

Parameter | Description
----------| -----------
status| true if successful, false otherwise
message| Message indicating registration status
token | The auth token to be used to authenticate this user in subsequent requests
id | The id of the user to be included in the URL in subsequent requests where id is required
name | Full name of the user
email | Confirmation of the email id the user entered. Email id also serves as the user name
phone | mandatory field during registration, it could also be used with login instead of email


## Login

This endpoint logs an existing user into the Carnot backend. Successfully logged in users get access to an auth token that should be used in subsequent authenticated requests.

The login can be done using email or phone.

```shell
curl "http://<BASE_URL>/users/login/"
  -H "Content-Type: application/json"
  -H "Apikey: <api_key>"  
  -X POST
  -d '{"email":"<email/phone>","password":"xyz"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "Success",
  "data":
      {
        "token": "ae4e00bf6a08cf9cd56a37b99d0162e69db4fd74",
        "id": 43,
        "email": "abc@xyz.com",
        "phone": 9988776655,
        "name" : "App Dev",
        "cars":[
          {
            "stmid":"36ffd6054755303723820743",
            "nrfid":"9de2e874b2fc593a",
            "fuel":"Diesel",
            "key":"743ae859e2fc",
            "id":18,
            "device_pk":14
          },
          {
            "stmid":"36ffd10547553037268FFFFF",
            "nrfid":"123456789012FFFF",
            "fuel":"Petrol",
            "key":"78FF56FF3412",
            "id":19,
            "device_pk":21
          }
        ]
      }
}


```

### HTTP Request

`POST http://<BASE_URL>/users/login/`

### URL Parameters

Parameter | Description
--------- | -----------
email | Email address (or phone number) of the user attempting to login. This should be the email or phone used when registering
password | Password of the registering user

### Response Parameters

Parameter| Description
----------| -----------
token |The auth token to be used to authenticate this user in subsequent requests
id | The id of the user to be included in the URL in subsequent requests where id is required
email | Confirmation of the email id the user entered. Email id also serves as the user name
phone | Phone number of current user
name  | Full name of the user
status |true if successful, false otherwise
message |Message indicating login status


## Logout

This endpoint logs out the user from Carnot backend.

```shell
curl "http://<BASE_URL>/users/logout/"
  -H "Content-Type: application/json"
  -H "Apikey: <api_key>"
  -X POST
  -d '{"email":"<email/phone>"}'
```

> The above command returns JSON structured like this:

```json
{
    "status": true,
    "message": "Success"
}
```

### HTTP Request

`POST http://<BASE_URL>/users/logout/`

### URL Parameters

Parameter | Description
--------- | -----------
email | Email address of the user logging out of system.
phone | Phone number used during registration

### Response Parameters

Parameter | Description
----------| -----------
status| true if successful, false otherwise
message| Message indicating logout status

<aside class="notice">
 On successful logout, user token is deleted. Upon re-login new token gets created.
</aside>

## Forgot Password

```shell
curl "http://<BASE_URL>/users/<number>/fgpwd/"
  -H "ApiKey: <api_key>"
```
> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "OTP Sent!",
  "data":
  {
    "otp": "916985",
    "phone": 8123664830
  }
}
```

```json
"Once OTP is verified, user should be asked his
new password and second WS to be called
to set the new password."
```

```shell
curl "http;//<BASE_URL>/users/<number>/chpwd/"
  -H "ApiKey: <api_key>"
  -X POST
  -d '{"pwd": "<new password>"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "Password updated"
}
```

The endpoints are used to verify user and set new password. User is verified using OTP. Once OTP on SMS and WS response matches, second WS should be called to set the new password.

### HTTP Request (Verify user)

`GET http://<BASE_URL>/users/<number>/fgpwd/`

### HTTP Request (Set new password)

`POST http://<BASE_URL>/users/<number>/chpwd/`

### URL Parameters

Parameter|Description
---------|----------------
number | Users phone number


# Alerts / Notifications


## Cancel Accident Alert
```shell
curl "http://<BASE_URL>/users/cancel/"
  -H "ApiKey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"id":"<notification id>"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "Job removed"
}

OR

{
  "status": false,
  "message": "No such job"
}
```

The endpoint is used when accident alert is pushed on phone and dismiss is clicked within 3 minutes of time.

### HTTP Request

`POST http://<BASE_URL>/users/cancel/`


### Request Parameters

Parameter | Description
----------|------------
id | Notification id for alert code M1005


## Rash Driving

```shell
Set Speed Limit

curl "http://<BASE_URL>/cars/<ID>/speedlimit/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"sl":<limit>}'
```

> THe above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "success"
}

```

```shell
Get Speed Limit

curl "http://<BASE_URL>/cars/<ID>/speedlimit/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X GET
```

> The above command returns JSON structured like this

```json
{
  "status": true,
  "message": "success",
  "data": {
    "speed_limit": 40
  }
}
```
This endpoint sets and retrieves speed limit for a car.  

### HTTP Request (Get Speed Limit)

`GET http://<BASE_URL>/cars/<ID>/speedlimit/`


### HTTP Request (Set Speed Limit)

`POST http://<BASE_URL>/cars/<ID>/speedlimit/`


### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be set/retrieved



# DTC

## Get Diagnostic Info for a car

```shell
curl "http://<BASE_URL>/cars/<ID>/diagnostics/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":
  {
      "tyre_pressure_front_left":0,
      "cabin_temperature":40,
      "battery_health":50,
      "tyre_pressure_bottom_left":0,
      "engine_oil":true,
      "tyre_pressure_front_right":0,
      "coolant_temperature":80,
      "tyre_pressure_bottom_right":0,
      "car_errors":
      [
          {
            "category":2,
            "code":"N1002",
            "title":"Critically low battery",
            "timestamp":"2016-06-09 07:21:46+00:00",
            "longitude":68.22,
            "latitude":23.99,
            "metadata":"No Data",
            "desc":"Consider charging"
          }
      ]
  }
}
```

This endpoint retrieves the diagnostic info for a car.  

### HTTP Request

`GET http://<BASE_URL>/cars/<ID>/diagnostics/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved


### Response Parameters

Parameter | Description
----------|-------------
tyre_pressure_front/bottom_left/right | Tyre pressures
engine_oil | True if OK, False otherwise
cabin_temperature | Cabin temperature in degree celsius
battery_health | Battary health percentage
coolant_temperature |  Coolant temperatur in degree celsius
car errors | List of car errors

### Car Error Parameters

Parameter | Description
----------|-------------
Category | Severity of the error (LOW   = 0, MEDIUM  = 1, CRITICAL= 2)
Code | Error code
Title | Error Title
timestamp | The time when the error occurred
longitude - latitude | The location where the error occurred
metadata | Any string metadata related to the error to be displayed as is
desc | Error Description

# Trip

## Get a specific Trip

```shell
curl "http://<BASE_URL>/data/trips/<Trip ID>/<Car ID>/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
```

> The above command returns JSON structured like this:

```json
{
  "status":true,
  "message":"Success",
  "data":
  [
    {
      "start": "Chandivali",
      "avg_mileage": 14.52,
      "gc_p": "",
      "total_running_time": 1506,
      "gc_m": 15,
      "hab_p": "19.0213_73.012335,19.0447016667_73.0082683333,19.0213166667_73.0124216667",
      "i_sc": 14.10891056060791,
      "ed_m": 25,
      "trip_id": 421,
      "os_sc": 10,
      "end_lat": 19.025861666666664,
      "gc_sc": 14.800000190734863,
      "distance": 12.12,
      "trip_time": 1820,
      "ed_p": "19.0453616667_73.0082933333,19.02279_73.0083316667,19.0257383333_73.032385",
      "route": [
        {
          "latitude": 19.037053333333333,
          "id": 56143,
          "longitude": 73.02429833333333
        },
        {
          "latitude": 19.037901666666667,
          "id": 56151,
          "longitude": 73.02513833333335
        },
        {
          "latitude": 19.038588333333333,
          "id": 56157,
          "longitude": 73.02582333333334
        },
        ...
      ],
      "free_space": 0,
      "end": " Belapur CBD",
      "end_lon": 73.03227833333334,
      "total_idling_time": 314,
      "avg_speed": 24.03,
      "total_fuel": 0.8344447016716003,
      "message_id": 57765,
      "id": 88,
      "start_lon": 73.02429833333333,
      "drive_score": 75,
      "timestamp": "2016-09-01T16:50:04Z",
      "hab_sc": 18.8118953704834,
      "name": "",
      "os_m": 10,
      "start_lat": 19.037053333333333,
      "photo": "",
      "os_p": "19.0453616667_73.0082933333,19.02279_73.0083316667,19.0257383333_73.032385",
      "i_p": "19.0655483333_72.9988733333,19.0258616667_73.0322783333,19.044715_73.0082616667",
      "end_time": "2016-09-01T16:50:04Z",
      "hab_m": 35,
      "start_time": "2016-09-01T16:18:22Z",
      "i_m": 15,
      "car_id": 5,
      "ed_sc": 16.78877830505371
    },
    ...
  ]
}
```

This endpoint retrieves bunch of next 5 trips of a car, from trip ID provided.

### HTTP Request

`GET http://<BASE_URL>/data/trips/<Trip ID>/<Car ID>/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the trip which is to be retrieved  

### Response Parameters

Parameter | Description
----------|------------
route | Trips ODB points (max 23)
car_id | Car ID for which the trip belongs
name | Name of the driver who has made the trip
start_lat, start_lon | Trip start lat-longs
end_lat, end_long | Trip end lat-longs
start, end | Start and end addresses of a trip
trip_id | ID of the next trip
overspeeding | drive score when overspeeding
hard_accl_brakes | drive score when hard acceleration / hard brakes are used
eco_driving | drive score when driven properly
idling | drive score lost due to idling of car
gear_change | drive score due to proper gear changes


### Notes
id | Note
----|-----
1. | max points in route will be 23
2. | max points in drive scores break-down are 3  
3. | sum of breakdown points (overspeeding ... gear change) is the drive score in response


# Documents

## Car Passport


```shell
Car Document Upload

curl "http://<BASE_URL>/cars/<car_id>/upload/"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X POST
  -d '{"data": {"dtype": "<document type>", "dinfo":"<document info>",
     "content_type": "image/<extension>", "file": "<base64 encoded image byte string>",
     "meta": "<optional placeholder for meta info of document>"}}'
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "success"
}
```


```shell
Car Document Download

curl "http://<BASE_URL>/cars/<car_id>/download/<dtype>"
  -H "Apikey: <api_key>"
  -H "Authorization: Token <auth_token>"
  -X GET
```

> The above command returns JSON structured like this

> 1. Car Profile Download
> 2. Car Document (PUC/DL/Insurance/Service) Download

```json

{
  "status": true,
  "message": "Success",
  "data": {
    "np": "MH01CD007",
    "nm": "My Celerio",
    "img": "http://carnotimgs.s3.amazonaws.com/pictures/img_20_profile.jpg?Signature=Llyb%2BY9ASg4JJXqKGx%2FDAxGZsag%3D&Expires=1494583772&AWSAccessKeyId=AKIAJCDK5W4ISB6FL7RA"
  }
}


{
  "status": true,
  "message": "Success",
  "data": {
    "info": "car registration details",
    "meta": {
      "date": "2015-03-23"
    },
    "img": "http://carnotimgs.s3.amazonaws.com/pictures/img_20_registration.jpg?Signature=R86aQe0sGnpBpV44Utcsixih6gg%3D&Expires=1494587758&AWSAccessKeyId=AKIAJCDK5W4ISB6FL7RA",
    "type": "registration"
  }
}

```

This endpoint sets and retrieves document details of a specific car. This is useful for displaying a car's passport view.

The Document type here:

Parameter|Description
---------|-------------
profile| Car Profile
reg| Registration Document
puc| Car PUC Document
ins| Insurance Document
dl| Driver's License
ser| Car Service Document

### HTTP Request (Upload Documents)

`POST http://<BASE_URL>/cars/<ID>/upload/`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved

### HTTP Request (Download Documents)

`GET http://<BASE_URL>/cars/<ID>/download/<doc type>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the car, the data of which is to be retrieved
doc type | Document type

For more info on base64 encoded image byte strings, see:
<br/><br/>[1] Encode image: https://www.base64-image.de/
<br/>[2] Decode image: http://codebeautify.org/base64-to-image-converter

API yet to be published

# Servicing

API yet to be published

# Badges

API yet to be published


#CRM

## Add Ticket

```shell
Save ticket

curl "http://<BASE_URL>/crm/add_ticket/"
  -H "Authorization: Token <auth_token>"
  -X POST
```

> The above command returns JSON structured like this:

```json
{
  "staus": "Sync failed/successful/Wrong input params"
}

```

This endpoint saves data for ticket in the CRM system.  


### HTTP Request (Add Ticket)

`POST http://<BASE_URL>/crm/add_ticket/`


### URL Parameters

Parameter | Description
--------- | -----------
email | Email of the person filling the form. (String -- valid email)
name | Name of the person filling the form. (String -- Without special characters)
phone | Phone of the person filling the form. (String -- 10 digits)
isCarnot | Check if the person is a Carnot Customer. (String -- 'Y' or 'N')
problem | Email of the person filling the form. (String)
