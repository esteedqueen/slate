---
title: Tress API Reference

language_tabs:
  - swift
  - java

toc_footers:
  - <a href="mailto:esther@tressapp.co?Subject=Request for Developer Client Key" target="_top">Email for Client Authentication Key</a>

<!-- includes:
  - errors -->

search: true
---

# Introduction

Welcome to the Tress API! You can use our API to access Tress API endpoints.

The base url for the staging server is:

`https://tressapi-staging.herokuapp.com/api/v3`

This doc contains all the HTTP Requests for the endpoints.


# Client Authentication

> For client authentication, use this code:


```swift
# With Swift, you can just pass the correct header with each request
let headers = [
  "x-tress-client-key-id": "meowmeowmeow",
  "x-tress-client-key-secret": "meowmeowmeow"
]
```

```java
# With Java OkHttp, you can just pass the correct header with each request
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("url")
  .get()
  .addHeader("x-tress-client-key-id", "meowmeowmeow")
  .addHeader("x-tress-client-key-secret", "meowmeowmeow")
  .build();

```


> Make sure to replace `meowmeowmeow` with the give Client Key ID and Key Secret.
 
Tress uses Client Key ID and Client Key Secret to allow access to the API. You can email [our developer team](esther@tressapp.co) to request for access.

Tress expects the Client Key ID and Client Key Secret to be included in all API requests to the server in a header that looks like the following:

`X-Tress-Client-Key-Id: meowmeowmeow`

`X-Tress-Client-Key-Secret: meowmeowmeowmeowmeowmeowmeowmeowmeow`


<aside class="notice">
You must replace <code>meowmeowmeow</code> with the Client key Id and secret provided.
</aside>

# Users

## Create a User Account
The endpoints in this section creates a new user account via several options.


### Via email

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
]
let parameters = ["user": [
    "email": "ea.olatunde@gmail.com",
    "username": "monalisa",
    "password": "1234567890"
  ]]

```

```java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\n\t\"user\": {\n\t\t\"email\": \"ea.olatunde@gmail.com\",\n\t\t\"username\": \"monalisa\",\n\t\t\"password\": \"1234567890\"\n\t}\n}");
Request request = new Request.Builder()
  .url("https://tressapi-staging.herokuapp.com/api/v3/users")
  .post(body)
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("content-type", "application/json")
  .build();

```

> A successful sign up request returns JSON structured like this:

```json
{
  "id": 58,
  "email": "example@gmail.com",
  "digits_id": null,
  "username": "monalisa",
  "country_code": null,
  "firstname": null,
  "lastname": null,
  "fullname": " ",
  "hair_type_id": null,
  "phone_number": null,
  "bio": null,
  "avatar": "http://gravatar.com/avatar/6163882cbdd07b65079f41cf50e95c52?s=350&d=www.tressapp.co/images/esther.jpg",
  "authentication_token": "meowmeowmeowmeowmeowmeowmeowmeowmeowdf2196d42cb12cabae7b43298",
  "posts": [],
  "most_popular_posts": [],
  "followers": [],
  "following": [],
  "comments": [],
  "posts_count": 0,
  "comments_count": 0,
  "followers_count": 0,
  "following_count": 0,
  "posts_total_likes": 0,
  "posts_liked": [],
  "posts_bookmarked": [],
  "posts_bookmarked_count": 0,
  "created_at": "2016-10-04T10:46:39Z",
  "updated_at": "2016-10-04T10:46:39Z"
}
```
> An unsuccessful sign up request returns JSON structured like this:

```json
{
  "success": false,
  "message": "Invalid username"
}
```

#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/users`

#### Request Body Parameters

Parameter | Description
--------- | -----------
username | Required. Must be unique and match this format: `/\A[a-zA-Z0-9\-\_\.]+\z/` - usernames can only use letters, numbers, underscores and periods. No spaces allowed.
email | Required
password | Required


<aside class="notice">
Persist the User JSON object on the client including the authentication_token for future user authenticated requests.
</aside>

### Via Facebook

