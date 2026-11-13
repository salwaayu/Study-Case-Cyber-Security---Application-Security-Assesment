<img width="756" height="96" alt="image" src="https://github.com/user-attachments/assets/3e3f713a-e50a-4244-95f5-e12b831e11ce" />

Hasil scanning menunjukan API endpoint berikut ini

***/api/v1/user/profile?id=***

Mengapa disebut rentan terhadap vulnerability IDOR? karena attacker dapat mengganti nilai id dan dapat melihat profil user lain yang seharusnya hanya dapat diakses oleh user terkait. 
Namun, dari sisi sistem/server mengizinkan user mengubah parameter id dan mengembalikan data tanpa validasi authorization yang benar. Misalnya parameter id dapat diganti-ganti seperti pada contoh;

/api/v1/user/profile?id=**1001**

/api/v1/user/profile?id=**1002**

/api/v1/user/profile?id=**1003**

Dengan adanya kesalahan konfigurasi tersebut dapat berpotensi **Sensitive Information Disclosure**, seorang attacker bisa saja menemukan informasi milik user lain ataupun user dengan role tinggi, termasuk informasi email, nomor HP (yang bisa jadi sasaran untuk mengirim link phishing) dan informasi sensitif lainnya. 

User ID : 1003

Name : Finance Lead

Email : finance.lead@example.com

Phone : 08xxxxxxxxxx

Role : Finance

Attacker menggunakan informasi tersebut untuk menentukan finance_lead sebagai target.


**Recommendation Mitigation**
- Pastikan server melakukan object-level authorization berdasarkan identitas pengguna yang sedang terautentikasi. (validasi id object dengan id user melalui JWT Token)
- Gunakan UUID / GUID Sebagai Pengganti Auto-Increment ID, (contoh: 550e8400-e29b-41d4-a716-446655440000) sebagai identifier publik yang terekspos di URL API.
- Hindari Mengirim User ID melalui Parameter URL seperti /api/v1/users/me/profile.
