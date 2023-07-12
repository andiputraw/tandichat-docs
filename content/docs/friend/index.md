---
title: "Friend"
date: 2023-06-23T19:27:37+10:00
weight: 5
---

- [Request Friend](#request-friend)
- [Accept Friend](#accept-friend)
- [Decline Friend Request](#Decline-friend)
- [Cancel Friend Request](#cancel-friend-request)
- [Get Pending Friend Request](#get-pending-friend)
- [Get All Friend](#get-accepted-friend)
- [Delete Friend](#delete-friend)

---

API untuk menghandle pertemanan

Update terakhir menambah Delete Friend

# Request Friend

API untuk membuat request kepada user lain

Jika user mencoba untuk menambahkan teman yang sudah terlebih dahulu menambahkan user. maka status pertemanan user secara otomatis akan menjadi "accepted"

URL : /api/friends/request

Header :

    - Authorization : jwt

body :

    - "friend_id" : number

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
const friend_id = 123;

const url = "/api/friends/request";
const headers = {
  Authorization: jwt,
  "Content-Type": "application/json",
};

const body = JSON.stringify({
  friend_id: friend_Id,
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
const friend_id = 123;

fetch("/api/friends/reject", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: jwtToken,
  },
  body: JSON.stringify({
    friend_id: friend_id,
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

# Decline Friend

API untuk membuat Menolak friend request user lain

Url : /api/friends/decline

Method : POST

Header :

    - Authorization : jwt

body :

    - "friend_id" : number

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
const user_id = 123;

fetch("/api/friends/accept", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: jwtToken,
  },
  body: JSON.stringify({
    user_id: user_id,
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

# Cancel Friend Request

API untuk membuat membatalkan friend request

Url : /api/friends/cancel

Method : POST

Header :

    - Authorization : jwt

body :

    - "friend_id" : number

response :

    - "message": string,
    - "status": number

error response :

    - code : number
    - data : null
    - error : string
    - details : string

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

# Delete Friend

API untuk membuat Menghapus teman dari daftar teman

Url : /api/friends/

Method : DELETE

Header :

    - Authorization : jwt

body :

    - "friend_id" : number

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
const friend_id = 123;

fetch("/api/friends/reject", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: jwtToken,
  },
  body: JSON.stringify({
    friend_id: friend_id,
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