Authenticate via the [iOS](https://developers.facebook.com/docs/ios/) or [Android](https://developers.facebook.com/docs/android) [Facebook SDK](https://developers.facebook.com/docs/apis-and-sdks) and make a request with the authenticated response containing the user's access token as query parameter and facebook user details + user entered details as body parameters to the endpoint below.
Please contact [our developer team](esther@tressapp.co) for Facebook API Key and Secret.

```swift

```

```java

```
> The request returns JSON structured like this:

```json
{
  "id": 58,
  "email": "example@gmail.com",
  "digits_id": null,
  "username": "monalisa",
  "country_code": null,
  "firstname": "example",
  "lastname": "here",
  "fullname": "example here ",
  "hair_type_id": 1,
  "phone_number": null,
  "bio": null,
  "avatar": "http://gravatar.com/avatar/6163882cbdd07b65079f41cf50e95c52?s=350&d=www.tressapp.co/images/esther.jpg",
  "authentication_token": "meowmeowmeowmeowmeowmeowmeowmeowmeowdf2196d42cb12cabae7b43298",
  "posts": [],
  "most_popular_posts": [],
  "followers": [],
  "following": [],
  "comments": [],
  "posts_count": 0,
  "comments_count": 0,
  "followers_count": 0,
  "following_count": 0,
  "posts_total_likes": 0,
  "posts_liked": [],
  "posts_bookmarked": [],
  "posts_bookmarked_count": 0,
  "created_at": "2016-10-04T10:46:39Z",
  "updated_at": "2016-10-04T10:46:39Z"
}
```

#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/users/auth/facebook/callback`

#### Request Query Parameter

Parameter | Description
--------- | -----------
access_token | Required. Obtained from Facebook SDK authenticated response

#### Request Body Parameters

Parameter | Description
--------- | -----------
access_token | Required. Obtained from Facebook SDK authenticated response
email | Required. Obtained from Facebook SDK authenticated response. If email is an `@facebook.com` email, you must require the user to enter a valid email.
avatar | Required. Obtained from Facebook SDK authenticated response
username | Required. You must require the user to enter a username
firstname | Required. Obtained from Facebook SDK authenticated response
lastname | Required. Obtained from Facebook SDK authenticated response
gender | Required. Obtained from Facebook SDK authenticated response
birthday | Required. Obtained from Facebook SDK authenticated response
hair_type_id | Required. You must require the user to choose from a dropdown of hair type options


<aside class="notice">
Persist the User JSON object on the client including the authentication_token for future user authenticated requests.
</aside>

### Via Instagram

No official SDK for Instagram. I implemented the webviews myself on the Android Client. See Instagram [official docs](https://www.instagram.com/developer/authentication/). See Instagram Tress Client for App ID and Secret Key.

```swift

```

```java

```
> The request returns JSON structured like this:

```json
{
  "id": 58,
  "email": "example@gmail.com",
  "digits_id": null,
  "username": "monalisa",
  "country_code": null,
  "firstname": "example",
  "lastname": "here",
  "fullname": "example here ",
  "hair_type_id": 1,
  "phone_number": null,
  "bio": null,
  "avatar": "http://gravatar.com/avatar/6163882cbdd07b65079f41cf50e95c52?s=350&d=www.tressapp.co/images/esther.jpg",
  "authentication_token": "meowmeowmeowmeowmeowmeowmeowmeowmeowdf2196d42cb12cabae7b43298",
  "posts": [],
  "most_popular_posts": [],
  "followers": [],
  "following": [],
  "comments": [],
  "posts_count": 0,
  "comments_count": 0,
  "followers_count": 0,
  "following_count": 0,
  "posts_total_likes": 0,
  "posts_liked": [],
  "posts_bookmarked": [],
  "posts_bookmarked_count": 0,
  "social_access_tokens": {
    "instagram": "blahdie30422i4459"
  },
  "created_at": "2016-10-04T10:46:39Z",
  "updated_at": "2016-10-04T10:46:39Z"
}
```

#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/users/auth/instagram/callback`

#### Request Query Parameter

Parameter | Description
--------- | -----------
code | Required. Obtained from Facebook SDK authenticated response

#### Request Body Parameters

Parameter | Description
--------- | -----------
email | Required. 
avatar | Required. 
username | Required.
firstname | Required. 
lastname | Required.
hair_type_id | Required. You must require the user to choose from a dropdown of hair type options


<aside class="notice">
Persist the User JSON object on the client including the authentication_token for future user authenticated requests
Also, please note the social_access_token json object nested in the user object, persist the Instagram access token for future request to Instagram API to retrieve the user's images.
</aside>


### Via Phone Number
Authenticate via the [iOS](https://docs.fabric.io/apple/digits/sign-in-with-phone-number.html) or [Android](https://docs.fabric.io/android/digits/sign-in-with-phone-number.html) [Fabric Digits SDK](https://docs.fabric.io/ios/fabric/overview.html) on the client and make a request with the authenticated response containing the user's Auth Headers Hashmap and phone number to the endpoint below to verify on the server.

Please contact [our developer team](esther@tressapp.co) for Twitter Key & Secret required.

```swift

```

```java
(1) Verify Digits User on Server
OkHttpClient client = new OkHttpClient();

FormBody.Builder formBuilder = new FormBody.Builder()
        // dynamically add more parameter like this:
        .add("phone_number", phone_number);

RequestBody formBody = formBuilder.build();
Headers headers = Headers.of(hashMap);
Request request = new Request.Builder()
        .url(AppController.digitsVerifyUrl)
        .headers(headers)
        .post(formBody)
        .build();

```
> If the digits server verification is successful, there are two possible responses:


```json
{
  "id": 58,
  "email": "example@gmail.com",
  "digits_id": 938708492,
  "username": "monalisa",
  "country_code": null,
  "firstname": null,
  "lastname": null,
  "fullname": " ",
  "hair_type_id": null,
  "phone_number": null,
  "bio": null,
  "avatar": "http://gravatar.com/avatar/6163882cbdd07b65079f41cf50e95c52?s=350&d=www.tressapp.co/images/esther.jpg",
  "authentication_token": "meowmeowmeowmeowmeowmeowmeowmeowmeowdf2196d42cb12cabae7b43298",
  "posts": [],
  "most_popular_posts": [],
  "followers": [],
  "following": [],
  "comments": [],
  "posts_count": 0,
  "comments_count": 0,
  "followers_count": 0,
  "following_count": 0,
  "posts_total_likes": 0,
  "posts_liked": [],
  "posts_bookmarked": [],
  "posts_bookmarked_count": 0,
  "created_at": "2016-10-04T10:46:39Z",
  "updated_at": "2016-10-04T10:46:39Z"
}
```

```json
 { 
  "success": true, 
  "digits_auth_id": "444hjsfkszk" 
 }
```

#### HTTP Requests
 - (1) Verify Digits User on Server

    `POST https://tressapi-staging.herokuapp.com/api/v3/verify_digits_account` 

    #### Request Headers
    Hashmap of Auth Headers | (contains different params shown below) Obtained from Digits SDK authenticated response

    Parameter | Description
    --------- | -----------
    X-Auth-Service-Providers  |
    X-Verify-Credentials-Authorization |

    Send the Hashmap of the parameters above as a Request Header


    #### Request Body Parameters

    Parameter | Description
    --------- | -----------
    phone_number | Required. Obtained from Digits SDK authenticated response

If the digits server verification is successful, there are two possible responses:

(1) If there's user with the number and matching digits token, it means the user already has an account on Tress, then you will get the User JSON:

(2) But if there's no matching number or token, you will get a non User JSON with two elements `success` and `digits_auth_id`    

<aside class="notice">
<ol>
  <li>If you get a User JSON object, persist the User on the client including the authentication_token for future user authenticated requests.</li>

  <li>If you get response a non User JSON with two elements `success` and `digits_auth_id`, continue to make the HTTP Request (2)</li>
</ol>

</aside>

 - (2) Create a New Digits User on Server

 ```swift

```

```java

```

    `POST https://tressapi-staging.herokuapp.com/api/v3/digits_users`
    #### Request Body Parameters

    Parameter | Description
    --------- | -----------
    phone_number | Required. Obtained from Digits SDK authenticated response 
    digits_id | Required. Obtained from Digits SDK authenticated response 
    email | Required. User must enter this
    username | Required. User must enter this
    firstname | Required. User must enter this
    lastname | Required. User must enter this
    hair_type_id | Required. User must choose this from dropdown


<aside class="notice">
The above returns User JSON object response.
</aside>



## User Sign In

### Via email
```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "content-type": "application/json"
]
let parameters = ["user": [
    "email": "ea.olatunde@gmail.com",
    "password": "1234567890"
  ]]

```

```java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\n    \"user\": {\n        \"email\": \"oliverakol@gmail.com\",\n        \"password\": \"oliverakol009\"\n    }\n}");
Request request = new Request.Builder()
  .url("https://www.tressapp.co/api/v3/users/sign_in")
  .post(body)
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("content-type", "application/json")
  .build();

```

> A successful sign in request returns JSON structured like this:

```json
{
  "id": 58,
  "email": "example@gmail.com",
  "digits_id": null,
  "username": "monalisa",
  "country_code": null,
  "firstname": null,
  "lastname": null,
  "is_salon": false,
  "fullname": " ",
  "hair_type_id": null,
  "phone_number": null,
  "bio": null,
  "avatar": "http://gravatar.com/avatar/6163882cbdd07b65079f41cf50e95c52?s=350&d=www.tressapp.co/images/esther.jpg",
  "authentication_token": "meowmeowmeowmeowmeowmeowmeowmeowmeowdf2196d42cb12cabae7b43298",
  "posts": [],
  "followers_count": 0,
  "following_count": 0,
  "posts_total_likes": 0,
  "posts_bookmarked_count": 0,
  "created_at": "2016-10-04T10:46:39Z",
  "updated_at": "2016-10-04T10:46:39Z"
}
```

> An unsuccessful sign in request returns JSON structured like this:

```json
{
  "success": false,
  "message": "Error with your email or password"
}
```
#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/users/sign_in`

#### Request Body Parameters

Parameter | Description
--------- | -----------
email | Required
password | Required

<aside class="notice">
Persist the User JSON object on the client including the authentication_token for future user authenticated requests.
</aside>

## User Sign Out

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "authorization": ""
]

var request = NSMutableURLRequest(URL: NSURL(string: "https://tressapi-staging.herokuapp.com/api/v3/users/sign_out")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "DELETE"
request.allHTTPHeaderFields = headers

```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://tressapi-staging.herokuapp.com/api/v3/users/sign_out")
  .delete(null)
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();

Response response = client.newCall(request).execute();

```

> A successful sign out request returns 204 No content

```json

```

> An unsuccessful sign in request returns JSON structured like this:

```json
{
  "success": false,
  "message": "Unauthorised"
}
```
#### HTTP Request

`DELETE https://tressapi-staging.herokuapp.com/api/v3/users/sign_out`

##### Headers

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user who is logging out

<aside class="notice">
Delete all persisted records on client
</aside>

## Change Password

```swift
let headers = [
  "content-type": "multipart/form-data; boundary=---011000010111000001101001",
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "authorization": ""
]
let parameters = [
  [
    "name": "current_password",
    "value": ""
  ],
  [
    "name": "password",
    "value": ""
  ],
  [
    "name": "password_confirmation",
    "value": ""
  ]
]

let boundary = "---011000010111000001101001"

var body = ""
var error: NSError? = nil
for param in parameters {
  let paramName = param["name"]!
  body += "--\(boundary)\r\n"
  body += "Content-Disposition:form-data; name=\"\(paramName)\""
  if let filename = param["fileName"] {
    let contentType = param["content-type"]!
    let fileContent = String(contentsOfFile: filename, encoding: NSUTF8StringEncoding, error: &error)
    if (error != nil) {
      println(error)
    }
    body += "; filename=\"\(filename)\"\r\n"
    body += "Content-Type: \(contentType)\r\n\r\n"
    body += fileContent!
  } else if let paramValue = param["value"] {
    body += "\r\n\r\n\(paramValue)"
  }
}

var request = NSMutableURLRequest(URL: NSURL(string: "https://tressapi-staging.herokuapp.com/api/v3/users/29/update_password")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "PATCH"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData

```

```java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("multipart/form-data; boundary=---011000010111000001101001");
RequestBody body = RequestBody.create(mediaType, "-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"current_password\"\r\n\r\n\r\n-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"password\"\r\n\r\n\r\n-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"password_confirmation\"\r\n\r\n\r\n-----011000010111000001101001--");
Request request = new Request.Builder()
  .url("https://tressapi-staging.herokuapp.com/api/v3/users/29/update_password")
  .patch(body)
  .addHeader("content-type", "multipart/form-data; boundary=---011000010111000001101001")
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();

Response response = client.newCall(request).execute();
```

> A successful request returns JSON structured like this:

```json
{
  "id": 58,
  "email": "example@gmail.com",
  "digits_id": null,
  "username": "monalisa",
  "country_code": null,
  "firstname": null,
  "lastname": null,
  "fullname": " ",
  "hair_type_id": null,
  "phone_number": null,
  "bio": null,
  "avatar": "http://gravatar.com/avatar/6163882cbdd07b65079f41cf50e95c52?s=350&d=www.tressapp.co/images/esther.jpg",
  "authentication_token": "meowmeowmeowmeowmeowmeowmeowmeowmeowdf2196d42cb12cabae7b43298",
  "posts": [],
  "followers_count": 0,
  "following_count": 0,
  "posts_total_likes": 0,
  "posts_liked": [],
  "posts_bookmarked": [],
  "posts_bookmarked_count": 0,
  "created_at": "2016-10-04T10:46:39Z",
  "updated_at": "2016-10-04T10:46:39Z"
}
```

> An unsuccessful request returns JSON structured like this:

```json
{
  "success": false,
  "message": "Wrong password"
}
```
#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/users/<id>/update_password`

##### Headers

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user whose id is on the request path


#### Request Body Parameters

Parameter | Description
--------- | -----------
current_password | Required
password | Required
password_confirmation | Required

<aside class="notice">
Persist the User JSON object on the client including the authentication_token for future user authenticated requests.
</aside>

## Update or Edit User

### Without Avatar Image Upload

```swift
let headers = [
  "content-type": "multipart/form-data; boundary=---011000010111000001101001",
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "authorization": ""
]
let parameters = [
  [
    "name": "hair_type_id",
    "value": "1"
  ]
]

let boundary = "---011000010111000001101001"

var body = ""
var error: NSError? = nil
for param in parameters {
  let paramName = param["name"]!
  body += "--\(boundary)\r\n"
  body += "Content-Disposition:form-data; name=\"\(paramName)\""
  if let filename = param["fileName"] {
    let contentType = param["content-type"]!
    let fileContent = String(contentsOfFile: filename, encoding: NSUTF8StringEncoding, error: &error)
    if (error != nil) {
      println(error)
    }
    body += "; filename=\"\(filename)\"\r\n"
    body += "Content-Type: \(contentType)\r\n\r\n"
    body += fileContent!
  } else if let paramValue = param["value"] {
    body += "\r\n\r\n\(paramValue)"
  }
}

```

```java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("multipart/form-data; boundary=---011000010111000001101001");
RequestBody body = RequestBody.create(mediaType, "-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"hair_type_id\"\r\n\r\n1\r\n-----011000010111000001101001--");
Request request = new Request.Builder()
  .url("https://stage.tressapp.co/api/v3/users/95")
  .patch(body)
  .addHeader("content-type", "multipart/form-data; boundary=---011000010111000001101001")
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();

Response response = client.newCall(request).execute();

```

> A successful user update request returns JSON structured like this:

```json
{
  "id": 58,
  "email": "example@gmail.com",
  "digits_id": null,
  "username": "monalisa",
  "country_code": null,
  "firstname": null,
  "lastname": null,
  "fullname": " ",
  "hair_type_id": null,
  "phone_number": null,
  "bio": null,
  "avatar": "http://gravatar.com/avatar/6163882cbdd07b65079f41cf50e95c52?s=350&d=www.tressapp.co/images/esther.jpg",
  "authentication_token": "meowmeowmeowmeowmeowmeowmeowmeowmeowdf2196d42cb12cabae7b43298",
  "posts": [],
  "most_popular_posts": [],
  "followers": [],
  "following": [],
  "comments": [],
  "posts_count": 0,
  "comments_count": 0,
  "followers_count": 0,
  "following_count": 0,
  "posts_total_likes": 0,
  "posts_liked": [],
  "posts_bookmarked": [],
  "posts_bookmarked_count": 0,
  "created_at": "2016-10-04T10:46:39Z",
  "updated_at": "2016-10-04T10:46:39Z"
}
```
#### HTTP Request

`PATCH https://tressapi-staging.herokuapp.com/api/v3/users/<id>`

#### Request Parameters

##### Path

Parameter | Description
--------- | -----------
id | Required. This is the id of the user


##### Headers

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user whose id is on the request path

##### Body

Parameter | Description
--------- | -----------
hair_type_id | Hair Type ID
email | Email address
firstname | Firstname
lastname | Lastname
username | username



### With Avatar Image Upload

```swift
let headers = [
  "content-type": "multipart/form-data; boundary=---011000010111000001101001",
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "authorization": ""
]
let parameters = [
  [
    "name": "user[avatar]",
    "fileName": ["0": []]
  ]
]

let boundary = "---011000010111000001101001"

var body = ""
var error: NSError? = nil
for param in parameters {
  let paramName = param["name"]!
  body += "--\(boundary)\r\n"
  body += "Content-Disposition:form-data; name=\"\(paramName)\""
  if let filename = param["fileName"] {
    let contentType = param["content-type"]!
    let fileContent = String(contentsOfFile: filename, encoding: NSUTF8StringEncoding, error: &error)
    if (error != nil) {
      println(error)
    }
    body += "; filename=\"\(filename)\"\r\n"
    body += "Content-Type: \(contentType)\r\n\r\n"
    body += fileContent!
  } else if let paramValue = param["value"] {
    body += "\r\n\r\n\(paramValue)"
  }
}

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/users/53")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "PATCH"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData

```

```java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("multipart/form-data; boundary=---011000010111000001101001");
RequestBody body = RequestBody.create(mediaType, "-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"user[avatar]\"; filename=\"[object Object]\"\r\nContent-Type: false\r\n\r\n\r\n-----011000010111000001101001--");
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/users/53")
  .patch(body)
  .addHeader("content-type", "multipart/form-data; boundary=---011000010111000001101001")
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();

Response response = client.newCall(request).execute();

```

> A successful user update request returns JSON structured like this:

```json
{
  "id": 58,
  "email": "example@gmail.com",
  "digits_id": null,
  "username": "monalisa",
  "country_code": null,
  "firstname": null,
  "lastname": null,
  "fullname": " ",
  "hair_type_id": null,
  "phone_number": null,
  "bio": null,
  "avatar": "http://gravatar.com/avatar/6163882cbdd07b65079f41cf50e95c52?s=350&d=www.tressapp.co/images/esther.jpg",
  "authentication_token": "meowmeowmeowmeowmeowmeowmeowmeowmeowdf2196d42cb12cabae7b43298",
  "posts": [],
  "most_popular_posts": [],
  "followers": [],
  "following": [],
  "comments": [],
  "posts_count": 0,
  "comments_count": 0,
  "followers_count": 0,
  "following_count": 0,
  "posts_total_likes": 0,
  "posts_liked": [],
  "posts_bookmarked": [],
  "posts_bookmarked_count": 0,
  "created_at": "2016-10-04T10:46:39Z",
  "updated_at": "2016-10-04T10:46:39Z"
}
```
#### HTTP Request

`PATCH https://tressapi-staging.herokuapp.com/api/v3/users/<id>`

#### Request Parameters

##### Path

Parameter | Description
--------- | -----------
id | Required. This is the id of the user


##### Headers

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user whose id is on the request path

##### Body

Parameter | Description
--------- | -----------
avatar | uploaded image filename
hair_type_id | Hair Type id
email | Email address
firstname | Firstname
lastname | Lastname
username | Username

<aside class="notice">
Persist the User JSON object on the client including the authentication_token for future user authenticated requests.
</aside>

## Create Salon user account/Update user if is_salon is true
A salon profile is essentially a User Account with a salon object relationship. The process to create a salon account is the same as higlighted above in all these steps. The distinction is in the additional workflow of adding an `is_salon` boolean param to the user object. If the `is_salon` is `true`. Then there will be additional parameters to be filled when updating the user's profile as follows:

```swift
let headers = [
  "content-type": "multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW",
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "authorization": "",
]
let parameters = [
  [
    "name": "is_salon",
    "value": "true"
  ],
  [
    "name": "salon_name",
    "value": "CoCo HairTalk Salon"
  ],
  [
    "name": "salon_location",
    "value": "Dzorwulu, Accra, Greater Accra Region, Ghana"
  ],
  [
    "name": "salon_longitude",
    "value": "-0.203367"
  ],
  [
    "name": "salon_latitude",
    "value": "5.611593199999999"
  ],
  [
    "name": "salon_cover_image",
    "fileName": "576A5648.jpg"
  ],
  [
    "name": "salon_website_link",
    "value": "www.cocohairtalk.gh"
  ],
  [
    "name": "avatar",
    "fileName": "IMG-20161219-WA0000.jpg"
  ],
  [
    "name": "bio",
    "value": "I'm a hair doctor and specialist"
  ],
  [
    "name": "phone_number",
    "value": "+233231873639"
  ],
  [
    "name": "hair_type_id",
    "value": "2"
  ]
]

let boundary = "----WebKitFormBoundary7MA4YWxkTrZu0gW"

var body = ""
var error: NSError? = nil
for param in parameters {
  let paramName = param["name"]!
  body += "--\(boundary)\r\n"
  body += "Content-Disposition:form-data; name=\"\(paramName)\""
  if let filename = param["fileName"] {
    let contentType = param["content-type"]!
    let fileContent = String(contentsOfFile: filename, encoding: String.Encoding.utf8)
    if (error != nil) {
      print(error)
    }
    body += "; filename=\"\(filename)\"\r\n"
    body += "Content-Type: \(contentType)\r\n\r\n"
    body += fileContent
  } else if let paramValue = param["value"] {
    body += "\r\n\r\n\(paramValue)"
  }
}

let request = NSMutableURLRequest(url: NSURL(string: "http://localhost:5000/api/v3/users/67")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "PATCH"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()


```

```java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW");
RequestBody body = RequestBody.create(mediaType, "------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"is_salon\"\r\n\r\ntrue\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"salon_name\"\r\n\r\nCoCo HairTalk Salon\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"salon_location\"\r\n\r\nDzorwulu, Accra, Greater Accra Region, Ghana\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"salon_longitude\"\r\n\r\n-0.203367\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"salon_latitude\"\r\n\r\n5.611593199999999\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"salon_cover_image\"; filename=\"576A5648.jpg\"\r\nContent-Type: image/jpeg\r\n\r\n\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"salon_website_link\"\r\n\r\nwww.cocohairtalk.gh\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"avatar\"; filename=\"IMG-20161219-WA0000.jpg\"\r\nContent-Type: image/jpeg\r\n\r\n\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"bio\"\r\n\r\nI'm a hair doctor and specialist\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"phone_number\"\r\n\r\n+233231873639\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"hair_type_id\"\r\n\r\n2\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW--");
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/users/67")
  .patch(body)
  .addHeader("content-type", "multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW")
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();

Response response = client.newCall(request).execute();

```

> A successful salon user update request returns JSON structured like this:

```json
{
  "id": 58,
  "email": "example@gmail.com",
  "digits_id": null,
  "username": "monalisa",
  "country_code": null,
  "firstname": null,
  "lastname": null,
  "fullname": " ",
  "hair_type_id": null,
  "phone_number": null,
  "is_salon": true,
  "salon_data": {
    "id": 11315,
    "name": "Anowas Parlour",
    "location": "East Legon, Accra, Greater Accra Region, Ghana",
    "latitude": 5.6378865,
    "longitude": -0.1612029,
    "website_link": "",
    "user_id": 2,
    "cover_image_url": "/cover_images/medium/missing.png",
    "email": "priscahazel@gmail.com"
  },  
  "bio": "best stylist",
  "avatar": "http://gravatar.com/avatar/6163882cbdd07b65079f41cf50e95c52?s=350&d=www.tressapp.co/images/esther.jpg",
  "authentication_token": "meowmeowmeowmeowmeowmeowmeowmeowmeowdf2196d42cb12cabae7b43298",
  "posts": [],
  "most_popular_posts": [],
  "followers": [],
  "following": [],
  "comments": [],
  "posts_count": 0,
  "comments_count": 0,
  "followers_count": 0,
  "following_count": 0,
  "posts_total_likes": 0,
  "posts_liked": [],
  "posts_bookmarked": [],
  "posts_bookmarked_count": 0,
  "created_at": "2016-10-04T10:46:39Z",
  "updated_at": "2016-10-04T10:46:39Z"
}
```
#### HTTP Request

`PATCH https://tressapi-staging.herokuapp.com/api/v3/users/<id>`

#### Request Parameters

##### Path

Parameter | Description
--------- | -----------
id | Required. This is the id of the user


##### Headers

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user whose id is on the request path

##### Body

Parameter (all required) | Description
--------- | -----------
is_salon | is_salon params
avatar | uploaded image filename
hair_type_id | Hair Type id
email | Email address
firstname | Firstname
lastname | Lastname
username | Username
salon_website_link | Username
salon_name | Salon Name
salon_location | Salon Location (Google Place Autocomplete)
salon_longitude | Salon Longitude (Google Place Autocomplete)
salon_latitude | Salon Latitude (Google Place Autocomplete)
phone_number | Phone Number
salon_cover_image | Salon cover image
bio | Salon's bio


<aside class="notice">
Please note that, going all user object now has an `is_salon` boolean attribute that is false by default. It is the process of switching or creating a salon profile that changes it to true.
</aside>

## Reset Password

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "content-type": "application/json"
]
let parameters = ["user": ["email": "example@gmail.com"]]

let postData = NSJSONSerialization.dataWithJSONObject(parameters, options: nil, error: nil)

var request = NSMutableURLRequest(URL: NSURL(string: "https://tressapi-staging.herokuapp.com/api/v3/users/password")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "POST"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData
```

```java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\n    \"user\": {\n        \"email\": \"example@gmail.com\"\n    }\n}");
Request request = new Request.Builder()
  .url("https://tressapi-staging.herokuapp.com/api/v3/users/password")
  .post(body)
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("content-type", "application/json")
  .build();

Response response = client.newCall(request).execute();
```

> A successful reset password returns JSON structured like this:

```json
{
  "success": true,
  "status": 200,
  "email": "ea.olatunde@gmail.com"
}
```

> An unsuccessful reset password returns JSON structured like this:

```json
{
  "success": false,
  "status": 200,
  "message": "Email not found"
}
```

This endpoint helps a user resets their password.

#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/users/password`

#### Body Parameters

Parameter | Description
--------- | -----------
email | The email of the user to reset the password


## Get Users


```swift

```

```java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("multipart/form-data; boundary=---011000010111000001101001");
Request request = new Request.Builder()
  .url("https://tressapi-staging.herokuapp.com/api/v3/users")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .build();

```

> All users request returns JSON structured like this:

```json
{
  "users": [
    {
      "id": 25,
      "username": "Obi",
      "avatar": "http://gravatar.com/avatar/2f1a045b41776275e79517ad7ffc8ab9?s=350&d=www.tressapp.co/images/esther.jpg",
      "fullname": " "
    },
    {
      "id": 18,
      "username": "gerald",
      "avatar": "http://gravatar.com/avatar/f297a7254188da5e2741f654724a4fc3?s=350&d=www.tressapp.co/images/esther.jpg",
      "fullname": " "
    },
    {
      "id": 20,
      "username": "akosua.kesewa",
      "avatar": "http://gravatar.com/avatar/063e87f56fda4c58d02e9f27c35488c9?s=350&d=www.tressapp.co/images/esther.jpg",
      "fullname": " "
    },
    {
      "id": 22,
      "username": "Tress",
      "avatar": "http://gravatar.com/avatar/1521f4e439ec418c8f71a56ad9470492?s=350&d=www.tressapp.co/images/esther.jpg",
      "fullname": " "
    },
    {
      "id": 15,
      "username": "product lead",
      "avatar": "https://s3.amazonaws.com/tress-api-staging/users/avatars/000/000/015/small/1449750973685.?1449751040",
      "fullname": " "
    },
    {
      "id": 23,
      "username": "mseolatunde",
      "avatar": "https://s3.amazonaws.com/tress-api-staging/users/avatars/000/000/023/small/imageName\"_.?1454660075",
      "fullname": "Bolanle Oni"
    },
    {
      "id": 52,
      "username": "Mo",
      "avatar": "http://gravatar.com/avatar/ace2dbcbae76d8e11e6829453ff475ed?s=350&d=www.tressapp.co/images/esther.jpg",
      "fullname": "Moji Shola"
    },
    {
      "id": 53,
      "username": "Cascas",
      "avatar": "http://gravatar.com/avatar/7b0aecbc91e1bf7b4af2d2cac9d181b8?s=350&d=www.tressapp.co/images/esther.jpg",
      "fullname": "Cass Sarfo"
    },
    {
      "id": 55,
      "username": "Morenike",
      "avatar": "http://gravatar.com/avatar/8062e42ee074b6dbb7b1091f44dc70c6?s=350&d=www.tressapp.co/images/esther.jpg",
      "fullname": "More Nike"
    },
    {
      "id": 56,
      "username": "Princess",
      "avatar": "https://s3.amazonaws.com/tress-api-staging/users/avatars/000/000/056/small/avatar_name\"_.?1471268402",
      "fullname": "Princess Sarfo"
    },
    {
      "id": 19,
      "username": "esther2",
      "avatar": "https://s3.amazonaws.com/tress-api-staging/users/avatars/000/000/019/small/1449208576522.?1454660074",
      "fullname": "1234 Olatunde"
    },
    {
      "id": 29,
      "username": "CoCo",
      "avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "fullname": "Shola Lewis"
    },
    {
      "id": 24,
      "username": "jjhuj",
      "avatar": "https://s3.amazonaws.com/tress-api-staging/users/avatars/000/000/024/small/avatar_name\"_.?1454660076",
      "fullname": "Hellokjhh Jhjn"
    },
    {
      "id": 40,
      "username": "esther222",
      "avatar": "https://s3.amazonaws.com/tress-api-staging/users/avatars/000/000/040/small/avatar_name\"_.?1459043911",
      "fullname": "Bolanle  Lewis"
    },
    {
      "id": 42,
      "username": "bolanlemi",
      "avatar": "https://s3.amazonaws.com/tress-api-staging/users/avatars/000/000/042/small/avatar_name\"_.?1460374996",
      "fullname": "Gerald Pharin"
    },
    {
      "id": 54,
      "username": "Fbuser",
      "avatar": "https://s3.amazonaws.com/tress-api-staging/users/avatars/000/000/054/small/picture.?1466030510",
      "fullname": "Open Graph"
    },
    {
      "id": 58,
      "username": "monalisa",
      "avatar": "http://gravatar.com/avatar/6163882cbdd07b65079f41cf50e95c52?s=350&d=www.tressapp.co/images/esther.jpg",
      "fullname": " "
    }
  ],
  "meta": {
    "pagination": {
      "per_page": 25,
      "total_pages": 1,
      "total_objects": 17
    }
  }
}
```

This shows the various ways you can retrieve users from the server.

### By Pagination

`GET https://tressapi-staging.herokuapp.com/api/v3/users?per_page=25,page=1`

This endpoint retrieves all users by pagination, 25 at a time.

#### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
per_page | 25 | Numbers of users to return at a time
page | 1 | Page number.

### Search by Username, Firstname or Lastname

`GET https://tressapi-staging.herokuapp.com/api/v3/users?search=bola,per_page=25,page=1`

This endpoint retrieves all users whose username, firstname or lastname match the search query param by pagination, 25 at a time.

#### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
search |  | Username, Firstname or Lastname
per_page | 25 | Numbers of users to return at a time
page | 1 | Page number.

<aside class="success">
Remember — Same Users JSONArray Response as above
</aside>

### Search by Username Only 
NB: Useful for @mentions users query

`GET https://tressapi-staging.herokuapp.com/api/v3/users?search=bola,per_page=25,page=1`

This endpoint retrieves all users whose username, firstname or lastname match the search query param by pagination, 25 at a time.

#### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
search |  | Username, Firstname or Lastname
per_page | 25 | Numbers of users to return at a time
page | 1 | Page number.

<aside class="success">
Remember — Same Users JSONArray Response as above
</aside>

## Get a Specific User

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
]

var request = NSMutableURLRequest(URL: NSURL(string: "https://tressapi-staging.herokuapp.com/api/v3/users/18731")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://tressapi-staging.herokuapp.com/api/v3/users/18731")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .build();

Response response = client.newCall(request).execute();
```

> The above command returns JSON structured like this:

```json
{
  "id": 18731,
  "username": "syl",
  "firstname": "Sylvia",
  "lastname": "Gyabaah",
  "fullname": "Sylvia Gyabaah",
  "bio": null,
  "avatar": "http://gravatar.com/avatar/698fe0523825f063c4af68ded1ea7691?s=350&d=www.tressapp.co/images/esther.jpg",
  "country_code": null,
  "hair_type_id": null,
  "phone_number": null,
  "posts": [],
  "most_popular_posts": [],
  "followers": [
    318,
    313,
    319
  ],
  "following": [
    1479,
    263,
    12673,
    10127,
    12586,
    319,
    318,
    313,
    98
  ],
  "comments": [],
  "posts_count": 0,
  "comments_count": 0,
  "followers_count": 3,
  "following_count": 9,
  "posts_total_likes": 0,
  "posts_liked": [
    2791,
    2878,
    2906,
    2980,
    2984,
    3423,
    3392
  ],
  "posts_bookmarked": [],
  "posts_bookmarked_count": 0,
  "verified": false,
  "created_at": "2016-07-04T18:55:51Z",
  "updated_at": "2016-08-17T07:54:42Z"
}
```

This endpoint retrieves a specific user.

### By ID

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<id>`

#### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the user to retrieve

### By Username

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<username>`

#### URL Parameters

Parameter | Description
--------- | -----------
username | The username of the user to retrieve



## Get Recommended Users to Follow

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "authorization": ""
]

var request = NSMutableURLRequest(URL: NSURL(string: "https://tressapi-staging.herokuapp.com/api/v3/suggestions?per_page=25%2Cpage%3D1")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData
```

```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
  .url("https://tressapi-staging.herokuapp.com/api/v3/suggestions?per_page=25%2Cpage%3D1")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();

Response response = client.newCall(request).execute();
```

> The above command returns JSON structured like this:

```json
{
  "top users": [
    {
      "id": 319,
      "username": "Beauty",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/000/319/small/1454594435048.?1454662651",
      "fullname": "Chique Laddo",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/002/484/medium/image_name%22_.?1466247733",
          "id": 2484
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/001/973/medium/image_name%22_.?1464095649",
          "id": 1973
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/000/375/medium/1455109251590.?1455110137",
          "id": 375
        }
      ],
      "popularity": 321.25
    },
    {
      "id": 20659,
      "username": "Onifaari",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/020/659/small/picture.?1468059388",
      "fullname": "Shade Oni",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/005/588/medium/image_name%22_.?1469633825",
          "id": 5588
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/006/190/medium/image_name%22_.?1470142303",
          "id": 6190
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/003/779/medium/image_name%22_.?1468063142",
          "id": 3779
        }
      ],
      "popularity": 252.75
    },
    {
      "id": 10930,
      "username": "Olayinka11",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/010/930/small/avatar_name\"_.?1467280654",
      "fullname": "Olayinka Hassan",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/364/medium/image_name%22_.?1468708239",
          "id": 4364
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/363/medium/image_name%22_.?1468707950",
          "id": 4363
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/002/737/medium/image_name%22_.?1466754293",
          "id": 2737
        }
      ],
      "popularity": 179.8125
    },
    {
      "id": 15489,
      "username": "_lhizzle",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/015/489/small/picture.?1467151688",
      "fullname": " Oyinlola Makinde",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/564/medium/image_name%22_.?1468925456",
          "id": 4564
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/322/medium/image_name%22_.?1468676422",
          "id": 4322
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/321/medium/image_name%22_.?1468676420",
          "id": 4321
        }
      ],
      "popularity": 179.333333333333
    },
    {
      "id": 34802,
      "username": "MissMalaikaGh",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/034/802/small/avatar_name\"_.?1470424409",
      "fullname": "Miss Malaika Gh",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/006/546/medium/image_name%22_.?1470414575",
          "id": 6546
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/006/403/medium/image_name%22_.?1470334072",
          "id": 6403
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/006/411/medium/image_name%22_.?1470337978",
          "id": 6411
        }
      ],
      "popularity": 141.741379310345
    },
    {
      "id": 17510,
      "username": "Prettyjeny",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/017/510/small/picture.?1467397047",
      "fullname": "Jennifer Kelechi",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/003/392/medium/image_name%22_.?1467618101",
          "id": 3392
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/003/245/medium/image_name%22_.?1467445786",
          "id": 3245
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/172/medium/image_name%22_.?1468492708",
          "id": 4172
        }
      ],
      "popularity": 123.2
    },
    {
      "id": 318,
      "username": "Aina",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/000/318/small/avatar_name\"_.?1468355069",
      "fullname": "Aina  Gray",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/000/950/medium/image_name%22_.?1458347695",
          "id": 950
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/000/350/medium/1454588277094.?1454662301",
          "id": 350
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/000/417/medium/image_name%22_.?1455541820",
          "id": 417
        }
      ],
      "popularity": 122.25
    },
    {
      "id": 3691,
      "username": "Hajia4real",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/003/691/small/avatar_name\"_.?1469193226",
      "fullname": "Charity Yeboah",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/005/310/medium/image_name%22_.?1469436844",
          "id": 5310
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/005/007/medium/image_name%22_.?1469193640",
          "id": 5007
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/005/006/medium/image_name%22_.?1469192248",
          "id": 5006
        }
      ],
      "popularity": 119.727272727273
    },
    {
      "id": 6391,
      "username": "AnAfricanCityTv",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/006/391/small/avatar_name\"_.?1463655267",
      "fullname": "An African City",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/003/650/medium/image_name%22_.?1467910027",
          "id": 3650
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/005/803/medium/image_name%22_.?1469816783",
          "id": 5803
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/002/300/medium/image_name%22_.?1465574437",
          "id": 2300
        }
      ],
      "popularity": 114.222222222222
    },
    {
      "id": 42195,
      "username": "Meritned",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/042/195/small/avatar_name\"_.?1472324382",
      "fullname": "Merit Nwaneri",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/009/513/medium/image_name%22_.?1473084712",
          "id": 9513
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/008/489/medium/image_name%22_.?1472325285",
          "id": 8489
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/010/056/medium/image_name%22_.?1473883985",
          "id": 10056
        }
      ],
      "popularity": 107.714285714286
    },
    {
      "id": 24379,
      "username": "E.Bee",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/024/379/small/avatar_name\"_.?1468850976",
      "fullname": "Reuelah Bee",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/525/medium/image_name%22_.?1468854833",
          "id": 4525
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/514/medium/image_name%22_.?1468848824",
          "id": 4514
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/010/515/medium/image_name%22_.?1474751136",
          "id": 10515
        }
      ],
      "popularity": 107.333333333333
    },
    {
      "id": 10933,
      "username": "Oyiwosa",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/010/933/small/avatar_name\"_.?1466706231",
      "fullname": "Princess  Gift",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/003/564/medium/image_name%22_.?1467807827",
          "id": 3564
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/003/452/medium/image_name%22_.?1467704406",
          "id": 3452
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/187/medium/image_name%22_.?1468507651",
          "id": 4187
        }
      ],
      "popularity": 106.416666666667
    },
    {
      "id": 8067,
      "username": "Ezi",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/008/067/small/avatar_name\"_.?1473928772",
      "fullname": "Ezi Ayesu",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/003/785/medium/image_name%22_.?1468071660",
          "id": 3785
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/010/041/medium/image_name%22_.?1473879293",
          "id": 10041
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/002/233/medium/image_name%22_.?1465373483",
          "id": 2233
        }
      ],
      "popularity": 103.666666666667
    },
    {
      "id": 128,
      "username": "Daaviyawa",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/000/128/small/1447875460237.?1454662589",
      "fullname": "Ellen Tsetse",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/003/573/medium/image_name%22_.?1467820137",
          "id": 3573
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/003/449/medium/image_name%22_.?1467702243",
          "id": 3449
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/006/866/medium/image_name%22_.?1470651041",
          "id": 6866
        }
      ],
      "popularity": 94.4158415841584
    },
    {
      "id": 7772,
      "username": "Shola",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/007/772/small/avatar_name\"_.?1467896402",
      "fullname": "Sholastica Jones",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/002/894/medium/image_name%22_.?1467028395",
          "id": 2894
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/007/589/medium/image_name%22_.?1471295809",
          "id": 7589
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/005/819/medium/image_name%22_.?1469819388",
          "id": 5819
        }
      ],
      "popularity": 89.0588235294118
    },
    {
      "id": 26758,
      "username": "Cicipearls",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/026/758/small/avatar_name\"_.?1469085890",
      "fullname": "Cynthia Eires",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/941/medium/image_name%22_.?1469129684",
          "id": 4941
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/865/medium/image_name%22_.?1469086793",
          "id": 4865
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/005/353/medium/image_name%22_.?1469462537",
          "id": 5353
        }
      ],
      "popularity": 81.6666666666667
    },
    {
      "id": 828,
      "username": "Pat",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/000/828/small/avatar_name\"_.?1465929173",
      "fullname": "Pat Ladyp",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/002/624/medium/image_name%22_.?1466597371",
          "id": 2624
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/002/850/medium/image_name%22_.?1466949684",
          "id": 2850
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/001/673/medium/image_name%22_.?1462221721",
          "id": 1673
        }
      ],
      "popularity": 78.9130434782609
    },
    {
      "id": 37682,
      "username": "Lissyswissy",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/037/682/small/avatar_name\"_.?1471083213",
      "fullname": "Liss Okoh",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/007/328/medium/image_name%22_.?1471084194",
          "id": 7328
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/007/705/medium/image_name%22_.?1471381577",
          "id": 7705
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/007/327/medium/image_name%22_.?1471083404",
          "id": 7327
        }
      ],
      "popularity": 78.3333333333333
    },
    {
      "id": 24174,
      "username": "Ebony124",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/024/174/small/picture.?1468805394",
      "fullname": "Princess Nkem",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/484/medium/image_name%22_.?1468824413",
          "id": 4484
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/485/medium/image_name%22_.?1468824490",
          "id": 4485
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/481/medium/image_name%22_.?1468805992",
          "id": 4481
        }
      ],
      "popularity": 72.3333333333333
    },
    {
      "id": 25600,
      "username": "Gg",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/025/600/small/avatar_name\"_.?1468936580",
      "fullname": "Adeola Morenikeji",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/636/medium/image_name%22_.?1468938574",
          "id": 4636
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/630/medium/image_name%22_.?1468938113",
          "id": 4630
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/628/medium/image_name%22_.?1468937509",
          "id": 4628
        }
      ],
      "popularity": 70.75
    },
    {
      "id": 31609,
      "username": "Tekyiwaa",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/031/609/small/avatar_name\"_.?1469800631",
      "fullname": "Sandra Mensah-Arthur ",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/005/944/medium/image_name%22_.?1469916111",
          "id": 5944
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/006/409/medium/image_name%22_.?1470335860",
          "id": 6409
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/008/022/medium/image_name%22_.?1471771145",
          "id": 8022
        }
      ],
      "popularity": 67.78125
    },
    {
      "id": 21628,
      "username": "Hothot",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/021/628/small/avatar_name\"_.?1469394491",
      "fullname": "Millicent Saya",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/003/969/medium/image_name%22_.?1468293725",
          "id": 3969
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/195/medium/image_name%22_.?1468520429",
          "id": 4195
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/006/754/medium/image_name%22_.?1470544070",
          "id": 6754
        }
      ],
      "popularity": 62
    },
    {
      "id": 36928,
      "username": "womaninthejungle",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/036/928/small/avatar_name\"_.?1470912716",
      "fullname": "Wunmi Akinlagun",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/007/120/medium/image_name%22_.?1470832428",
          "id": 7120
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/007/179/medium/image_name%22_.?1470912429",
          "id": 7179
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/007/178/medium/image_name%22_.?1470912297",
          "id": 7178
        }
      ],
      "popularity": 58.3333333333333
    },
    {
      "id": 18967,
      "username": "Mzz_EpHyA",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/018/967/small/avatar_name\"_.?1468404586",
      "fullname": "Natalia Dassah",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/058/medium/image_name%22_.?1468403645",
          "id": 4058
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/003/936/medium/image_name%22_.?1468247398",
          "id": 3936
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/004/059/medium/image_name%22_.?1468404130",
          "id": 4059
        }
      ],
      "popularity": 57.5
    },
    {
      "id": 39899,
      "username": "Tee55",
      "avatar": "https://s3.amazonaws.com/tress-api-production/users/avatars/000/039/899/small/avatar_name\"_.?1471630733",
      "fullname": "Tina Paul",
      "most_popular_posts": [
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/008/381/medium/image_name%22_.?1472212381",
          "id": 8381
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/008/106/medium/image_name%22_.?1471877334",
          "id": 8106
        },
        {
          "image": "https://s3.amazonaws.com/tress-api-production/posts/images/000/008/025/medium/image_name%22_.?1471775085",
          "id": 8025
        }
      ],
      "popularity": 56.6923076923077
    }
  ],
  "meta": {
    "pagination": {
      "per_page": 25,
      "total_pages": 36,
      "total_objects": 896
    }
  }
}
```

This endpoint retrieves suggested/recommended top users and their top 3 posts for users to follow.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/suggestions?per_page=25,page=1`

##### Headers

`Authorization: xxxxxxxxxxxxxxxxxx8790730598790`

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user whose is making the request

#### Query Parameters

For pagination and endless scrolling

Parameter | Default | Description
--------- | ------- | -----------
per_page | 25 | Numbers of objects to return at a time
page | 1 | Page number.

## Follow a User

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "authorization": ""
]

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/users/solapemi/links/following/70")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "POST"
request.allHTTPHeaderFields = headers


```

```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/users/solapemi/links/following/ronketinker")
  .post(null)
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();


Response response = client.newCall(request).execute();
```

> A successful follow request returns:


```http
204 No Content
```

> An unsuccessful follow request (if the user is already being followed) returns:


```http
304 Not Modified
```

This endpoint creates a follow relationship between 2 users.

#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/users/<followee_id_or_username>/links/following/<followed_id>`

##### Headers

`Authorization: xxxxxxxxxxxxxxxxxx8790730598790`

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user who is making the request

#### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
followee_id_or_username | Required. This is id or username of the user who is making the follow request
followed_id | Required. This is id of the user who is being followed

## UnFollow a User

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "authorization": ""
]

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/users/solapemi/links/following/70")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "DELETE"
request.allHTTPHeaderFields = headers


```

```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/users/solapemi/links/following/ronketinker")
  .delete(null)
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();


Response response = client.newCall(request).execute();
```

> A successful unfollow request returns:


```http
204 No Content
```

This endpoint creates a follow relationship between 2 users.

#### HTTP Request

`DELETE https://tressapi-staging.herokuapp.com/api/v3/users/<followee_id_or_username>/links/following/<followed_id>`

##### Headers

`Authorization: xxxxxxxxxxxxxxxxxx8790730598790`

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user who is making the request

#### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
followee_id_or_username | Required. This is id or username of the user who is making the follow request
followed_id | Required. This is id of the user who is being followed

## Get List of Following (Users)

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
]

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/users/solapemi/links/following")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData


