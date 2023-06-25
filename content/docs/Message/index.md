---
title: "Message"
date: 2023-06-23T19:27:37+10:00
weight: 5
---

- [Get Message](#get-message)

---

Api untuk menghandle segala sesuatu yang berurusan dengan Message.

# Get Message

Mengambil semua message dari user dan untuk user tujuan. API ini menggunakan Teknik Cursor Pagination [referensi](https://stackoverflow.com/questions/18314687/how-to-implement-cursors-for-pagination-in-an-api)

Method : GET

LIMIT : 100

URL : /api/message

Query Params :

    - to : number
    - cursor : number (optional)

Header :

    - Authorization : jwt

response :

    - "message": string,
    - "status": number,
    - "data":
        - message :
            - id number
            - user_id number
            - created_at time.Time
            - content string
        - next_cursor : number

error response :

    - code : number
    - data : null
    - error : string
    - details : string
