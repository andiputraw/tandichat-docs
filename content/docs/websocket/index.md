---
title: "Websocket"
date: 2023-06-23T19:27:37+10:00
weight: 5
---

- [Get Websocket Auth](#get-websocket-auth)
- [Cara Menggunakan Websocket](#cara-menggunakan-websocket)
- [Tipe-tipe message](#message-type) (UPDATE)

---

Tata cara menggunakan websocket dan juga referensi type message

# Get Websocket Auth

Generate Websocket Authentication code yang hanya bisa digunakna 1x

Method : GET

URL : /ws/auth

Header :

    - Authorization : jwt

response :

    - "message": string,
    - "status": number,
    - "data":
        - websocketAuthCode : websocketAuth

error response :

    - code : number
    - data : null
    - error : string
    - details : string

websocketAuth Payload :

    - authID : string
    - userID : number

```javascript
const jwt = jwt;

const header = new Headers();
header.set("authorization", jwt);

const result = await fetch("http://localhost:5050/ws/auth", {
  method: "GET",
  headers: header,
});
const json = await result.json();
const auth = json.data.websocketAuthCode;
```

# Cara Menggunakan Websocket

Generate Token 1x pakai dari [Get Websocket Auth](#get-websocket-auth).

Gunakan fungsi konstructor Websocket dengan params auth yang valuenya websocket auth

```javascript
const ws = new Websocket(`127.0.0.1:5050/ws/connect?auth=${auth}`);
```

untuk mengirim pesan. gunakan fungsi `ws.send()`

```javascript
//Referensi structur message cek di bawah
const message = {
  type: 0,
  data: {
    to: destionation,
    message: messageInput.value,
  },
};
const json = JSON.stringify(message); // Jangan lupa untuk memparse object menjadi string JSON
ws.send(json);
```

Untuk mendengar dari server. buat fungsi listener

```javascript
ws.onmessage = (ev) => {
  const msg = ev.data;

  message = JSON.parse(msg);

  if (message.type == 1) {
    messageContainer.innerHTML += `<p>${message.data.message}</p>`;
  }
};
```

lebih lengkapnya lihat di [Dokumentasi MDN](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket) Terutama pada bagian event

# Message Type

    Message :
        Type : MessageType (int)
        Data : (tergantung MessageType)

    TYPE_ERROR = -1

        Data :
            Message : string

    TYPE_MESSAGE = 0

        Data :
            To : number
            Message : string

    TYPE_INCOMING_MESSAGE = 1

        Data :
            From : number
            Message : string

    TYPE_NOTIFICATION = 2

        Data :
            Message : string

    TYPE_FRIEND_REQUEST = 3

        Data :
            FROM : number