```

```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/users/solapemi/links/following")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .build();

Response response = client.newCall(request).execute();
```

> The above command returns the JSON structure below:


```json
{
  "following": [
    {
      "id": 70,
      "username": "RonkeTinker",
      "avatar": "http://gravatar.com/avatar/291f32bb9dca7e5fee2ed32fa05877ea?s=350&d=www.tressapp.co/images/esther.jpg",
      "fullname": " "
    },
    {
      "id": 67,
      "username": "ronke",
      "avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "fullname": " "
    }
  ]
}
```

This endpoint retrieves a list of users a user is following.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<id_or_username>/links/following`


#### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
id_or_username | Required. This is id or username of the user

## Get List of Followers (Users)

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
]

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/users/solapemi/links/followers")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData


```

```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/users/solapemi/links/followers")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .build();

Response response = client.newCall(request).execute();
```

> The above command returns the JSON structure below:


```json
{
  "followers": [
    {
      "id": 70,
      "username": "RonkeTinker",
      "avatar": "http://gravatar.com/avatar/291f32bb9dca7e5fee2ed32fa05877ea?s=350&d=www.tressapp.co/images/esther.jpg",
      "fullname": " "
    },
    {
      "id": 67,
      "username": "ronke",
      "avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "fullname": " "
    }
  ]
}
```

This endpoint retrieves a list of followers a user has.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<id_or_username>/links/followers`


