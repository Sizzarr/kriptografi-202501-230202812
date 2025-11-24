# Laporan Praktikum Kriptografi
Minggu ke-: 7  
Topik: Diffie-Hellman Key Exchange  
Nama: Indra Fata Nizar Azizi  
NIM:230202812    
Kelas: 5IKRA 

---

## 1. Tujuan
(Tuliskan tujuan pembelajaran praktikum sesuai modul.)

1. Melakukan simulasi protokol **Diffie-Hellman** untuk pertukaran kunci publik.  
2. Menjelaskan mekanisme pertukaran kunci rahasia menggunakan bilangan prima dan logaritma diskrit.  
3. Menganalisis potensi serangan pada protokol Diffie-Hellman (termasuk serangan **Man-in-the-Middle / MITM**).  

---

## 2. Dasar Teori
(Ringkas teori relevan (cukup 2–3 paragraf).  
Contoh: definisi cipher klasik, konsep modular aritmetika, dll.  )

Protokol Diffie-Hellman adalah metode pertukaran kunci kriptografi yang memungkinkan dua pihak untuk membuat kunci rahasia bersama melalui saluran komunikasi publik yang tidak aman. Protokol ini didasarkan pada kesulitan komputasional problem logaritma diskrit, yaitu mencari nilai x dari persamaan g^x ≡ y (mod p), di mana p adalah bilangan prima besar dan g adalah generator. Kedua pihak (Alice dan Bob) masing-masing memilih bilangan rahasia pribadi, kemudian menukar hasil perhitungan publik untuk menghasilkan kunci rahasia yang identik tanpa pernah mengirimkan kunci tersebut secara langsung.

Keamanan protokol Diffie-Hellman bergantung pada pemilihan parameter yang tepat: bilangan prima p harus cukup besar (minimal 2048-bit untuk standar modern) dan generator g harus dipilih dengan cermat. Meskipun matematikanya kuat, protokol ini rentan terhadap serangan Man-in-the-Middle (MITM) karena tidak menyediakan autentikasi identitas. Penyerang dapat memposisikan diri di antara Alice dan Bob, melakukan pertukaran kunci terpisah dengan masing-masing pihak, sehingga dapat mendekripsi dan memodifikasi pesan tanpa terdeteksi. Oleh karena itu, implementasi praktis memerlukan mekanisme autentikasi tambahan seperti sertifikat digital atau tanda tangan digital.

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
LANGKAH 1: SIMULASI DIFFIE-HELLMAN NORMAL
1. INISIALISASI Parameter Publik
   - Tentukan p (bilangan prima) = 23
   - Tentukan g (generator) = 5
   - Parameter ini diketahui publik

2. GENERATE Private Key
   - a ← random(1, p-1)  // Private key Alice
   - b ← random(1, p-1)  // Private key Bob
   - Private key TIDAK PERNAH dikirim

3. HITUNG Public Key
   - A ← g^a mod p      // Public key Alice
   - B ← g^b mod p      // Public key Bob

4. PERTUKARAN Public Key (melalui saluran publik)
   - Alice mengirim A ke Bob
   - Bob mengirim B ke Alice

5. HITUNG Shared Secret
   - Alice: shared_secret_A ← B^a mod p
   - Bob:   shared_secret_B ← A^b mod p

6. VERIFIKASI
   - Jika shared_secret_A = shared_secret_B
     MAKA komunikasi aman berhasil
   - RETURN shared_secret_A, shared_secret_B
  

LANGKAH 2: SIMULASI SERANGAN MITM (MAN-IN-THE-MIDDLE)

LANGKAH:
1. INISIALISASI Parameter Publik
   - p = 23 (bilangan prima)
   - g = 5 (generator)

2. GENERATE Private Key (3 pihak)
   - a ← random(1, p-1)  // Private key Alice
   - b ← random(1, p-1)  // Private key Bob
   - e ← random(1, p-1)  // Private key Eve (attacker)

3. HITUNG Public Key
   - A ← g^a mod p      // Public key Alice
   - B ← g^b mod p      // Public key Bob
   - E ← g^e mod p      // Public key Eve

