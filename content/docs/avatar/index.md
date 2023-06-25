---
title: "Avatar"
date: 2023-06-23T19:27:37+10:00
weight: 5
---

- [Get Avatar](#get-avatar)
- [Change Avatar](#change-avatar)

---

# Get Avatar

Rest untuk mengambil profile picture

URL : /api/avatar

Method : GET

query params

    - name (optional) : Image name (default jika tidak diberikan : default)

response :

    - image

error response :

    - code : number
    - data : null
    - error : string
    - details : string

```javascript
const fetchProfilePicture = async (imageName = "default") => {
  try {
    const queryParams = new URLSearchParams({ name: imageName }).toString();
    const url = `/api/profile?${queryParams}`;

    //Fetch image
    const response = await fetch(url);

    //Error handling
    if (!response.ok) {
      const errorData = await response.json();
      throw new Error(errorData.error);
    }

    //Ambil blob nya
    const imageBlob = await response.blob();
    //Buat object
    return URL.createObjectURL(imageBlob);
  } catch (error) {
    console.error("Error fetching profile picture:", error.message);
  }
};

fetchProfilePicture()
  .then((imageUrl) => {
    console.log("Profile picture URL:", imageUrl);
  })
  .catch((error) => {
    console.error("Failed to fetch profile picture:", error);
  });
```

# Change Avatar

API untuk mengubah profile picture

URL : /api/avatar

Method : PATCH
Header :

    - Authorization : jwt

Form Data

    - avatar : blob(?)

response :

    - "data":

        - "filename": string

    - "message": string,
    - "status": number

error response :

    - code : number
    - data : null
    - error : string
    - details : string

```javascript
const fileInput = document.getElementById("file-input"); // Assuming you have an input element of type "file" with id "file-input"

const formData = new FormData();
formData.append("avatar", fileInput.files[0]); // Assuming you want to send the first selected file

fetch("/api/avatar", {
  method: "POST",
  headers: {
    Authorization: "jwt", // Replace 'jwt' with the actual JWT token
  },
  body: formData,
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