#### URL Parameters


Parameter | Default | Description
--------- | ------- | -----------
id_or_username | Required. This is id or username of the user


## User's IDs Lists
Endpoints in this section retreived IDs in JSONArray format


```swift

```

```java

```

> The above commands returns JSONArray of IDs structure below:


```json
[
  67,
  72,
  70
]

```
### User's Post Bookmarked IDs

This endpoint retrieves IDs of posts a user has bookmarked.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<id_or_username>/bookmarked_posts_ids/`

#### Header Parameters

Parameter | Default | Description
--------- | ------- | -----------
Authorization | Required. authentication_token of the user

#### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
id_or_username | Required. This is id or username of the user

### User's Following IDs

This endpoint retrieves IDs of users a user has followed.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<id_or_username>/following_ids/`

#### Header Parameters

Parameter | Default | Description
--------- | ------- | -----------
Authorization | Required. authentication_token of the user

#### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
id_or_username | Required. This is id or username of the user

### User's Post Liked IDs

This endpoint retrieves IDs of posts a user has liked.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<id_or_username>/liked_posts_ids/`

#### Header Parameters

Parameter | Default | Description
--------- | ------- | -----------
Authorization | Required. authentication_token of the user

#### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
id_or_username | Required. This is id or username of the user

### User's Question Liked IDs

This endpoint retrieves IDs of questions a user has liked.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<id_or_username>/liked_questions_ids/`

#### Header Parameters

Parameter | Default | Description
--------- | ------- | -----------
Authorization | Required. authentication_token of the user

#### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
id_or_username | Required. This is id or username of the user

### User's Answer's Upvoted IDs

This endpoint retrieves IDs of answers a user has upvoted.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<id_or_username>/upvoted_answers_ids/`

#### Header Parameters

Parameter | Default | Description
--------- | ------- | -----------
Authorization | Required. authentication_token of the user

#### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
id_or_username | Required. This is id or username of the user

### User's Answer's Downvoted IDs

This endpoint retrieves IDs of answers a user has downvoted.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<id_or_username>/downvoted_answers_ids/`

#### Header Parameters

Parameter | Default | Description
--------- | ------- | -----------
Authorization | Required. authentication_token of the user

#### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
id_or_username | Required. This is id or username of the user

### User's HairTips Bookmarked IDs

This endpoint retrieves IDs of hair tips a user has bookmarked.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<id_or_username>/bookmarked_hair_tips/`

#### Header Parameters

Parameter | Default | Description
--------- | ------- | -----------
Authorization | Required. authentication_token of the user

#### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
id_or_username | Required. This is id or username of the user

## User's Social Media Friends

The endpoints in this section retrieves a list of users on Tress that have matched with a user's Facebook, Digits & Instagram friends.


```swift

```

```java

```

> The above command returns the JSON structure below:


```json
{
  "users": [],
  "meta": {
    "pagination": {
      "per_page": 0,
      "total_pages": 0,
      "total_objects": 0
    }
  }
}

```

### Facebook Friends
This endpoint retrieves a list of users on Tress that have matched with a user's Facebook friends.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/v3/users/<id_or_username>/friends?facebook_ids=<fbId>,<fbId>`

#### Header Parameters

Parameter | Default | Description
--------- | ------- | -----------
Authorization | Required. authentication_token of the user

#### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
id_or_username | Required. This is id or username of the user
fbId| Required. Facebook Id, can be more than one, seperated by commas

### Instagram Friends
This endpoint retrieves a list of users on Tress that have matched with a user's Instagram friends.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/v3/users/<id_or_username>/friends?instagram_ids=<instagram_id>,<instagram_id>`

#### Header Parameters

Parameter | Default | Description
--------- | ------- | -----------
Authorization | Required. authentication_token of the user

#### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
id_or_username | Required. This is id or username of the user
instagram_id| Required. instagram_id, can be more than one, seperated by commas

### Digits (Phone Contact) Friends
This endpoint retrieves a list of users on Tress that have matched with a user's Digits (Phone Contact) friends.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/v3/users/<id_or_username>/friends?digits_ids=<digits_id>,<digits_id>`

#### Header Parameters

Parameter | Default | Description
--------- | ------- | -----------
Authorization | Required. authentication_token of the user

#### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
id_or_username | Required. This is id or username of the user
digits_id| Required. digits_id, can be more than one, seperated by commas

# Posts (Hairstyles)

## Create a Post
This endpoint creates a post.

```swift
let headers = [
  "content-type": "multipart/form-data; boundary=---011000010111000001101001",
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "authorization": ""
]
let parameters = [
  [
    "name": "caption",
    "value": "@CoCo check this out"
  ],
  [
    "name": "image",
    "fileName": ["0": []]
  ],
  [
    "name": "products",
    "value": "KeraCare Natural Hair Range"
  ],
  [
    "name": "price_range_id",
    "value": "1"
  ],
  [
    "name": "category_id",
    "value": "2"
  ],
  [
    "name": "new_salon_name",
    "value": "La Villa Hair Shop"
  ],
  [
    "name": "new_salon_location",
    "value": "East Legon, Accra"
  ]
    [
    "name": "new_salon_latitude",
    "value": "0.00000"
  ],
  [
    "name": "new_salon_longitude",
    "value": "0.0000"
  ]
]

let boundary = "---011000010111000001101001"

var body = ""
var error: NSError? = nil
for param in parameters {
  let paramName = param["name"]!
  body += "--\(boundary)\r\n"
  body += "Content-Disposition:form-data; name=\"\(paramName)\""
  if let filename = param["fileName"] {
    let contentType = param["content-type"]!
    let fileContent = String(contentsOfFile: filename, encoding: NSUTF8StringEncoding, error: &error)
    if (error != nil) {
      println(error)
    }
    body += "; filename=\"\(filename)\"\r\n"
    body += "Content-Type: \(contentType)\r\n\r\n"
    body += fileContent!
  } else if let paramValue = param["value"] {
    body += "\r\n\r\n\(paramValue)"
  }
}

var request = NSMutableURLRequest(URL: NSURL(string: "https://tressapi-staging.herokuapp.com/api/v3/users/29/posts")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "POST"
request.allHTTPHeaderFields =

```

```java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("multipart/form-data; boundary=---011000010111000001101001");
RequestBody body = RequestBody.create(mediaType, "-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"caption\"\r\n\r\n@CoCo check this out\r\n-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"image\"; filename=\"[object Object]\"\r\nContent-Type: false\r\n\r\n\r\n-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"products\"\r\n\r\nKeraCare Natural Hair Range\r\n-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"price_range_id\"\r\n\r\n1\r\n-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"category_id\"\r\n\r\n2\r\n-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"new_salon_name\"\r\n\r\nLa Villa Hair Shop\r\n-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"new_salon_location\"\r\n\r\nEast Legon, Accra\r\n-----011000010111000001101001--");
Request request = new Request.Builder()
  .url("https://tressapi-staging.herokuapp.com/api/v3/users/29/posts")
  .post(body)
  .addHeader("content-type", "multipart/form-data; boundary=---011000010111000001101001")
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", 
  .build();

Response response = client.newCall(request).execute();
```

> A successful create post request returns JSON structured like this:

```json
{
  "id": 79,
  "user_id": 29,
  "fullname": "Shola Lewis",
  "username": "CoCo",
  "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
  "salon_name": null,
  "salon_location": null,
  "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/079/medium/ronkeraji.jpg.jpg?1475618385",
  "comments_count": 0,
  "comments": [],
  "category": {
    "id": 2,
    "name": "Natural Hair",
    "created_at": "2015-10-06T17:10:20.535Z",
    "updated_at": "2015-10-06T17:10:20.535Z"
  },
  "price_range": {
    "id": 1,
    "price": "0 - 50",
    "created_at": "2015-10-06T18:15:52.758Z",
    "updated_at": "2016-02-09T11:21:37.935Z",
    "price_gh": "0 - 50",
    "price_ng": "0 - 1500"
  },
  "time_ago": "a minute",
  "likes": 0,
  "caption": "@CoCo check this out",
  "stylename": null,
  "price_range_id": 1,
  "duration": null,
  "products": "KeraCare Natural Hair Range",
  "category_id": 2,
  "salon": ", ",
  "slug": "suldwu5ohzd5dlqrpvtphq",
  "created_at": "2016-10-04T21:59:45Z",
  "updated_at": "2016-10-04T21:59:45Z"
}
```

#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/users/29/posts`

##### Headers

`Authorization: xxxxxxxxxxxxxxxxxx8790730598790`

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user whose is making the request


#### Request Body Parameters

Parameter | Description
--------- | -----------
image | Required. File image
products | Required. Products used on hairstyle
price_range_id | Required. Must choose one from dropdown
category_id | Required. Must choose one from dropdown
new_salon_name | Required. Name of Salon
new_salon_location | Required. Salon Location Text of chosen Location (From Google Maps API Autocompleter)
new_salon_latitude | Required. Salon Latitude of chosen Location  (From Google Maps API Autocompleter)
new_salon_longitude | Required. Name of Salon
caption | Optional. Free style text on User's feeling
tag_list | Optional. Always check if caption string has hashtags, if yes, add the strings of the hashtags seperated by commas as tag_list. E.g if caption has `Rocking my hairstyle #throwbackthursday #blessed`. `tag_list` will be: `throwbackthursday, blessed`

<aside class="notice">
Persist the Post JSON object on the client.
</aside>

## Edit a Post

This endpoint updates a post.


```swift
let headers = [
  "content-type": "multipart/form-data; boundary=---011000010111000001101001",
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "authorization": ""
]

let parameters = [
  [
    "name": "caption",
    "value": "@ronketinker @solapemi Tress is in YCombinator W17!!!"
  ],
  [
    "name": "products",
    "value": "shea butter"
  ],
  [
    "name": "category_id",
    "value": "2"
  ],
  [
    "name": "price_range_id",
    "value": "1"
  ],
  [
    "name": "salon_name",
    "value": "God is Good Salon"
  ],
  [
    "name": "tag_list",
    "value": "#teamnatural, #TressUpNaturalista"
  ]
]

let boundary = "---011000010111000001101001"

var body = ""
var error: NSError? = nil
for param in parameters {
  let paramName = param["name"]!
  body += "--\(boundary)\r\n"
  body += "Content-Disposition:form-data; name=\"\(paramName)\""
  if let filename = param["fileName"] {
    let contentType = param["content-type"]!
    let fileContent = String(contentsOfFile: filename, encoding: NSUTF8StringEncoding, error: &error)
    if (error != nil) {
      println(error)
    }
    body += "; filename=\"\(filename)\"\r\n"
    body += "Content-Type: \(contentType)\r\n\r\n"
    body += fileContent!
  } else if let paramValue = param["value"] {
    body += "\r\n\r\n\(paramValue)"
  }
}

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/users/67/posts/83")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "PATCH"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData


```

```java
OkHttpClient client = new OkHttpClient();


MediaType mediaType = MediaType.parse("multipart/form-data; boundary=---011000010111000001101001");
RequestBody body = RequestBody.create(mediaType, "-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"caption\"\r\n\r\n@ronketinker @solapemi Tress is in YCombinator W17!!!\r\n-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"products\"\r\n\r\nshea butter\r\n-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"category_id\"\r\n\r\n2\r\n-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"price_range_id\"\r\n\r\n1\r\n-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"salon_name\"\r\n\r\nGod is Good Salon\r\n-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"tag_list\"\r\n\r\n#teamnatural, #TressUpNaturalista\r\n-----011000010111000001101001--");
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/users/67/posts/83")
  .patch(body)
  .addHeader("content-type", "multipart/form-data; boundary=---011000010111000001101001")
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", 
  .build();

Response response = client.newCall(request).execute();
```

> A successful update post request returns JSON structured like this:

```json
{
  "id": 79,
  "user_id": 29,
  "fullname": "Shola Lewis",
  "username": "CoCo",
  "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
  "salon_name": null,
  "salon_location": null,
  "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/079/medium/ronkeraji.jpg.jpg?1475618385",
  "comments_count": 0,
  "comments": [],
  "category": {
    "id": 2,
    "name": "Natural Hair",
    "created_at": "2015-10-06T17:10:20.535Z",
    "updated_at": "2015-10-06T17:10:20.535Z"
  },
  "price_range": {
    "id": 1,
    "price": "0 - 50",
    "created_at": "2015-10-06T18:15:52.758Z",
    "updated_at": "2016-02-09T11:21:37.935Z",
    "price_gh": "0 - 50",
    "price_ng": "0 - 1500"
  },
  "time_ago": "a minute",
  "likes": 0,
  "caption": "@CoCo check this out",
  "stylename": null,
  "price_range_id": 1,
  "duration": null,
  "products": "KeraCare Natural Hair Range",
  "category_id": 2,
  "salon": ", ",
  "slug": "suldwu5ohzd5dlqrpvtphq",
  "created_at": "2016-10-04T21:59:45Z",
  "updated_at": "2016-10-04T21:59:45Z"
}
```

#### HTTP Request

`PATCH https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/posts/<post_id>`

##### Headers

`Authorization: xxxxxxxxxxxxxxxxxx8790730598790`

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user whose is making the request

#### URL Parameters

Parameter | Description
--------- | -----------
user_id | Required. ID of the user
post_id | Required. ID of the post


#### Request Body Parameters

Parameter | Description
--------- | -----------
image | Required. File image
products | Required. Products used on hairstyle
price_range_id | Required. Must choose one from dropdown
category_id | Required. Must choose one from dropdown
new_salon_name | Required. Name of Salon
new_salon_location | Required. Salon Location Text of chosen Location (From Google Maps API Autocompleter)
new_salon_latitude | Required. Salon Latitude of chosen Location  (From Google Maps API Autocompleter)
new_salon_longitude | Required. Name of Salon
caption | Optional. Free style text on User's feeling
tag_list | Optional. Always check if caption string has hashtags, if yes, add the strings of the hashtags seperated by commas as tag_list. E.g if caption has `Rocking my hairstyle #throwbackthursday #blessed`. `tag_list` will be: `throwbackthursday, blessed`

## Delete a Post

This endpoint creates a post.


```swift
let headers = [
  "content-type": "multipart/form-data; boundary=---011000010111000001101001",
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "authorization": ""
]

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/users/67/posts/83")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "DELETE"
request.allHTTPHeaderFields = headers


```

```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/users/67/posts/83")
  .delete(null)
  .addHeader("content-type", "multipart/form-data; boundary=---011000010111000001101001")
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", 
  .build();

Response response = client.newCall(request).execute();
```

> A successful delete post request returns:

```http
204 No Content

```

#### HTTP Request

`DELETE https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/posts/<post_id>`

##### Headers

`Authorization: xxxxxxxxxxxxxxxxxx8790730598790`

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user whose is making the request

#### URL Parameters

Parameter | Description
--------- | -----------
user_id | Required. ID of the user
post_id | Required. ID of the post

## Get a Specific Post

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
]

