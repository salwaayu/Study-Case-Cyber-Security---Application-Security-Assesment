# 🎯 Bagian 2 — Red Team: Exploitation Chain (Vulnerability Chaining) 

Terdapat **skenario**:

Anda diminta mendemonstrasikan bagaimana beberapa kerentanan **low/medium severity** bisa dirangkai menjadi impact **critical**.

Temuan mentah dari automated scanner (Burp/Nessus) terhadap aplikasi target:
<img width="761" height="517" alt="image" src="https://github.com/user-attachments/assets/e5a8d404-3343-4f35-9ab7-190c8cc39b5b" />

**Tugas Anda:**

1. Rangkai keempat temuan di atas menjadi satu **attack narrative** yang menunjukkan bagaimana attacker bisa melakukan **full account takeover** terhadap user finance_lead, mulai dari reconnaissance hingga impact akhir. Jelaskan urutan logis dan mengapa masing-masing temuan yang "hanya Low/Medium" menjadi krusial ketika digabungkan.
2. Hitung ulang **CVSS v3.1 vector** untuk chain ini sebagai satu kesatuan risiko (bukan skor individual), dan jelaskan mengapa risk rating gabungan berbeda dari rata-rata skor individual.
3. Tulis PoC teknis untuk brute-force OTP 4 digit (F-02 + F-03): berapa lama secara realistis waktu yang dibutuhkan tanpa rate limiting, sertakan perhitungan matematis sederhana (bukan hanya menjalankan tools).
4. F-04 (JWT `alg: none`) oleh scanner otomatis dianggap "sulit dieksploitasi". Jelaskan mengapa penilaian otomatis ini keliru dan bagaimana seorang pentester berpengalaman membuktikan sebaliknya (deskripsikan proses manipulasi token secara konseptual).
5. Susun bagian **Business Impact** dari laporan (bukan technical detail) yang menjelaskan konsekuensi nyata bila chain ini dieksploitasi terhadap akun finance_lead — kaitkan dengan regulasi yang relevan di industri fintech Indonesia (boleh disebutkan secara umum karena ini simulasi).