4. SERANGAN: Eve Mencegat dan Mengganti Public Key
   a) Komunikasi Alice → Bob:
      - Alice mengirim A
      - Eve MENCEGAT dan mengganti dengan E
      - Bob menerima E (bukan A)
   
   b) Komunikasi Bob → Alice:
      - Bob mengirim B
      - Eve MENCEGAT dan mengganti dengan E
      - Alice menerima E (bukan B)

5. HITUNG Shared Secret (3 pasang kunci berbeda)
   - shared_secret_Alice ← E^a mod p    // Alice dengan "Bob" (sebenarnya Eve)
   - shared_secret_Bob ← E^b mod p      // Bob dengan "Alice" (sebenarnya Eve)
   - shared_secret_Eve_Alice ← A^e mod p // Eve dengan Alice
   - shared_secret_Eve_Bob ← B^e mod p   // Eve dengan Bob

6. ANALISIS HASIL
   - shared_secret_Alice = shared_secret_Eve_Alice (Eve tahu kunci Alice)
   - shared_secret_Bob = shared_secret_Eve_Bob (Eve tahu kunci Bob)
   - shared_secret_Alice ≠ shared_secret_Bob (Alice dan Bob punya kunci berbeda!)

7. DAMPAK
   - Eve dapat DEKRIPSI semua pesan dari Alice
   - Eve dapat DEKRIPSI semua pesan dari Bob
   - Eve dapat MODIFIKASI pesan tanpa terdeteksi
   - Alice dan Bob tidak sadar komunikasi mereka disadap

---