var request = NSMutableURLRequest(URL: NSURL(string: "https://tressapi-staging.herokuapp.com/api/v3/posts/53")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://tressapi-staging.herokuapp.com/api/v3/users/53")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .build();

Response response = client.newCall(request).execute();
```

> The above command returns JSON structured like this:

```json
{
  "id": 53,
  "user_id": 40,
  "fullname": "Bolanle  Lewis",
  "username": "esther222",
  "user_avatar": "https://s3.amazonaws.com/tress-api-staging/users/avatars/000/000/040/small/avatar_name\"_.?1459043911",
  "salon_name": "Lolavitahair Salon",
  "salon_location": "Apapa, Lagos, Nigeria",
  "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/053/medium/image_name%22_.?1459115640",
  "comments_count": 0,
  "comments": [],
  "category": {
    "id": 1,
    "name": "Braids",
    "created_at": "2015-10-06T17:08:59.307Z",
    "updated_at": "2015-10-06T17:08:59.307Z"
  },
  "price_range": {
    "id": 1,
    "price": "0 - 50",
    "created_at": "2015-10-06T18:15:52.758Z",
    "updated_at": "2016-02-09T11:21:37.935Z",
    "price_gh": "0 - 50",
    "price_ng": "0 - 1500"
  },
  "time_ago": "6 months",
  "likes": 2,
  "caption": "Fleeky fleeky!",
  "stylename": null,
  "price_range_id": 1,
  "duration": null,
  "products": "Kinky Twists",
  "category_id": 1,
  "salon": "Lolavitahair Salon, Apapa, Lagos, Nigeria",
  "slug": "wxg53kdu-jdy7-itpwis_a",
  "created_at": "2016-03-27T21:53:55Z",
  "updated_at": "2016-06-06T15:09:22Z"
}
```

This endpoint retrieves a specific post.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/posts/<id>`

#### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the post to retrieve

## Like a Post

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
  "authorization": ""
]

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/users/28/posts/62/like")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/users/28/posts/62/like")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();

Response response = client.newCall(request).execute();
```

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "count": 1
}
```

This endpoint likes a specific post by a user.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/posts/<post_id>/like`

##### Headers

`Authorization: xxxxxxxxxxxxxxxxxx8790730598790`

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user whose is making the request


#### URL Parameters

Parameter | Description
--------- | -----------
user_id | The ID of the user that is carrying out the action
post_id | The ID of the post

## Unlike a Post

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
  "authorization": ""
]

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/users/28/posts/62/unlike")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/users/28/posts/62/unlike")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();

Response response = client.newCall(request).execute();
```

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "count": 0
}
```

This endpoint unlikes a specific post by a user.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/posts/<post_id>/unlike`

##### Headers

`Authorization: xxxxxxxxxxxxxxxxxx8790730598790`

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user whose is making the request


#### URL Parameters

Parameter | Description
--------- | -----------
user_id | The ID of the user that is carrying out the action
post_id | The ID of the post

## Bookmark a Post

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
  "authorization": ""
]

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/users/28/posts/62/bookmark")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/users/28/posts/62/bookmark")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();

Response response = client.newCall(request).execute();
```

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "count": 1
}
```

This endpoint bookmarks a specific post by a user.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/posts/<post_id>/bookmark`

##### Headers

`Authorization: xxxxxxxxxxxxxxxxxx8790730598790`

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user whose is making the request


#### URL Parameters

Parameter | Description
--------- | -----------
user_id | The ID of the user that is carrying out the action
post_id | The ID of the post

## UnBookmark a Post

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
  "authorization": ""
]

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/users/28/posts/62/unbookmark")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/users/28/posts/62/unbookmark")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();

Response response = client.newCall(request).execute();
```

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "count": 0
}
```

This endpoint unbookmark a specific post by a user.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/posts/<post_id>/unbookmark`

##### Headers

`Authorization: xxxxxxxxxxxxxxxxxx8790730598790`

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user whose is making the request


#### URL Parameters

Parameter | Description
--------- | -----------
user_id | The ID of the user that is carrying out the action
post_id | The ID of the post

## List of Users who have Liked a Post
```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
]

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/posts/68/likers")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/posts/68/likers")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .build();

Response response = client.newCall(request).execute();
```

> The above command returns JSON structured like this:

```json
{
  "likers": [
    {
      "id": 29,
      "username": "olame",
      "avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/029/small/_IGP3572.jpg.jpg?1454659780",
      "fullname": "OlaEsther Tunde"
    },
    {
      "id": 26,
      "username": "xxolaxxxxx",
      "avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/026/small/B8Vo-6yIEAER-_C.jpg.jpg?1454659779",
      "fullname": " "
    },
    {
      "id": 67,
      "username": "ronke",
      "avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "fullname": " "
    }
  ]
}
```

This endpoint retrieves a list of users who have liked a post.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/posts/<post_id>/likers`


#### URL Parameters

Parameter | Description
--------- | -----------
post_id | The ID of the post


## List of a User's Bookmarked Posts

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
  "authorization": ""
]

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/users/solapemi/bookmarked_posts")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/users/solapemi/bookmarked_posts")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();

Response response = client.newCall(request).execute();
```

> The above command returns JSON structured like this:

```json
{
  "bookmarked posts": [
    {
      "id": 62,
      "user_id": 29,
      "fullname": "OlaEsther Tunde",
      "username": "olame",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/029/small/_IGP3572.jpg.jpg?1454659780",
      "salon_name": null,
      "salon_location": null,
      "image": "https://s3.amazonaws.com/tress-api-development/posts/images/000/000/062/medium/_IGP3962.jpg.jpg?1454659830",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 1,
        "name": "Braids",
        "created_at": "2015-08-28T11:17:56.555Z",
        "updated_at": "2015-08-28T11:17:56.555Z"
      },
      "price_range": {
        "id": 2,
        "price": "60 - 100",
        "created_at": "2015-09-18T14:13:42.274Z",
        "updated_at": "2016-02-09T10:53:43.549Z",
        "price_gh": "60 - 100",
        "price_ng": "1600 - 2500"
      },
      "time_ago": "11 months",
      "likes": 0,
      "caption": "ats",
      "stylename": "ats",
      "price_range_id": 2,
      "duration": "ats",
      "products": null,
      "category_id": 1,
      "salon": ", ",
      "slug": "rpw1fyi3apup4zcd_hshuw",
      "created_at": "2015-11-08T23:48:21Z",
      "updated_at": "2016-10-11T16:31:06Z"
    }
  ]
}
```

This endpoint retrieves a list of posts bookmarked by a user.

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/bookmarked_posts`

##### Headers

`Authorization: xxxxxxxxxxxxxxxxxx8790730598790`

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user who is making the request


#### URL Parameters

Parameter | Description
--------- | -----------
user_id | The ID of the user that is carrying out the action

## Feeds

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
]

var request = NSMutableURLRequest(URL: NSURL(string: "https://tressapi-staging.herokuapp.com/api/v3/posts/discover/all?per_page=10%2Cpage%3D1")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://tressapi-staging.herokuapp.com/api/v3/posts/discover/all?per_page=10%2Cpage%3D1")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .build();

Response response = client.newCall(request).execute();
```

> The above command returns JSON structured like this:

