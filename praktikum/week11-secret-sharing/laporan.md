# Laporan Praktikum Kriptografi
Minggu ke-: 11  
Topik: [Secret Sharing (Shamir’s Secret Sharing)]  
Nama: [Indra Fata Nizar Azizi]  
NIM: [230202812]  
Kelas: [5IKRA]  

---

## 1. Tujuan
(Tuliskan tujuan pembelajaran praktikum sesuai modul.)
1. Menjelaskan konsep **Shamir Secret Sharing** (SSS).  
2. Melakukan simulasi pembagian rahasia ke beberapa pihak menggunakan skema SSS.  
3. Menganalisis keamanan skema distribusi rahasia.  

---

## 2. Dasar Teori
(Ringkas teori relevan (cukup 2–3 paragraf).  
Contoh: definisi cipher klasik, konsep modular aritmetika, dll.  )

Shamir’s Secret Sharing merupakan cara “membagi rahasia” supaya tidak ada satu orang pun yang pegang rahasia utuh, tapi tetap bisa dipulihkan kalau pihak yang cukup berkumpul. Skemanya ditulis (k, n): rahasia dipecah jadi n bagian (shares), dan butuh minimal k shares untuk membangun kembali rahasianya. Jadi kalau cuma pegang 1 atau 2 share padahal threshold-nya 3, kita tidak dapat rahasia apa-apa yang berguna, cuma dapat angka random yang bikin pusing.

Inti matematikanya pakai polinomial derajat (k−1) di aritmetika modulo bilangan prima p. Rahasia disimpan sebagai konstanta polinomial (a0), lalu koefisien lainnya dipilih acak. Setiap share adalah pasangan titik (x, f(x)). Karena polinomial derajat (k−1) butuh k titik untuk ditentukan secara unik, maka punya k shares berarti bisa melakukan Lagrange interpolation untuk menghitung f(0) dan mendapatkan a0 (rahasianya). Semua operasi dilakukan mod p supaya aman dan konsisten.

Keamanannya kuat secara teori jika penyerang hanya punya kurang dari k shares, masih ada banyak polinomial berbeda yang cocok dengan shares itu, sehingga nilai rahasia (a0) tetap tidak bisa dipastikan. Itu sebabnya SSS jauh lebih aman daripada “copy-paste kunci ke beberapa orang”, karena satu kebocoran tidak langsung membocorkan semuanya. Di dunia nyata, ini sering dipakai untuk backup kunci kripto, kontrol akses internal perusahaan (misalnya butuh 3 dari 5 admin untuk membuka kunci master), atau skenario recovery penting lain yang butuh gabungan otoritas.


---

## 3. Alat dan Bahan
(- Python 3.14  
- Visual Studio Code   
- Git dan akun GitHub)

---