## 5. Source Code
(Salin kode program utama yang dibuat atau dimodifikasi.  
Gunakan blok kode:

```python
import random

def print_header(title):
    """Fungsi untuk mencetak header dengan format yang rapi"""
    print("\n" + "="*60)
    print(f"  {title}")
    print("="*60)

def diffie_hellman_normal():
    """Simulasi Diffie-Hellman normal tanpa serangan"""
    print_header("SIMULASI DIFFIE-HELLMAN NORMAL")
    
    # Langkah 1: Parameter publik (disepakati bersama)
    p = 23  # bilangan prima
    g = 5   # generator
    
    print(f"\n[1] Parameter Publik:")
    print(f"    Bilangan Prima (p) = {p}")
    print(f"    Generator (g)      = {g}")
    
    # Langkah 2: Generate private key untuk Alice dan Bob
    a = random.randint(1, p-1)  # secret Alice
    b = random.randint(1, p-1)  # secret Bob
    
    print(f"\n[2] Private Key (Rahasia):")
    print(f"    Alice (a)          = {a}")
    print(f"    Bob (b)            = {b}")
    
    # Langkah 3: Hitung public key
    A = pow(g, a, p)  # A = g^a mod p
    B = pow(g, b, p)  # B = g^b mod p
    
    print(f"\n[3] Public Key (Dikirim melalui saluran publik):")
    print(f"    Alice menghitung: A = {g}^{a} mod {p} = {A}")
    print(f"    Bob menghitung:   B = {g}^{b} mod {p} = {B}")
    
    # Langkah 4: Pertukaran public key
    print(f"\n[4] Pertukaran Public Key:")
    print(f"    Alice mengirim A = {A} ke Bob")
    print(f"    Bob mengirim B = {B} ke Alice")
    
    # Langkah 5: Hitung shared secret
    shared_secret_A = pow(B, a, p)  # Alice: s = B^a mod p
    shared_secret_B = pow(A, b, p)  # Bob: s = A^b mod p
    
    print(f"\n[5] Perhitungan Shared Secret:")
    print(f"    Alice menghitung: s = B^a mod p = {B}^{a} mod {p} = {shared_secret_A}")
    print(f"    Bob menghitung:   s = A^b mod p = {A}^{b} mod {p} = {shared_secret_B}")
    
    # Verifikasi
    print(f"\n[6] HASIL:")
    print(f"    Kunci bersama Alice: {shared_secret_A}")
    print(f"    Kunci bersama Bob:   {shared_secret_B}")
    
    if shared_secret_A == shared_secret_B:
        print(f"    ✓ SUKSES! Kedua pihak memiliki kunci yang sama.")
    else:
        print(f"    ✗ GAGAL! Kunci tidak sama.")
    
    return shared_secret_A, shared_secret_B


def diffie_hellman_mitm():
    """Simulasi serangan Man-in-the-Middle pada Diffie-Hellman"""
    print_header("SIMULASI SERANGAN MAN-IN-THE-MIDDLE (MITM)")
    
    # Langkah 1: Parameter publik
    p = 23
    g = 5
    
    print(f"\n[1] Parameter Publik:")
    print(f"    Bilangan Prima (p) = {p}")
    print(f"    Generator (g)      = {g}")
    
    # Langkah 2: Private key untuk Alice, Bob, dan Eve (attacker)
    a = random.randint(1, p-1)  # secret Alice
    b = random.randint(1, p-1)  # secret Bob
    e = random.randint(1, p-1)  # secret Eve (attacker)
    
    print(f"\n[2] Private Key:")
    print(f"    Alice (a)          = {a}")
    print(f"    Bob (b)            = {b}")
    print(f"    Eve/Attacker (e)   = {e}")
    
    # Langkah 3: Hitung public key
    A = pow(g, a, p)  # Public key Alice
    B = pow(g, b, p)  # Public key Bob
    E = pow(g, e, p)  # Public key Eve
    
    print(f"\n[3] Public Key:")
    print(f"    Alice: A = {g}^{a} mod {p} = {A}")
    print(f"    Bob:   B = {g}^{b} mod {p} = {B}")
    print(f"    Eve:   E = {g}^{e} mod {p} = {E}")
    
    # Langkah 4: SERANGAN! Eve mencegat dan mengganti public key
    print(f"\n[4] SERANGAN MITM:")
    print(f"    ⚠ Alice ingin mengirim A = {A} ke Bob")
    print(f"    ⚠ Eve MENCEGAT dan mengganti dengan E = {E}")
    print(f"    → Bob menerima E = {E} (bukan A = {A})")
    print()
    print(f"    ⚠ Bob ingin mengirim B = {B} ke Alice")
    print(f"    ⚠ Eve MENCEGAT dan mengganti dengan E = {E}")
    print(f"    → Alice menerima E = {E} (bukan B = {B})")
    
    # Langkah 5: Perhitungan shared secret
    # Alice menghitung dengan public key Eve (bukan Bob)
    shared_secret_Alice = pow(E, a, p)  # Alice: s = E^a mod p
    
    # Bob menghitung dengan public key Eve (bukan Alice)
    shared_secret_Bob = pow(E, b, p)    # Bob: s = E^b mod p
    
    # Eve menghitung dua kunci berbeda
    shared_secret_Eve_Alice = pow(A, e, p)  # Eve dengan Alice: s = A^e mod p
    shared_secret_Eve_Bob = pow(B, e, p)    # Eve dengan Bob: s = B^e mod p
    
    print(f"\n[5] Perhitungan Shared Secret:")
    print(f"    Alice menghitung: s = E^a mod p = {E}^{a} mod {p} = {shared_secret_Alice}")
    print(f"    Bob menghitung:   s = E^b mod p = {E}^{b} mod {p} = {shared_secret_Bob}")
    print(f"    Eve dengan Alice: s = A^e mod p = {A}^{e} mod {p} = {shared_secret_Eve_Alice}")
    print(f"    Eve dengan Bob:   s = B^e mod p = {B}^{e} mod {p} = {shared_secret_Eve_Bob}")
    
    # Hasil
    print(f"\n[6] HASIL SERANGAN:")
    print(f"    Kunci Alice:       {shared_secret_Alice}")
    print(f"    Kunci Bob:         {shared_secret_Bob}")
    print(f"    Kunci Eve-Alice:   {shared_secret_Eve_Alice}")
    print(f"    Kunci Eve-Bob:     {shared_secret_Eve_Bob}")
    
    print(f"\n    ⚠ ANALISIS:")
    if shared_secret_Alice == shared_secret_Eve_Alice:
        print(f"    ✓ Eve dapat mendekripsi pesan dari Alice (kunci sama)")
    if shared_secret_Bob == shared_secret_Eve_Bob:
        print(f"    ✓ Eve dapat mendekripsi pesan dari Bob (kunci sama)")
    if shared_secret_Alice != shared_secret_Bob:
        print(f"    ✗ Alice dan Bob memiliki kunci BERBEDA!")
        print(f"    ✗ Mereka tidak dapat berkomunikasi dengan benar")
    
    print(f"\n    💀 Eve berhasil melakukan MITM attack!")
    print(f"    💀 Eve dapat membaca dan memodifikasi semua pesan!")
    
    return {
        'alice': shared_secret_Alice,
        'bob': shared_secret_Bob,
        'eve_alice': shared_secret_Eve_Alice,
        'eve_bob': shared_secret_Eve_Bob
    }


def demonstrate_mitm_attack_flow():
    """Demonstrasi alur komunikasi dengan MITM"""
    print_header("ALUR KOMUNIKASI DENGAN MITM ATTACK")
    
    print("""
    SKENARIO: Alice ingin mengirim pesan "HELLO" ke Bob
    
    [Tanpa MITM - Normal]
    Alice --[enkripsi dengan kunci bersama]--> Bob
          Bob dapat dekripsi dengan kunci yang sama
    
    [Dengan MITM - Serangan]
    Alice --[enkripsi dengan kunci_Eve_Alice]--> Eve --[dekripsi]
                                                   |
                                                   | Eve baca pesan: "HELLO"
                                                   | Eve bisa ubah jadi: "HALLO"
                                                   |
    Eve --[enkripsi ulang dengan kunci_Eve_Bob]--> Bob --[dekripsi]
    
    DAMPAK:
    ✗ Bob menerima "HALLO" (bukan "HELLO")
    ✗ Alice dan Bob tidak tahu pesan sudah diubah
    ✗ Eve dapat membaca semua komunikasi
    ✗ Eve dapat memodifikasi pesan tanpa terdeteksi
    """)


def mitigasi_mitm():
    """Penjelasan cara mitigasi serangan MITM"""
    print_header("MITIGASI SERANGAN MITM")
    
    print("""
    CARA MENCEGAH SERANGAN MITM:
    
    1. AUTENTIKASI DENGAN SERTIFIKAT DIGITAL
       - Gunakan PKI (Public Key Infrastructure)
       - Verifikasi identitas dengan Certificate Authority (CA)
       - Contoh: TLS/SSL certificates
    
    2. DIGITAL SIGNATURE
       - Tandatangani public key dengan private key
       - Verifikasi signature sebelum pertukaran kunci
       - Pastikan public key berasal dari pihak yang benar
    
    3. PRE-SHARED SECRET (Out-of-Band Verification)
       - Verifikasi fingerprint melalui saluran terpisah
       - Contoh: PIN, QR code, phone call
       - WhatsApp: verifikasi security code
    
    4. STATION-TO-STATION (STS) PROTOCOL
       - Kombinasi Diffie-Hellman dengan digital signatures
       - Autentikasi mutual antara kedua pihak
       - Mencegah MITM attack
    
    5. PERFECT FORWARD SECRECY
       - Generate kunci baru setiap sesi
       - Jika satu kunci bocor, sesi lain tetap aman
       - Digunakan dalam TLS 1.3
    
    CONTOH IMPLEMENTASI NYATA:
    • HTTPS (TLS/SSL) = Diffie-Hellman + Certificates
    • SSH = Diffie-Hellman + Host key verification
    • Signal/WhatsApp = Extended Diffie-Hellman + Digital signatures
    • VPN (IPSec) = Diffie-Hellman + Pre-shared keys atau certificates
    """)


def main():
    
    # Simulasi 1: Diffie-Hellman Normal
    diffie_hellman_normal()
    
    input("\n\nTekan ENTER untuk melanjutkan ke simulasi MITM...")
    
    # Simulasi 2: Serangan MITM
    diffie_hellman_mitm()
    
    input("\n\nTekan ENTER untuk melihat alur serangan MITM...")
    
    # Demonstrasi alur MITM
    demonstrate_mitm_attack_flow()
    
    input("\n\nTekan ENTER untuk melihat cara mitigasi...")
    
    # Cara mitigasi
    mitigasi_mitm()
    
    print("\n" + "▓"*60)
    print("▓" + "  SIMULASI SELESAI".center(58) + "▓")
    print("▓"*60 + "\n")


if __name__ == "__main__":
    main()
```
)

