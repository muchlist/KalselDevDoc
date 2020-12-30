---
title: "Error"
weight: 2
description: >
  Penjelasan error endpoint.
---

### Error Response

Ketika berkomunikasi dengan server, selain mendapatkan balikan sukses, http client juga bisa mendapatkan balikan error. Misalnya ketika data yang diminta tidak sesuai, password terlalu pendek, token sudah tidak berlaku dsb.

Pada Kalseldev error response diseragamkan menjadi seperti dibawah ini, apapun status code httpnya.

```json
{
    "status": 422,
    "message": "Token tidak valid",
    "error": "jwt_error",
    "causes": [
        "token contains an invalid number of segments"
    ]
}
```

`status` : copy balikan dari code response http  
`message` : isi pesan untuk ditampilkan ke user  
`error` : jenis error yang didapatkan  
`causes` : array berisi string penyebab mengapa terjadi error  

---


### Error Limiter

Pada kalseldev ada beberapa error yang biasanya tidak terjadi di service-service lain. Error tersebut adalah error yang dihasilkan oleh rate limiter. 
Client dibatasi hanya dapat melakukan sejumlah request pada suatu waktu per IP Address. Hal ini dimaksudkan untuk menjaga keamanan server dari tindakan peretasan seperti DOS, Selain itu juga demi kestabilan server mengingat resourcenya kecil.

```json
{
    "status": 429,
    "message": "Terlalu banyak request",
    "error": "rate_limiter",
    "causes": [
        "too many requests in a given amount of time"
    ]
}
```

---

### Error Tips

Pada library Android Retrofit2 untuk menangkap respon error biasanya dengan menangkap Error Body lalu di unmarshal agar dapat dikonsumsi pada aplikasi.  
`Sangat disarankan untuk menggunakan error message dari server sebagai balikan ke user Android secara langsung untuk menghindari pesan error yang ambigu`.


