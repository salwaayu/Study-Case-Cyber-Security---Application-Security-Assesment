
Hasil scanning menunjukan API endpoint berikut ini

/api/v1/user/profile?id=

Mengapa disebut rentan terhadap vulnerability IDOR? karena attacker dapat mengganti nilai id dan dapat melihat profil user lain yang seharusnya hanya dapat diakses oleh user terkait. 
Namun, dari sisi sistem/server mengizinkan user mengubah parameter id tanpa validasi authorization yang benar. Misalnya parameter id dapat diganti-ganti seperti pada contoh;

/api/v1/user/profile?id=1001
/api/v1/user/profile?id=1002
/api/v1/user/profile?id=1003

Dari sini attacker menemukan informasi milik user finance_lead, termasuk email
dan nomor HP.
User ID : 1003
Name : Finance Lead
Email : finance.lead@example.com
Phone : 08xxxxxxxxxx
Role : Finance
Attacker menggunakan informasi tersebut untuk menentukan finance_lead
sebagai target.


**Recommendation Mitigation**
