---
title: Tress API Reference

language_tabs:
  - swift
  - java

toc_footers:
  - <a href="mailto:esther@tressapp.co?Subject=Request for Developer Client Key" target="_top">Email for a Client Authentication</a>

includes:
  - errors

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
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```java
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint helps a user resets their password.

<aside class="notice">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve


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
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```http
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

