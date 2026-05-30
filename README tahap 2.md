# Hybrid Campus-Core Interconnection with Network Hardening (Cisco Packet Tracer)

![Network Topology](topology.png)

## 📝 Deskripsi Projek
Projek ini mensimulasikan perancangan, konfigurasi, dan pengamanan arsitektur jaringan Enterprise berskala menengah. Topologi ini menghubungkan **Kantor Pusat (HQ)** yang memiliki segmentasi VLAN dan server internal dengan **Kantor Cabang (Branch)** melalui jalur WAN yang dikendalikan oleh **Router-ISP** simulasi. 

Projek ini diselesaikan dalam dua tahapan utama: pembangunan infrastruktur routing-switching mendasar, dilanjutkan dengan implementasi kebijakan keamanan jaringan (*network hardening*) menggunakan Extended Access Control List (ACL).

---

## 🛠️ Fitur & Teknologi Jaringan

### Tahap 1: Infrastruktur & Routing Inti
- **Segmentation & Inter-VLAN Routing:** Menggunakan metode *Router-on-a-Stick* pada `Router-HQ` untuk memisahkan dan menjembatani lalu lintas data antara **VLAN 10 (Admin)** dan **VLAN 20 (Mahasiswa)**.
- **Dynamic Routing Protocol:** Implementasi **OSPFv2 Area 0** di ketiga router (`Router-HQ`, `Router-ISP`, `Router-Branch`) untuk pertukaran tabel routing secara dinamis dan otomatis.
- **Dynamic IP Allocation (DHCP Server):** Konfigurasi DHCP Pool langsung di dalam `Router-Branch` untuk mengotomatisasi distribusi IP Address ke komputer *client* di kantor cabang.
- **Server Deployment:** Penyediaan layanan internal **HTTP (Web Server)** dan **DNS Server** yang terisolasi dengan aman di bawah Switch Pusat.

### Tahap 2: Keamanan & Hardening Jaringan
- **Traffic Filtering via Extended ACL:** Penerapan aturan *firewall* selektif di `Router-HQ` untuk memblokir akses protokol TCP pada port `80 (HTTP)` dan `443 (HTTPS)` khusus dari segmen Mahasiswa (VLAN 20) menuju Web Server, tanpa mengganggu konektivitas ke jaringan luar lainnya.
- **Device Management Security:** Pengamanan jalur komunikasi remote manajemen perangkat menggunakan enkripsi **Enable Secret** tingkat tinggi dan autentikasi berlapis pada jalur **Line VTY (0 4)**.

---

## 📋 Detail Alokasi IP & Port (IP Addressing Space)

### Jaringan Lokal (LAN)
| Lokasi / Segmen | Network Address | Default Gateway | Alokasi IP Penting |
| :--- | :--- | :--- | :--- |
| **VLAN 10 (Admin)** | `192.168.10.0/24` | `192.168.10.1` | `192.168.10.100` (HTTP Server) <br> `192.168.10.200` (DNS Server) |
| **VLAN 20 (Mahasiswa)** | `192.168.20.0/24` | `192.168.20.1` | Alokasi via Static/Local |
| **Kantor Cabang (Branch)** | `192.168.30.0/24` | `192.168.30.1` | Alokasi Otomatis via DHCP Pool |

### Jaringan Luas (WAN)
- **Jalur Interkoneksi HQ - ISP:** `10.10.10.0/30`
  - IP Router-HQ (`Serial 0/3/0`): `10.10.10.1`
  - IP Router-ISP (`Serial 0/3/0`): `10.10.10.2` (Clock rate: 64000)
- **Jalur Interkoneksi Branch - ISP:** `20.20.20.0/30`
  - IP Router-Branch (`Serial 0/3/0`): `20.20.20.1`
  - IP Router-ISP (`Serial 0/3/1`): `20.20.20.2` (Clock rate: 64000)

---

## 🎯 Status Pengujian & Verifikasi (Verification Log)

Pengujian dilakukan menggunakan fitur *Simulation & Packet Inspection (PDU)* pada Cisco Packet Tracer dengan hasil sebagai berikut:

- [x] **DHCP Verification:** `PC-A` & `PC-B` di Kantor Cabang sukses menarik konfigurasi IP otomatis dari router.
- [x] **OSPF Convergence:** Seluruh router berhasil melakukan *converge* dan mencatat rute asing di tabel routing masing-masing.
- [x] **VLAN 10 Access Test:** User Admin sukses mengakses halaman website via browser menggunakan IP Server (`192.168.10.100`).
- [x] **VLAN 20 Security Isolation Test:** User Mahasiswa dialihkan ke status **Request Time Out (RTO) / Failed** saat mencoba membuka Web Server (ACL Berhasil memblokir).
- [x] **VLAN 20 Connectivity Test:** User Mahasiswa tetap sukses melakukan `ping` ke Kantor Cabang (Akses luar tidak terganggu).
- [x] **VTY Security Test:** Jalur remote akses meminta autentikasi password sebelum mengizinkan konfigurasi CLI global.

---

## 🚀 Cara Menjalankan Lab
1. *Download* file `tahap 1.pkt` yang ada di repositori ini.
2. Buka aplikasi **Cisco Packet Tracer** (Direkomendasikan versi terbaru).
3. Jalankan file `.pkt` tersebut.
4. Anda dapat melakukan verifikasi langsung dengan mengirimkan *Packet PDU* atau masuk ke mode CLI pada masing-masing perangkat.