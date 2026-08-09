# Switching

## 📌 Gambaran Umum

Switching merupakan proses meneruskan frame dari satu perangkat ke perangkat lain dalam jaringan berdasarkan informasi pada MAC Address.

Switch bekerja terutama pada Layer 2 (Data Link) pada model OSI. Switch menggunakan MAC Address Table untuk menentukan ke mana frame harus diteruskan.

Dalam praktik CCNA, switching mencakup beberapa konsep seperti:

- MAC Address Table
- VLAN
- Access Port
- Trunk Port
- 802.1Q
- Inter-VLAN Routing
- Spanning Tree Protocol (STP)
- EtherChannel

Pada lab ini, fokus praktik adalah VLAN dan Inter-VLAN Routing menggunakan dua metode:

1. Multilayer Switch
2. Router-on-a-Stick (ROAS)

---

## 🎯 Tujuan

- Memahami konsep dasar switching
- Memahami fungsi VLAN
- Mengkonfigurasi access port
- Mengkonfigurasi trunk port
- Memahami komunikasi antar-VLAN
- Mengkonfigurasi Inter-VLAN Routing
- Membandingkan metode Multilayer Switch dan Router-on-a-Stick

---

## 🧪 Lab

### 1. Inter-VLAN Routing menggunakan Multilayer Switch

Pada metode ini, Multilayer Switch digunakan untuk melakukan switching sekaligus routing antar-VLAN menggunakan SVI.

➡️ [Dokumentasi Multilayer Switch](./multilayer-switch.md)

### 2. Router-on-a-Stick

Pada metode ini, routing antar-VLAN dilakukan oleh router menggunakan subinterface dan trunk link.

➡️ [Dokumentasi Router-on-a-Stick](./router-on-a-stick.md)

---

## 📚 Konsep yang Dipelajari

| Konsep | Keterangan |
|---|---|
| MAC Address | Identitas Layer 2 pada perangkat jaringan |
| MAC Address Table | Tabel yang digunakan switch untuk meneruskan frame |
| VLAN | Memisahkan jaringan menjadi beberapa broadcast domain |
| Access Port | Port yang membawa satu VLAN |
| Trunk Port | Port yang membawa beberapa VLAN |
| 802.1Q | Standar tagging VLAN pada trunk |
| Inter-VLAN Routing | Memungkinkan komunikasi antar-VLAN |
| SVI | Interface virtual pada switch Layer 3 |
| Subinterface | Interface virtual pada router untuk ROAS |

---

## 📂 File Lab

### Multilayer Switch

`inter-vlan-multilayer-switch.pkt`

### Router-on-a-Stick

`router-on-a-stick.pkt`

---

## 📝 Kesimpulan

Switching merupakan salah satu dasar penting dalam jaringan komputer.

Melalui lab ini, saya mempraktikkan konfigurasi VLAN, trunk, dan Inter-VLAN Routing menggunakan Multilayer Switch serta Router-on-a-Stick.
