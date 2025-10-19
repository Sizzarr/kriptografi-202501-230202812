# Laporan Praktikum Kriptografi

Minggu ke-: 2  
Topik: cryptosystem    
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


---

## 3. Alat dan Bahan
- Python 3.14.0  
- Visual Studio Code
- Git dan akun GitHub  

---

## 4. Langkah Percobaan
---

## 5. Source Code
(Salin kode program utama yang dibuat atau dimodifikasi.  
Gunakan blok kode:

```python
def vigenere_enkripsi(plaintext, kunci):
    ciphertext = ""
    kunci = kunci.upper()
    kunci_index = 0
    
    for char in plaintext:
        if 'A' <= char.upper() <= 'Z':
            # Tentukan pergeseran
            shift = ord(kunci[kunci_index % len(kunci)]) - ord('A')
            
            # Tentukan base (A=0 atau a=0)
            base = ord('A') if char.isupper() else ord('a')
            
            # Enkripsi: (char_index + shift) mod 26
            enkripsi_char = chr((ord(char) - base + shift) % 26 + base)
            ciphertext += enkripsi_char
            
            # Pindah ke huruf kunci berikutnya
            kunci_index += 1
        else:
            # Karakter non-alfabet (spasi, tanda baca) tidak diubah
            ciphertext += char
            
    return ciphertext

def vigenere_dekripsi(ciphertext, kunci):
    plaintext = ""
    kunci = kunci.upper()
    kunci_index = 0
    
    for char in ciphertext:
        if 'A' <= char.upper() <= 'Z':
            # Tentukan pergeseran
            shift = ord(kunci[kunci_index % len(kunci)]) - ord('A')
            
            # Tentukan base (A=0 atau a=0)
            base = ord('A') if char.isupper() else ord('a')
            
            # Dekripsi: (char_index - shift) mod 26
            dekripsi_char = chr((ord(char) - base - shift) % 26 + base)
            plaintext += dekripsi_char
            
            # Pindah ke huruf kunci berikutnya
            kunci_index += 1
        else:
            # Karakter non-alfabet (spasi, tanda baca) tidak diubah
            plaintext += char
            
    return plaintext

# Contoh Penggunaan
teks_asli = "pesan"
kunci_vigenere = "kunci"
teks_terenkripsi = vigenere_enkripsi(teks_asli, kunci_vigenere)
teks_terdekripsi = vigenere_dekripsi(teks_terenkripsi, kunci_vigenere)

print(f"Plaintext: {teks_asli}")
print(f"Kunci: {kunci_vigenere}")
print(f"Ciphertext (Vigenere): {teks_terenkripsi}")
print(f"Decrypted Text: {teks_terdekripsi}")
```
)

Ekspektasi keluaran:  
```
Plaintext : Indra Fata Nizar Aziz
Ciphertext: Snqai Pagj Vszna Ijimr
Decrypted : Indra Fata Nizar Aziz
```

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
