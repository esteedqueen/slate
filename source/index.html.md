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

`https://tressapi-staging.herokuapp.com/api/v2`

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
  "x-tress-client-key-id": "fjsdkfas4904952",
  "x-tress-client-key-secret": "ri04r0-8r5-34089-52589",
  "content-type": "application/json",
  "cache-control": "no-cache",
  "postman-token": "10ae502f-a306-5529-0a83-dddbbffd03b9"
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
  .url("https://tressapi-staging.herokuapp.com/api/v2/users")
  .post(body)
  .addHeader("x-tress-client-key-id", "irr0283-1=8573028")
  .addHeader("x-tress-client-key-secret", "123jr59kled85903")
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

`POST https://tressapi-staging.herokuapp.com/api/v2/users`

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

`POST https://tressapi-staging.herokuapp.com/api/v2/users/auth/facebook/callback`

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

    `POST https://tressapi-staging.herokuapp.com/api/v2verify_digits_account` 

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

    `POST https://tressapi-staging.herokuapp.com/api/v2digits_user`
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
  .url("https://www.tressapp.co/api/v2/users/sign_in")
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

> An unsuccessful sign in request returns JSON structured like this:

```json
{
  "success": false,
  "message": "Error with your email or password"
}
```
#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v2/users/sign_in`

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

var request = NSMutableURLRequest(URL: NSURL(string: "https://tressapi-staging.herokuapp.com/api/v2/users/sign_out")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "DELETE"
request.allHTTPHeaderFields = headers

```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://tressapi-staging.herokuapp.com/api/v2/users/sign_out")
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

`DELTE https://tressapi-staging.herokuapp.com/api/v2/users/sign_out`

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

var request = NSMutableURLRequest(URL: NSURL(string: "https://tressapi-staging.herokuapp.com/api/v2/users/29/update_password")!,
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
  .url("https://tressapi-staging.herokuapp.com/api/v2/users/29/update_password")
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

> An unsuccessful request returns JSON structured like this:

```json
{
  "success": false,
  "message": "Wrong password"
}
```
#### HTTP Request

`POST https://tressapi-staging.herokuapp.com/api/v2/users/<id>/update_password`

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
  .url("https://stage.tressapp.co/api/v2/users/95")
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

`PATCH https://tressapi-staging.herokuapp.com/api/v2/users/<id>`

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

var request = NSMutableURLRequest(URL: NSURL(string: "http://localhost:5000/api/v2/users/53")!,
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
  .url("http://localhost:5000/api/v2/users/53")
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

`PATCH https://tressapi-staging.herokuapp.com/api/v2/users/<id>`

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

## Reset Password

```swift
let headers = [
  "x-tress-client-key-id": "",
  "x-tress-client-key-secret": "",
  "content-type": "application/json"
]
let parameters = ["user": ["email": "example@gmail.com"]]

let postData = NSJSONSerialization.dataWithJSONObject(parameters, options: nil, error: nil)

var request = NSMutableURLRequest(URL: NSURL(string: "https://tressapi-staging.herokuapp.com/api/v2/users/password")!,
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
  .url("https://tressapi-staging.herokuapp.com/api/v2/users/password")
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

`POST https://tressapi-staging.herokuapp.com/api/v2/users/password`

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
  .url("https://tressapi-staging.herokuapp.com/api/v2/users")
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

`GET https://tressapi-staging.herokuapp.com/api/v2/users?per_page=25,page=1`

This endpoint retrieves all users by pagination, 25 at a time.

#### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
per_page | 25 | Numbers of users to return at a time
page | 1 | Page number.

### Pagination + Search by Username, Firstname or Lastname

`GET https://tressapi-staging.herokuapp.com/api/v2/users?search=bola,per_page=25,page=1`

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

### Pagination + Search by Username Only 
NB: Useful for @mentions users query

`GET https://tressapi-staging.herokuapp.com/api/v2/users?search=bola,per_page=25,page=1`

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

var request = NSMutableURLRequest(URL: NSURL(string: "https://tressapi-staging.herokuapp.com/api/v2/users/18731")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://tressapi-staging.herokuapp.com/api/v2/users/18731")
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

`GET https://tressapi-staging.herokuapp.com/api/v2/users/<id>`

#### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the user to retrieve

### By Username

#### HTTP Request

`GET https://tressapi-staging.herokuapp.com/api/v2/users/<username>`

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

var request = NSMutableURLRequest(URL: NSURL(string: "https://tressapi-staging.herokuapp.com/api/v2/suggestions?per_page=25%2Cpage%3D1")!,
                                        cachePolicy: .UseProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = headers
request.HTTPBody = postData
```

```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
  .url("https://tressapi-staging.herokuapp.com/api/v2/suggestions?per_page=25%2Cpage%3D1")
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

`GET https://tressapi-staging.herokuapp.com/api/v2/suggestions?per_page=25,page=1`

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

var request = NSMutableURLRequest(URL: NSURL(string: "https://tressapi-staging.herokuapp.com/api/v2/users/29/posts")!,
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
  .url("https://tressapi-staging.herokuapp.com/api/v2/users/29/posts")
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

`POST https://tressapi-staging.herokuapp.com/api/v2/users/29/posts`

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

