# Laporan Praktikum Kriptografi
Minggu ke-: 12  
Topik: [Aplikasi TLS & E-commerce]  
Nama: [Indra Fata Nizar Azizi]  
NIM: [230202812]  
Kelas: [5IKRA]  

---

## 1. Tujuan
(Tuliskan tujuan pembelajaran praktikum sesuai modul.)
Setelah mengikuti praktikum ini, mahasiswa diharapkan mampu:  
1. Menganalisis penggunaan kriptografi pada **email** dan **SSL/TLS**.  
2. Menjelaskan enkripsi dalam transaksi **e-commerce**.  
3. Mengevaluasi isu **etika & privasi** dalam penggunaan kriptografi di kehidupan sehari-hari.
---

## 2. Dasar Teori
(Ringkas teori relevan (cukup 2–3 paragraf).  
Contoh: definisi cipher klasik, konsep modular aritmetika, dll.  )

Aplikasi TLS & E-commerce membahas bagaimana kriptografi dipakai untuk mengamankan komunikasi digital, khususnya pada email dan koneksi web. Pada email, konsep keamanan umumnya mencakup kerahasiaan isi pesan dan pembuktian keaslian pengirim melalui enkripsi dan tanda tangan digital (misalnya konsep PGP/S/MIME). Sementara pada TLS (SSL/TLS), kriptografi bekerja lewat proses handshake untuk memverifikasi identitas server menggunakan sertifikat, lalu membentuk kunci sesi agar pertukaran data selanjutnya terenkripsi dan terlindungi dari penyadapan maupun manipulasi selama transmisi.

Dalam konteks e-commerce, TLS menjadi lapisan utama yang melindungi data sensitif seperti kredensial login, alamat, hingga detail transaksi saat dikirim antara client dan server. Namun keamanan transaksi tidak berhenti di “ikon gembok” browser. Sistem e-commerce juga menerapkan prinsip kriptografi di sisi aplikasi, seperti penyimpanan password menggunakan hash yang aman, penggunaan token/sesi untuk autentikasi, serta mekanisme integritas data transaksi agar nilai pembayaran atau identitas pesanan tidak bisa diubah pihak lain. Kombinasi perlindungan jalur komunikasi dan pengamanan data aplikasi ini memastikan transaksi tetap rahasia, utuh, dan dapat dipercaya.

Selain aspek teknis, penggunaan kriptografi menimbulkan isu etika dan privasi di kehidupan sehari-hari. Enkripsi melindungi pengguna dari pencurian data dan pelacakan, tetapi juga memunculkan perdebatan soal akses pihak tertentu, keamanan metadata (pola komunikasi bisa tetap terlihat meski isi terenkripsi), serta tanggung jawab penyedia layanan untuk tidak mengumpulkan data berlebihan. Karena itu evaluasi tidak hanya menilai “apakah terenkripsi”, tetapi juga apakah penerapan kriptografi mendukung prinsip privasi, transparansi, dan perlindungan pengguna secara nyata, bukan sekadar formalitas keamanan.

---

## 3. Alat dan Bahan
(- Visual Studio Code 
- Git dan akun GitHub
- browser chrome )

---

## 4. Langkah Percobaan
(Tuliskan langkah yang dilakukan sesuai instruksi.  
Contoh format:


---

## 5. Source Code
(Salin kode program utama yang dibuat atau dimodifikasi.  
Gunakan blok kode:

```python
# contoh potongan kode
def encrypt(text, key):
    return ...
```
)

---

## 6. Hasil dan Pembahasan
(- Lampirkan screenshot hasil eksekusi program (taruh di folder `screenshots/`).  
- Berikan tabel atau ringkasan hasil uji jika diperlukan.  
- Jelaskan apakah hasil sesuai ekspektasi.  
- Bahas error (jika ada) dan solusinya. 

Hasil eksekusi program Caesar Cipher:

![Hasil Eksekusi](screenshots/output.png)
![Hasil Input](screenshots/input.png)
![Hasil Output](screenshots/output.png)
)

---

## 7. Jawaban Pertanyaan
(Jawab pertanyaan diskusi yang diberikan pada modul.  
- Pertanyaan 1: …  
- Pertanyaan 2: …  
)
---

## 8. Kesimpulan
(Tuliskan kesimpulan singkat (2–3 kalimat) berdasarkan percobaan.  )

---

## 9. Daftar Pustaka
(Cantumkan referensi yang digunakan.  
Contoh:  
- Katz, J., & Lindell, Y. *Introduction to Modern Cryptography*.  
- Stallings, W. *Cryptography and Network Security*.  )

---

## 10. Commit Log
(Tuliskan bukti commit Git yang relevan.  
Contoh:
```
week12-aplikasi-tls
Author: Indra Fata Nizar Azizi <indrafata980@gmail.com>
Date:   2025-12-30

    week12-aplikasi-tls
```