## 4. Langkah Percobaan
(Tuliskan langkah yang dilakukan sesuai instruksi.  
### Langkah 1 — Implementasi Shamir Secret Sharing
### Langkah 2 — Simulasi Manual (Tanpa Library)
### Langkah 3 — Analisis Keamanan


---

## 5. Source Code
(Salin kode program utama yang dibuat atau dimodifikasi.  
Gunakan blok kode:

```python
import secrets
from typing import List, Tuple

PRIME = 2**521 - 1
Share = Tuple[int, int]


def _eval_poly(coeffs: List[int], x: int, p: int) -> int:
    y = 0
    for a in reversed(coeffs):
        y = (y * x + a) % p
    return y


def _encode_secret_to_int(secret: str) -> int:
    """Encode string ke integer (simple: langsung dari bytes)"""
    data = secret.encode("utf-8")
    return int.from_bytes(data, "big")


def _decode_int_to_secret(secret_int: int, expected_len: int = None) -> str:
    """Decode integer ke string"""
    if secret_int < 0:
        raise ValueError("Secret integer invalid")
    
    if secret_int == 0:
        return ""
    
    # Konversi ke bytes
    blen = (secret_int.bit_length() + 7) // 8
    data = secret_int.to_bytes(blen, "big")
    
    try:
        return data.decode("utf-8")
    except UnicodeDecodeError:
        raise ValueError("Decode gagal: shares kurang dari threshold atau data corrupt")


def split_secret(secret: str, k: int, n: int, p: int = PRIME) -> List[Share]:
    if not (2 <= k <= n):
        raise ValueError("Harus 2 <= k <= n")
    if n > 255:
        raise ValueError("n maksimal 255")
    
    a0 = _encode_secret_to_int(secret)
    if a0 >= p:
        raise ValueError("Secret terlalu besar untuk modulus p")
    
    # Buat polynomial derajat k-1
    coeffs = [a0] + [secrets.randbelow(p) for _ in range(k - 1)]
    
    shares = []
    for x in range(1, n + 1):
        y = _eval_poly(coeffs, x, p)
        shares.append((x, y))
    return shares


def _lagrange_interpolate_at_0(shares: List[Share], p: int) -> int:
    """Rekonstruksi f(0) menggunakan Lagrange interpolation"""
    x_s = [x for x, _ in shares]
    y_s = [y for _, y in shares]
    k = len(shares)
    
    total = 0
    for i in range(k):
        xi, yi = x_s[i], y_s[i]
        num = 1
        den = 1
        for j in range(k):
            if i == j:
                continue
            xj = x_s[j]
            num = (num * (-xj)) % p
            den = (den * (xi - xj)) % p
        
        inv_den = pow(den, -1, p)
        total = (total + yi * num * inv_den) % p
    
    return total


def recover_secret(shares: List[Share], k: int, p: int = PRIME) -> str:
    if len(shares) < k:
        raise ValueError("Shares kurang dari threshold k")
    
    used = shares[:k]
    secret_int = _lagrange_interpolate_at_0(used, p)
    return _decode_int_to_secret(secret_int)


def format_share(share: Share) -> str:
    x, y = share
    return f"{x}-{y:x}"


def parse_share(s: str) -> Share:
    x_str, y_hex = s.split("-", 1)
    return int(x_str), int(y_hex, 16)


def main():
    print("=" * 50)
    print("SHAMIR SECRET SHARING")
    print("=" * 50)
    
    # Input secret
    secret = input("\nMasukkan secret: ")
    
    # Input k dan n
    while True:
        try:
            k = int(input("Masukkan k (threshold): "))
            n = int(input("Masukkan n (jumlah shares): "))
            
            if k < 2 or k > n:
                print("Error: Harus 2 <= k <= n")
                continue
            if n > 255:
                print("Error: n maksimal 255")
                continue
            break
        except ValueError:
            print("Error: Masukkan angka yang valid")
    
    # Split secret
    print("\n" + "=" * 50)
    print("MEMBUAT SHARES...")
    print("=" * 50)
    
    try:
        shares = split_secret(secret, k, n)
        
        print(f"\nSecret berhasil dibagi menjadi {n} shares")
        print(f"Minimal {k} shares diperlukan untuk rekonstruksi\n")
        
        print("Shares:")
        for i, sh in enumerate(shares, 1):
            print(f"  Share {i}: {format_share(sh)}")
        
        # Rekonstruksi
        print("\n" + "=" * 50)
        print("REKONSTRUKSI SECRET")
        print("=" * 50)
        
        print(f"\nMenggunakan {k} shares pertama untuk rekonstruksi...")
        recovered = recover_secret(shares[:k], k)
        
        print(f"\nSecret berhasil direkonstruksi: {recovered}")
        
        if recovered == secret:
            print("✓ Rekonstruksi BERHASIL!")
        else:
            print("✗ Rekonstruksi GAGAL!")
            
    except Exception as e:
        print(f"\nError: {e}")


if __name__ == "__main__":
    main()
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
- Pertanyaan 1: Keuntungan utamanya adalah tidak ada pihak yang memegang rahasia utuh. Jika kunci dibagikan sebagai salinan langsung, maka kebocoran satu salinan saja sudah membocorkan seluruh rahasia. Pada SSS, kebocoran beberapa shares (< k) tidak cukup untuk mengetahui secret, sehingga risiko kompromi berkurang dan kontrol akses lebih baik.  
- Pertanyaan 2: Threshold (k) menentukan batas minimum shares yang diperlukan untuk rekonstruksi. Jika k terlalu kecil, rahasia jadi lebih mudah dipulihkan oleh pihak tidak berwenang (keamanan menurun). Jika k terlalu besar, rahasia menjadi sulit dipulihkan saat kondisi darurat karena perlu terlalu banyak pihak (ketersediaan/availability menurun). Jadi k adalah pilihan kita untuk memilih antara keamanan dan ketersediaan.
- Pertanyaan 3:  Trezor Model T, hardware wallet cryptocurrency, mengimplementasikan Shamir's Secret Sharing melalui fitur "Shamir Backup" (sekarang disebut Multi-share Backup) sejak 2019 sebagai hardware wallet pertama di dunia yang menerapkan standar SLIP-39. Pengguna dapat membuat beberapa recovery shares (misalnya 3 shares dengan threshold 2-of-3) dari private key wallet mereka, di mana setiap share berupa 20 atau 33 kata. Jika satu share hilang atau dicuri, wallet tetap aman dan dapat diakses menggunakan shares yang tersisa. Sistem ini memungkinkan distributed recovery - wallet dapat dipulihkan tanpa menggabungkan semua shares di satu tempat, dengan mengunjungi lokasi berbeda secara berurutan menggunakan perangkat Trezor yang mengingat progress recovery. Implementasi ini digunakan ribuan pengguna untuk melindungi aset cryptocurrency mereka dari risiko kehilangan atau pencurian.
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

Author: Indra Fata Nizar Azizi <indrafata980@gmail.com>
Date:   2025-12-28

      week11-secret-sharing
```
