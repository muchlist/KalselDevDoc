+++
title = "Register"
description = ""
weight = 3
+++

### Register Endpoint

`POST` https://kalsel.dev/api/v1/users  

---
  

### Register Request

**-- HEADERS :** 
| key | value |
| :---  | :--- |
| Content-Type | application/json |

**-- BODY raw :**
```json
{
    "email":"whos.who@gmail.com",
    "name": "Muchlis",
    "password":"password"
}
```  

Pada frontend pastikan inputan password selalu dibarengi dengan konfirmasi password untuk menghindari kesalahan input, karena password yang akan dimasukkan selalu dianggap benar saat register.  

---
  
### Register Response

`status` 200 Ok

```json
{
    "msg": "Register berhasil, ID: 5fe2cc1cd79edd95ade9e6b8"
}
```

Terdapat 2 prilaku yang biasanya dilakukan pada client ketika berhasil registrasi, yaitu :  
1. User diminta untuk login ulang
2. User masuk secara otomatis ketika sukses registrasi. 

Pada prilaku yang ke-dua server akan mengembalikan akses token dan informasi tambahan lainnya seperti respon pada endpoint login, namun pada kalseldev prilaku pertama yang dipilih sehingga user diharuskan untuk login lagi setelah selesai registrasi.  

---
  
### Register Tips

Cobalah untuk melakukan kesalahan input seperti menghilangkan simbol @ pada email untuk mendapatkan balikan error.  

Untuk kesalahan input Kalseldev menggunakan library validator-go sehingga pesan errornya akan berbahasa inggris.  
Umumnya validasi email, validasi password (misalnya password kosong) dilakukan di sisi frontend sehingga tidak perlu sampai ke server untuk memberitahu client bahwa inputan yang diberikan salah.

`Sangat disarankan untuk menggunakan error message dari server sebagai balikan ke user Android secara langsung untuk menghindari pesan error yang ambigu`.


