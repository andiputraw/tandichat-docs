---
title: "User"
date: 2023-06-23T19:27:37+10:00
weight: 5
---

- [Get User](#get-user)
- [Modify Username](#modify-username)
- [Modify About](#modify-about)

---

API untuk menghandler user

# Get User

API untuk mengambil data user. Jika Email atau ID tidak diberikan, maka akan merespon dengan data user itu sendiri. Jika Email dan ID diberikan, ID akan di prioritaskan

Method : GET

URL : /api/user

Query Params :

    - id : number  (optional)
    - email : string (optional)

Header :

    - Authorization : jwt

response :

    - "message": string,
    - "status": number,
    - "data":
        - id number
        - Email string
        - Img string
        - About string

error response :

    - code : number
    - data : null
    - error : string
    - details : string

# Modify Username

API untuk mengubah username orang yang sedang login

URL : /api/user/username

Method : PATCH

Header :

    - Authorization : jwt

body :

    - "new_username" : string

response :

    - "message": string,
    - "status": number

error response :

    - code : number
    - data : null
    - error : string
    - details : string

# Modify About

API untuk mengubah about orang yang sedang login

URL : /api/user/about

Method : PATCH

Header :

    - Authorization : jwt

body :

    - "new_about" : string

response :

    - "message": string,
    - "status": number

error response :

    - code : number
    - data : null
    - error : string
    - details : string

# Block User

API untuk memblock user. User yang di block tidak dapat dikirimi pesan dan tidak akan muncul di pencarian teman

URL : /api/user/bloc

Method : POST

Header :

    - Authorization : jwt

body :

    - "blocked_user_id" : number

response :

    - "message": string,
    - "status": number

error response :

    - code : number
    - data : null
    - error : string
    - details : string
