---
title: "Upload"
weight: 7
description: >
  This is how the shortcodes would look like in action
---

### Upload Endpoint

`POST` https://kalsel.dev/api/v1/avatar  

Endpoint upload avatar diproteksi sehingga wajib memasukkan token JWT pada header dengan key `Authorization` dengan value kata `Bearer` spasi lalu `token_jwtnya`.  

---
  

### Upload Request

**-- HEADERS :**
| key | value |
| :---  | :--- |
| Authorization | Bearer `masukkan_token_disini` |
| Content-Type | multipart/form-data |


**-- BODY formdata :**

| key | value |
| :---  | :--- |
| avatar | `file_gambar_yang_di_upload` |


Masukkan file ke Form-Data dengan key 'avatar'

---
  
### Upload Response

`status` 200 Ok

```json
{
    "id": "5f969f62259eae481fb0e856",
    "email": "whois.muchlis@gmail.com",
    "name": "Real Muchlis",
    "is_admin": false,
    "avatar": "images/whois.muchlis@gmail.com.jpg",
    "timestamp": 1608783963
}
```

`id` : id user profil  
`avatar` : url foto hasil dari upload avatar  
`timestamp` : kapan terakhir kali data user diubah dalam format unix timestamp  

---

  
### Upload Tips

Server hanya mengijinkan upload file dalam format .jpg .png dengan ukuran file kurang dari 1 MB.  
Praktek terbaik adalah dengan melakukan kompresi gambar terlebih dahulu pada frontend sebelum melakukan upload atau hanya mengupload thumbnailnya saja.

Library android untuk melakukan kompresi gambar : [zetbaitsu/Compressor][1]


[1]: https://github.com/zetbaitsu/Compressor