```json
{
  "posts": [
    {
      "id": 79,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": null,
      "salon_location": null,
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/079/medium/ronkeraji.jpg.jpg?1475618387",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-10-06T17:10:20.535Z",
        "updated_at": "2015-10-06T17:10:20.535Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "1 hour",
      "likes": 0,
      "caption": "@CoCo check this out",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "KeraCare Natural Hair Range",
      "category_id": 2,
      "salon": ", ",
      "slug": "suldwu5ohzd5dlqrpvtphq",
      "created_at": "2016-10-04T21:59:45Z",
      "updated_at": "2016-10-04T21:59:50Z"
    },
    {
      "id": 78,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": null,
      "salon_location": null,
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/078/medium/9109768995_f6c2675fd4_c.jpg.jpg?1473780658",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-10-06T17:10:20.535Z",
        "updated_at": "2015-10-06T17:10:20.535Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "21 days",
      "likes": 0,
      "caption": "@CoCo @gerald @obi check this out",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Mongolian Hair",
      "category_id": 2,
      "salon": ", ",
      "slug": "mixes1yls6_0z_6ioo7lkg",
      "created_at": "2016-09-13T15:30:51Z",
      "updated_at": "2016-09-13T15:31:00Z"
    },
    {
      "id": 77,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": null,
      "salon_location": null,
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/077/medium/ronke.jpg.jpg?1472725902",
      "comments_count": 10,
      "comments": [
        {
          "id": 69,
          "content": "@Obi @gerald check this out!",
          "post_id": 77,
          "user_id": 29,
          "username": "CoCo",
          "time_ago": "21 days"
        },
        {
          "id": 70,
          "content": "@Obi @gerald check this out!",
          "post_id": 77,
          "user_id": 29,
          "username": "CoCo",
          "time_ago": "21 days"
        }
      ],
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-10-06T17:10:20.535Z",
        "updated_at": "2015-10-06T17:10:20.535Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "1 month",
      "likes": 1,
      "caption": "@CoCo check this out",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Mongolian Hair",
      "category_id": 2,
      "salon": ", ",
      "slug": "o1dp5sb4h5wtiyjlvnkefq",
      "created_at": "2016-09-01T10:31:36Z",
      "updated_at": "2016-09-01T10:33:29Z"
    },
    {
      "id": 76,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Black Cotton Natural Hair Salon",
      "salon_location": "Dzorwulu, Accra, Greater Accra, Ghana",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/076/medium/image_name%22_.?1471345416",
      "comments_count": 4,
      "comments": [
        {
          "id": 58,
          "content": "Looks great! #tressupnaturalista",
          "post_id": 76,
          "user_id": 29,
          "username": "CoCo",
          "time_ago": "2 months"
        },
        {
          "id": 60,
          "content": "Amazing .. Love this😘😘😘😘😘😘😘😘😘😘😘😘😘😘😘😘😘😘😘😘👏👏👏👏👏👏👏",
          "post_id": 76,
          "user_id": 56,
          "username": "Princess",
          "time_ago": "2 months"
        }
      ],
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-10-06T17:10:20.535Z",
        "updated_at": "2015-10-06T17:10:20.535Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "2 months",
      "likes": 1,
      "caption": "Love my #hair #tressupnaturalista",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Shea Butter",
      "category_id": 2,
      "salon": "Black Cotton Natural Hair Salon, Dzorwulu, Accra, Greater Accra, Ghana",
      "slug": "2wsjfzu8ykmzsmd4jtxira",
      "created_at": "2016-08-16T11:03:29Z",
      "updated_at": "2016-08-22T14:32:52Z"
    },
    {
      "id": 75,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Native Touch",
      "salon_location": "Leeds, United Kingdom",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/075/medium/image_name%22_.?1470901386",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-10-06T17:10:20.535Z",
        "updated_at": "2015-10-06T17:10:20.535Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "2 months",
      "likes": 2,
      "caption": "I love this @mseolatunde @Morenike",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "LOL cat",
      "category_id": 2,
      "salon": "Native Touch, Leeds, United Kingdom",
      "slug": "ghd4jiqhzauapggh6gsnww",
      "created_at": "2016-08-11T07:43:00Z",
      "updated_at": "2016-08-22T14:32:32Z"
    },
    {
      "id": 74,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Self",
      "salon_location": "Accra, Greater Accra, Ghana",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/074/medium/image_name%22_.?1470826829",
      "comments_count": 5,
      "comments": [
        {
          "id": 53,
          "content": "@esther222 heyyyyyy",
          "post_id": 74,
          "user_id": 29,
          "username": "CoCo",
          "time_ago": "2 months"
        },
        {
          "id": 54,
          "content": "Hello @esther222",
          "post_id": 74,
          "user_id": 29,
          "username": "CoCo",
          "time_ago": "2 months"
        }
      ],
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-10-06T17:10:20.535Z",
        "updated_at": "2015-10-06T17:10:20.535Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "2 months",
      "likes": 1,
      "caption": "#naturalhair @esther",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Shea Butter",
      "category_id": 2,
      "salon": "Self, Accra, Greater Accra, Ghana",
      "slug": "faoo0bxoadnuulqc0ijyaw",
      "created_at": "2016-08-10T11:00:24Z",
      "updated_at": "2016-08-19T14:26:38Z"
    },
    {
      "id": 73,
      "user_id": 54,
      "fullname": "Open Graph",
      "username": "Fbuser",
      "user_avatar": "https://s3.amazonaws.com/tress-api-staging/users/avatars/000/000/054/small/picture.?1466030510",
      "salon_name": "Holla Salon",
      "salon_location": "East Palo Alto, CA, United States",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/073/medium/image_name%22_.?1466030672",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-10-06T17:10:20.535Z",
        "updated_at": "2015-10-06T17:10:20.535Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "4 months",
      "likes": 2,
      "caption": "",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Shea Butter",
      "category_id": 2,
      "salon": "Holla Salon, East Palo Alto, CA, United States",
      "slug": "ac6zxeeu2amkt-tfeys2zg",
      "created_at": "2016-06-15T22:44:28Z",
      "updated_at": "2016-08-15T16:03:58Z"
    },
    {
      "id": 71,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Black Cotton Salon",
      "salon_location": "Surulere, Lagos, Nigeria",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/071/medium/image_name%22_.?1466004158",
      "comments_count": 1,
      "comments": [
        {
          "id": 59,
          "content": "I love what I'm seeing. This will be my next hair. Oooh and I think it will actually fit my face. Love this so much",
          "post_id": 71,
          "user_id": 56,
          "username": "Princess",
          "time_ago": "2 months"
        }
      ],
      "category": {
        "id": 4,
        "name": "Weaves",
        "created_at": "2015-10-06T18:12:33.442Z",
        "updated_at": "2015-10-06T18:12:33.442Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "4 months",
      "likes": 0,
      "caption": "Love my hair",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Shea Butter",
      "category_id": 4,
      "salon": "Black Cotton Salon, Surulere, Lagos, Nigeria",
      "slug": "almog9fejygmpepuot3y7g",
      "created_at": "2016-06-15T15:22:33Z",
      "updated_at": "2016-08-22T14:32:21Z"
    },
    {
      "id": 70,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Lagoon Villa Salon",
      "salon_location": "Lekki Phase 1, Lekki, Lagos, Nigeria",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/070/medium/image_name%22_.?1465989570",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-10-06T17:10:20.535Z",
        "updated_at": "2015-10-06T17:10:20.535Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "4 months",
      "likes": 0,
      "caption": "",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Heat Protectant, Shea Butter",
      "category_id": 2,
      "salon": "Lagoon Villa Salon, Lekki Phase 1, Lekki, Lagos, Nigeria",
      "slug": "b1y933xfj6lw3vdzbwji1g",
      "created_at": "2016-06-15T11:19:27Z",
      "updated_at": "2016-08-19T14:26:54Z"
    },
    {
      "id": 69,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Solape Salon",
      "salon_location": "Enugu, Nigeria",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/069/medium/image_name%22_.?1465988129",
      "comments_count": 2,
      "comments": [
        {
          "id": 45,
          "content": "@bolanlemi",
          "post_id": 69,
          "user_id": 29,
          "username": "CoCo",
          "time_ago": "2 months"
        },
        {
          "id": 49,
          "content": "#hair",
          "post_id": 69,
          "user_id": 29,
          "username": "CoCo",
          "time_ago": "2 months"
        }
      ],
      "category": {
        "id": 4,
        "name": "Weaves",
        "created_at": "2015-10-06T18:12:33.442Z",
        "updated_at": "2015-10-06T18:12:33.442Z"
      },
      "price_range": {
        "id": 3,
        "price": "110 - 200",
        "created_at": "2015-10-06T18:16:43.027Z",
        "updated_at": "2016-02-09T11:25:29.023Z",
        "price_gh": "110 - 200",
        "price_ng": "2600 - 5000"
      },
      "time_ago": "4 months",
      "likes": 1,
      "caption": "Love the hair",
      "stylename": null,
      "price_range_id": 3,
      "duration": null,
      "products": "Brazilian Weaves",
      "category_id": 4,
      "salon": "Solape Salon, Enugu, Nigeria",
      "slug": "dt2g7zn5utin3wffm3vdrq",
      "created_at": "2016-06-15T10:55:24Z",
      "updated_at": "2016-08-15T13:45:13Z"
    },
    {
      "id": 68,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Auntie Linda",
      "salon_location": "Somolu, Lagos, Nigeria",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/068/medium/image_name%22_.?1465970941",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 5,
        "name": "Perm Cut",
        "created_at": "2015-10-06T18:13:12.703Z",
        "updated_at": "2015-10-06T18:13:12.703Z"
      },
      "price_range": {
        "id": 2,
        "price": "60 - 100",
        "created_at": "2015-10-06T18:16:24.895Z",
        "updated_at": "2016-02-09T11:25:29.008Z",
        "price_gh": "60 - 100",
        "price_ng": "1600 - 2500"
      },
      "time_ago": "4 months",
      "likes": 0,
      "caption": "",
      "stylename": null,
      "price_range_id": 2,
      "duration": null,
      "products": "Bleh",
      "category_id": 5,
      "salon": "Auntie Linda, Somolu, Lagos, Nigeria",
      "slug": "_gycx2q1k8ttzougmwmd5g",
      "created_at": "2016-06-15T06:08:57Z",
      "updated_at": "2016-06-15T06:09:03Z"
    },
    {
      "id": 67,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Lola Salon",
      "salon_location": "North Legon, Greater Accra, Ghana",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/067/medium/image_name%22_.?1465836144",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 5,
        "name": "Perm Cut",
        "created_at": "2015-10-06T18:13:12.703Z",
        "updated_at": "2015-10-06T18:13:12.703Z"
      },
      "price_range": {
        "id": 2,
        "price": "60 - 100",
        "created_at": "2015-10-06T18:16:24.895Z",
        "updated_at": "2016-02-09T11:25:29.008Z",
        "price_gh": "60 - 100",
        "price_ng": "1600 - 2500"
      },
      "time_ago": "4 months",
      "likes": 0,
      "caption": "",
      "stylename": null,
      "price_range_id": 2,
      "duration": null,
      "products": "Lolavitahair",
      "category_id": 5,
      "salon": "Lola Salon, North Legon, Greater Accra, Ghana",
      "slug": "82nxemr7o8rrvj6umaegsg",
      "created_at": "2016-06-13T16:42:19Z",
      "updated_at": "2016-06-13T16:42:25Z"
    },
    {
      "id": 66,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Bolanle Villa Salon",
      "salon_location": "Oshodi-Isolo, Lagos, Nigeria",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/066/medium/image_name%22_.?1465835389",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 1,
        "name": "Braids",
        "created_at": "2015-10-06T17:08:59.307Z",
        "updated_at": "2015-10-06T17:08:59.307Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "4 months",
      "likes": 0,
      "caption": "",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Holla Holla",
      "category_id": 1,
      "salon": "Bolanle Villa Salon, Oshodi-Isolo, Lagos, Nigeria",
      "slug": "gaybf6b7cio6h37tgig-ng",
      "created_at": "2016-06-13T16:29:47Z",
      "updated_at": "2016-06-13T16:29:51Z"
    },
    {
      "id": 65,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Auntie Mary",
      "salon_location": "Gbagada, Lagos, Nigeria",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/065/medium/image_name%22_.?1465834465",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 1,
        "name": "Braids",
        "created_at": "2015-10-06T17:08:59.307Z",
        "updated_at": "2015-10-06T17:08:59.307Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "4 months",
      "likes": 0,
      "caption": "You would love this!",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Kinky Twists",
      "category_id": 1,
      "salon": "Auntie Mary, Gbagada, Lagos, Nigeria",
      "slug": "appedeijdktque51axdtua",
      "created_at": "2016-06-13T16:14:23Z",
      "updated_at": "2016-06-13T16:14:26Z"
    },
    {
      "id": 64,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Bolanle Salon",
      "salon_location": "Apapa, Lagos, Nigeria",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/064/medium/image_name%22_.?1465832220",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 1,
        "name": "Braids",
        "created_at": "2015-10-06T17:08:59.307Z",
        "updated_at": "2015-10-06T17:08:59.307Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "4 months",
      "likes": 0,
      "caption": "Bliss!",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Kinky Twists",
      "category_id": 1,
      "salon": "Bolanle Salon, Apapa, Lagos, Nigeria",
      "slug": "qgfmdxqulhy6fhsiufxt6w",
      "created_at": "2016-06-13T15:36:57Z",
      "updated_at": "2016-06-13T15:37:01Z"
    },
    {
      "id": 63,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Auntie Shirley Salon",
      "salon_location": "East Legon, Accra, Greater Accra, Ghana",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/063/medium/image_name%22_.?1465831664",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 1,
        "name": "Braids",
        "created_at": "2015-10-06T17:08:59.307Z",
        "updated_at": "2015-10-06T17:08:59.307Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "4 months",
      "likes": 0,
      "caption": "Love love love love this",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Kinky Twists",
      "category_id": 1,
      "salon": "Auntie Shirley Salon, East Legon, Accra, Greater Accra, Ghana",
      "slug": "sm8x7bl21gx9_f5fqhhrow",
      "created_at": "2016-06-13T15:27:42Z",
      "updated_at": "2016-06-13T15:27:46Z"
    },
    {
      "id": 62,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Black Cotton Salon",
      "salon_location": "Dzorwulu, Accra, Greater Accra, Ghana",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/062/medium/image_name%22_.?1465831091",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-10-06T17:10:20.535Z",
        "updated_at": "2015-10-06T17:10:20.535Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "4 months",
      "likes": 0,
      "caption": "#Throwback",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Heat Protectant, Shea Butter",
      "category_id": 2,
      "salon": "Black Cotton Salon, Dzorwulu, Accra, Greater Accra, Ghana",
      "slug": "1eehofjj-4ztr5bnwsydaq",
      "created_at": "2016-06-13T15:18:04Z",
      "updated_at": "2016-06-13T15:18:17Z"
    },
    {
      "id": 61,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "HairTalk",
      "salon_location": "Dansoman, Accra, Greater Accra, Ghana",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/061/medium/image_name%22_.?1465830636",
      "comments_count": 1,
      "comments": [
        {
          "id": 56,
          "content": "I remember this @esther2",
          "post_id": 61,
          "user_id": 56,
          "username": "Princess",
          "time_ago": "2 months"
        }
      ],
      "category": {
        "id": 1,
        "name": "Braids",
        "created_at": "2015-10-06T17:08:59.307Z",
        "updated_at": "2015-10-06T17:08:59.307Z"
      },
      "price_range": {
        "id": 2,
        "price": "60 - 100",
        "created_at": "2015-10-06T18:16:24.895Z",
        "updated_at": "2016-02-09T11:25:29.008Z",
        "price_gh": "60 - 100",
        "price_ng": "1600 - 2500"
      },
      "time_ago": "4 months",
      "likes": 0,
      "caption": "Yagazie shot this!",
      "stylename": null,
      "price_range_id": 2,
      "duration": null,
      "products": "Havana Mambo Twists",
      "category_id": 1,
      "salon": "HairTalk, Dansoman, Accra, Greater Accra, Ghana",
      "slug": "uvorulizrma2jbfcaoed-q",
      "created_at": "2016-06-13T15:10:29Z",
      "updated_at": "2016-06-13T15:10:41Z"
    },
    {
      "id": 60,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Auntie Agatha's Salon",
      "salon_location": "East Legon, Accra, Greater Accra, Ghana",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/060/medium/image_name%22_.?1465829410",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 1,
        "name": "Braids",
        "created_at": "2015-10-06T17:08:59.307Z",
        "updated_at": "2015-10-06T17:08:59.307Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "4 months",
      "likes": 0,
      "caption": "",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Kinky Bulk Twist",
      "category_id": 1,
      "salon": "Auntie Agatha's Salon, East Legon, Accra, Greater Accra, Ghana",
      "slug": "yfizmdcj_m4gdcwtm7u3zq",
      "created_at": "2016-06-13T14:50:05Z",
      "updated_at": "2016-06-13T14:50:11Z"
    },
    {
      "id": 59,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Solape Salon",
      "salon_location": "East Legon, Accra, Ghana",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/059/medium/image_name%22_.?1465820518",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 7,
        "name": "Corn Row",
        "created_at": "2015-12-16T12:36:12.119Z",
        "updated_at": "2015-12-16T12:36:12.119Z"
      },
      "price_range": {
        "id": 3,
        "price": "110 - 200",
        "created_at": "2015-10-06T18:16:43.027Z",
        "updated_at": "2016-02-09T11:25:29.023Z",
        "price_gh": "110 - 200",
        "price_ng": "2600 - 5000"
      },
      "time_ago": "4 months",
      "likes": 0,
      "caption": "",
      "stylename": null,
      "price_range_id": 3,
      "duration": null,
      "products": "Bleh blah",
      "category_id": 7,
      "salon": "Solape Salon, East Legon, Accra, Ghana",
      "slug": "qvm3bpf79jq_ns9tkosvtg",
      "created_at": "2016-06-13T12:21:55Z",
      "updated_at": "2016-06-13T12:22:00Z"
    },
    {
      "id": 58,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Good luck Salon",
      "salon_location": "Accra, Greater Accra, Ghana",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/058/medium/image_name%22_.?1465819764",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 5,
        "name": "Perm Cut",
        "created_at": "2015-10-06T18:13:12.703Z",
        "updated_at": "2015-10-06T18:13:12.703Z"
      },
      "price_range": {
        "id": 3,
        "price": "110 - 200",
        "created_at": "2015-10-06T18:16:43.027Z",
        "updated_at": "2016-02-09T11:25:29.023Z",
        "price_gh": "110 - 200",
        "price_ng": "2600 - 5000"
      },
      "time_ago": "4 months",
      "likes": 0,
      "caption": "",
      "stylename": null,
      "price_range_id": 3,
      "duration": null,
      "products": "Shea Butter",
      "category_id": 5,
      "salon": "Good luck Salon, Accra, Greater Accra, Ghana",
      "slug": "ldu1czao2g8qpmmcijyrkg",
      "created_at": "2016-06-13T12:09:18Z",
      "updated_at": "2016-06-13T12:09:26Z"
    },
    {
      "id": 56,
      "user_id": 29,
      "fullname": "Shola Lewis",
      "username": "CoCo",
      "user_avatar": "http://gravatar.com/avatar/66b9fef912a402988908283d30f80ae4?s=350&d=www.tressapp.co/images/esther.jpg",
      "salon_name": "Omoge Wuraola Salon",
      "salon_location": "Ojuelegba Bus Stop, Surulere, Lagos, Nigeria",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/056/medium/image_name%22_.?1460436368",
      "comments_count": 1,
      "comments": [
        {
          "id": 43,
          "content": "Holla",
          "post_id": 56,
          "user_id": 29,
          "username": "CoCo",
          "time_ago": "5 months"
        }
      ],
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-10-06T17:10:20.535Z",
        "updated_at": "2015-10-06T17:10:20.535Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "6 months",
      "likes": 1,
      "caption": "In love with my bun!",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Obia Natural Hair Curl Butter",
      "category_id": 2,
      "salon": "Omoge Wuraola Salon, Ojuelegba Bus Stop, Surulere, Lagos, Nigeria",
      "slug": "yu-hdnwphyfdhvvnajs5mg",
      "created_at": "2016-04-12T04:46:06Z",
      "updated_at": "2016-06-06T15:09:22Z"
    },
    {
      "id": 55,
      "user_id": 42,
      "fullname": "Gerald Pharin",
      "username": "bolanlemi",
      "user_avatar": "https://s3.amazonaws.com/tress-api-staging/users/avatars/000/000/042/small/avatar_name\"_.?1460374996",
      "salon_name": "Auntie Mary's Salon",
      "salon_location": "Adenta Municipality, Greater Accra, Ghana",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/055/medium/image_name%22_.?1460383428",
      "comments_count": 5,
      "comments": [
        {
          "id": 47,
          "content": "@mseolatunde",
          "post_id": 55,
          "user_id": 29,
          "username": "CoCo",
          "time_ago": "2 months"
        },
        {
          "id": 48,
          "content": "@CoCo",
          "post_id": 55,
          "user_id": 29,
          "username": "CoCo",
          "time_ago": "2 months"
        }
      ],
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-10-06T17:10:20.535Z",
        "updated_at": "2015-10-06T17:10:20.535Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "6 months",
      "likes": 2,
      "caption": "Looks great for grad!",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Twist Butter",
      "category_id": 2,
      "salon": "Auntie Mary's Salon, Adenta Municipality, Greater Accra, Ghana",
      "slug": "lbrc1ms-kotyqbkwj72ykw",
      "created_at": "2016-04-11T14:03:41Z",
      "updated_at": "2016-06-06T15:09:22Z"
    },
    {
      "id": 54,
      "user_id": 40,
      "fullname": "Bolanle  Lewis",
      "username": "esther222",
      "user_avatar": "https://s3.amazonaws.com/tress-api-staging/users/avatars/000/000/040/small/avatar_name\"_.?1459043911",
      "salon_name": null,
      "salon_location": null,
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/054/medium/image_name%22_.?1459182997",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-10-06T17:10:20.535Z",
        "updated_at": "2015-10-06T17:10:20.535Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "6 months",
      "likes": 2,
      "caption": "Fluff",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Fluffy kitten",
      "category_id": 2,
      "salon": ", ",
      "slug": "noz0ruhc286r3cgew2lo4w",
      "created_at": "2016-03-28T16:36:35Z",
      "updated_at": "2016-06-06T15:09:22Z"
    },
    {
      "id": 53,
      "user_id": 40,
      "fullname": "Bolanle  Lewis",
      "username": "esther222",
      "user_avatar": "https://s3.amazonaws.com/tress-api-staging/users/avatars/000/000/040/small/avatar_name\"_.?1459043911",
      "salon_name": "Lolavitahair Salon",
      "salon_location": "Apapa, Lagos, Nigeria",
      "image": "https://s3.amazonaws.com/tress-api-staging/posts/images/000/000/053/medium/image_name%22_.?1459115640",
      "comments_count": 0,
      "comments": [],
      "category": {
        "id": 1,
        "name": "Braids",
        "created_at": "2015-10-06T17:08:59.307Z",
        "updated_at": "2015-10-06T17:08:59.307Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-10-06T18:15:52.758Z",
        "updated_at": "2016-02-09T11:21:37.935Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "6 months",
      "likes": 2,
      "caption": "Fleeky fleeky!",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "Kinky Twists",
      "category_id": 1,
      "salon": "Lolavitahair Salon, Apapa, Lagos, Nigeria",
      "slug": "wxg53kdu-jdy7-itpwis_a",
      "created_at": "2016-03-27T21:53:55Z",
      "updated_at": "2016-06-06T15:09:22Z"
    }
  ],
  "meta": {
    "pagination": {
      "per_page": 0,
      "total_pages": 2,
      "total_objects": 47
    }
  }
}
```

This section contains endpoints that retrieve several types of feeds on Tress.

### All

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/posts/discover/all?per_page=10,page=1`

This endpoint retrieves all posts by pagination, 10 at a time.

#### Query Parameters

Pagination for endless scrolling

Parameter | Default | Description
--------- | ------- | -----------
per_page | 10 | Numbers of users to return at a time
page | 1 | Page number.

<aside class="notice">
The Posts JSONArray response structure is the same as returned in the main feed top category
</aside>

### Following

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/posts?per_page=10,page=1`

#### Query Parameters

Pagination for endless scrolling

Parameter | Default | Description
--------- | ------- | -----------
per_page | 10 | Numbers of users to return at a time
page | 1 | Page number.

##### Headers

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user whose feed you're requesting.

<aside class="notice">
The Posts JSONArray response structure is the same as returned in the main feed top category
</aside>


### Trending

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/posts/discover/trending?per_page=10,page=1`

#### Query Parameters

Pagination for endless scrolling

Parameter | Default | Description
--------- | ------- | -----------
per_page | 10 | Numbers of users to return at a time
page | 1 | Page number.

<aside class="notice">
The Posts JSONArray response structure is the same as returned in the main feed top category
</aside>


### Hashtagged Feed

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/tags/<hashtag_param>?per_page=10,page=1`

#### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
hashtag_param | | The string value after the sign `#`. Please note, DO NOT include the `#` sign to the request endpoint, only include the value after it.

#### Query Parameters

Pagination for endless scrolling

Parameter | Default | Description
--------- | ------- | -----------
per_page | 10 | Numbers of users to return at a time
page | 1 | Page number.

<aside class="notice">
The Posts JSONArray response structure is the same as returned in the main feed top category
</aside>

### Category Feed

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/posts/categories/<category_id>?per_page=10,page=1`

#### Query Parameters

Pagination for endless scrolling

Parameter | Default | Description
--------- | ------- | -----------
category_id | | id of category selected
per_page | 25 | Numbers of users to return at a time
page | 1 | Page number.

<aside class="notice">
The Posts JSONArray response structure is the same as returned in the main feed top category
</aside>


### Price Range Feed

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/posts/price_ranges/<price_range_id>?per_page=10,page=1`

#### Query Parameters

Pagination for endless scrolling

Parameter | Default | Description
--------- | ------- | -----------
price_range_id | | id of price_range selected
per_page | 25 | Numbers of users to return at a time
page | 1 | Page number.

<aside class="notice">
The Posts JSONArray response structure is the same as returned in the main feed top category
</aside>

### Extensive Filter Feed

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/posts/discover/filter?salon=<salon_name_or_location_string>,price_range_ids=<price_range_id,price_range_id>&category_ids=<category_id>&page=2&per_page=25`

#### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
salon_name_or_location_string | | salon name or salon location string
category_id | | id of category selected. Multiple selections are seperated by `,`
price_range_id | | id of price_range selected. Multiple selections are seperated by `,`
per_page | 25 | Numbers of users to return at a time
page | 1 | Page number.

<aside class="notice">
The Posts JSONArray response structure is the same as returned in the main feed top category
</aside>

# Comments

## Create a Comment
This endpoint creates a comment on a post.


```swift
let headers = [
  "content-type": "multipart/form-data; boundary=---011000010111000001101001",
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "authorization": ""
]

let parameters = [
  [
    "name": "content",
    "value": "@ronketinker @solapemi Tress is in YCombinator W17!!!"
  ]
]

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/posts/68/comments")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "POST"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData


```

```java
OkHttpClient client = new OkHttpClient();
MediaType mediaType = MediaType.parse("multipart/form-data; boundary=---011000010111000001101001");
RequestBody body = RequestBody.create(mediaType, "-----011000010111000001101001\r\nContent-Disposition: form-data; name=\"content\"\r\n\r\n@ronketinker @solapemi Tress is in YCombinator W17!!!\r\n-----011000010111000001101001--");
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/posts/68/comments")
  .post(body)
  .addHeader("content-type", "multipart/form-data; boundary=---011000010111000001101001")
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", 
  .build();

Response response = client.newCall(request).execute();
```

> A successful create comment request returns JSON structured like this:

```json
{
  "id": 47,
  "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
  "full_name": " ",
  "username": "ronke",
  "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
  "time_ago": "a minute",
  "user_id": 67
}

```

#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/posts/<post_id>/comments`

##### Headers

`Authorization: xxxxxxxxxxxxxxxxxx8790730598790`

