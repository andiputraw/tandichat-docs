---
title: "Friend"
date: 2023-06-23T19:27:37+10:00
weight: 5
---

- [Request Friend](#request-friend)
- [Accept Friend](#accept-friend)
- [Get Accepted Friend](#get-accepted-friend)
- [Get Pending Friend](#get-pending-friend)

---

API untuk menghandle pertemanan

# Request Friend

API untuk membuat request kepada user lain

URL : /api/friends/request

Header :

    - Authorization : jwt

body :

    - "friendid" : number

Method : POST
response :

    - "message": string,
    - "status": number

error response :

    - code : number
    - data : null
    - error : string
    - details : string

```javascript
const jwt = "your-jwt-token";
const friendId = 123;

const url = "/api/friends/request";
const headers = {
  Authorization: jwt,
  "Content-Type": "application/json",
};

const body = JSON.stringify({
  friendid: friendId,
});

fetch(url, {
  method: "POST",
  headers: headers,
  body: body,
})
  .then((response) => response.json())
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.error(error);
  });
```

# Accept Friend

API untuk membuat Mengaccept friend request user lain

Url : /api/friends/accept

Method : POST

Header :

    - Authorization : jwt

body :

    - "friendid" : number

response :

    - "message": string,
    - "status": number

error response :

    - code : number
    - data : null
    - error : string
    - details : string

```javascript
const jwtToken = "your_jwt_token_here";
const friendId = 123;

fetch("/api/friends/accept", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: jwtToken,
  },
  body: JSON.stringify({
    friendid: friendId,
  }),
})
  .then((response) => response.json())
  .then((data) => {
    // Handle the response data
    console.log(data);
  })
  .catch((error) => {
    // Handle any errors
    console.error(error);
  });
```

# Get Accepted Friend

API untuk mengambil semua teman yang sudah berstatus accepted

Url : /api/friends

Method : GET

Header :

    - Authorization : jwt

response :

    - "message": string,
    - "status": number,
    - "data":
        - array
            - Id number
            - Username string
            - Email string
            - Img string
            - About string

error response :

    - code : number
    - data : null
    - error : string
    - details : string

```javascript
const jwtToken = "your_jwt_token_here";

fetch("/api/friends", {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
    Authorization: jwtToken,
  },
})
  .then((response) => response.json())
  .then((data) => {
    // Handle the response data
    console.log(data);
  })
  .catch((error) => {
    // Handle any errors
    console.error(error);
  });
```

# Get Pending Friend

API untuk mengambil semua teman yang sedang berstatus Pending

Url : /api/friends/pending

Method : GET

Header :

    - Authorization : jwt

response :

    - "message": string,
    - "status": number,
    - "data":
        "sended" :
            - array
                - Id number
                - Username string
                - Email string
                - Img string
                - About string
        "recieved" :
            - array
                - Id number
                - Username string
                - Email string
                - Img string
                - About string

error response :

    - code : number
    - data : null
    - error : string
    - details : string

```javascript
const jwtToken = "your_jwt_token_here";

fetch("/api/friends/pending", {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
    Authorization: jwtToken,
  },
})
  .then((response) => response.json())
  .then((data) => {
    // Handle the response data
    console.log(data);
  })
  .catch((error) => {
    // Handle any errors
    console.error(error);
  });
```
