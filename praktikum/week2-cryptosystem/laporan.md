# Laporan Praktikum Kriptografi

Minggu ke-: 2  
Topik: week2-02_cryptosystem    
Nama: Indra Fata Nizar Azizi   
NIM: 230202812  
Kelas: 5IKRA  

---

## 1. Tujuan
(Tuliskan tujuan pembelajaran praktikum sesuai modul.)
1. Mengidentifikasi komponen dasar kriptosistem (plaintext, ciphertext, kunci, algoritma).
2. Menggambarkan proses enkripsi dan dekripsi sederhana.
3. Mengklasifikasikan jenis kriptosistem (simetris dan asimetris).

---

## 2. Dasar Teori
(Ringkas teori relevan (cukup 2–3 paragraf).  
Contoh: definisi cipher klasik, konsep modular aritmetika, dll.  )

---

## 3. Alat dan Bahan
- Python 3.14.0  
- Visual Studio Code
- Git dan akun GitHub  

---

## 4. Langkah Percobaan
Langkah 1 — Membuat Skema Kriptosistem
Buat diagram sederhana (pakai draw.io lalu screenshot) dengan elemen:
Plaintext → [Algoritma + Kunci] → Ciphertext
Ciphertext → [Algoritma + Kunci] → Plaintext
Simpan diagram di folder screenshots/diagram_kriptosistem.png.
Lampirkan ke laporan menggunakan Markdown:
![Diagram Kriptosistem](screenshots/diagram_kriptosistem.png)
Langkah 2 — Implementasi Program Sederhana
Tulis program Python untuk simulasi enkripsi & dekripsi menggunakan substitusi sederhana (misalnya Caesar Cipher).

# file: praktikum/week2-cryptosystem/src/simple_crypto.py

def encrypt(plaintext, key):
    result = ""
    for char in plaintext:
        if char.isalpha():
            shift = 65 if char.isupper() else 97
            result += chr((ord(char) - shift + key) % 26 + shift)
        else:
            result += char
    return result

def decrypt(ciphertext, key):
    result = ""
    for char in ciphertext:
        if char.isalpha():
            shift = 65 if char.isupper() else 97
            result += chr((ord(char) - shift - key) % 26 + shift)
        else:
            result += char
    return result

if __name__ == "__main__":
    message = "<nim><nama>"
    key = 5

    enc = encrypt(message, key)
    dec = decrypt(enc, key)

    print("Plaintext :", message)
    print("Ciphertext:", enc)
    print("Decrypted :", dec)
Ekspektasi keluaran:

Plaintext : Cryptosystem Test
Ciphertext: Hwduytxzjxytr Yjxy
Decrypted : Cryptosystem Test

Langkah 3 — Klasifikasi Simetris & Asimetris
Tambahkan penjelasan di laporan mengenai perbedaan kriptografi simetris dan asimetris.
Sertakan minimal 1 contoh algoritma dari masing-masing:
Simetris → AES, DES
Asimetris → RSA, ECC

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

![Diagram Kriptosistem](screenshots/diagram_kriptosistem.png)
)

---

## 7. Jawaban Pertanyaan
(Jawab pertanyaan diskusi yang diberikan pada modul.  
- Pertanyaan 1: plaintext,chipertext,algoritma enkripsi,algoritma dekripsi,key
- Pertanyaan 2: Keunggulan dari symmetric key cryptography adalah proses enkripsi dan dekripsinya relatif cepat dibandingkan dengan jenis
kriptografi lainnya. Namun, kekurangan dari metode ini adalah distribusi kunci yang aman dikarenakan kriptografi simetris memiliki
kunci enkripsi dan dekripsi yang sama maka penggunaan kriptografi simetris rentan terhadap kebocoran apabila si penyadap mengetahui kuncinya.
- Pertanyaan 3: karena saat distribusi kunci terdapat Penyadap (eavesdropper), penyadap adalah orang yang mencoba menangkap pesan selama
ditransmisikan. Tujuan penyadap adalah untuk mendapatkan informasi sebanyakbanyaknya mengenai sistem kriptografi yang digunakan untuk berkomunikasi
dengan maksud untuk memecahkan cipherteks dikarenakan kriptografi simetris memiliki kunci enkripsi dan dekripsi yang sama maka penggunaan
kriptografi simetris rentan terhadap kebocoran apabila si penyadap mengetahui kuncinya.
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
02_cryptosystem
Author: Nama Mahasiswa <email>
Date:   2025-09-20

    week2-cryptosystem: implementasi Caesar Cipher dan laporan )
```
