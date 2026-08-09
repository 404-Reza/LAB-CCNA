# Router on A Stick

## 📌 Gambaran Umum

Pada lab ini dilakukan konfigurasi Inter-VLAN Routing menggunakan metode Router-on-a-Stick (ROAS).

Router-on-a-Stick menggunakan satu interface fisik router yang dibagi menjadi beberapa subinterface.

Setiap subinterface digunakan untuk melayani satu VLAN.

Koneksi antara router dan switch dikonfigurasi sebagai trunk menggunakan 802.1Q.

---

## 🎯 Tujuan

- Membuat VLAN
- Mengatur access port
- Mengatur trunk(dot1Q)
- Membuat SVI
- Menentukan default gateway di sub-interface
- Menguji konektivitas antar-VLAN

---

## 🖥️ Topologi

Perangkat yang digunakan:

- 1 Router
- 1 Switch(L2) core
- 2 Switch(L2) Distribusi
- PC / End Device
- Beberapa VLAN

---

## 🌐 VLAN dan IP Address

| VLAN | Nama | Network | Default Gateway |
|---|---|---|---|
| 10 | ADMIN | 192.168.10.0/24 | 192.168.10.1 |
| 20 | KEUANGAN | 192.168.20.0/24 | 192.168.20.1 |

---

## ⚙️ FULL KODE

### 1. Router

```cisco
enable
conf t
vlan 10
 name ADMIN
 exit
vlan 20
 name KEUANGAN
 exit

int gig0/1
  no shutdown
  exit

int gig0/1.10
  encapsulation dot1Q 10
  ip address 192.168.10.1 255.255.255.0
  exit

int gig0/1.20
  encapsulation dot1Q 20
  ip address 192.168.20.1 255.255.255.0
  exit
```

### 2. SW-CORE

```cisco
enable
conf t
vlan 10
 name ADMIN
 exit
vlan 20
 name KEUANGAN
 exit

int fa0/1
  switchport mode trunk
  switchport trunk allow vlan 10,20
  exit

int range fa0/2-3
  channel-group 1 mode active
  exit
int port-channel 1
  switchport mode trunk
  switchport trunk allow vlan 10,20
  exit

int range fa0/4-5
  channel-group 2 mode active
  exit
int port-channel 2
  switchport mode trunk
  switchport trunk allow vlan 10,20
  exit
```

### 3. SW-1

```cisco
enable
conf t
vlan 10
 name ADMIN
 exit
vlan 20
 name KEUANGAN
 exit

int range fa0/1-2
  channel-group 1 mode active
  exit
int port-channel 1
  switchport mode trunk
  switchport trunk allow vlan 10,20
  exit

int range fa0/3-4
  switchport mode access
  switchport access vlan 10
  switchport port-security
  switchport port-security maximum 1
  switchport port-security mac-address sticky
  switchport port-security violation shutdown
  exit
```

### 4. SW-2

```cisco
enable
conf t
vlan 10
 name ADMIN
 exit
vlan 20
 name KEUANGAN
 exit

int range fa0/1-2
  channel-group 2 mode active
  exit
int port-channel 2
  switchport mode trunk
  switchport trunk allow vlan 10,20
  exit

int range fa0/3-4
  switchport mode access
  switchport access vlan 20
  switchport port-security
  switchport port-security maximum 1
  switchport port-security mac-address sticky
  switchport port-security violation shutdown
  exit
```