Parameter | Description
--------- | -----------
Authorization | Required. This is the authentication_token of the user whose is making the request


#### URL Parameters

Parameter | Description
--------- | -----------
post_id | Required. ID of the post

#### Body Parameters

Parameter | Description
--------- | -----------
content | Required. Content of the comment

## Get Comments

This endpoint retrieves all comments on a post.


```swift
let headers = [
  "content-type": "multipart/form-data; boundary=---011000010111000001101001",
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
]
var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/posts/68/comments")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData


```

```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/posts/68/comments")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .build();

Response response = client.newCall(request).execute();
```

> A successful create comment request returns JSON structured like this:

```json
{
  "comments": [
    {
      "id": 12,
      "content": "hair looks great!",
      "full_name": " ",
      "username": "xxolaxxxxx",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/026/small/B8Vo-6yIEAER-_C.jpg.jpg?1454659779",
      "time_ago": "10 months",
      "user_id": 26
    },
    {
      "id": 13,
      "content": "hair looks great!",
      "full_name": " ",
      "username": "xxolaxxxxx",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/026/small/B8Vo-6yIEAER-_C.jpg.jpg?1454659779",
      "time_ago": "10 months",
      "user_id": 26
    },
    {
      "id": 16,
      "content": "hair looks great!",
      "full_name": "OlaEsther Tunde",
      "username": "olame",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/029/small/_IGP3572.jpg.jpg?1454659780",
      "time_ago": "8 months",
      "user_id": 29
    },
    {
      "id": 30,
      "content": "Tress on Blavity! Tress is in YCombinator!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 31,
      "content": "@ronke @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 32,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 33,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 34,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 35,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 36,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 37,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 38,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 39,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 40,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 41,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 42,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 43,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 44,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "2 months",
      "user_id": 67
    },
    {
      "id": 45,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "28 days",
      "user_id": 67
    },
    {
      "id": 46,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "9 days",
      "user_id": 67
    },
    {
      "id": 47,
      "content": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "full_name": " ",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/Screenshot_20160503-130140.png.png?1468909319",
      "time_ago": "3 minutes",
      "user_id": 67
    }
  ],
  "meta": {
    "pagination": {
      "per_page": 0,
      "total_pages": 1,
      "total_objects": 21
    }
  }
}

```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/posts/<post_id>/comments`


#### URL Parameters

Parameter | Description
--------- | -----------
post_id | Required. ID of the post


# Salons

## Get Salons

This endpoint retrieves all salons.


```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
]
var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/salons")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData


```

```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/salons")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .build();

Response response = client.newCall(request).execute();
```

> A successful get salons request returns JSON structured like this:

```json
{
  "salons": [
    {
      "id": 39,
      "name": null,
      "location": null,
      "latitude": null,
      "longitude": null
    },
    {
      "id": 38,
      "name": "twists & locs",
      "location": "East Legon, Accra, Ghana",
      "latitude": 5.6378865,
      "longitude": -0.1612029
    },
    {
      "id": 36,
      "name": null,
      "location": "East Legon, Accra, Ghana",
      "latitude": null,
      "longitude": null
    }
  ]
}

```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/salons`

# Categories

## Get Categories

This endpoint retrieves all categories.


```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
]
var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/categories")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData


```

```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/categories")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .build();

Response response = client.newCall(request).execute();
```

> A successful get categories request returns JSON structured like this:

```json
{
  "categories": [
    {
      "id": 1,
      "name": "Braids"
    },
    {
      "id": 2,
      "name": "Natural Hair"
    },
    {
      "id": 4,
      "name": "Relaxed Hair"
    },
    {
      "id": 3,
      "name": "Weaves"
    }
  ]
}

```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/categories`

# Price Ranges

## Get Price Ranges

This endpoint retrieves all price_ranges.


```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
]
var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/price_ranges")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData


```

```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/price_ranges")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .build();

Response response = client.newCall(request).execute();
```

> A successful get price ranges request returns JSON structured like this:

```json
{
  "price_ranges": [
    {
      "id": 1,
      "price": "0 - 50",
      "price_gh": "0 - 50",
      "price_ng": "0 - 1500"
    },
    {
      "id": 2,
      "price": "60 - 100",
      "price_gh": "60 - 100",
      "price_ng": "1600 - 2500"
    },
    {
      "id": 3,
      "price": "110 - 200",
      "price_gh": "110 - 200",
      "price_ng": "2500 - 5000"
    },
    {
      "id": 4,
      "price": "200 - 400",
      "price_gh": "300 - 600",
      "price_ng": "5100 - 10,000"
    },
    {
      "id": 5,
      "price": "400+",
      "price_gh": "600+",
      "price_ng": "10,000+"
    }
  ]
}

```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/price_ranges`

# Hair Types

## Get Hair Types

This endpoint retrieves all hair types.


```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": ""
]
var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v3/hair_types")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData


```

```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/hair_types")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .build();

Response response = client.newCall(request).execute();
```

> A successful get hair_types request returns JSON structured like this:

```json
{
  "hair_types": [
    {
      "id": 1,
      "name": "Locs / Dreadlocs"
    },
    {
      "id": 2,
      "name": "Natural / Kinky Curls"
    },
    {
      "id": 3,
      "name": "Relaxed / Permed Hair"
    },
    {
      "id": 4,
      "name": "Texlaxed Hair"
    }
  ]
}

```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/hair_types`

# Questions

## Create Question
This endpoint creates a new question.


```swift

let request = NSMutableURLRequest(url: NSURL(string: "http://localhost:5000/api/v2/users/67/questions")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})


```

```java
Request request = new Request.Builder()
  .url("http://localhost:5000/api/v2/users/67/questions")
  .post(body)
  .addHeader("content-type", "multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW")
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();

Response response = client.newCall(request).execute();
```

> A successful question creation request returns JSON structured like this:

```json
{
  "id": 7,
  "title": "How to achieve healthy natural hair growth?",
  "description": "@ronketinker @solapemi Why do I have hard time growing Nigerian natural hair? Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque venenatis lacinia facilisis. Sed non enim hendrerit, gravida magna eu, pharetra orci.",
  "category_id": 1,
  "user_id": 67,
  "fullname": "Kemi CoolBraids",
  "username": "ronke",
  "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/IMG-20161219-WA0000.jpg.jpg?1484079895",
  "user_is_salon": true,
  "answers_count": 0,
  "time_ago": "a minute",
  "likes_count": 0,
  "created_at": "2017-02-20T18:08:41Z",
  "updated_at": "2017-02-20T18:08:41Z"
}

```

#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/questions`

#### Header Parameters

Parameter | Description
--------- | -----------
Authorization | Required. authentication_token of the user    

#### URL Parameters

Parameter | Description
--------- | -----------
user_id | Required. ID of the user

#### Body Parameters

Parameter | Description
--------- | -----------
title | Required. title of the question
description | Required. question description
category | Required. category ID of the question

## Get all Questions by Category
This endpoint retrieves a feed of questions by category.


```swift

let request = NSMutableURLRequest(url: NSURL(string: "http://localhost:5000/api/v3/questions/discover/filter?category_ids=2%2C1%3Fper_page%3D10%2Cpage%3D1")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()


```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/questions/discover/filter?category_ids=2%2C1%3Fper_page%3D10%2Cpage%3D1")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .addHeader("authorization", "")
  .build();

Response response = client.newCall(request).execute();
```

> A successful questions feed request returns JSON structured like this:

```json
{
  "questions": [
    {
      "id": 7,
      "title": "How to achieve healthy natural hair growth?",
      "description": "@ronketinker @solapemi Why do I have hard time growing Nigerian natural hair? Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque venenatis lacinia facilisis. Sed non enim hendrerit, gravida magna eu, pharetra orci.",
      "category_id": 1,
      "user_id": 67,
      "fullname": "Kemi CoolBraids",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/IMG-20161219-WA0000.jpg.jpg?1484079895",
      "user_is_salon": true,
      "answers_count": 0,
      "time_ago": "6 minutes",
      "likes_count": 0,
      "created_at": "2017-02-20T18:08:41Z",
      "updated_at": "2017-02-20T18:08:41Z"
    }
  ],
  "meta": {
    "pagination": {
      "per_page": 0,
      "total_pages": 1,
      "total_objects": 1
    }
  }
}

```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/questions/categories/<category_id>,<category_id>?per_page=20,page=1`

#### URL Parameters

Parameter | Description
--------- | -----------
category_id | Required. CategoryID. Can be more than 1, seperated by commas
per_page | Required. Pagination param for endless scroll
page | Required. Pagination param for endless scroll

## Get Question
This endpoint retrieves a question by it's ID.


```swift


```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("http://localhost:5000/api/v3/questions/7")
  .get()
  .addHeader("x-tress-client-key-id", "")
  .addHeader("x-tress-client-key-secret", "")
  .build();

Response response = client.newCall(request).execute();

```

> A successful request returns JSON structured like this:

```json
{
  "id": 7,
  "title": "How to achieve healthy natural hair growth?",
  "description": "@ronketinker @solapemi Why do I have hard time growing Nigerian natural hair? Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque venenatis lacinia facilisis. Sed non enim hendrerit, gravida magna eu, pharetra orci.",
  "category_id": 1,
  "user_id": 67,
  "fullname": "Kemi CoolBraids",
  "username": "ronke",
  "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/IMG-20161219-WA0000.jpg.jpg?1484079895",
  "user_is_salon": true,
  "answers_count": 0,
  "time_ago": "a minute",
  "likes_count": 0,
  "created_at": "2017-02-20T18:08:41Z",
  "updated_at": "2017-02-20T18:08:41Z"
}

```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/questions/<id>`

#### URL Parameters

Parameter | Description
--------- | -----------
id | Required. ID of the question

## Like Question 
This is the endpoint to like a question.


```swift


```

```java

```

> A successful request returns JSON structured like this:

```json
{
  "success": true,
  "count": 1
}

```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/questions/<id>/like`

#### Header Parameters

Parameter | Description
--------- | -----------
Authorization | Required. authentication token of the user liking the question

#### URL Parameters

Parameter | Description
--------- | -----------
user_id | Required. ID of the user liking the question
id | Required. ID of the question

## Unlike Question 
This is the endpoint to unlike a question.


```swift


```

```java

```

> A successful request returns JSON structured like this:

```json
{
  "success": true,
  "count": 1
}

```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/questions/<id>/unlike`

#### Header Parameters

Parameter | Description
--------- | -----------
Authorization | Required. authentication token of the user unliking the question

#### URL Parameters

Parameter | Description
--------- | -----------
user_id | Required. ID of the user liking the question
id | Required. ID of the question

# Answers

## Create Answer
This endpoint creates an answer to a question.


```swift

```

```java

```

> A successful answer creation request returns JSON structured like this:

```json
{
  "id": 7,
  "content": "@ronketinker @solapemi Protective style it, less heat and easy detangle",
  "question_id": 7,
  "user_id": 67,
  "fullname": "Kemi CoolBraids",
  "username": "ronke",
  "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/IMG-20161219-WA0000.jpg.jpg?1484079895",
  "user_is_salon": true,
  "time_ago": "a minute",
  "upvote_count": 0,
  "downvote_count": 0,
  "created_at": "2017-02-20T18:46:08Z",
  "updated_at": "2017-02-20T18:46:08Z"
}


```

#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/questions/<question_id>/answers`

#### Header Parameters

Parameter | Description
--------- | -----------
Authorization | Required. authentication_token of the user answering the question   

#### URL Parameters

Parameter | Description
--------- | -----------
question_id | Required. ID of the question

#### Body Parameters

Parameter | Description
--------- | -----------
content | Required. content of the answer

## Get Answers to a Question
This endpoint retreives all the answers to a question.

```swift

```

```java

```

> A successful request returns JSON structured like this:

```json
{
  "answers": [
    {
      "id": 7,
      "content": "@ronketinker @solapemi Protective style it, less heat and easy detangle",
      "question_id": 7,
      "user_id": 67,
      "fullname": "Kemi CoolBraids",
      "username": "ronke",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/IMG-20161219-WA0000.jpg.jpg?1484079895",
      "user_is_salon": true,
      "time_ago": "32 minutes",
      "upvote_count": 0,
      "downvote_count": 0,
      "created_at": "2017-02-20T18:46:08Z",
      "updated_at": "2017-02-20T18:46:08Z"
    }
  ],
  "meta": {
    "pagination": {
      "per_page": 20,
      "total_pages": 1,
      "total_objects": 1
    }
  }
}


```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/questions/<question_id>/answers?per_page=20,page=1`

#### URL Parameters

Parameter | Description
--------- | -----------
question_id | Required. ID of the question
per_page | Required. pagination params for endless scroll
page | Required. pagination params for endless scroll

## Get one Answer
This endpoint retreives an answer


```swift

```

```java

```

> A successful request returns JSON structured like this:

```json
{
  "id": 7,
  "content": "@ronketinker @solapemi Protective style it, less heat and easy detangle",
  "question_id": 7,
  "user_id": 67,
  "fullname": "Kemi CoolBraids",
  "username": "ronke",
  "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/IMG-20161219-WA0000.jpg.jpg?1484079895",
  "user_is_salon": true,
  "time_ago": "37 minutes",
  "upvote_count": 0,
  "downvote_count": 0,
  "created_at": "2017-02-20T18:46:08Z",
  "updated_at": "2017-02-20T18:46:08Z"
}


```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/questions/<question_id>/answers/<answer_id>`

#### URL Parameters

Parameter | Description
--------- | -----------
question_id | Required. ID of the question
answer_id | Required. ID of the answer

## Upvote Answer
This is the endpoint to upvote an answer


```swift

```

```java

```

> A successful request returns JSON structured like this:

```json
{
  "success": true,
  "count": 1
}


```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/questions/<question_id>/answers/<answer_id>/upvote`


#### Header Parameters

Parameter | Description
--------- | -----------
Authorization | Required. authentication_token of the user upvoting

#### URL Parameters

Parameter | Description
--------- | -----------
question_id | Required. ID of the question
answer_id | Required. ID of the answer

## UndoUpvote Answer
This is the endpoint to undo an upvoted answer


```swift

```

```java

```

> A successful request returns JSON structured like this:

```json
{
  "success": true,
  "count": 1
}


```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/questions/<question_id>/answers/<answer_id>/undoupvote`


#### Header Parameters

Parameter | Description
--------- | -----------
Authorization | Required. authentication_token of the user undoing the upvote

#### URL Parameters

Parameter | Description
--------- | -----------
question_id | Required. ID of the question
answer_id | Required. ID of the answer

## Downvote Answer 
This is the endpoint to undo a downvoted answer


```swift

```

```java

```

> A successful request returns JSON structured like this:

```json
{
  "success": true,
  "count": 1
}


```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/questions/<question_id>/answers/<answer_id>/downvote`


#### Header Parameters

Parameter | Description
--------- | -----------
Authorization | Required. authentication_token of the user downvoting

#### URL Parameters

Parameter | Description
--------- | -----------
question_id | Required. ID of the question
answer_id | Required. ID of the answer

## Undo Downvote Answer 
This is the endpoint to undo a downvoted answer


```swift

```

```java

```

> A successful request returns JSON structured like this:

```json
{
  "success": true,
  "count": 1
}


```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/questions/<question_id>/answers/<answer_id>/undodownvote`


#### Header Parameters

Parameter | Description
--------- | -----------
Authorization | Required. authentication_token of the user undoing the downvote

#### URL Parameters

Parameter | Description
--------- | -----------
question_id | Required. ID of the question
answer_id | Required. ID of the answer

# Hair Tips

## Filter HairTips by Type & Category

This is the endpoint to retrieve a feed of hair tips by type and category


```swift

```

```java

```

> A successful request returns JSON structured like this:

```json
{
  "hair_tips": [
    {
      "id": 1,
      "title": "4C Natural Hairstyles: Finger Coils!",
      "cover_image": "https://s3.amazonaws.com/tress-api-development/hair_tips/cover_images/000/000/001/medium/fingercoil.png.png?1473944227",
      "url": "http://www.thekinkandi.com/finger-coils/",
      "brief_intro": "Simply put, a Finger coil is achieved by twirling and twirling a section of hair with, and round your finger.\r\n\r\n‘Finger Coils’ are pretty much the same as ‘Comb coils’ except that here, you use your fingers to coil, instead of a rat tail comb. Stay with me, okay?",
      "hair_tips_type": "article",
      "category": "Natural Hair",
      "author": "AfrikanButterfly on thekinkandi.com",
      "views_count": 2,
      "time_ago": "5 months",
      "comments_count": 1,
      "created_at": "2016-09-15T12:46:10Z",
      "updated_at": "2017-02-20T19:47:18Z"
    }
  ],
  "meta": {
    "pagination": {
      "per_page": 10,
      "total_pages": 1,
      "total_objects": 1
    }
  }
}


```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/hair_tips/types/filter?hair_tips_type=<type>&category_id=<catId>,<catId>&page=1&per_page=10`


#### URL Parameters

Parameter | Description
--------- | -----------
type | Required. It's either "article" or "video"
catId | Required. Category ID, can be more than one, seperated by commas
per_page | Required. Pagination param
page | Required. Pagination param

## GET HairTip
This is the endpoint to retrieve a feed of hair tips by type and category

Once retrieve, the tip url is loaded in a webview on the client.


```swift

