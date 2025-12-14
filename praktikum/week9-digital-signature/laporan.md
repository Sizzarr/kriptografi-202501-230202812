# Laporan Praktikum Kriptografi
Minggu ke-: 9  
Topik: [Digital Signature (RSA/DSA)]  
Nama: [Indra Fata Nizar Azizi]  
NIM: [230202812]  
Kelas: [5IKRA]  

---

## 1. Tujuan
(Tuliskan tujuan pembelajaran praktikum sesuai modul.)
1. Mengimplementasikan tanda tangan digital menggunakan algoritma RSA/DSA.  
2. Memverifikasi keaslian tanda tangan digital.  
3. Menjelaskan manfaat tanda tangan digital dalam otentikasi pesan dan integritas data.  
---

## 2. Dasar Teori
(Ringkas teori relevan (cukup 2–3 paragraf).  
Contoh: .  )

Digital Signature adalah mekanisme otentikasi penting dalam keamanan sistem informasi yang memungkinkan pengirim pesan untuk melampirkan kode unik sebagai bukti identitas. Tanda tangan digital dibentuk dengan cara mengambil intisari (hash) dari pesan asli, yang kemudian dienkripsi menggunakan kunci privat (private key) milik pengirim. Karena kunci privat hanya dimiliki oleh pengirim, tanda tangan ini berfungsi sebagai stempel elektronik yang menjamin bahwa pesan tersebut benar-benar berasal dari sumber yang sah dan isinya belum dimanipulasi oleh pihak lain selama proses pengiriman

Proses verifikasi keaslian dilakukan oleh penerima pesan untuk memastikan validitas tanda tangan tersebut. Penerima akan menjalankan algoritma verifikasi menggunakan kunci publik (public key) milik pengirim terhadap pesan dan tanda tangan yang diterima. Secara teknis, sistem akan melakukan perhitungan matematis untuk membandingkan nilai yang dihasilkan dari pesan yang diterima dengan komponen tanda tangan digitalnya. Jika hasil perhitungan (nilai $v$) sama dengan parameter tanda tangan (nilai $r$), maka tanda tangan dinyatakan valid. Status valid ini mengonfirmasi bahwa pesan tersebut otentik dan pengirimnya adalah pemilik asli dari kunci publik tersebut.

Manfaat utama dari teknologi ini terletak pada jaminan otentikasi pesan dan integritas data. Dalam hal otentikasi, tanda tangan digital memberikan kepastian kepada penerima bahwa mereka sedang berkomunikasi dengan entitas yang benar, bukan penipu. Sedangkan untuk integritas data, mekanisme ini memastikan bahwa data yang diterima persis sama dengan data yang dikirim. Jika terjadi perubahan sekecil apa pun pada pesan saat transmisi, proses verifikasi akan gagal, sehingga penerima mengetahui bahwa data tersebut telah rusak atau diubah. Selain itu, terdapat juga manfaat non-repudiation (anti-penyangkalan), yang mencegah pengirim menyangkal bahwa ia telah mengirim data tersebut

Pendekatan keamanan berlapis dengan menggabungkan algoritma RSA dan DSA. RSA digunakan untuk mengenkripsi pesan agar isinya tidak bisa dibaca (kerahasiaan), sementara DSA (Digital Signature Algorithm) digunakan khusus untuk membuat dan memverifikasi tanda tangan digital. Penelitian ini menyimpulkan bahwa kombinasi RSA 1024-bit untuk enkripsi dan DSA 512-bit untuk tanda tangan digital adalah metode yang paling efisien, karena mampu meningkatkan keamanan data dengan waktu proses enkripsi dan penandatanganan 60% lebih cepat dibandingkan metode lainnya [1]

---

## 3. Alat dan Bahan
(- Python 3.14  
- Visual Studio Code 
- Git dan akun GitHub  
- Library tambahan hashlib, random )

---

