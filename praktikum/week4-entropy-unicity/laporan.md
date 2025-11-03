# Laporan Praktikum Kriptografi
Minggu ke-: 4  
Topik: Entropy & Unicity Distance  
Nama: Indra Fata Nizar Azizi  
NIM: 230202812  
Kelas: 5IKRA  

---

## 1. Tujuan
(Tuliskan tujuan pembelajaran praktikum sesuai modul.)
1. Menyelesaikan perhitungan sederhana terkait entropi kunci.  
2. Menggunakan teorema Euler pada contoh perhitungan modular & invers.  
3. Menghitung **unicity distance** untuk ciphertext tertentu.  
4. Menganalisis kekuatan kunci berdasarkan entropi dan unicity distance.  
5. Mengevaluasi potensi serangan brute force pada kriptosistem sederhana. 
---

## 2. Dasar Teori
(Ringkas teori relevan (cukup 2–3 paragraf).  
Berikut ringkasan teori relevan yang sesuai dengan tujuan pembelajaran yang Anda tulis:

Dalam kriptografi, **entropi kunci** merupakan ukuran ketidakpastian atau kompleksitas suatu kunci yang digunakan dalam sistem kriptografi. Semakin tinggi entropi, semakin sulit bagi penyerang untuk menebak kunci melalui percobaan acak (brute force). Entropi biasanya dinyatakan dalam bit, dan untuk sebuah kunci yang dipilih secara uniform dari himpunan kunci (K), entropi (H(K)) didefinisikan sebagai (H(K) = log2 |K|), di mana (|K|) adalah jumlah kemungkinan kunci. Pemahaman entropi penting untuk mengevaluasi keamanan kunci terhadap serangan brute force.

Teorema **Euler** dan perhitungan modular menjadi dasar dalam kriptografi modern, terutama pada algoritma berbasis bilangan bulat seperti RSA. Fungsi totien Euler (ϕ(n)) digunakan untuk menentukan jumlah bilangan bulat positif kurang dari (n) yang relatif prima terhadap (n), yang selanjutnya memungkinkan perhitungan invers modular. Misalnya, untuk mencari kunci privat (d) pada RSA, kita perlu menyelesaikan (e ⋅ d ≡ 1 ( mod ϕ(n)). Pemahaman modular arithmetic dan invers modular membantu mahasiswa menyelesaikan perhitungan sederhana dalam praktikum. 

Konsep **unicity distance** mengukur panjang minimum ciphertext yang diperlukan agar plaintext dapat diidentifikasi secara unik dengan probabilitas tinggi. Unicity distance (U) dihitung sebagai (U = H (K)​/ D), di mana (D) adalah redundansi informasi dalam bahasa plaintext. Semakin besar entropi kunci dan semakin kecil redundansi plaintext, semakin tinggi unicity distance, sehingga ciphertext lebih tahan terhadap analisis kriptoanalisis. Dengan memahami hubungan antara entropi, unicity distance, dan jumlah percobaan brute force yang mungkin, mahasiswa dapat menilai kekuatan suatu kriptosistem secara praktis. 
)

---

## 3. Alat dan Bahan
(- Python 3.14  
- Visual Studio Code 
- Git dan akun GitHub  
- Library tambahan (misalnya pycryptodome, jika diperlukan)  )

---

## 4. Langkah Percobaan
(Tuliskan langkah yang dilakukan sesuai instruksi.  
Contoh format:
1. Membuat file `caesar_cipher.py` di folder `praktikum/week2-cryptosystem/src/`.
2. Menyalin kode program dari panduan praktikum.
3. Menjalankan program dengan perintah `python caesar_cipher.py`.)

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
commit abc12345
Author: Nama Mahasiswa <email>
Date:   2025-09-20

    week2-cryptosystem: implementasi Caesar Cipher dan laporan )
```
