# Inter-VLAN Routing - Multilayer Switch

## 📌 Gambaran Umum

Pada lab ini dilakukan konfigurasi Inter-VLAN Routing menggunakan Multilayer Switch atau Layer 3 Switch.

Multilayer Switch dapat melakukan fungsi switching pada Layer 2 sekaligus routing pada Layer 3.

Routing antar-VLAN dilakukan menggunakan Switch Virtual Interface (SVI).

---

## 🎯 Tujuan

- Membuat VLAN
- Mengatur access port
- Mengatur trunk
- Membuat SVI
- Mengaktifkan fungsi routing pada Multilayer Switch
- Menentukan default gateway setiap VLAN
- Menguji konektivitas antar-VLAN

---

## 🖥️ Topologi

Perangkat yang digunakan:

- 1 Multilayer(L3) Switch
- 2 Switch(L2)
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

### 1. SW-CORE

```cisco
enable
conf t
vlan 10
 name ADMIN
 exit
vlan 20
 name KEUANGAN
 exit

int vlan 10
  ip address 192.168.10.1 255.255.255.0
  exit

int vlan 20
  ip address 192.168.20.1 255.255.255.0
  exit

int range fa0/1-2
  channel-group 1 mode active
  exit
int port-channel 1
  switchport mode trunk
  switchport trunk allow vlan 10,20
  exit

int range fa0/3-4
  channel-group 2 mode active
  exit
int port-channel 2
  switchport mode trunk
  switchport trunk allow vlan 10,20
  exit

ip routing
```

### 2. SW-1

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

### 2. SW-2

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
