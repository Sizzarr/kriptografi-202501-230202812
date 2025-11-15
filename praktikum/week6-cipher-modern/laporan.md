# Laporan Praktikum Kriptografi
Minggu ke-: 6  
Topik: Cipher Modern (DES, AES, RSA)  
Nama: Indra Fata Nizar Azizi  
NIM: 230202812  
Kelas: 5ikra  

---

## 1. Tujuan
(Tuliskan tujuan pembelajaran praktikum sesuai modul.)
Setelah mengikuti praktikum ini, mahasiswa diharapkan mampu:  
1. Mengimplementasikan algoritma **DES** untuk blok data sederhana.  
2. Menerapkan algoritma **AES** dengan panjang kunci 128 bit.  
3. Menjelaskan proses pembangkitan kunci publik dan privat pada algoritma **RSA**.
---

## 2. Dasar Teori
(Ringkas teori relevan (cukup 2–3 paragraf).  
Contoh: definisi cipher klasik, konsep modular aritmetika, dll.  )

DES (Data Encryption Standard) adalah algoritma enkripsi simetris block cipher yang dikembangkan pada tahun 1970-an dan menjadi standar federal AS, DES menggunakan kunci 56-bit dan memproses data dalam blok 64-bit melalui 16 putaran struktur Feistel yang melibatkan permutasi, substitusi, dan operasi XOR. Kelemahan utama DES terletak pada panjang kuncinya yang terlalu pendek untuk standar keamanan modern, membuatnya rentan terhadap serangan brute force. Untuk mengatasi ini, dikembangkan Triple DES (3DES) yang menerapkan DES tiga kali secara berurutan, namun solusi ini mengorbankan efisiensi komputasi.

AES (Advanced Encryption Standard) menggantikan DES sebagai standar enkripsi sejak 2001 setelah melalui kompetisi yang ketat. AES adalah algoritma simetris berbasis substitution-permutation network (SPN) yang bekerja pada blok 128-bit dengan variasi panjang kunci 128, 192, atau 256-bit. Setiap putaran AES (10/12/14 putaran tergantung panjang kunci) melakukan transformasi SubBytes menggunakan S-box, ShiftRows untuk permutasi baris, MixColumns untuk difusi pada kolom state, dan AddRoundKey untuk kombinasi dengan kunci putaran. AES unggul dalam efisiensi implementasi hardware dan software, serta memiliki fondasi matematis yang kuat dalam teori finite field (Galois Field), menjadikannya standar enkripsi global yang digunakan dalam berbagai aplikasi termasuk protokol blockchain.

RSA (Rivest-Shamir-Adleman) adalah algoritma kriptografi kunci publik fundamental yang keamanannya bergantung pada kesulitan komputasi masalah faktorisasi bilangan bulat besar. RSA menggunakan pasangan kunci asimetris: kunci publik (n, e) untuk enkripsi dan kunci privat (n, d) untuk dekripsi, di mana n adalah hasil perkalian dua bilangan prima besar. RSA bersama dengan algoritma kunci publik lainnya (seperti ECDSA) menjadi fondasi untuk digital signatures dan manajemen identitas dalam sistem blockchain. Meskipun RSA lebih lambat dibanding enkripsi simetris, perannya krusial dalam key exchange protocols, digital signatures, dan Public Key Infrastructure (PKI) yang juga diterapkan dalam smart contract security seperti yang didokumentasikan dalam Ethereum & Solidity Documentation.

---

## 3. Alat dan Bahan
(- Python 3.14  
- Visual Studio Code / editor lain  
- Git dan akun GitHub  
- Library tambahan misalnya pycryptodome  )

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
- Pertanyaan 1:

DES
1. Jenis kunci: Simetris
2. Ukuran kunci: 56 bit
3. Keamanan: Tidak aman di era modern ini karena dapat di-brute-force dengan hardware saat ini

AES
1. Jenis kunci: Simetris
2. Ukuran kunci: 128, 192, 256 bit
3. Keamanan: Sangat kuat dan dirancang untuk tahan terhadap kriptanalisis modern.

RSA
1. Jenis kunci: Asimetris
2. Ukuran kunci: 1024–4096 bit.
3. Keamanan: Berdasarkan sulitnya memfaktorkan bilangan komposit besar (integer factorization problem).
    
- Pertanyaan 2:
1. Keamanan jauh lebih tinggi
   
   DES hanya menggunakan 56-bit key, yang dapat dipecahkan dengan brute force sedangkan AES memiliki 128–256-bit key, yang       jauh lebih sulit diserang.
2. Desain algoritma AES lebih kuat

   AES menggunakan struktur substitution–permutation network (SPN) yang tahan terhadap
   - differential cryptanalysis
   - linear cryptanalysis
   - serangan brute force
3. Lebih cepat dan lebih efisien, bekerja optimal pada prosesor modern (ada instruksi AES-NI), lebih efisien dalam perangkat mobile dan embedded
4. Diakui sebagai standar internasional, AES dipilih oleh NIST (2001) sebagai pengganti resmi DES dan digunakan secara global (TLS, VPN, Wi-Fi, disk encryption).
- Pertanyaan 3:
1. Karena RSA menggunakan dua kunci berbeda
2. Kunci publik (public key) → boleh dibagikan untuk enkripsi atau verifikasi tanda tangan.
3. Kunci privat (private key) → dirahasiakan untuk dekripsi atau membuat tanda tangan.

proses pembangkitan kunci RSA
- Pilih dua bilangan prima besar: p dan q, misal p = 61, q = 53
- Hitung n = p × q,  n = 61 × 53 = 3233
- Hitung Fungsi Euler φ(n) = (p-1)(q-1), φ (n) = (61 − 1) x (53 − 1) = 60 × 52  = 3120
- Pilih eksponen publik 1 < 𝑒 < φ(n) dan gcd (e , φ(n)) = 1, e=17 (karena 17 relatif prima terhadap 3120)
- Hitung eksponen privat 𝑑,
  d × e ≡ 1 (mod φ(n))
  d × e (mod φ(n)) = 1 ,
  d = 2753 karena( 2753 × 17 ) mod 3120 = 1
- Bentuk pasangan kunci 
  1. Kunci publik (e,n), Kunci publik (17 , 3233)
  2. Kunci privat (d,n), Kunci privat (2753 , 3233)
 Penggunaan:
- Enkripsi: C = M^e mod n
- Dekripsi: M = C^e mod n

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
