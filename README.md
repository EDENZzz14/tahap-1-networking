# tahap-1-networking
# Hybrid Campus-Core Interconnection (Cisco Packet Tracer)

![Network Topology](topology.png)

## 📝 Deskripsi Projek
Projek ini mensimulasikan perancangan arsitektur jaringan Enterprise berskala menengah yang menghubungkan Kantor Pusat (HQ) dan Kantor Cabang (Branch) melalui jalur WAN (Router-ISP). Projek ini dirancang sebagai implementasi standar laboratorium CCNA.

## 🛠️ Fitur & Teknologi Jaringan
- **Inter-VLAN Routing:** Menggunakan metode *Router-on-a-Stick* untuk memisahkan lalu lintas data VLAN 10 (Admin) dan VLAN 20 (Mahasiswa).
- **Dynamic Routing:** Menggunakan protokol **OSPFv2 Area 0** untuk pertukaran rute otomatis antar 3 Router.
- **Dynamic IP Allocation:** Implementasi **DHCP Server** langsung pada Router Cabang untuk efisiensi distribusi IP ke client.
- **Server Deployment:** Penyediaan layanan internal HTTP (Web Server) dan DNS Server terpusat di Kantor Pusat.

## 📋 Detail Alokasi IP (IP Addressing Space)
- **VLAN 10 (Admin):** 192.168.10.0/24
- **VLAN 20 (Mahasiswa):** 192.168.20.0/24
- **Kantor Cabang:** 192.168.30.0/24
- **Jalur WAN HQ-ISP:** 10.10.10.0/30
- **Jalur WAN Branch-ISP:** 20.20.20.0/30

## 🎯 Status Pengujian (Verification Log)
- [x] DHCP Client di Kantor Cabang Berhasil menarik IP otomatis.
- [x] Routing OSPF Berhasil melakukan *converge* antar 3 router.
- [x] Pengujian PDU Packet (ICMP/Ping) Lintas Cabang ke Web Server berstatus **SUCCESSFUL**.
