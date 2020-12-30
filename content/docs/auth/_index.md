---
title: "Otorisasi API"
weight: 1
---

Layanan Otorisasi bisa diakses melalui https://kalsel.dev/api/v1

Endpoint Otorisasi mencakup semua hal yang berkaitan dengan hak akses dan identitas user.  
Endpoint yang tersedia antara lain :

1. `Login` (mengembalikan data user, access_token dan refresh_token)
2. `Register`
2. `Refresh` token (mengembalikan access_token baru)
3. (protected) `Upload` Foto
4. (protected) `Konten` pariwisata kota Banjarmasin (mengembalikan `list data`)

Sistem otorisasi api ini menggunakan JWT (JSON Web Token).  
Endpoint yang ditandai sebagai `protected` artinya membutuhkan token JWT yang valid pada header untuk setiap kali request.

{{< button "./error/" "Mulai" >}}