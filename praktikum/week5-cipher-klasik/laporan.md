# Laporan Praktikum Kriptografi
Minggu ke-: 5  
Topik: Cipher Klasik (Caesar, Vigenère, Transposisi)  
Nama: Indra Fata Nizar Azizi  
NIM: 230202812 
Kelas: 5IKRA  

---

## 1. Tujuan
(Tuliskan tujuan pembelajaran praktikum sesuai modul.)
1. Menerapkan algoritma **Caesar Cipher** untuk enkripsi dan dekripsi teks.  
2. Menerapkan algoritma **Vigenère Cipher** dengan variasi kunci.  
3. Mengimplementasikan algoritma transposisi sederhana.  
4. Menjelaskan kelemahan algoritma kriptografi klasik.  
---

## 2. Dasar Teori
(Ringkas teori relevan (cukup 2–3 paragraf).  
Contoh: definisi cipher klasik, konsep modular aritmetika, dll.  )
Cipher klasik merupakan metode kriptografi yang digunakan untuk menyandikan pesan agar tidak dapat dibaca oleh pihak yang tidak berwenang. Salah satu metode paling sederhana adalah Caesar Cipher, yang mengenkripsi teks dengan menggeser setiap huruf sejumlah posisi tertentu dalam alfabet. Misalnya, dengan pergeseran 3, huruf 'A' menjadi 'D'. Dekripsinya hanya dengan menggeser huruf kembali ke posisi semula. Caesar Cipher mudah dipahami dan diimplementasikan, tetapi sangat rentan terhadap serangan analisis frekuensi karena pola huruf dalam bahasa tetap terlihat.

Vigenère Cipher adalah pengembangan dari Caesar Cipher dengan menggunakan kunci kata yang lebih panjang dan berulang untuk menentukan pergeseran setiap huruf. Hal ini membuat pola lebih kompleks dan meningkatkan keamanan dibanding Caesar Cipher. Misalnya, kunci “LEMON” digunakan untuk mengenkripsi teks “ATTACK”, di mana setiap huruf teks digeser sesuai huruf kunci. Meski lebih aman, Vigenère tetap memiliki kelemahan jika kunci pendek atau dapat ditebak, karena pola pergeseran bisa dianalisis dengan metode Kasiski atau analisis frekuensi.

Cipher transposisi berbeda dengan Caesar dan Vigenère karena tidak mengubah huruf, melainkan menyusun ulang posisi huruf sesuai aturan tertentu, seperti baris-ke-kolom (rail fence) atau pengurutan kolom berdasarkan kunci. Metode ini menjaga frekuensi huruf asli, tetapi pesan dapat dipulihkan jika pola transposisi diketahui. Secara umum, kelemahan utama cipher klasik adalah mudah diretas dengan analisis frekuensi dan pola, serta tidak cukup aman untuk komunikasi modern yang memerlukan keamanan tinggi.

---

## 3. Alat dan Bahan
(- Python 3.14  
- Visual Studio Code / editor lain  
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
commit week5-cipher-klasik
Author: Indra Fata Nizar Azizi <indrafata980@gmail.com>
Date:   2025-11-04

    week5-cryptosystem: Cipher Klasik (Caesar, Vigenère, Transposisi)  
```
