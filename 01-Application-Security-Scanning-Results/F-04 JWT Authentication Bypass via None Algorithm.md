# Vulnerability Description

Hasil security assessment menunjukkan bahwa mekanisme autentikasi aplikasi menggunakan JSON Web Token (JWT) dengan konfigurasi algoritma yang tidak aman, yaitu:

"alg": "none"

algoritma none menunjukkan bahwa token tidak menggunakan digital signature untuk memastikan keaslian dan integritas token. Dalam pengujian, ditemukan bahwa server masih menerima JWT ketika header token dimodifikasi menggunakan algoritma none, tanpa melakukan validasi signature sebagaimana mestinya. Kondisi ini memungkinkan attacker berpotensi memodifikasi isi token, seperti informasi user ID atau role pengguna, kemudian menggunakannya untuk mencoba mendapatkan akses yang seharusnya tidak dimiliki.

# Attack Scenario
Modifikasi claim pada JWT

{

 "user": "financial_lead",
 
 "role": "finance"
 
}


menjadi

{

 "user": "financial_lead",
 
 "role": "admin"
 
}

Jika server tidak melakukan validasi signature dan authorization dengan benar,
token tersebut dapat diterima sebagai admin. Attacker berpotensi mengakses
fitur admin, melihat/mengubah data yang seharusnya terbatas, serta melakukan
aksi administratif. 


# Potential Impact
- Authentication Bypass: Attacker dapat melewati mekanisme autentikasi.

- Privilege Escalation: Attacker berpotensi memperoleh hak akses yang lebih tinggi.

- Unauthorized Access: Akses ke fitur atau informasi yang seharusnya dibatasi.

# Recommendation Mitigation

- Jangan gunakan algoritma none untuk token autentikasi.

- Pastikan server hanya menerima algoritma JWT yang telah ditentukan dan diizinkan, misalnya HS256 atau RS256 sesuai kebutuhan arsitektur.

- Lakukan validasi signature JWT pada setiap request yang membutuhkan autentikasi.

