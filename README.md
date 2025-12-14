# Final-Project-Jarkom-Kelompok-3

## Anggota Kelompok

| No. | Nama Lengkap                          | NRP         |
|-----|----------------------------------------|-------------|
| 1   | Diva Aulia Rosa                        | 5027241003  |
| 2   | Clarissa Aydin Rahmazea                | 5027241014  |
| 3   | Muhammad Rakha Hananditya Rauf         | 5027241015  |
| 4   | Muhammad Rafi' Adly                    | 5027241082  |


## 1. Topologi Jaringan

<img width="806" height="337" alt="Topologi_FP Jarkom Kel 2" src="https://github.com/user-attachments/assets/08de104c-2c49-4319-8774-a7e50053b644" />

Topologi jaringan terdiri dari tiga lokasi utama:

- Gedung Utama Yayasan ARA: berisi unit pendidikan, kurikulum, sarana prasarana, pembinaan sekolah, IT pendidikan, dan layanan operasional yayasan.
- Gedung ARA Tech: pusat teknologi dengan 5 lantai, masing-masing lantai memiliki departemen berbeda (IT Support, Data Center, Cybersecurity, Marketing, Sales, HR, R&D, People Development, Keuangan, Legal, Customer Service, Executive Office, Guest Lounge, Auditorium).
- Kantor Cabang: terdiri dari regional office.

Router 0 berfungsi sebagai backbone utama yang menghubungkan Gedung Utama, Gedung ARA Tech, dan Kantor Cabang. Setiap lantai/unit memiliki switch layer-2 untuk menghubungkan host dan server.

Koneksi antar lantai di Gedung ARA Tech menggunakan link point-to-point (/30) untuk memudahkan static routing internal.

## 2. Tabel Subnet Infrastruktur Jaringan

Tabel berikut menunjukkan pembagian subnet berdasarkan jumlah host tiap unit/departemen.

- Subnet besar diberikan ke unit dengan host banyak (misalnya Layanan Operasional Yayasan).
- Subnet kecil digunakan untuk koneksi point-to-point antar router/lantai.

| Nama Subnet | Rute | Jumlah Host | Jumlah Host + Gateway | Netmask |
|-------------|------|--------------|------------------------|---------|
| A1  | Router 0 › Router 1                                      | 2   | 2   | /30 |
| A2  | Router 1 › Switch8 › SDM Pendidikan                      | 95  | 96  | /25 |
| A3  | Router 1 › Switch9 › Kurikulum & Penjaminan Mutu        | 220 | 221 | /24 |
| A4  | Router 1 › Switch10 › Sarana Prasarana                  | 45  | 46  | /26 |
| A5  | Router 1 › Switch11 › Pembinaan & Pengawasan Sekolah    | 18  | 19  | /27 |
| A6  | Router 1 › Switch12 › Layanan Operasional Yayasan       | 380 | 381 | /23 |
| A7  | Router 1 › Switch13 › IT Pendidikan                     | 6   | 7   | /29 |
| A8  | Lantai 1 › Switch14 › Dept. IT Support                  | 45  | 46  | /26 |
| A9  | Lantai 1 › Switch15 › Server & Data Center              | 12  | 13  | /28 |
| A10 | Lantai 1 › Switch16 › Cybersecurity                     | 22  | 23  | /27 |
| A11 | Lantai 2 › Switch17 › Marketing                         | 35  | 36  | /26 |
| A12 | Lantai 2 › Switch18 › Sales                             | 25  | 26  | /27 |
| A13 | Lantai 2 › Switch19 › Human Resources                   | 25  | 26  | /27 |
| A14 | Lantai 3 › Switch20 › R&D                               | 55  | 56  | /26 |
| A15 | Lantai 3 › Switch21 › People Development                | 18  | 19  | /27 |
| A16 | Lantai 4 › Switch22 › Keuangan                          | 28  | 29  | /27 |
| A17 | Lantai 4 › Switch23 › Legal                             | 18  | 19  | /27 |
| A18 | Lantai 4 › Switch24 › Customer Service                  | 40  | 41  | /26 |
| A19 | Lantai 5 › Switch25 › Executive Office                  | 12  | 13  | /28 |
| A20 | Lantai 5 › Switch26 › Guest Lounge                      | 10  | 11  | /28 |
| A21 | Lantai 5 › Switch27 › Auditorium                        | 15  | 16  | /27 |
| A22 | Lantai 4 › Lantai 5                                     | 2   | 2   | /30 |
| A23 | Lantai 3 › Lantai 4                                     | 2   | 2   | /30 |
| A24 | Lantai 2 › Lantai 3                                     | 2   | 2   | /30 |
| A25 | Lantai 1 › Lantai 2                                     | 2   | 2   | /30 |
| A26 | Router 0 › Lantai 3                                     | 2   | 2   | /30 |
| A27 | Router 0 › Kantor Cabang                                | 2   | 2   | /30 |
| A28 | Kantor Cabang › Switch6 › Regional Office               | 40  | 41  | /26 |
| **Total** | — | **1178** | **1199** | **/21** |

