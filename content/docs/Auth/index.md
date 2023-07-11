---
title: "Auth"
date: 2023-06-23T19:27:37+10:00
weight: 5
---

- [Register](#register)
- [Login](#login) (UPDATE)
- [Logout](#logout)
- [Send Email Verification](#send-email-verification) 
- [Verify Email](#verify-email) 
- [Error Code](#error-code) (NEW)

---

# Register

API untuk Register

URL : /api/register

Method : POST

request body : application/json

payload :

    - Email (string) (required)
    - username (string) (required)
    - Password (string) (required)

response :

    - code : number
    - data : { }

error response :

    - code : number
    - data : null
    - error : string
    - details : string

Contoh

```javascript
const email = "foo@gmail.com";
const username = "bar";
const password = "baz";

const requestOptions = {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ email, username, password }),
};

const response = await fetch("/api/register", requestOptions);
console.log(response);
// {code: 200, data : {}}
```

# Login

API untuk login

Jika EMAIL_VERIFICATION diisi 1. maka user yang belum terverifikasi tidak akan bisa login.

URL: /api/login

request body : application/json

Method : POST

payload :

    - email (string) (required)
    - Password (string) (required)

response :

    - code : number
    - data : { jwt : string }

error response :

    - code : number
    - data : null
    - error : string
    - details : string

JWT payload :

    - "Sessionid": number,
    - "email": string,
    - "userID": number,

Contoh

```javascript
const email = "bar";
const password = "baz";

const requestOptions = {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ email, password }),
};

const response = await fetch("/api/login", requestOptions);
console.log(response);
/* {
  code: 200,
  data : { 
    token : eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJTZXNzaW9uaWQiOjIsImFib3V0IjoiSGVsbG8gaW0gdXNpbmcgdGFuZGljaGF0IiwiZW1haWwiOiJiYXJAZ21haWwuY29tIiwicHJvZmlsZSI6ImQzMDM1OGMzLTMwNmItNGE5YS1hZTIwLWQyM2Y0YWQ1MzQ2OSIsInVzZXJJRCI6MSwidXNlcm5hbWUiOiJmb28ifQ.jBokpV84B6N7SZAF_svkFWvvciHGpPaHDBdR9nWjte0
    }
  }*/
```

# Logout

Rest untuk logout

url : /api/logout

Request body : application/json

Method : POST

Header :

    - Authorization : JWT

response :

    - code : number
    - data : { }

error response :

    - code : number
    - data : null
    - error : string
    - details : string

```javascript
const token = "your_jwt_token_here"; // Ganti dengan jwt token yang diterima dari /api/login

const myHeaders = new Headers();

myHeaders.append("Content-Type", "application/json");
myHeaders.append("Authorization", token);

const requestOptions = {
  method: "POST",
  headers: myHeaders,
};

const response = await fetch("/api/logout", requestOptions);
console.log(response);
/*
{
    "code": 200,
    "data": {}
} 
*/
```

# Send Email Verification

Mengirim Email Verification.

Setelah user mencoba memverifikasi email. user akan mendapatkan email yang berisikan link ke : 
{Address Client Side Server}/api/verifiyemail/{code unik}

Client side diharapkan mengirimkan code tersebut kembali ke server menggunakan API dibawah

url : /api/verifyemail

Request body : application/json

Method : POST

body :

    - email : string

response :

    - code : number
    - message : string

error response :

    - code : number
    - data : null
    - error : string
    - details : string


# Verify Email

Memverifikasi Email

url : /api/verifyemail/:code

Request body : application/json

Method : PATCH

response :

    - code : number
    - message : string

error response :

    - code : number
    - data : null
    - error : string
    - details : string

# Error Code

    - 0 error: User Not Found
	- 1 error: Password not match
	- 2 error: User is not verified
	- 3 error: Session Not Found
	- 4 error: Already Registered 
	- 69 error: Sign JWT Fail
	- 70 error: Failed To Parse JWT