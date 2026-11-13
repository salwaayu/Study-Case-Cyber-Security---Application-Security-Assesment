# Vulnerability Description

Hasil security assessment menunjukkan bahwa API endpoint **/api/v1/password/reset** menerima parameter email **/api/v1/password/reset?email=user@example.com** kemudian aplikasi tidak menerapkan pembatasan jumlah permintaan OTP pada proses password reset. Akibatnya, attacker dapat mengirimkan permintaan OTP secara berulang kali menggunakan alamat email yang sama tanpa adanya mekanisme pembatasan (request throttling) dari sisi server.

# Attack Scenario
Sebagai contoh, Attacker dapat mengirimkan permintaan password reset secara berulang menggunakan email target seperti berikut:

/api/v1/password/reset?email=salwa@example.com

Karena server tidak menerapkan rate limiting, setiap permintaan dapat diproses tanpa pembatasan jumlah request dalam periode tertentu. Attacker dapat menyalahgunakan fitur password reset untuk mengirimkan OTP secara terus-menerus kepada pengguna yang menjadi target. Akibatnya, inbox korban berpotensi menerima banyak email berisi OTP password reset. Kondisi ini dapat dimanfaatkan untuk mengganggu pengguna maupun menyalahgunakan infrastruktur pengiriman email aplikasi.

# Potential Impact

- OTP Flooding: Attacker dapat membanjiri email korban dengan permintaan OTP secara berulang kali.

- Email Bombing: Pengguna menerima email OTP dalam jumlah besar sehingga mengganggu aktivitas komunikasi normal.

- Service Abuse: Fitur pengiriman email atau layanan OTP dapat disalahgunakan sehingga meningkatkan konsumsi resource dan biaya operasional aplikasi.

# Recommendation Mitigation

- Terapkan Rate Limiting jumlah permintaan OTP berdasarkan kombinasi IP address, akun/email tujuan, dan perangkat dalam periode waktu tertentu.
- Implementasi Request Cooldown (jeda waktu) sebelum pengguna dapat meminta OTP berikutnya, misalnya 60 detik.
- Tambahkan mekanisme CAPTCHA atau bot protection untuk mengurangi penyalahgunaan endpoint oleh automated scripts.
- Pastikan OTP sebelumnya dinonaktifkan ketika OTP baru diterbitkan, serta gunakan masa berlaku (expiration time) yang terbatas.
- Hindari memberikan respons API yang dapat digunakan untuk melakukan enumerasi alamat email user.