## Langkah Perhitungan + Cadangan

| Langkah | Keterangan                                                                 |
|---------|------------------------------------------------------------------------------|
| 1       | Total kebutuhan host: **1199**                                              |
| 2       | Cadangan 20%: 1199 × 0.2 = 239.8 ≈ **240**                                  |
| 3       | Total dengan cadangan: 1199 + 240 = **1439**                                |
| 4       | Prefix length untuk total host (setelah ditambah cadangan 20%): **/21**    |

```
Total kebutuhan host adalah 1199, ditambah cadangan 20% menjadi 1439 host, sehingga prefix global yang digunakan adalah /21.
```

## 3. VLSM (Gedung Utama)

### Pembagian Subnet Topologi

Teknik VLSM (Variable Length Subnet Mask) digunakan untuk Gedung Utama agar efisiensi IP lebih maksimal.

- Subnet besar diberikan ke unit dengan host banyak.
- Subnet kecil diberikan ke unit dengan host sedikit.
  
<img width="815" height="347" alt="Topologi FP Jarkom Kel 2 (Pembagian Subnet)" src="https://github.com/user-attachments/assets/a4740844-dcc0-4b1d-929c-fd2fab32c564" />

### VLSM Tree

VLSM tree menunjukkan pembagian hierarki subnet dari blok utama /22 menjadi subnet yang lebih kecil sesuai kebutuhan.

Total kebutuhan host Gedung Utama
- Jumlah host: ±772
- Ditambah cadangan 20%: ±926

Prefix /22 menyediakan 1022 usable host, sehingga pas untuk menampung seluruh kebutuhan unit di Gedung Utama.

<img width="768" height="573" alt="VLSM TREE FP Jarkom" src="https://github.com/user-attachments/assets/7596de8a-4515-4d95-9838-5631a220e332" />



### Tabel Subnetting VLSM

| Subnet | Prefix | Usable Hosts | Netmask           | Network ID     | Broadcast       | Usable Range                          |
|--------|--------|--------------|-------------------|----------------|------------------|----------------------------------------|
| A6     | /23    | 510          | 255.255.254.0     | 192.168.0.0    | 192.168.1.255    | 192.168.0.1 – 192.168.1.254            |
| A3     | /24    | 254          | 255.255.255.0     | 192.168.2.0    | 192.168.2.255    | 192.168.2.1 – 192.168.2.254            |
| A2     | /25    | 126          | 255.255.255.128   | 192.168.3.0    | 192.168.3.127    | 192.168.3.1 – 192.168.3.126            |
| A4     | /26    | 62           | 255.255.255.192   | 192.168.3.128  | 192.168.3.191    | 192.168.3.129 – 192.168.3.190          |
| A5     | /27    | 30           | 255.255.255.224   | 192.168.3.192  | 192.168.3.223    | 192.168.3.193 – 192.168.3.222          |
| A7     | /29    | 6            | 255.255.255.248   | 192.168.3.224  | 192.168.3.231    | 192.168.3.225 – 192.168.3.230          |
| A1     | /30    | 2            | 255.255.255.252   | 192.168.3.232  | 192.168.3.235    | 192.168.3.233 – 192.168.3.234          |

## 4. CIDR (Gedung ARA Tech)

### Penggabungan Subnet CIDR

Untuk Gedung ARA Tech digunakan teknik CIDR (Classless Inter-Domain Routing).

- Subnet-subnet kecil digabungkan (supernetting) agar routing antar lantai lebih sederhana.
- Hasil akhir penggabungan menghasilkan blok /23 yang mencakup seluruh lantai 3–5.

<img width="1629" height="693" alt="Topologi CIDR FP Jarkom Kel 2" src="https://github.com/user-attachments/assets/7d05971e-a2e8-4892-b55c-6d357bff99ba" />

### Tabel Gabungan Subnet CIDR

#### Penggabungan 1

| Subnet | Gabungan dari 1 | Netmask 1 | Gabungan dari 2 | Netmask 2 | Netmask Akhir |
|--------|------------------|-----------|------------------|-----------|----------------|
| B1     | A9               | /28       | A10              | /27       | /26            |
| B2     | A12              | /27       | A13              | /27       | /26            |
| B3     | A14              | /26       | A15              | /27       | /25            |
| B4     | A16              | /27       | A17              | /27       | /26            |
| B5     | A19              | /28       | A20              | /28       | /27            |

#### Penggabungan 2