```

```java

```

> A successful request returns JSON structured like this:

```json
{
  "id": 1,
  "title": "4C Natural Hairstyles: Finger Coils!",
  "cover_image": "https://s3.amazonaws.com/tress-api-development/hair_tips/cover_images/000/000/001/medium/fingercoil.png.png?1473944227",
  "url": "http://www.thekinkandi.com/finger-coils/",
  "brief_intro": "Simply put, a Finger coil is achieved by twirling and twirling a section of hair with, and round your finger.\r\n\r\n‘Finger Coils’ are pretty much the same as ‘Comb coils’ except that here, you use your fingers to coil, instead of a rat tail comb. Stay with me, okay?",
  "hair_tips_type": "article",
  "category": "Natural Hair",
  "author": "AfrikanButterfly on thekinkandi.com",
  "views_count": 2,
  "time_ago": "5 months",
  "comments_count": 1,
  "created_at": "2016-09-15T12:46:10Z",
  "updated_at": "2017-02-20T19:47:18Z"
}


```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/hair_tips/<id>`


#### URL Parameters

Parameter | Description
--------- | -----------
id | Required. ID of the hair tip


# Unauthenticated User Access

## Register Temp Session for with Temp ID

Register temporary session of unauthenticated user

```swift

```

```java

```
> The request returns JSON structured like this:

```json
{
  "temp_id": 58
}
```

#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/users/temporary_session`

#### Request Body Parameters

Parameter | Description
--------- | -----------
temp_id | Required. Randomly generatedd on the Client
device_id | Required.
device_type | Required. 


<aside class="notice">
Persist temp_id on the client for future unauthenticated requests.
</aside>

## Fetch Home Feed with Temp ID for Unauthenticated User

Get Feed Post for unauthenticated users

```swift

```

```java

```
> The request returns Post Feed JSON structured like this:

```json
{
}
```

#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/posts/discover/temporary_session?per_page=10,page=1`

#### Query Parameters


Parameter | Default | Description
--------- | ------- | -----------
temp_id | temporary id
per_page | 10 | Numbers of users to return at a time
page | 1 | Page number.
(Pagination for endless scrolling)

<aside class="notice">
The Posts JSONArray response structure is the same as returned in the home feed for authenticated users
</aside>



## Fetch User Suggestions with Temp ID for Unauthenticated User

Get User Suggestions for unauthenticated users

```swift

```

```java

```
> The request returns User JSONArray structured like this:

```json
{
}
```

#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/suggestions/discover/temporary_session?temp_id=845904,per_page=10,page=1`

#### Query Parameters


Parameter | Default | Description
--------- | ------- | -----------
temp_id | temporary id
per_page | 10 | Numbers of users to return at a time
page | 1 | Page number.
(Pagination for endless scrolling)

<aside class="notice">
The Users JSONArray response structure is the same as returned in the recommended user suggestions for authenticated users
</aside>



# Handling Branch Deeplinking on Tress
Here's Branch's [doc](https://dev.branch.io/getting-started/deep-link-routing/guide/android/) on how to retrieve the deeplink parameters and route to the appropriate screen on the client. 


## Handling Post Mobile Web Url 
A typical mobile web shared url looks like this `https://www.tressapp.com/p/_-eukhdy5o1a9l1699o0gq`, when the url is visited, the Branch Web SDK passes some parameters that when implemented and handled on the android & ios clients, will open the app and redirect to the post detailed view based on the post attributes passed.

You need to retrieve these params and route to the appropriate post's detail view.

#### Mobile Web Post Url Parameters

Parameter | Description
--------- | -----------
post_id | Post ID
post_image_url | Post Image
user_id | User ID 
username | Username

<aside class="notice">
This leads to the Post Detail Screen. Please take note of the action_header values with sub parameters as they are used to make a request to an endpoint or fill the screen in the destination screens
</aside>

## Other Branch Deeplinks with Parameters
There are several other links we've created with attributes that need to handled and sent to their appropriate views on the client/app.

#### Deeplinks Parameters

Parameters | Screens They Link to
--------- | -----------
upload_profile | Edit Profile Screen
upload_photo | Add Post Screen

#### Deeplinks Parameters Depending action_header Values
If a deeplink parameter has action_header, the screen it leads to depends on the value of the action_header

Parameters | Value | Screens They Lead To
--------- |----------- |-----------
action_header | isTrending | Trending Screen
action_header | isSuggestion |Search / Suggestion Screen
action_header | isAddPostInstagram | Instagram Add Post Screen
action_header | isStylistOptIn | Stylist OptIn Screen to choose if you're a stylist or not
action_header | isQuestionFeed | Question Feed Screen - has sub parameter of `category_id` to determine the category of the question feed to lead to. By default `category_id: 3`
action_header | isTipFeed | Tips Feed Screen - has sub parameters of `category_id` and `hair_tips_type` to determine the category of the question feed to lead to. By default `category_id: 3` and `hair_tips_type: "article"`
action_header | isAskQuestion | Ask Question Screen

<aside class="notice">
Please take note of the action_header values with sub parameters as they are used to make a request to an endpoint or fill the screen in the destination screens
</aside>

# Handling One Signal Notifications Received on Tress

Check out One Signal's [doc](https://documentation.onesignal.com/docs/android-native-sdk) to see how to access the additional data payload received for each notifications.

All notifications received have action_header, the screen a notification leads to depends on the value of the action_header

## Handling Notifications Depending on the action_header and parameters

Parameters | Value | Screens They Lead To
--------- |----------- |-----------
action_header | isTrending | Trending Screen
action_header | isSuggestion |People Suggestion Screen
action_header | isAddPostInstagram | Instagram Add Post Screen
action_header | isStylistOptIn | Stylist OptIn Screen to choose if you're a stylist or not
action_header | isQuestionFeed | Question Feed Screen - has sub parameter of `category_id` to determine the category of the question feed to lead to. By default `category_id: 3`
action_header | isHairTipFeed | Tips Feed Screen - has sub parameters of `category_id` and `hair_tips_type` to determine the category of the question feed to lead to. By default `category_id: 3` and `hair_tips_type: "article"`
action_header | isAskQuestion | Ask Question Screen
action_header | isLike | Post Detail Screen (sub params are: `model_id`, `post_image`, `user_id`, `username`, `post_username`)
action_header | isHairTipDetail | HairTip Detail Screen (sub params are: `model_id` and `tip_url`)
action_header | isAddPost | Add Post Screen
action_header | isComment | Comments Screen (sub params are: `model_id` - this is the post's id to retrieve its comments)
action_header | isFollowing | User Profile Screen (sub params are: `user_id` and `username`)
action_header | isAddAvatar | Edit Profile Screen
action_header | isInviteFriends | Invite Friends Screen
action_header | isChooseTrendsetter | Home Feed Screen
action_header | isHashTag | HashTag Feed Screen (sub param is: `tagged_name` - e.g #naturalhair this is the param sent to posts hashtag feed endpoint )
action_header | isHairCategory | Category Feed Screen Screen (sub param are: `user_id`, `category_id`, `category_name` )
action_header | isHairPriceRange | Price Range Feed Screen (sub param are: `user_id`, `price_range_id`, `price_range_name` )
action_header | isFilter | Filter Screen
action_header | isHairstyleSuggestion | Hairstyle Suggestion Screen
action_header | isLaunchUrl | Launch the Url in the sub param in a webview (sub param is: `launch_url`)
action_header | isUpvoteAnswer | Question Detail Screen (sub params are: `model_id`, `user_avatar`, `fullname`, `username`, `title`, `description`, `time`, `responses_count`, `likes_count, `user_id` )
action_header | isLikeQuestion | Question Detail Screen ( same as above)
action_header | isQuestion | Question Detail Screen ( same as above)
action_header | isAnswer | Question Detail Screen ( same as above)

<aside class="notice">
Please take note of the action_header values with sub parameters as they are used to make a request to an endpoint or fill the screen in the destination screens
</aside>

# Collections

## Get Collections
This endpoint retrieves a user's collections.


```swift


```

```java

```

> A successful collections request returns JSON structured like this:

```json
{
  "collections": [
    {
      "id": 3,
      "title": "playful",
      "description": "playful",
      "user_id": 29,
      "posts": [
        {
          "id": 84,
          "user_id": 67,
          "username": "ronke",
          "fullname": "Kemi CoolBraids",
          "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/IMG-20161219-WA0000.jpg.jpg?1484079895",
          "salon_name": null,
          "salon_location": null,
          "image": "https://s3.amazonaws.com/tress-api-development/posts/images/000/000/084/medium/hair2.jpg.jpg.jpg?1471331126",
          "comments": [],
          "comments_count": 0,
          "category": {
            "id": 2,
            "name": "Natural Hair",
            "created_at": "2015-08-28T11:18:28.904Z",
            "updated_at": "2015-08-28T11:18:28.904Z"
          },
          "price_range": {
            "id": 1,
            "price": "0 - 50",
            "created_at": "2015-09-18T14:13:29.759Z",
            "updated_at": "2016-02-09T10:52:40.942Z",
            "price_gh": "0 - 50",
            "price_ng": "0 - 1500"
          },
          "time_ago": "8 months",
          "likes": 0,
          "caption": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
          "stylename": null,
          "price_range_id": 1,
          "duration": null,
          "products": "shea butter",
          "category_id": 2,
          "salon": "",
          "user_is_salon": true,
          "slug": "m0xilzepmopmsdyh3yzgja",
          "created_at": "2016-08-16T07:05:19Z",
          "updated_at": "2016-08-16T07:05:28Z"
        },
        {
          "id": 101,
          "user_id": 67,
          "username": "ronke",
          "fullname": "Kemi CoolBraids",
          "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/IMG-20161219-WA0000.jpg.jpg?1484079895",
          "salon_name": null,
          "salon_location": null,
          "image": "https://s3.amazonaws.com/tress-api-development/posts/images/000/000/101/medium/IMG_20150507_091654_edit.jpg.jpg?1472570378",
          "comments": [],
          "comments_count": 0,
          "category": {
            "id": 2,
            "name": "Natural Hair",
            "created_at": "2015-08-28T11:18:28.904Z",
            "updated_at": "2015-08-28T11:18:28.904Z"
          },
          "price_range": {
            "id": 1,
            "price": "0 - 50",
            "created_at": "2015-09-18T14:13:29.759Z",
            "updated_at": "2016-02-09T10:52:40.942Z",
            "price_gh": "0 - 50",
            "price_ng": "0 - 1500"
          },
          "time_ago": "7 months",
          "likes": 0,
          "caption": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
          "stylename": null,
          "price_range_id": 1,
          "duration": null,
          "products": "shea butter",
          "category_id": 2,
          "salon": "",
          "user_is_salon": true,
          "slug": "baa7luhewgu-t3noaggttg",
          "created_at": "2016-08-30T15:19:18Z",
          "updated_at": "2017-02-23T22:21:37Z"
        }
      ]
    }
  ],
  "meta": {
    "pagination": {
      "per_page": 0,
      "total_pages": 1,
      "total_objects": 1
    }
  }
}

```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/collections?per_page=10,page=1`

#### URL Parameters

Parameter | Description
--------- | -----------
user_id | Required. ID of the user
per_page | Required. Number of items per page for pagination
page | Required. Page number for pagination


## Get Collection
This endpoint retrieves a user's collections.


```swift


```

```java

```

> A successful collection creation request returns JSON structured like this:

```json
{
  "id": 4,
  "title": "Corporate Hairstyles",
  "description": "suitable for office looks blah",
  "user_id": 67,
  "posts": [
    {
      "id": 84,
      "user_id": 67,
      "username": "ronke",
      "fullname": "Kemi CoolBraids",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/IMG-20161219-WA0000.jpg.jpg?1484079895",
      "salon_name": null,
      "salon_location": null,
      "image": "https://s3.amazonaws.com/tress-api-development/posts/images/000/000/084/medium/hair2.jpg.jpg.jpg?1471331126",
      "comments": [],
      "comments_count": 0,
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-08-28T11:18:28.904Z",
        "updated_at": "2015-08-28T11:18:28.904Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-09-18T14:13:29.759Z",
        "updated_at": "2016-02-09T10:52:40.942Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "8 months",
      "likes": 0,
      "caption": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "shea butter",
      "category_id": 2,
      "salon": "",
      "user_is_salon": true,
      "slug": "m0xilzepmopmsdyh3yzgja",
      "created_at": "2016-08-16T07:05:19Z",
      "updated_at": "2016-08-16T07:05:28Z"
    }
  ]
}

```

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/collections/<collection_id>`

#### URL Parameters

Parameter | Description
--------- | -----------
user_id | Required. ID of the user
collection_id | Required. ID of the collection


## Create Collection
This endpoint creates a new collection.


```swift


```

```java

```

> A successful collection creation request returns JSON structured like this:

```json
{
  "id": 4,
  "title": "Corporate Hairstyles",
  "description": "suitable for office looks blah",
  "user_id": 67,
  "posts": [
    {
      "id": 84,
      "user_id": 67,
      "username": "ronke",
      "fullname": "Kemi CoolBraids",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/IMG-20161219-WA0000.jpg.jpg?1484079895",
      "salon_name": null,
      "salon_location": null,
      "image": "https://s3.amazonaws.com/tress-api-development/posts/images/000/000/084/medium/hair2.jpg.jpg.jpg?1471331126",
      "comments": [],
      "comments_count": 0,
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-08-28T11:18:28.904Z",
        "updated_at": "2015-08-28T11:18:28.904Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-09-18T14:13:29.759Z",
        "updated_at": "2016-02-09T10:52:40.942Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "8 months",
      "likes": 0,
      "caption": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "shea butter",
      "category_id": 2,
      "salon": "",
      "user_is_salon": true,
      "slug": "m0xilzepmopmsdyh3yzgja",
      "created_at": "2016-08-16T07:05:19Z",
      "updated_at": "2016-08-16T07:05:28Z"
    }
  ]
}

```

#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/collections/`

#### Header Parameters

Parameter | Description
--------- | -----------
Authorization | Required. authentication_token of the user    

#### URL Parameters

Parameter | Description
--------- | -----------
user_id | Required. ID of the user

#### Body Parameters

Parameter | Description
--------- | -----------
title | Required. title of the question
description | Required. question description
tag_list | add tags to a collection, seperated by commas
post_id | Required. ID of the post you're adding to the collection

## Update Collection
This endpoint updates an existing collection. It's specifically for removing a post from a collection or editing the title and description of a collection


```swift


```

```java

```

> A successful collection update request returns JSON structured like this:

```json
{
  "id": 4,
  "title": "Corporate Hairstyles",
  "description": "suitable for office looks blah",
  "user_id": 67,
  "posts": [
    {
      "id": 84,
      "user_id": 67,
      "username": "ronke",
      "fullname": "Kemi CoolBraids",
      "user_avatar": "https://s3.amazonaws.com/tress-api-development/users/avatars/000/000/067/small/IMG-20161219-WA0000.jpg.jpg?1484079895",
      "salon_name": null,
      "salon_location": null,
      "image": "https://s3.amazonaws.com/tress-api-development/posts/images/000/000/084/medium/hair2.jpg.jpg.jpg?1471331126",
      "comments": [],
      "comments_count": 0,
      "category": {
        "id": 2,
        "name": "Natural Hair",
        "created_at": "2015-08-28T11:18:28.904Z",
        "updated_at": "2015-08-28T11:18:28.904Z"
      },
      "price_range": {
        "id": 1,
        "price": "0 - 50",
        "created_at": "2015-09-18T14:13:29.759Z",
        "updated_at": "2016-02-09T10:52:40.942Z",
        "price_gh": "0 - 50",
        "price_ng": "0 - 1500"
      },
      "time_ago": "8 months",
      "likes": 0,
      "caption": "@ronketinker @solapemi Tress is in YCombinator W17!!!",
      "stylename": null,
      "price_range_id": 1,
      "duration": null,
      "products": "shea butter",
      "category_id": 2,
      "salon": "",
      "user_is_salon": true,
      "slug": "m0xilzepmopmsdyh3yzgja",
      "created_at": "2016-08-16T07:05:19Z",
      "updated_at": "2016-08-16T07:05:28Z"
    }
  ]
}

```

#### HTTP Request

`PATCH https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/collections/<collection_id>`

#### Header Parameters

Parameter | Description
--------- | -----------
Authorization | Required. authentication_token of the user    

#### URL Parameters

Parameter | Description
--------- | -----------
user_id | Required. ID of the user
collection_id | Required. ID of the collection that is being edited

#### Body Parameters

Parameter | Description
--------- | -----------
title| Title
description| Description
tag_list| Tags, seperated by commas
post_ids | IDs seperated by commas, of all the posts in the collection, including or excluding the ID(s) you're adding or removing


## Delete Collection
This endpoint deletes a user's existing collection


```swift


```

```java

```

> A successful collection update request returns JSON structured like this:

```json
STATUS: 204

```

#### HTTP Request

`DELETE https://tressapi-staging.herokuapp.com/api/v3/users/<user_id>/collections/<collection_id>`

#### Header Parameters

Parameter | Description
--------- | -----------
Authorization | Required. authentication_token of the user    

#### URL Parameters

Parameter | Description
--------- | -----------
user_id | Required. ID of the user
collection_id | Required. ID of the collection that is being edited




