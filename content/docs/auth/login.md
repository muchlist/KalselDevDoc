---
title: "Login"
weight: 4
description: >
  Penjelasan login endpoint.
---

### Login Endpoint

`POST` https://kalsel.dev/api/v1/login  

---
  

### Login Request

**-- HEADERS :**

| key | value |
| :---  | :--- |
| Content-Type | application/json |

**-- BODY raw :**
```json
{
    "email":"whos.who@gmail.com",
    "password":"password",
    "limit": 10
}
```  

`limit` : berapa menit token akan kadaluarsa dan harus di refresh, minimal 10 menit, max 7 hari (10080), default (dengan menghilangkan limit dari body) 7 hari (10080).

Pada aplikasi Web biasanya umur token dibuat pendek-pendek karena web sangat rentan terhadap pencurian data, untuk mensiasati agar user tidak terlogout dalam waktu 10 menit maka digunakanlah refresh token dalam waktu berkala sehingga sebelum 10 menit akan mendapatkan token baru (namun tidak fresh).   

Pada aplikasi mobile umur token bisa sangat panjang karena tempat penyimpanan datanya relative lebih aman, makanya pada kebanyakan aplikasi Android, user tidak perlu login berulang-ulang.


> Masa hidup dari sebuah token JWT biasanya ditentukan oleh backend administrator, namun untuk pembelajaran kita bisa menentukannya sendiri.


---
  
### Login Response

`status` 200 Ok

```json
{
    "email": "whos.who@gmail.com",
    "name": "Muchlis",
    "is_admin": false,
    "avatar": "images/whos.who@gmail.com.jpg",
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2MTEzMTgyMTksImlkZW50aXR5Ijoid2hvaXMubXVjaGxpc0BnbWFpbC5jb20iLCJpc19hZG1pbiI6dHJ1ZSwianRpIjoiIiwibmFtZSI6IlJlYWwgTXVjaGxpcyJ9.ibIOYkYHpeV5pPRNKSNQ4oCvIjuV4VrT_-4SGCjVqsc",
    "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2MTEzMTgyMTksImlkZW50aXR5Ijoid2hvaXMubXVjaGxpc0BnbWFpbC5jb20iLCJpc19hZG1pbiI6dHJ1ZSwianRpIjoiIiwibmFtZSI6IlJlYWwgTXVjaGxpcyJ9.ibIOYkYHpeV5pPRNKSNQ4oCvIjuV4VrT_-4SGCjVqsc",
    "expired": 1608781116
}
```

`is_admin` : role user yang sedang login, apakah dia admin  
`avatar` : url foto hasil dari upload avatar  
`access_token` : kunci untuk setiap endpoin yang membutuhkan identitas siapa si pengakses  
`refresh_token` : kunci yang digunakan untuk mendapatkan token baru tanpa harus login. Refresh token memiliki waktu kadaluarsa yang panjang.  
`expired` : copy nilai dari masa expired token untuk memudahkan developer dalam menggunakan refresh token. Angka tersebut adalah time unix detik sejak Jan 01 1970. (UTC)

Ketika login berhasil dan mengembalikan response, maka yang harus dilakukan adalah menyimpan akses token dan refresh token sebagai identitas login. Misalnya pada Android bisa disimpan pada shared preference, room, atau sqlite.  
akses Token akan selalu disertakan pada header disetiap request yang membutuhkan otorisasi. 


Token tersebut diatas merupakan token JWT. Pelajari karakteristik JWT lainnya pada halaman ini.

---
  
### Login Tips

Jika masih bingung dengan apa itu refresh token maka pemanfaatan refresh token bisa dilewati saja terlebih dahulu. Maka ketika login, buatlah umur access token yang panjang.

Sederhananya selain menggunakan endpoint login, server memiliki endpoint khusus untuk mendapatkan token baru dengan menggunakan refresh token. Bedanya, dengan refresh token user tidak harus memasukkan username dan password.    
Token berumur pendek sedangkan refresh token berumur panjang sehigga user bisa mendapatkan masa kada luarsa sepanjang umur refresh token. 

lalu apa bedanya jika hacker bisa mengambil refresh token ?

Nah token hasil generate refresh token itu ditandai sebagai tidak fresh sehingga ada akses terbatas. Misalnya token tidak fresh tidak bisa mengakses endpoint ganti password atau halaman admin.