## 4. Langkah Percobaan
(Tuliskan langkah yang dilakukan sesuai instruksi.  
Contoh format:


---

## 5. Source Code
(Salin kode program utama yang dibuat atau dimodifikasi.  
Gunakan blok kode:

```python
import hashlib
import random

# --- FUNGSI MATEMATIKA DASAR (SESUAI TEORI) ---

def gcd(a, b):
    """Mencari Faktor Persekutuan Terbesar (Greatest Common Divisor)"""
    while b != 0:
        a, b = b, a % b
    return a

def multiplicative_inverse(e, phi):
    """
    Mencari kunci privat 'd' dimana (d * e) % phi == 1
    Sesuai PDF: d . e = 1 (mod phi(n))
    """
    d = 0
    x1 = 0
    x2 = 1
    y1 = 1
    temp_phi = phi
    
    while e > 0:
        temp1 = temp_phi // e
        temp2 = temp_phi - temp1 * e
        temp_phi = e
        e = temp2
        
        x = x2 - temp1 * x1
        y = d - temp1 * y1
        
        x2 = x1
        x1 = x
        d = y1
        y1 = y
        
    if temp_phi == 1:
        return d + phi

def generate_keypair(p, q):
    """
    Langkah 1: Key Generation (Pembangkitan Kunci)
    Sesuai PDF [cite: 65-72]
    """
    # 1. Hitung n = p * q 
    n = p * q

    # 2. Hitung phi(n) = (p-1)(q-1) 
    phi = (p - 1) * (q - 1)

    # 3. Pilih public key 'e' yg relatif prima dengan phi(n) [cite: 69]
    # Biasanya e=65537, tapi kita cari random kecil untuk demo
    e = random.randrange(1, phi)
    g = gcd(e, phi)
    while g != 1:
        e = random.randrange(1, phi)
        g = gcd(e, phi)

    # 4. Generate secret key 'd' 
    d = multiplicative_inverse(e, phi)
    
    # Return ((Public Key), (Private Key))
    # Public = (e, n), Private = (d, n) [cite: 71-72]
    return ((e, n), (d, n))

def sign_message(message, private_key):
    """
    Langkah 2: Signing (Pembuatan Tanda Tangan)
    Konsep: Signature = HashedMessage^d mod n
    """
    d, n = private_key
    
    # Buat Hash dari pesan (SHA-256) agar integritas terjaga [cite: 133]
    # Kita ubah hash hex menjadi integer agar bisa dihitung matematika
    hash_obj = hashlib.sha256(message.encode())
    hash_int = int(hash_obj.hexdigest(), 16)
    
    # Rumus RSA untuk Signing: S = M^d mod n
    # (Di Python: pow(base, exp, mod))
    signature = pow(hash_int, d, n)
    
    return signature

def verify_signature(message, signature, public_key):
    """
    Langkah 3: Verifying (Verifikasi)
    Konsep: Hash' = Signature^e mod n. Jika Hash' == Hash Asli, maka Valid.
    """
    e, n = public_key
    
    # Hitung ulang hash dari pesan yang diterima
    hash_obj = hashlib.sha256(message.encode())
    hash_int = int(hash_obj.hexdigest(), 16)
    
    # Dekripsi Tanda Tangan: HashDecrypted = Signature^e mod n
    # Sesuai konsep invers enkripsi [cite: 79-81]
    hash_from_signature = pow(signature, e, n)
    
    print(f"   > Hash Asli Pesan:   {hash_int % n} (disederhanakan mod n)")
    print(f"   > Hash dari Signature: {hash_from_signature}")

    if hash_int % n == hash_from_signature:
        return True
    else:
        return False

# --- BAGIAN UTAMA (MAIN) ---
if __name__ == "__main__":
    print("=== PROGRAM DIGITAL SIGNATURE RSA (MANUAL) ===")
    
    # A. INPUT BILANGAN PRIMA (P dan Q)
    # Di dunia nyata P dan Q harus sangaaat besar. 
    # Di sini kita pakai angka kecil supaya proses hitungnya kelihatan cepat.
    p = 61
    q = 53
    print(f"1. Menggunakan bilangan prima p={p}, q={q}")

    # B. GENERATE KEY
    public_key, private_key = generate_keypair(p, q)
    print(f"2. Kunci Publik (e, n)  : {public_key}")
    print(f"   Kunci Privat (d, n)  : {private_key}")

    # C. PROSES TANDA TANGAN (SIGNING)
    pesan = "Transfer Gaji"
    print(f"\n3. Pesan yang akan dikirim: '{pesan}'")
    
    signature = sign_message(pesan, private_key)
    print(f"   Digital Signature (Hasil Hitung S = M^d mod n): {signature}")

    # D. PROSES VERIFIKASI (VERIFYING)
    print(f"\n4. Verifikasi Tanda Tangan...")
    is_valid = verify_signature(pesan, signature, public_key)
    
    if is_valid:
        print("   [HASIL]: Tanda Tangan VALID! (Pesan Asli & Pengirim Terpercaya)")
    else:
        print("   [HASIL]: Tanda Tangan PALSU!")

    # E. SIMULASI PEMALSUAN
    print(f"\n5. Simulasi Serangan (Pesan Diubah)...")
    pesan_palsu = "Transfer Gaji (Ditambah Bonus)"
    print(f"   Pesan berubah jadi: '{pesan_palsu}'")
    is_valid_palsu = verify_signature(pesan_palsu, signature, public_key)
    if is_valid_palsu:
        print("   [HASIL]: Tanda Tangan VALID!")
    else:
        print("   [HASIL]: Tanda Tangan TIDAK VALID! (Integritas Data Terjaga)")
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
[1] F. J. Aufa, Endroyono, and A. Affandi, "Security System Analysis in Combination Method: RSA Encryption and Digital            Signature Algorithm," in 2018 4th International Conference on Science and Technology (ICST), Yogyakarta, Indonesia, 2018.

---

## 10. Commit Log
(Tuliskan bukti commit Git yang relevan.  
Contoh:
```
Author: Indra Fata Nizar Azizi <indrafata980@gmail.com>
Date:   2025-12-15

    week9-digital-signature: Digital Signature (RSA/DSA) )
```
