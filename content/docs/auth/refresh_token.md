---
title: "Refresh Token"
weight: 5
description: >
  Refresh token explained.
---


### Refresh Endpoint

`POST` https://kalsel.dev/api/v1/refresh 

---
  

### Refresh Request

**-- HEADERS :**
| key | value |
| :---  | :--- |
| Content-Type | application/json |

**-- BODY raw :**
```json
{
    "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2MTEzMTgyMTksImlkZW50aXR5Ijoid2hvaXMubXVjaGxpc0BnbWFpbC5jb20iLCJpc19hZG1pbiI6dHJ1ZSwianRpIjoiIiwibmFtZSI6IlJlYWwgTXVjaGxpcyJ9.ibIOYkYHpeV5pPRNKSNQ4oCvIjuV4VrT_-4SGCjVqsc",
    "limit": 10
}
```  

`limit` : berapa menit token akan kadaluarsa dan harus di refresh, minimal 10 menit, max 7 hari (10080), default (dengan menghilangkan limit dari body) 7 hari (10080).

Pada aplikasi Web biasanya umur token dibuat pendek-pendek karena web sangat rentan terhadap pencurian data, untuk mensiasati agar user tidak terlogout dalam waktu 5 menit maka digunakanlah refresh token dalam waktu berkala sehingga sebelum 5 menit akan mendapatkan token baru (namun tidak fresh).   

---

  
### Refresh Response

`status` 200 Ok

```json
{
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2MTEzMTgyMTksImlkZW50aXR5Ijoid2hvaXMubXVjaGxpc0BnbWFpbC5jb20iLCJpc19hZG1pbiI6dHJ1ZSwianRpIjoiIiwibmFtZSI6IlJlYWwgTXVjaGxpcyJ9.ibIOYkYHpeV5pPRNKSNQ4oCvIjuV4VrT_-4SGCjVqsc",
    "expired": 1608781116
}
```

`access_token` : kunci untuk setiap endpoin yang membutuhkan identitas siapa si pengakses  
`expired` : copy nilai dari masa expired token untuk memudahkan developer dalam menggunakan refresh token. Angka tersebut adalah time unix detik sejak Jan 01 1970. (UTC)

Akses token yang baru harus disimpan seperti pada saat mendapatkan respon login. Token baru menimpa token yang lama.  

---

### Refresh Response Expired

`status` 421  
Response 421 akan dikembalikan jika ternyata refresh token sudah expired.  

```json
{
    "status": 421,
    "message": "Token expired",
    "error": "jwt_error",
    "causes": [
        "token has expired"
    ]
}
```

---

  
### Refresh Tips

Dengan menggunakan refresh token kita bisa mendapatkan akses token tanpa harus berulang ulang memasukkan username dan password (Dengan asumsi umur akses tokennya pendek).

Bagaimana caranya frontend tahu waktu yang tepat untuk merefresh token ?  
1. Dengan melihat expired token yang sudah ada (sedang disimpan) maka bisa dibuat kondisi "lakukan refresh jika waktu saat ini (dalam unix time) melebihi waktu expired".
2. Dengan melakukan refresh terus menerus pada halaman tertentu. Misalnya jika membuka dashboard otomatis waktu login diperpanjang dengan merefresh token.

Refresh token juga bisa expired, jika itu terjadi maka user sudah harus dipaksa menggunakan login dengan memasukkan username dan password.