---

## 6. Hasil dan Pembahasan
(- Lampirkan screenshot hasil eksekusi program (taruh di folder `screenshots/`).  
- Berikan tabel atau ringkasan hasil uji jika diperlukan.  
- Jelaskan apakah hasil sesuai ekspektasi.  
- Bahas error (jika ada) dan solusinya. 

Hasil eksekusi program Caesar Cipher:
![Hasil Output](screenshots/output.png)

![Hasil Output](screenshots/output.png)

![Hasil Output](screenshots/output.png)
)

---

## 7. Jawaban Pertanyaan
(Jawab pertanyaan diskusi yang diberikan pada modul.  
- Pertanyaan 1: Diffie-Hellman memungkinkan pertukaran kunci di saluran publik yang tidak aman karena protokol ini menggunakan prinsip matematika satu arah yang sangat unik. Bayangkan dua pihak, Alice dan Bob, ingin menyepakati sebuah rahasia bersama. Mereka masing-masing memilih angka rahasia pribadi yang tidak pernah dikirimkan, lalu menggabungkannya dengan angka publik melalui perhitungan matematika kompleks. Hasil perhitungan inilah yang dikirimkan lewat jaringan. Keamanannya terjamin karena bagi peretas yang menyadap jaringan, membalikkan proses perhitungan tersebut untuk menemukan angka rahasia aslinya (dikenal sebagai masalah logaritma diskrit) adalah hal yang sangat sulit dan membutuhkan waktu ribuan tahun dengan teknologi saat ini. Jadi, meskipun peretas melihat apa yang dikirim, mereka tidak bisa mendapatkan kunci akhirnya.  
- Pertanyaan 2: kelemahan utama dari protokol Diffie-Hellman murni adalah tidak adanya proses autentikasi atau pengenalan identitas. Protokol ini hanya menjamin bahwa sebuah jalur aman telah terbentuk, tetapi tidak memberi tahu Anda dengan siapa jalur itu terhubung. Celah ini membuka peluang serangan Man-in-the-Middle (MITM), di mana seorang peretas bisa mencegat komunikasi di tengah jalan. Peretas tersebut bisa berpura-pura menjadi Bob di hadapan Alice, dan menjadi Alice di hadapan Bob, lalu membuat kunci enkripsi terpisah dengan keduanya. Akibatnya, peretas bisa membaca semua pesan yang lewat tanpa disadari oleh Alice maupun Bob yang mengira mereka berbicara langsung satu sama lain.
- Pertanyaan 3: Untuk mencegah serangan MITM tersebut, protokol Diffie-Hellman harus digabungkan dengan metode autentikasi, seperti tanda tangan digital (digital signatures) atau sertifikat digital. Dalam skenario ini, ketika Alice mengirimkan data kuncinya, dia juga menyertakan bukti identitas digital yang terverifikasi. Bob kemudian dapat memeriksa bukti tersebut untuk memastikan bahwa data yang ia terima benar-benar berasal dari Alice yang asli, bukan dari peretas. Dengan memastikan identitas lawan bicara sebelum menyepakati kunci, celah bagi orang ketiga untuk menyusup di tengah percakapan dapat ditutup sepenuhnya.  
)
---

## 8. Kesimpulan
(Tuliskan kesimpulan singkat (2–3 kalimat) berdasarkan percobaan.  )

Protokol Diffie-Hellman berhasil memungkinkan dua pihak menghasilkan kunci rahasia yang identik melalui saluran publik tanpa mengirimkan kunci privat, dengan memanfaatkan kesulitan komputasional problem logaritma diskrit. Namun, protokol ini rentan terhadap serangan Man-in-the-Middle (MITM) karena tidak menyediakan mekanisme autentikasi identitas, sehingga penyerang dapat mengintersepsi dan mengganti kunci publik untuk mendekripsi seluruh komunikasi. Oleh karena itu, implementasi praktis Diffie-Hellman memerlukan lapisan keamanan tambahan seperti sertifikat digital atau tanda tangan digital untuk memastikan autentikasi dan mencegah serangan MITM

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
commit week7-diffie-hellman
Author: Indra Fata Nizar Azizi <indrafata980@gmail.com>
Date:   2025-11-24

    week7-diffie-hellman: Key Exchange )
```
