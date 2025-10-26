# Laporan Praktikum Kriptografi
Minggu ke-: 3  
Topik: Modular Math  
Nama: Indra Fata Nizar Azizi  
NIM: 230202812  
Kelas: 5IKRA  

---

## 1. Tujuan
(Tuliskan tujuan pembelajaran praktikum sesuai modul.)
1. Menyelesaikan operasi aritmetika modular.  
2. Menentukan bilangan prima dan menghitung GCD (Greatest Common Divisor).  
3. Menerapkan logaritma diskrit sederhana dalam simulasi kriptografi. 
---

## 2. Dasar Teori
  
**1. Aritmetika Modular**

Aritmetika modular adalah sistem perhitungan yang dilakukan berdasarkan sisa hasil bagi dari suatu bilangan terhadap modulus tertentu. Jika dua bilangan ( a ) dan ( b ) memiliki sisa yang sama ketika dibagi dengan ( n ). Operasi penjumlahan, pengurangan, dan perkalian dalam aritmetika modular dilakukan dengan cara biasa, tetapi hasilnya selalu direduksi dengan modulus ( n ). Konsep ini sangat penting dalam kriptografi, teori bilangan, dan komputasi karena efisien dan aman untuk perhitungan besar.

**2. Greatest Common Divisor (GCD)**

GCD atau Faktor Persekutuan Terbesar dari dua bilangan ( a ) dan ( b ) adalah bilangan bulat terbesar yang dapat membagi keduanya tanpa sisa. GCD digunakan untuk menyederhanakan pecahan, menentukan keterbagian, dan menyelesaikan persamaan di aritmetika modular. Algoritma Euclidean adalah metode paling efisien untuk menghitung GCD, dengan prinsip bahwa gcd(a, b) = gcd(b, a mod b) ). Konsep ini juga mendasari pencarian invers modular yang digunakan dalam kriptografi seperti RSA.

**3. Bilangan Prima**

Bilangan prima adalah bilangan bulat lebih besar dari 1 yang hanya memiliki dua faktor, yaitu 1 dan dirinya sendiri. Bilangan prima memainkan peran sentral dalam teori bilangan dan keamanan sistem kriptografi modern. Setiap bilangan bulat positif lebih besar dari 1 dapat diuraikan menjadi perkalian faktor-faktor prima (Teorema Dasar Aritmetika). Distribusi bilangan prima digunakan dalam pembuatan kunci publik dan privat karena sifat faktorisasi bilangan besar yang sulit dihitung.

**4. Logaritma Diskrit**

Logaritma diskrit adalah kebalikan dari perpangkatan dalam sistem modular. Diberikan ( g^x = h mod p ), persoalan logaritma diskrit adalah menemukan nilai ( x ) yang memenuhi persamaan tersebut. Masalah ini dianggap sulit untuk diselesaikan jika ( p ) besar, dan sifat inilah yang menjadi dasar keamanan banyak algoritma kriptografi seperti Diffie-Hellman dan ElGamal. Tidak ada algoritma efisien yang diketahui untuk menyelesaikan logaritma diskrit pada bilangan prima besar, sehingga konsep ini penting dalam keamanan digital modern.

---

## 3. Alat dan Bahan
(- Python 3.14  
- Visual Studio Code / editor lain  
- Git dan akun GitHub )

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
- Pertanyaan 1: Aritmetika modular adalah tulang punggung kriptografi modern karena kemampuannya menciptakan sistem matematika yang terbatas dan siklik. Peran utamanya adalah sebagai fondasi untuk membangun fungsi satu arah (one-way functions).  
- Pertanyaan 2: invers modular menjadi sangat penting karena inilah mekanisme matematika yang memungkinkan proses dekripsi. Dalam algoritma seperti RSA, enkripsi dan dekripsi adalah operasi yang saling membatalkan satu sama lain. Sebuah pesan dienkripsi menggunakan eksponen publik (e), dan ciphertext yang dihasilkan didekripsi menggunakan eksponen privat (d). Hubungan inilah yang memastikan bahwa operasi enkripsi yang dilakukan oleh $e$ dapat secara sempurna "dibatalkan" oleh operasi dekripsi menggunakan $d$. Tanpa konsep invers modular, tidak akan ada cara yang andal untuk membalikkan proses enkripsi dan mengembalikan pesan asli dengan aman.
- Pertanyaan 3: Keamanan sistem ini bergantung pada tantangan utama dalam menyelesaikan Masalah Logaritma Diskrit (Discrete Logarithm Problem - DLP), yaitu komputasi yang sangat tidak efisien untuk modulus besar. Hingga saat ini, tidak ada algoritma klasik yang diketahui dapat menyelesaikan DLP dalam waktu yang wajar (waktu polinomial). Tantangannya terletak pada ruang pencarian yang sangat luas, yang membuat serangan brute-force menjadi mustahil, serta tidak adanya jalan pintas matematis untuk mengisolasi variabel eksponen dalam persamaan modular. Meskipun ada algoritma yang lebih baik dari brute-force, waktu yang dibutuhkan untuk menjalankannya masih tumbuh secara sub-eksponensial, membuatnya tidak praktis. Kesulitan fundamental inilah yang membuat sistem kriptografi berbasis DLP aman dari serangan komputer klasik, meskipun pengembangan komputer kuantum dengan algoritma Shor menjadi ancaman di masa depan.
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