| Subnet | Gabungan dari 1 | Netmask 1 | Gabungan dari 2 | Netmask 2 | Netmask Akhir |
|--------|------------------|-----------|------------------|-----------|----------------|
| C1     | B1               | /26       | A8               | /26       | /25            |
| C2     | B2               | /26       | A11              | /26       | /25            |
| C3     | B4               | /26       | A18              | /26       | /24            |
| C4     | B5               | /27       | A21              | /27       | /26            |

#### Penggabungan 3

| Subnet | Gabungan dari 1 | Netmask 1 | Gabungan dari 2 | Netmask 2 | Netmask Akhir |
|--------|------------------|-----------|------------------|-----------|----------------|
| D1     | C1               | /25       | C2               | /25       | /24            |
| D2     | C3               | /24       | B3               | /25       | /24            |

#### Penggabungan 4

| Subnet | Gabungan dari 1 | Netmask 1 | Gabungan dari 2 | Netmask 2 | Netmask Akhir |
|--------|------------------|-----------|------------------|-----------|----------------|
| E1     | D1               | /24       | D2               | /24       | /23            |

### Tabel Subnetting CIDR


| Subnet | CIDR  | Network ID     | Netmask         | Broadcast       | Range IP                          |
|--------|-------|----------------|------------------|------------------|-----------------------------------|
| A8     | /26   | 192.168.4.192  | 255.255.255.192  | 192.168.4.255    | 192.168.4.193 – 192.168.4.254     |
| A9     | /28   | 192.168.6.0    | 255.255.255.240  | 192.168.6.15     | 192.168.6.1 – 192.168.6.14        |
| A10    | /27   | 192.168.5.32   | 255.255.255.224  | 192.168.5.63     | 192.168.5.33 – 192.168.5.62       |
| A11    | /26   | 192.168.4.0    | 255.255.255.192  | 192.168.4.63     | 192.168.4.1 – 192.168.4.62        |
| A12    | /27   | 192.168.5.64   | 255.255.255.224  | 192.168.5.95     | 192.168.5.65 – 192.168.5.94       |
| A13    | /28   | 192.168.5.96   | 255.255.255.240  | 192.168.5.111    | 192.168.5.97 – 192.168.5.110      |
| A14    | /26   | 192.168.4.64   | 255.255.255.192  | 192.168.4.127    | 192.168.4.65 – 192.168.4.126      |
| A15    | /27   | 192.168.5.128  | 255.255.255.224  | 192.168.5.159    | 192.168.5.129 – 192.168.5.158     |
| A16    | /27   | 192.168.5.160  | 255.255.255.224  | 192.168.5.191    | 192.168.5.161 – 192.168.5.190     |
| A17    | /27   | 192.168.5.192  | 255.255.255.224  | 192.168.5.223    | 192.168.5.193 – 192.168.5.222     |
| A18    | /28   | 192.168.6.16   | 255.255.255.240  | 192.168.6.31     | 192.168.6.17 – 192.168.6.30       |
| A19    | /28   | 192.168.6.32   | 255.255.255.240  | 192.168.6.47     | 192.168.6.33 – 192.168.6.46       |
| A20    | /28   | 192.168.6.48   | 255.255.255.240  | 192.168.6.63     | 192.168.6.49 – 192.168.6.62       |
| A21    | /27   | 192.168.6.0    | 255.255.255.224  | 192.168.6.31     | 192.168.6.1 – 192.168.6.30        |
| A22    | /30   | 192.168.6.52   | 255.255.255.252  | 192.168.6.55     | 192.168.6.53 – 192.168.6.54       |
| A23    | /30   | 192.168.6.56   | 255.255.255.252  | 192.168.6.59     | 192.168.6.57 – 192.168.6.58       |
| A24    | /30   | 192.168.6.60   | 255.255.255.252  | 192.168.6.63     | 192.168.6.61 – 192.168.6.62       |
| A25    | /30   | 192.168.6.64   | 255.255.255.252  | 192.168.6.67     | 192.168.6.65 – 192.168.6.66       |
| A26    | /30   | 192.168.6.68   | 255.255.255.252  | 192.168.6.71     | 192.168.6.69 – 192.168.6.70       |

## 5. Routing
- Static Routing: antar lantai di Gedung ARA Tech.
- Dynamic Routing (OSPF): antar Gedung Utama ↔ ARA Tech, dan ARA Tech ↔ Kantor Cabang.
- Router pusat menjalankan OSPF area 0 sebagai backbone.


## 6. NAT Overload (PAT)
Router utama dikonfigurasi NAT overload agar semua host internal dapat mengakses internet.

## 7. GRE Tunnel
GRE Tunnel dibuat antara router Gedung Utama dan router Kantor Cabang untuk komunikasi aman.




