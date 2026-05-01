### **Topik: Threat, Vulnerability, Exploit, Risk, dan CIA Triad**

#### **1. Pendahuluan**
Dalam keamanan informasi, terdapat empat konsep inti yang saling terkait: **Threat**, **Vulnerability**, **Exploit**, dan **Risk**. Ketiga konsep ini dievaluasi dan dilindungi berdasarkan model paling fundamental dalam cybersecurity yang disebut **CIA Triad** (Confidentiality, Integrity, Availability).

Memahami CIA Triad sangat penting bagi Web Developer, karena hampir semua keputusan keamanan aplikasi web (otentikasi, penyimpanan data, API, dll) berputar di sekitar ketiga pilar ini.

---

### **2. Threat, Vulnerability, Exploit, dan Risk** (Ringkasan yang telah dikembangkan sebelumnya)

| Istilah          | Definisi Singkat                                      | Contoh dalam Web Development                  |
|------------------|-------------------------------------------------------|-----------------------------------------------|
| **Threat**       | Potensi serangan atau aksi yang dapat merugikan aset  | Phishing, brute force, SQL injection attack   |
| **Vulnerability**| Kelemahan inheren di sistem, kode, atau konfigurasi  | Form input tidak divalidasi, session tidak aman |
| **Exploit**      | Teknik/kode yang memanfaatkan vulnerability          | Payload XSS, script SQL Injection             |
| **Risk**         | Kemungkinan kerugian = Threat × Vulnerability × Impact| Data breach akibat SQL Injection pada situs UMKM |

**Analogi Rumah**:  
Maling (Threat) – Jendela rusak (Vulnerability) – Maling memecah jendela (Exploit) – Barang hilang (Risk).

---

### **3. CIA Triad – Pilar Utama Keamanan Informasi**

**CIA Triad** adalah model keamanan informasi paling klasik dan paling banyak digunakan di dunia. Singkatan **CIA** di sini **bukan** Central Intelligence Agency, melainkan:

- **Confidentiality** (Kerahasiaan)
- **Integrity** (Integritas)
- **Availability** (Ketersediaan)

Ketiga pilar ini menjadi **tujuan utama** dari semua upaya keamanan. Setiap risiko yang ada akan berdampak pada satu atau lebih pilar CIA.

#### **Penjelasan Detail Masing-Masing Pilar**

**1. Confidentiality (Kerahasiaan)**  
**Definisi**: Melindungi informasi agar hanya dapat diakses oleh pihak yang berwenang. Informasi sensitif tidak boleh bocor atau dilihat oleh orang yang tidak berhak.

**Fokus**: Privasi dan pembatasan akses.

**Contoh dalam Web Development**:
- Data password, nomor KTP, riwayat medis, atau data kartu kredit harus terlindungi.
- Serangan yang menyerang Confidentiality: Phishing, Man-in-the-Middle (MitM), SQL Injection yang membaca data user, akses tidak sah ke database.

**Cara Melindungi**:
- Enkripsi data (at rest & in transit) → HTTPS/TLS, AES
- Authentication & Authorization yang kuat (JWT, OAuth 2.0, Role-Based Access Control)
- Hashing password (bcrypt, Argon2)
- Data classification (Public, Internal, Confidential, Restricted)

**2. Integrity (Integritas)**  
**Definisi**: Menjamin bahwa data tetap **akurat, lengkap, konsisten**, dan tidak diubah oleh pihak yang tidak berwenang (baik sengaja maupun tidak sengaja).

**Fokus**: Kebenaran dan keandalan data.

**Contoh dalam Web Development**:
- Pesanan customer di e-commerce tidak boleh diubah nilainya setelah dibuat.
- Serangan yang menyerang Integrity: XSS (menyisipkan script berbahaya), CSRF (mengubah data tanpa sepengetahuan user), defacement website, perubahan data melalui vulnerability IDOR.

**Cara Melindungi**:
- Input validation + Output encoding (anti-XSS)
- Prepared Statement / Parameterized Query (anti-SQL Injection)
- Digital signature & Hashing (SHA-256)
- Version control & audit log
- File Integrity Monitoring (FIM)
- Checksum atau HMAC

**3. Availability (Ketersediaan)**  
**Definisi**: Menjamin bahwa sistem, data, dan layanan tetap dapat diakses dan digunakan oleh pengguna yang berwenang kapan saja dibutuhkan, tanpa gangguan yang berlebihan.

**Fokus**: Aksesibilitas dan kelangsungan layanan.

**Contoh dalam Web Development**:
- Website toko online harus tetap online saat ada banyak pengunjung (hari raya).
- Serangan yang menyerang Availability: DDoS attack, ransomware yang mengenkripsi data, server down karena tidak ada redundansi.

**Cara Melindungi**:
- Load balancing & auto-scaling
- CDN (Content Delivery Network)
- Backup rutin + Disaster Recovery Plan
- Rate limiting & Web Application Firewall (WAF)
- Redundansi server (multi-region/cloud)

---

### **4. Tabel CIA Triad dalam Praktik Web Development**

| Pilar            | Definisi Singkat                          | Ancaman Umum                  | Contoh Serangan                  | Mitigasi Utama                          |
|------------------|-------------------------------------------|-------------------------------|----------------------------------|-----------------------------------------|
| **Confidentiality** | Data hanya boleh diakses pihak berwenang | Pencurian data                | SQL Injection, Phishing, MitM    | Enkripsi, HTTPS, RBAC, Hashing          |
| **Integrity**    | Data tidak boleh diubah tanpa izin        | Pemalsuan / modifikasi data   | XSS, CSRF, IDOR                  | Validation, Sanitization, Digital Signature |
| **Availability** | Sistem & data selalu tersedia saat dibutuhkan | Denial of Service             | DDoS, Ransomware                 | WAF, Backup, Load Balancer, Rate Limiting |

---

### **5. Hubungan antara Threat, Vulnerability, Risk, dan CIA Triad**

- **Threat** dapat menyerang salah satu atau ketiga pilar CIA.
- **Vulnerability** adalah celah yang memungkinkan threat merusak Confidentiality, Integrity, atau Availability.
- **Exploit** adalah cara attacker merusak salah satu pilar tersebut.
- **Risk** diukur berdasarkan seberapa besar dampak terhadap **CIA Triad** + seberapa besar kemungkinan terjadinya.

**Contoh**:
- Vulnerability SQL Injection → dapat merusak **Confidentiality** (baca data) sekaligus **Integrity** (ubah data). Jika berhasil, **Risk** menjadi sangat tinggi karena berdampak pada dua pilar sekaligus.

---

### **6. Kesimpulan**

CIA Triad adalah **fondasi** dalam merancang, mengembangkan, dan mengevaluasi keamanan sistem. Sebagai Web Developer, setiap fitur yang Anda buat harus mempertimbangkan ketiga pilar ini:

- Apakah data pengguna tetap rahasia? (**Confidentiality**)
- Apakah data dapat dipercaya dan tidak mudah diubah? (**Integrity**)
- Apakah website tetap bisa diakses meski ada serangan? (**Availability**)

**Prinsip Penting**:
> “Keamanan yang baik bukan hanya mencegah serangan, tetapi juga menjaga **Confidentiality**, **Integrity**, dan **Availability** dari aset informasi.”

---