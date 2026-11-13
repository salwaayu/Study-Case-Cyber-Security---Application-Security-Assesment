# Vulnerability Description

Hasil security assessment menunjukkan bahwa API endpoint berikut ini:

/api/v1/password/reset/verify

kemudian Aplikasi tidak membatasi jumlah percobaan ketika pengguna memasukkan OTP yang salah. Artinya, attacker dapat mencoba berbagai kombinasi OTP secara berulang kali tanpa adanya mekanisme lockout atau pembatasan percobaan dari sisi server.

# Attack Scenario
Sebagai contoh, aplikasi menggunakan OTP 4 digit = 0000 – 9999, sehingga ada 10.000 kombinasi percobaan yang bisa
dilakukan. Jika tidak ada pembatasan percobaan, attacker berpotensi menebak OTP (Brute Force) yang benar melalui percobaan berulang.
Kondisi ini semakin berisiko apabila OTP memiliki masa berlaku yang cukup lama dan server tidak menerapkan mekanisme proteksi tambahan.

# Potential Impact

**Account Takeover**, attacker dapat mengambil alih akun apabila berhasil menebak OTP yang valid dan menyelesaikan proses password reset.

# Recommendation Mitigation

- Terapkan rate limiting untuk membatasi jumlah percobaan verifikasi OTP.
- Terapkan account lockout sementara setelah beberapa kali percobaan gagal, misalnya 5 kali.
- Gunakan OTP dengan masa berlaku singkat (misalnya 1 menit).
- Terapkan mekanisme invalidasi OTP setelah berhasil digunakan.
