# Jarkom-Modul-5-2026-K-63

# Soal 1
Pada perancangan jaringan markas, diperlukan pembagian alamat IP yang terstruktur agar setiap LAN dan koneksi antar-router memiliki alamat jaringan masing-masing. Pembagian alamat IP dilakukan menggunakan metode **VLSM (Variable Length Subnet Mask)**.

VLSM merupakan metode subnetting yang memungkinkan penggunaan subnet mask berbeda-beda sesuai dengan jumlah host yang dibutuhkan. Dengan metode ini, setiap subnet dapat menggunakan prefix terkecil yang masih mampu menampung seluruh kebutuhan host.

Pada perancangan ini, pembagian alamat IP dilakukan untuk:
- 17 LAN dengan jumlah host yang berbeda-beda.
- 16 link antar-router.
- Setiap LAN membutuhkan satu alamat IP tambahan untuk gateway.
- Setiap link antar-router membutuhkan dua alamat IP untuk kedua interface router yang terhubung.

Jaringan induk yang digunakan dalam perhitungan ini adalah `10.95.0.0/16`.

---

## Metode Perhitungan VLSM

Pembagian subnet dilakukan dengan mengurutkan kebutuhan host dari jumlah terbesar hingga terkecil. Hal ini bertujuan agar subnet dengan kebutuhan host terbesar mendapatkan blok alamat IP terlebih dahulu.

Rumus yang digunakan:

**Jumlah host yang dapat digunakan:**

\[
2^h-2
\]

Keterangan:
- h = jumlah bit host.
- Dikurangi 2 karena satu alamat digunakan sebagai Network ID dan satu alamat sebagai Broadcast.

**Menentukan prefix:**

\[
Prefix=32-h
\]

Langkah pembagian VLSM:
1. Menghitung kebutuhan host setiap LAN, termasuk satu IP untuk gateway.
2. Mengurutkan kebutuhan host dari yang terbesar hingga terkecil.
3. Menentukan jumlah bit host yang dapat memenuhi kebutuhan tersebut.
4. Menentukan prefix subnet berdasarkan jumlah bit host.
5. Membagi alamat IP secara berurutan tanpa terjadi tumpang tindih antar-subnet.
6. Mengalokasikan subnet `/30` untuk setiap link antar-router karena setiap link hanya membutuhkan dua alamat IP yang dapat digunakan.

---

## Tabel Pembagian VLSM untuk 17 LAN

Jumlah IP terpakai pada tabel berikut sudah termasuk alamat gateway. Sisa IP menunjukkan jumlah alamat host yang masih tersedia setelah kebutuhan host dan gateway dipenuhi.

| No. | Nama LAN | Network ID | Prefix | Gateway | Broadcast | IP Terpakai | Sisa IP |
|---:|---|---|---:|---|---|---:|---:|
| 1 | Quarters | 10.95.0.0 | /23 | 10.95.0.1 | 10.95.1.255 | 501 | 9 |
| 2 | Comm-Net | 10.95.2.0 | /24 | 10.95.2.1 | 10.95.2.255 | 201 | 53 |
| 3 | Hangar-Crew | 10.95.3.0 | /25 | 10.95.3.1 | 10.95.3.127 | 101 | 25 |
| 4 | Sachiel | 10.95.3.128 | /26 | 10.95.3.129 | 10.95.3.191 | 56 | 6 |
| 5 | Medic | 10.95.3.192 | /27 | 10.95.3.193 | 10.95.3.223 | 27 | 3 |
| 6 | Relay | 10.95.3.224 | /27 | 10.95.3.225 | 10.95.3.255 | 26 | 4 |
| 7 | Garden-Staff | 10.95.4.0 | /27 | 10.95.4.1 | 10.95.4.31 | 15 | 15 |
| 8 | Dock-Crew | 10.95.4.32 | /28 | 10.95.4.33 | 10.95.4.47 | 13 | 1 |
| 9 | Lab | 10.95.4.48 | /29 | 10.95.4.49 | 10.95.4.55 | 6 | 0 |
| 10 | Radar | 10.95.4.88 | /29 | 10.95.4.89 | 10.95.4.95 | 5 | 1 |
| 11 | Terminal | 10.95.4.56 | /29 | 10.95.4.57 | 10.95.4.63 | 4 | 2 |
| 12 | Cage | 10.95.4.64 | /29 | 10.95.4.65 | 10.95.4.71 | 4 | 2 |
| 13 | Dogma | 10.95.4.72 | /29 | 10.95.4.73 | 10.95.4.79 | 3 | 3 |
| 14 | Monolith | 10.95.4.80 | /29 | 10.95.4.81 | 10.95.4.87 | 3 | 3 |
| 15 | Archive | 10.95.4.96 | /30 | 10.95.4.97 | 10.95.4.99 | 2 | 0 |
| 16 | Intel | 10.95.4.100 | /30 | 10.95.4.101 | 10.95.4.103 | 2 | 0 |
| 17 | Cmd | 10.95.4.104 | /30 | 10.95.4.105 | 10.95.4.107 | 2 | 0 |

**Keterangan:**
- Network ID merupakan alamat awal subnet.
- Prefix menunjukkan ukuran subnet.
- Gateway merupakan alamat IP router yang digunakan sebagai pintu keluar LAN.
- Broadcast merupakan alamat terakhir subnet.
- IP Terpakai merupakan jumlah host yang dibutuhkan, termasuk gateway.
- Sisa IP merupakan jumlah alamat host yang masih dapat digunakan.

---

## Tabel Pembagian VLSM untuk 16 Link Antar-Router

Untuk koneksi antar-router digunakan prefix `/30`. Subnet `/30` memiliki empat alamat IP, yaitu satu Network ID, dua alamat host yang dapat digunakan, dan satu Broadcast.

| No. | Koneksi Router | Network ID | Prefix | IP Router A | IP Router B | Broadcast |
|---:|---|---|---:|---|---|---|
| 1 | Gendou – Fuyutsuki | 10.95.4.108 | /30 | 10.95.4.109 | 10.95.4.110 | 10.95.4.111 |
| 2 | Gendou – Shigeru | 10.95.4.112 | /30 | 10.95.4.113 | 10.95.4.114 | 10.95.4.115 |
| 3 | Gendou – Asuka | 10.95.4.116 | /30 | 10.95.4.117 | 10.95.4.118 | 10.95.4.119 |
| 4 | Gendou – Kaji | 10.95.4.120 | /30 | 10.95.4.121 | 10.95.4.122 | 10.95.4.123 |
| 5 | Gendou – Misato | 10.95.4.124 | /30 | 10.95.4.125 | 10.95.4.126 | 10.95.4.127 |
| 6 | Gendou – Hikari | 10.95.4.128 | /30 | 10.95.4.129 | 10.95.4.130 | 10.95.4.131 |
| 7 | Gendou – Yui | 10.95.4.132 | /30 | 10.95.4.133 | 10.95.4.134 | 10.95.4.135 |
| 8 | Shigeru – Makoto | 10.95.4.136 | /30 | 10.95.4.137 | 10.95.4.138 | 10.95.4.139 |
| 9 | Fuyutsuki – Maya | 10.95.4.140 | /30 | 10.95.4.141 | 10.95.4.142 | 10.95.4.143 |
| 10 | Fuyutsuki – Toji | 10.95.4.144 | /30 | 10.95.4.145 | 10.95.4.146 | 10.95.4.147 |
| 11 | Asuka – Kensuke | 10.95.4.148 | /30 | 10.95.4.149 | 10.95.4.150 | 10.95.4.151 |
| 12 | Asuka – Ritsuko | 10.95.4.152 | /30 | 10.95.4.153 | 10.95.4.154 | 10.95.4.155 |
| 13 | Hikari – Kaworu | 10.95.4.156 | /30 | 10.95.4.157 | 10.95.4.158 | 10.95.4.159 |
| 14 | Yui – Rei | 10.95.4.160 | /30 | 10.95.4.161 | 10.95.4.162 | 10.95.4.163 |
| 15 | Yui – Mari | 10.95.4.164 | /30 | 10.95.4.165 | 10.95.4.166 | 10.95.4.167 |
| 16 | Yui – Shinji | 10.95.4.168 | /30 | 10.95.4.169 | 10.95.4.170 | 10.95.4.171 |

Setiap link memiliki dua alamat IP yang dapat digunakan. IP Router A dan IP Router B diberikan pada dua interface yang saling terhubung.

---

## Contoh Perhitungan Salah Satu Subnet

Sebagai contoh, perhitungan dilakukan pada LAN Quarters yang membutuhkan 500 host.

**Langkah 1: Menghitung kebutuhan IP**

Quarters membutuhkan 500 alamat IP untuk perangkat. Selain itu, dibutuhkan satu alamat IP untuk gateway.

\[
500+1=501
\]

Dengan demikian, subnet harus dapat menampung minimal 501 alamat IP yang dapat digunakan.

**Langkah 2: Menentukan jumlah bit host**

Menggunakan rumus:

\[
2^h-2
\]

Percobaan pertama:

\[
2^8-2=254
\]

Hasil tersebut belum mencukupi karena hanya dapat menampung 254 host.

Percobaan kedua:

\[
2^9-2=510
\]

Hasil tersebut mencukupi karena dapat menampung 510 host.

Maka, jumlah bit host yang dibutuhkan adalah 9 bit.

**Langkah 3: Menentukan prefix**

\[
Prefix=32-9
\]

\[
Prefix=/23
\]

Dengan demikian, Quarters menggunakan prefix `/23`.

**Langkah 4: Menentukan alamat subnet**

Berdasarkan jaringan induk `10.95.0.0/16`, subnet Quarters mendapatkan alokasi:

| Keterangan | Alamat IP |
|---|---|
| Network ID | 10.95.0.0 |
| Prefix | /23 |
| Subnet Mask | 255.255.254.0 |
| Gateway | 10.95.0.1 |
| IP Host Pertama | 10.95.0.1 |
| IP Host Terakhir | 10.95.1.254 |
| Broadcast | 10.95.1.255 |

Rentang alamat host yang dapat digunakan adalah `10.95.0.1` sampai `10.95.1.254`.

Jumlah host yang tersedia: 510

Jumlah host yang digunakan: 501

Sisa alamat IP: 510-501=9 host

Jadi, subnet Quarters menggunakan `10.95.0.0/23` karena prefix tersebut merupakan prefix terkecil yang mampu menampung kebutuhan 500 perangkat beserta satu gateway.

## Contoh Perhitungan Link Antar-Router

Setiap link antar-router hanya membutuhkan dua alamat IP yang dapat digunakan, satu untuk masing-masing router.

Perhitungan kebutuhan host:

\[
2^h-2
\]

Jika menggunakan 2 bit host:

\[
2^2-2=2
\]

Maka prefix yang digunakan:

\[
32-2=/30
\]

Contohnya pada koneksi Gendou–Fuyutsuki:

| Keterangan | Alamat IP |
|---|---|
| Network ID | 10.95.4.108 |
| Prefix | /30 |
| Subnet Mask | 255.255.255.252 |
| IP Gendou | 10.95.4.109 |
| IP Fuyutsuki | 10.95.4.110 |
| Broadcast | 10.95.4.111 |

Subnet `/30` dipilih karena menyediakan tepat dua alamat IP host yang dapat digunakan. Dengan demikian, tidak ada alokasi alamat host yang berlebihan untuk koneksi point-to-point.

## Gambar Pohon IP

Pohon IP menggambarkan pembagian jaringan induk menjadi beberapa subnet berdasarkan kebutuhan host. Jaringan induk dibagi menjadi dua kelompok utama, yaitu 17 LAN dan 16 link antar-router.

Berikut struktur pembagiannya:

```text
10.95.0.0/16 (Jaringan Induk)
|
|-- 17 LAN
|   |
|   |-- Quarters       : 10.95.0.0/23
|   |-- Comm-Net       : 10.95.2.0/24
|   |-- Hangar-Crew    : 10.95.3.0/25
|   |-- Sachiel        : 10.95.3.128/26
|   |-- Medic          : 10.95.3.192/27
|   |-- Relay          : 10.95.3.224/27
|   |-- Garden-Staff   : 10.95.4.0/27
|   |-- Dock-Crew      : 10.95.4.32/28
|   |-- Lab            : 10.95.4.48/29
|   |-- Terminal       : 10.95.4.56/29
|   |-- Cage           : 10.95.4.64/29
|   |-- Dogma          : 10.95.4.72/29
|   |-- Monolith       : 10.95.4.80/29
|   |-- Radar          : 10.95.4.88/29
|   |-- Archive        : 10.95.4.96/30
|   |-- Intel          : 10.95.4.100/30
|   |-- Cmd            : 10.95.4.104/30
|
|-- 16 Link Antar-Router
    |
    |-- Gendou - Fuyutsuki : 10.95.4.108/30
    |-- Gendou - Shigeru   : 10.95.4.112/30
    |-- Gendou - Asuka     : 10.95.4.116/30
    |-- Gendou - Kaji      : 10.95.4.120/30
    |-- Gendou - Misato    : 10.95.4.124/30
    |-- Gendou - Hikari    : 10.95.4.128/30
    |-- Gendou - Yui       : 10.95.4.132/30
    |-- Shigeru - Makoto   : 10.95.4.136/30
    |-- Fuyutsuki - Maya   : 10.95.4.140/30
    |-- Fuyutsuki - Toji   : 10.95.4.144/30
    |-- Asuka - Kensuke    : 10.95.4.148/30
    |-- Asuka - Ritsuko    : 10.95.4.152/30
    |-- Hikari - Kaworu    : 10.95.4.156/30
    |-- Yui - Rei          : 10.95.4.160/30
    |-- Yui - Mari         : 10.95.4.164/30
    |-- Yui - Shinji       : 10.95.4.168/30
```

**Penandaan jalur Dummy-Plug ke Armisael:**

Berdasarkan konfigurasi alamat IP yang telah digunakan:
- Dummy-Plug memiliki alamat `10.95.4.51/29` dan berada pada subnet Lab `10.95.4.48/29`.
- Armisael memiliki alamat `10.95.4.83/29` dan berada pada subnet Monolith `10.95.4.80/29`.

Oleh karena itu, pada gambar pohon IP, bagian yang perlu ditandai adalah:

- **Lab — `10.95.4.48/29` (subnet Dummy-Plug).**
- **Monolith — `10.95.4.80/29` (subnet Armisael).**

Kedua subnet tersebut merupakan jaringan asal dan tujuan komunikasi. Keduanya bukan satu subnet yang sama dan tidak boleh dianggap sebagai satu link `/30` langsung.

# Soal 2

Pada tugas kedua dilakukan implementasi konfigurasi jaringan berdasarkan pembagian alamat IP menggunakan metode VLSM yang telah dikerjakan pada tugas sebelumnya.

Konfigurasi dilakukan pada seluruh router yang terdapat dalam topologi GNS3. Setiap interface diberikan alamat IP dan subnet mask sesuai dengan subnet yang telah ditentukan.

Selain konfigurasi alamat IP, seluruh router juga diaktifkan fitur IP forwarding agar dapat meneruskan paket jaringan dari satu interface ke interface lainnya.

Gendou berperan sebagai router utama yang terhubung dengan NAT1. Interface yang mengarah ke NAT1 menggunakan DHCP, sedangkan interface lainnya menggunakan alamat IP statis sesuai pembagian VLSM.

Tujuan pelaksanaan tugas ini adalah:

1. Mengimplementasikan pembagian alamat IP berdasarkan hasil perhitungan VLSM.
2. Mengonfigurasi alamat IP pada seluruh interface router.
3. Mengaktifkan IP forwarding pada seluruh router.
4. Menghubungkan Gendou dengan NAT1 menggunakan DHCP.
5. Memastikan seluruh interface router aktif dan memiliki alamat IP yang sesuai.
6. Melakukan pengujian konektivitas antar-router menggunakan perintah ping.

## Daftar Hubungan antar-router

| No. | Router pertama | Interface | Router kedua | Interface |
|---|---|---|---|---|
| 1 | Gendou | eth1 | Fuyutsuki | eth0 |
| 2 | Gendou | eth2 | Shigeru | eth0 |
| 3 | Gendou | eth3 | Asuka | eth0 |
| 4 | Gendou | eth4 | Kaji | eth0 |
| 5 | Gendou | eth5 | Misato | eth0 |
| 6 | Gendou | eth6 | Hikari | eth0 |
| 7 | Gendou | eth7 | Yui | eth0 |
| 8 | Shigeru | eth2 | Makoto | eth0 |
| 9 | Fuyutsuki | eth2 | Maya | eth0 |
| 10 | Fuyutsuki | eth3 | Toji | eth0 |
| 11 | Asuka | eth2 | Kensuke | eth0 |
| 12 | Asuka | eth3 | Ritsuko | eth0 |
| 13 | Hikari | eth2 | Kaworu | eth0 |
| 14 | Yui | eth1 | Rei | eth0 |
| 15 | Yui | eth2 | Mari | eth0 |
| 16 | Yui | eth3 | Shinji | eth0 |

Selain hubungan antar-router, masing-masing router juga terhubung dengan switch yang menghubungkan perangkat pada subnet LAN.

## Pembagian Alamat IP

Alamat IP diberikan berdasarkan hasil perhitungan VLSM pada tugas sebelumnya.

### Alamat IP Interface Router

| Router | Interface | Alamat IP | Prefix | Keterangan |
|---|---|---|---|---|
| Gendou | eth0 | DHCP | DHCP | NAT1 |
| Gendou | eth1 | 10.95.4.109 | /30 | Fuyutsuki |
| Gendou | eth2 | 10.95.4.113 | /30 | Shigeru |
| Gendou | eth3 | 10.95.4.117 | /30 | Asuka |
| Gendou | eth4 | 10.95.4.121 | /30 | Kaji |
| Gendou | eth5 | 10.95.4.125 | /30 | Misato |
| Gendou | eth6 | 10.95.4.129 | /30 | Hikari |
| Gendou | eth7 | 10.95.4.133 | /30 | Yui |
| Gendou | eth8 | 10.95.4.105 | /30 | Cmd |
| Fuyutsuki | eth0 | 10.95.4.110 | /30 | Gendou |
| Fuyutsuki | eth1 | 10.95.4.57 | /29 | Terminal |
| Fuyutsuki | eth2 | 10.95.4.141 | /30 | Maya |
| Fuyutsuki | eth3 | 10.95.4.145 | /30 | Toji |
| Shigeru | eth0 | 10.95.4.114 | /30 | Gendou |
| Shigeru | eth1 | 10.95.4.81 | /29 | Monolith |
| Shigeru | eth2 | 10.95.4.137 | /30 | Makoto |
| Asuka | eth0 | 10.95.4.118 | /30 | Gendou |
| Asuka | eth1 | 10.95.4.97 | /30 | Archive |
| Asuka | eth2 | 10.95.4.149 | /30 | Kensuke |
| Asuka | eth3 | 10.95.4.153 | /30 | Ritsuko |
| Kaji | eth0 | 10.95.4.122 | /30 | Gendou |
| Kaji | eth1 | 10.95.4.101 | /30 | Intel |
| Misato | eth0 | 10.95.4.126 | /30 | Gendou |
| Misato | eth1 | 10.95.4.65 | /29 | Cage |
| Hikari | eth0 | 10.95.4.130 | /30 | Gendou |
| Hikari | eth1 | 10.95.2.1 | /24 | Comm-Net |
| Hikari | eth2 | 10.95.4.157 | /30 | Kaworu |
| Yui | eth0 | 10.95.4.134 | /30 | Gendou |
| Yui | eth1 | 10.95.4.161 | /30 | Rei |
| Yui | eth2 | 10.95.4.165 | /30 | Mari |
| Yui | eth3 | 10.95.4.169 | /30 | Shinji |
| Yui | eth4 | 10.95.3.1 | /25 | Hangar-Crew |
| Rei | eth0 | 10.95.4.162 | /30 | Yui |
| Rei | eth1 | 10.95.0.1 | /23 | Quarters |
| Mari | eth0 | 10.95.4.166 | /30 | Yui |
| Mari | eth1 | 10.95.4.33 | /28 | Dock-Crew |
| Shinji | eth0 | 10.95.4.170 | /30 | Yui |
| Shinji | eth1 | 10.95.4.1 | /27 | Garden-Staff |
| Kaworu | eth0 | 10.95.4.158 | /30 | Hikari |
| Kaworu | eth1 | 10.95.3.225 | /27 | Relay |
| Kensuke | eth0 | 10.95.4.150 | /30 | Asuka |
| Kensuke | eth1 | 10.95.3.129 | /26 | Sachiel |
| Ritsuko | eth0 | 10.95.4.154 | /30 | Asuka |
| Ritsuko | eth1 | 10.95.4.49 | /29 | Lab |
| Maya | eth0 | 10.95.4.142 | /30 | Fuyutsuki |
| Maya | eth1 | 10.95.3.193 | /27 | Medic |
| Toji | eth0 | 10.95.4.146 | /30 | Fuyutsuki |
| Toji | eth1 | 10.95.4.73 | /29 | Dogma |
| Makoto | eth0 | 10.95.4.138 | /30 | Shigeru |
| Makoto | eth1 | 10.95.4.89 | /29 | Radar |

## Konfigurasi Seluruh Router

Setiap interface menggunakan konfigurasi static untuk alamat IP internal, sedangkan Gendou menggunakan DHCP pada interface eth0 untuk memperoleh alamat IP dari NAT1.

IP forwarding diaktifkan menggunakan perintah:

```bash
up sysctl -w net.ipv4.ip_forward=1
```

Berikut konfigurasi setiap router.

### Gendou

Gendou merupakan router pusat yang terhubung langsung dengan NAT1 dan tujuh router tingkat pertama.

```bash
auto lo
iface lo inet loopback

# NAT1
auto eth0
iface eth0 inet dhcp

# Gendou - Fuyutsuki
auto eth1
iface eth1 inet static
    address 10.95.4.109
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

# Gendou - Shigeru
auto eth2
iface eth2 inet static
    address 10.95.4.113
    netmask 255.255.255.252

# Gendou - Asuka
auto eth3
iface eth3 inet static
    address 10.95.4.117
    netmask 255.255.255.252

# Gendou - Kaji
auto eth4
iface eth4 inet static
    address 10.95.4.121
    netmask 255.255.255.252

# Gendou - Misato
auto eth5
iface eth5 inet static
    address 10.95.4.125
    netmask 255.255.255.252

# Gendou - Hikari
auto eth6
iface eth6 inet static
    address 10.95.4.129
    netmask 255.255.255.252

# Gendou - Yui
auto eth7
iface eth7 inet static
    address 10.95.4.133
    netmask 255.255.255.252

# Gendou - Cmd
auto eth8
iface eth8 inet static
    address 10.95.4.105
    netmask 255.255.255.252
```

### Fuyutsuki

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.110
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.4.57
    netmask 255.255.255.248

auto eth2
iface eth2 inet static
    address 10.95.4.141
    netmask 255.255.255.252

auto eth3
iface eth3 inet static
    address 10.95.4.145
    netmask 255.255.255.252
```

### Shigeru

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.114
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.4.81
    netmask 255.255.255.248

auto eth2
iface eth2 inet static
    address 10.95.4.137
    netmask 255.255.255.252
```

### Asuka

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.118
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.4.97
    netmask 255.255.255.252

auto eth2
iface eth2 inet static
    address 10.95.4.149
    netmask 255.255.255.252

auto eth3
iface eth3 inet static
    address 10.95.4.153
    netmask 255.255.255.252
```

### Kaji

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.122
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.4.101
    netmask 255.255.255.252
```

### Misato

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.126
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.4.65
    netmask 255.255.255.248
```

### Hikari

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.130
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.2.1
    netmask 255.255.255.0

auto eth2
iface eth2 inet static
    address 10.95.4.157
    netmask 255.255.255.252
```

### Yui

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.134
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.4.161
    netmask 255.255.255.252

auto eth2
iface eth2 inet static
    address 10.95.4.165
    netmask 255.255.255.252

auto eth3
iface eth3 inet static
    address 10.95.4.169
    netmask 255.255.255.252

auto eth4
iface eth4 inet static
    address 10.95.3.1
    netmask 255.255.255.128
```

### Rei

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.162
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.0.1
    netmask 255.255.254.0
```

### Mari

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.166
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.4.33
    netmask 255.255.255.240
```

### Shinji

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.170
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.4.1
    netmask 255.255.255.224
```

### Kaworu

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.158
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.3.225
    netmask 255.255.255.224
```

### Kensuke

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.150
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.3.129
    netmask 255.255.255.192
```

### Ritsuko

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.154
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.4.49
    netmask 255.255.255.248
```

### Maya

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.142
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.3.193
    netmask 255.255.255.224
```

### Toji

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.146
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.4.73
    netmask 255.255.255.248
```

### Makoto

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.138
    netmask 255.255.255.252
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.4.89
    netmask 255.255.255.248
```

## Aktivasi IP Forwarding

IP forwarding merupakan fitur pada sistem operasi router yang memungkinkan paket diteruskan dari satu interface ke interface lainnya.

IP forwarding diaktifkan pada seluruh router menggunakan perintah:

```bash
sysctl -w net.ipv4.ip_forward=1
```

Untuk memastikan IP forwarding telah aktif, digunakan perintah:

```bash
cat /proc/sys/net/ipv4/ip_forward
```

Hasil pemeriksaan menunjukkan nilai `1` pada seluruh router.

Nilai tersebut menandakan bahwa router telah diizinkan untuk meneruskan paket IP dari satu interface ke interface lainnya.

Konfigurasi IP forwarding juga dimasukkan ke dalam bagian `up` pada `/etc/network/interfaces` agar dapat diaktifkan kembali ketika interface terkait dijalankan.

## Pengujian dan Verifikasi

Setelah seluruh konfigurasi diterapkan, dilakukan pemeriksaan alamat IP dan konektivitas pada setiap router.

### Pemeriksaan alamat IP interface

Perintah yang digunakan:

```bash
ip -br addr
```

Perintah tersebut menampilkan daftar interface beserta alamat IP dan status interface secara ringkas.

Contoh hasil pada Gendou:

<img width="463" height="142" alt="2- ip addr" src="https://github.com/user-attachments/assets/915f7c52-42a2-479f-a91a-8f8e34677432" />

Alamat DHCP pada eth0 dapat berbeda sesuai alamat yang diberikan oleh NAT1.

### Pengujian konektivitas antar-router

Pengujian konektivitas dilakukan menggunakan perintah:

```bash
ping -c 3 <IP-address-tujuan>
```

Pengujian dilakukan menggunakan perintah ping untuk memastikan setiap router dapat berkomunikasi dengan router yang terhubung langsung dengannya.

| No. | Link | IP yang diuji dari sisi pertama | IP yang diuji dari sisi kedua |
|---|---|---|---|
| 1 | Gendou–Fuyutsuki | 10.95.4.110 | 10.95.4.109 |
| 2 | Gendou–Shigeru | 10.95.4.114 | 10.95.4.113 |
| 3 | Gendou–Asuka | 10.95.4.118 | 10.95.4.117 |
| 4 | Gendou–Kaji | 10.95.4.122 | 10.95.4.121 |
| 5 | Gendou–Misato | 10.95.4.126 | 10.95.4.125 |
| 6 | Gendou–Hikari | 10.95.4.130 | 10.95.4.129 |
| 7 | Gendou–Yui | 10.95.4.134 | 10.95.4.133 |
| 8 | Shigeru–Makoto | 10.95.4.138 | 10.95.4.137 |
| 9 | Fuyutsuki–Maya | 10.95.4.142 | 10.95.4.141 |
| 10 | Fuyutsuki–Toji | 10.95.4.146 | 10.95.4.145 |
| 11 | Asuka–Kensuke | 10.95.4.150 | 10.95.4.149 |
| 12 | Asuka–Ritsuko | 10.95.4.154 | 10.95.4.153 |
| 13 | Hikari–Kaworu | 10.95.4.158 | 10.95.4.157 |
| 14 | Yui–Rei | 10.95.4.162 | 10.95.4.161 |
| 15 | Yui–Mari | 10.95.4.166 | 10.95.4.165 |
| 16 | Yui–Shinji | 10.95.4.170 | 10.95.4.169 |

Pengujian dilakukan dari kedua sisi router. Contoh pengujian pada link Gendou dan Fuyutsuki:

Dari Gendou:

```bash
ping -c 3 10.95.4.110
```

Dari Fuyutsuki:

```bash
ping -c 3 10.95.4.109
```

Pola pengujian yang sama diterapkan pada seluruh link antar-router.

# Soal 3

Pada tugas ketiga, dilakukan konfigurasi static routing untuk menghubungkan seluruh subnet pada topologi jaringan yang telah dibuat menggunakan GNS3.

Pada konfigurasi sebelumnya, setiap router dan subnet telah memiliki alamat IP masing-masing, tetapi komunikasi antar-subnet belum sepenuhnya terhubung. Oleh karena itu, diperlukan konfigurasi routing agar paket dapat diteruskan dari satu jaringan menuju jaringan lainnya.

Metode yang digunakan adalah static routing. Gendou bertindak sebagai router utama, sedangkan router lainnya menjadi router cabang yang meneruskan paket menuju subnet di bawahnya.

Konfigurasi juga menerapkan default route untuk mengurangi jumlah entri routing serta route summarization untuk menggabungkan beberapa subnet yang berurutan dan dapat direpresentasikan menggunakan satu CIDR.

Tujuan pelaksanaan tugas ini adalah:

1. Menghubungkan seluruh subnet menggunakan static routing.
2. Menerapkan sistem routing secara bertingkat dari Gendou menuju router cabang.
3. Menggunakan default route untuk meminimalkan jumlah routing pada router cabang.
4. Menerapkan route summarization pada subnet yang dapat digabungkan menjadi satu CIDR.
5. Mengaktifkan IP forwarding pada seluruh router.
6. Memberikan IP sementara dan gateway pada node pengujian.
7. Membuktikan konektivitas antar-subnet melalui pengujian ping dari Armisael menuju Lilith, Sachiel, dan Comm-Net.

## Hubungan antar-router

| Router induk | Router cabang | IP induk | IP cabang |
|---|---|---|---|
| Gendou | Fuyutsuki | 10.95.4.109 | 10.95.4.110 |
| Gendou | Shigeru | 10.95.4.113 | 10.95.4.114 |
| Gendou | Asuka | 10.95.4.117 | 10.95.4.118 |
| Gendou | Kaji | 10.95.4.121 | 10.95.4.122 |
| Gendou | Misato | 10.95.4.125 | 10.95.4.126 |
| Gendou | Hikari | 10.95.4.129 | 10.95.4.130 |
| Gendou | Yui | 10.95.4.133 | 10.95.4.134 |
| Fuyutsuki | Maya | 10.95.4.141 | 10.95.4.142 |
| Fuyutsuki | Toji | 10.95.4.145 | 10.95.4.146 |
| Shigeru | Makoto | 10.95.4.137 | 10.95.4.138 |
| Asuka | Kensuke | 10.95.4.149 | 10.95.4.150 |
| Asuka | Ritsuko | 10.95.4.153 | 10.95.4.154 |
| Hikari | Kaworu | 10.95.4.157 | 10.95.4.158 |
| Yui | Rei | 10.95.4.161 | 10.95.4.162 |
| Yui | Mari | 10.95.4.165 | 10.95.4.166 |
| Yui | Shinji | 10.95.4.169 | 10.95.4.170 |

## Hubungan router dengan subnet LAN

| Router | Interface LAN | IP gateway | Subnet |
|---|---|---|---|
| Gendou | eth8 | 10.95.4.105 | Cmd |
| Fuyutsuki | eth1 | 10.95.4.57 | Terminal |
| Maya | eth1 | 10.95.3.193 | Medic |
| Toji | eth1 | 10.95.4.73 | Dogma |
| Shigeru | eth1 | 10.95.4.81 | Monolith |
| Makoto | eth1 | 10.95.4.89 | Radar |
| Asuka | eth1 | 10.95.4.97 | Archive |
| Kensuke | eth1 | 10.95.3.129 | Sachiel |
| Ritsuko | eth1 | 10.95.4.49 | Lab |
| Kaji | eth1 | 10.95.4.101 | Intel |
| Misato | eth1 | 10.95.4.65 | Cage |
| Hikari | eth1 | 10.95.2.1 | Comm-Net |
| Kaworu | eth1 | 10.95.3.225 | Relay |
| Yui | eth4 | 10.95.3.1 | Hangar-Crew |
| Rei | eth1 | 10.95.0.1 | Quarters |
| Mari | eth1 | 10.95.4.33 | Dock-Crew |
| Shinji | eth1 | 10.95.4.1 | Garden-Staff |

## Konsep dan Mekanisme Static Routing

Static routing merupakan metode routing dengan memasukkan jalur tujuan secara manual ke dalam routing table setiap router.

Gendou memiliki peran sebagai pusat jaringan. Router ini memiliki koneksi menuju NAT1 dan seluruh router tingkat pertama.

Gendou menggunakan DHCP pada interface eth0 untuk memperoleh alamat IP dan default gateway dari NAT1.

Untuk mencapai subnet di bawah router cabang, Gendou memiliki static route yang mengarah ke IP router tingkat pertama terkait.

Router cabang menggunakan default route yang mengarah ke router induknya.

Sebagai contoh, Fuyutsuki menggunakan default route menuju Gendou dengan alamat IP 10.95.4.109.

Dengan konfigurasi tersebut, apabila Fuyutsuki menerima paket yang tujuan jaringannya tidak terdapat dalam routing table secara langsung, paket akan diteruskan menuju Gendou.

Router yang memiliki router cabang harus mempunyai static route menuju subnet yang berada di bawah router tersebut.

Sebagai contoh, Fuyutsuki memiliki static route menuju jaringan Medic melalui Maya dan jaringan Dogma melalui Toji.

Sementara itu, jaringan Terminal tidak memerlukan static route karena terhubung langsung dengan interface eth1 Fuyutsuki.

## Konfigurasi Router

IP forwarding diaktifkan menggunakan:

```bash
up sysctl -w net.ipv4.ip_forward=1
```

Default route dan static route dikonfigurasi menggunakan `up ip route replace`.

Perintah `replace` digunakan agar route dapat ditambahkan atau diperbarui tanpa menghasilkan entri route duplikat.

### Gendou

Gendou merupakan router utama yang menghubungkan jaringan internal dengan NAT1.

**Konfigurasi alamat interface:**

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | DHCP | Koneksi NAT1 |
| eth1 | 10.95.4.109/30 | Fuyutsuki |
| eth2 | 10.95.4.113/30 | Shigeru |
| eth3 | 10.95.4.117/30 | Asuka |
| eth4 | 10.95.4.121/30 | Kaji |
| eth5 | 10.95.4.125/30 | Misato |
| eth6 | 10.95.4.129/30 | Hikari |
| eth7 | 10.95.4.133/30 | Yui |
| eth8 | 10.95.4.105/30 | Cmd |

**Konfigurasi IP forwarding dan routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1

# Fuyutsuki branch
up ip route replace 10.95.4.56/29 via 10.95.4.110
up ip route replace 10.95.3.192/27 via 10.95.4.110
up ip route replace 10.95.4.72/29 via 10.95.4.110

# Shigeru branch
up ip route replace 10.95.4.80/28 via 10.95.4.114

# Asuka branch
up ip route replace 10.95.4.96/30 via 10.95.4.118
up ip route replace 10.95.3.128/26 via 10.95.4.118
up ip route replace 10.95.4.48/29 via 10.95.4.118

# Kaji branch
up ip route replace 10.95.4.100/30 via 10.95.4.122

# Misato branch
up ip route replace 10.95.4.64/29 via 10.95.4.126

# Hikari branch
up ip route replace 10.95.2.0/24 via 10.95.4.130
up ip route replace 10.95.3.224/27 via 10.95.4.130

# Yui branch
up ip route replace 10.95.0.0/23 via 10.95.4.134
up ip route replace 10.95.4.32/28 via 10.95.4.134
up ip route replace 10.95.4.0/27 via 10.95.4.134
up ip route replace 10.95.3.0/25 via 10.95.4.134
```

Default route Gendou diperoleh melalui DHCP pada eth0, sehingga tidak perlu menambahkan default route manual selama DHCP telah memberikan gateway NAT1.

### Fuyutsuki

Fuyutsuki terhubung langsung dengan Gendou, Maya, Toji, dan subnet Terminal.

**Konfigurasi alamat interface:**

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.110/30 | Gendou |
| eth1 | 10.95.4.57/29 | Terminal |
| eth2 | 10.95.4.141/30 | Maya |
| eth3 | 10.95.4.145/30 | Toji |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1

# Default route menuju Gendou
up ip route replace default via 10.95.4.109

# Medic melalui Maya
up ip route replace 10.95.3.192/27 via 10.95.4.142

# Dogma melalui Toji
up ip route replace 10.95.4.72/29 via 10.95.4.146
```

Subnet Terminal tidak memerlukan static route karena terhubung langsung dengan Fuyutsuki.

### Shigeru

Shigeru terhubung dengan Gendou, Makoto, dan subnet Monolith.

**Konfigurasi alamat interface:**

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.114/30 | Gendou |
| eth1 | 10.95.4.81/29 | Monolith |
| eth2 | 10.95.4.137/30 | Makoto |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1

# Default route menuju Gendou
up ip route replace default via 10.95.4.113

# Radar melalui Makoto
up ip route replace 10.95.4.88/29 via 10.95.4.138
```

### Asuka

Asuka terhubung dengan Gendou, Kensuke, Ritsuko, dan subnet Archive.

**Konfigurasi alamat interface:**

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.118/30 | Gendou |
| eth1 | 10.95.4.97/30 | Archive |
| eth2 | 10.95.4.149/30 | Kensuke |
| eth3 | 10.95.4.153/30 | Ritsuko |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1

# Default route menuju Gendou
up ip route replace default via 10.95.4.117

# Sachiel melalui Kensuke
up ip route replace 10.95.3.128/26 via 10.95.4.150

# Lab melalui Ritsuko
up ip route replace 10.95.4.48/29 via 10.95.4.154
```

### Kaji

Kaji terhubung dengan Gendou dan subnet Intel.

**Konfigurasi alamat interface:**

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.122/30 | Gendou |
| eth1 | 10.95.4.101/30 | Intel |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1

# Default route menuju Gendou
up ip route replace default via 10.95.4.121
```

Subnet Intel sudah terhubung langsung dengan Kaji sehingga tidak memerlukan static route tambahan.

### Misato

Misato terhubung dengan Gendou dan subnet Cage.

**Konfigurasi alamat interface:**

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.126/30 | Gendou |
| eth1 | 10.95.4.65/29 | Cage |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1

# Default route menuju Gendou
up ip route replace default via 10.95.4.125
```

Subnet Cage sudah terhubung langsung dengan Misato.

### Hikari

Hikari terhubung dengan Gendou, Kaworu, dan subnet Comm-Net.

**Konfigurasi alamat interface:**

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.130/30 | Gendou |
| eth1 | 10.95.2.1/24 | Comm-Net |
| eth2 | 10.95.4.157/30 | Kaworu |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1

# Default route menuju Gendou
up ip route replace default via 10.95.4.129

# Relay melalui Kaworu
up ip route replace 10.95.3.224/27 via 10.95.4.158
```

### Yui

Yui terhubung dengan Gendou, Rei, Mari, Shinji, dan subnet Hangar-Crew.

**Konfigurasi alamat interface:**

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.134/30 | Gendou |
| eth1 | 10.95.4.161/30 | Rei |
| eth2 | 10.95.4.165/30 | Mari |
| eth3 | 10.95.4.169/30 | Shinji |
| eth4 | 10.95.3.1/25 | Hangar-Crew |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1

# Default route menuju Gendou
up ip route replace default via 10.95.4.133

# Quarters melalui Rei
up ip route replace 10.95.0.0/23 via 10.95.4.162

# Dock-Crew melalui Mari
up ip route replace 10.95.4.32/28 via 10.95.4.166

# Garden-Staff melalui Shinji
up ip route replace 10.95.4.0/27 via 10.95.4.170
```

Subnet Hangar-Crew terhubung langsung dengan Yui.

### Rei

Rei terhubung dengan Yui dan subnet Quarters.

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.162/30 | Yui |
| eth1 | 10.95.0.1/23 | Quarters |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1
up ip route replace default via 10.95.4.161
```

### Mari

Mari terhubung dengan Yui dan subnet Dock-Crew.

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.166/30 | Yui |
| eth1 | 10.95.4.33/28 | Dock-Crew |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1
up ip route replace default via 10.95.4.165
```

### Shinji

Shinji terhubung dengan Yui dan subnet Garden-Staff.

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.170/30 | Yui |
| eth1 | 10.95.4.1/27 | Garden-Staff |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1
up ip route replace default via 10.95.4.169
```

### Kaworu

Kaworu terhubung dengan Hikari dan subnet Relay.

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.158/30 | Hikari |
| eth1 | 10.95.3.225/27 | Relay |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1
up ip route replace default via 10.95.4.157
```

### Kensuke

Kensuke terhubung dengan Asuka dan subnet Sachiel.

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.150/30 | Asuka |
| eth1 | 10.95.3.129/26 | Sachiel |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1
up ip route replace default via 10.95.4.149
```

### Ritsuko

Ritsuko terhubung dengan Asuka dan subnet Lab.

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.154/30 | Asuka |
| eth1 | 10.95.4.49/29 | Lab |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1
up ip route replace default via 10.95.4.153
```

### Maya

Maya terhubung dengan Fuyutsuki dan subnet Medic.

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.142/30 | Fuyutsuki |
| eth1 | 10.95.3.193/27 | Medic |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1
up ip route replace default via 10.95.4.141
```

### Toji

Toji terhubung dengan Fuyutsuki dan subnet Dogma.

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.146/30 | Fuyutsuki |
| eth1 | 10.95.4.73/29 | Dogma |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1
up ip route replace default via 10.95.4.145
```

### Makoto

Makoto terhubung dengan Shigeru dan subnet Radar.

| Interface | Alamat IP | Keterangan |
|---|---|---|
| eth0 | 10.95.4.138/30 | Shigeru |
| eth1 | 10.95.4.89/29 | Radar |

**Konfigurasi routing:**

```bash
up sysctl -w net.ipv4.ip_forward=1
up ip route replace default via 10.95.4.137
```

## Konfigurasi IP Sementara pada Node Pengujian

Sesuai ketentuan tugas, setiap node pengujian diberikan alamat IP dan gateway sementara. Konfigurasi ini digunakan untuk menguji komunikasi antar-subnet sebelum penerapan konfigurasi IP permanen pada tugas berikutnya.

### Daftar IP dan gateway node

| Node | Alamat IP | Prefix | Gateway |
|---|---|---|---|
| Quarters | 10.95.0.2 | /23 | 10.95.0.1 |
| Dock-Crew | 10.95.4.34 | /28 | 10.95.4.33 |
| Garden-Staff | 10.95.4.2 | /27 | 10.95.4.1 |
| Hangar-Crew | 10.95.3.2 | /25 | 10.95.3.1 |
| Relay-Node | 10.95.3.226 | /27 | 10.95.3.225 |
| Comm-Net | 10.95.2.2 | /24 | 10.95.2.1 |
| Tokyo3-Core | 10.95.4.106 | /30 | 10.95.4.105 |
| Magi-Casper | 10.95.4.58 | /29 | 10.95.4.57 |
| Magi-Balthasar | 10.95.4.59 | /29 | 10.95.4.57 |
| Magi-Melchior | 10.95.4.60 | /29 | 10.95.4.57 |
| Pen-Pen | 10.95.3.194 | /27 | 10.95.3.193 |
| Medic-Bay | 10.95.3.195 | /27 | 10.95.3.193 |
| Adam | 10.95.4.75 | /29 | 10.95.4.73 |
| Lilith | 10.95.4.74 | /29 | 10.95.4.73 |
| Zeruel | 10.95.4.82 | /29 | 10.95.4.81 |
| Armisael | 10.95.4.83 | /29 | 10.95.4.81 |
| Radar-Array | 10.95.4.90 | /29 | 10.95.4.89 |
| Archive-Vault | 10.95.4.98 | /30 | 10.95.4.97 |
| Spy | 10.95.4.102 | /30 | 10.95.4.101 |
| Entry-Plug | 10.95.4.50 | /29 | 10.95.4.49 |
| Dummy-Plug | 10.95.4.51 | /29 | 10.95.4.49 |
| Unit-01 | 10.95.4.66 | /29 | 10.95.4.65 |
| Unit-02 | 10.95.4.67 | /29 | 10.95.4.65 |
| Unit-00 | 10.95.4.68 | /29 | 10.95.4.65 |
| Sachiel | 10.95.3.130 | /26 | 10.95.3.129 |

### Contoh konfigurasi IP sementara

Konfigurasi dilakukan pada interface `eth0` node pengujian.

Contoh konfigurasi Armisael:

```bash
auto eth0
iface eth0 inet static
    address 10.95.4.83
    netmask 255.255.255.248
    gateway 10.95.4.81
```

Contoh konfigurasi Lilith:

```bash
auto eth0
iface eth0 inet static
    address 10.95.4.74
    netmask 255.255.255.248
    gateway 10.95.4.73
```

Contoh konfigurasi Sachiel:

```bash
auto eth0
iface eth0 inet static
    address 10.95.3.130
    netmask 255.255.255.192
    gateway 10.95.3.129
```

Contoh konfigurasi Comm-Net:

```bash
auto eth0
iface eth0 inet static
    address 10.95.2.2
    netmask 255.255.255.0
    gateway 10.95.2.1
```

Node lainnya menggunakan pola konfigurasi yang sama dengan alamat IP, netmask, dan gateway sesuai tabel.

## Verifikasi Konfigurasi

Setelah konfigurasi routing diterapkan, dilakukan pemeriksaan untuk memastikan setiap router memiliki jalur yang sesuai.

### Memeriksa alamat IP interface

Perintah:

```bash
ip -br addr
```

Perintah ini digunakan untuk menampilkan alamat IP setiap interface secara ringkas.

### Memeriksa routing table

Perintah:

```bash
ip route
```

Perintah ini digunakan untuk memeriksa default route, static route, serta jaringan yang terhubung langsung.

### Memeriksa IP forwarding

Perintah:

```bash
sysctl net.ipv4.ip_forward
```

Hasil yang diharapkan:

```text
net.ipv4.ip_forward = 1
```

Nilai `1` menunjukkan bahwa IP forwarding sudah aktif sehingga router dapat meneruskan paket dari satu interface ke interface lainnya.

## Route Summarization

Route summarization merupakan teknik penggabungan beberapa jaringan menjadi satu entri routing apabila alamat jaringan tersebut berurutan dan memenuhi batasan CIDR.

Pada konfigurasi ini, Gendou memiliki dua route menuju jaringan yang berada di bawah Shigeru:

```text
10.95.4.80/29
10.95.4.88/29
```

Kedua subnet tersebut dapat digabung menjadi:

```text
10.95.4.80/28
```

Dengan demikian, konfigurasi yang digunakan adalah:

```bash
up ip route replace 10.95.4.80/28 via 10.95.4.114
```

Teknik ini mengurangi jumlah entri routing pada Gendou tanpa memasukkan subnet lain yang tidak termasuk dalam cabang tersebut.

## Pengujian Konektivitas End-to-End

Pengujian utama dilakukan dari node Armisael. Pengujian ini bertujuan membuktikan bahwa paket dapat melewati beberapa router dan mencapai subnet yang berbeda.

### Pengujian Armisael menuju Lilith

Alamat tujuan:

```text
10.95.4.74
```

Perintah:

```bash
ping -c 4 10.95.4.74
```

Jalur yang dilalui:

Armisael → Toji → Fuyutsuki → Gendou → Asuka → Ritsuko → Lilith.

### Pengujian Armisael menuju Sachiel

Alamat tujuan:

```text
10.95.3.130
```

Perintah:

```bash
ping -c 4 10.95.3.130
```

Jalur yang dilalui:

Armisael → Toji → Fuyutsuki → Gendou → Asuka → Kensuke → Sachiel.

### Pengujian Armisael menuju Comm-Net

Alamat tujuan:

```text
10.95.2.2
```

Perintah:

```bash
ping -c 4 10.95.2.2
```

Jalur yang dilalui:

Armisael → Toji → Fuyutsuki → Gendou → Hikari → Comm-Net.

### Hasil pengujian

<img width="449" height="359" alt="3-pengujian" src="https://github.com/user-attachments/assets/309c3caa-27e6-45d0-9d0a-e59d303aedba" />

Pengujian dinyatakan berhasil apabila setiap node tujuan memberikan balasan ICMP dan tidak mengalami packet loss.

# Soal 4

Menghubungkan seluruh jaringan internal pada topologi GNS3 agar dapat mengakses internet melalui satu pintu keluar, yaitu router Gendo yang terhubung langsung dengan NAT1.

Konfigurasi dilakukan menggunakan NAT dengan metode MASQUERADE agar jaringan internal tetap dapat mengakses internet meskipun alamat IP yang diperoleh Gendo dari NAT1 berubah sewaktu-waktu.

Selain itu, konfigurasi juga memastikan bahwa:
1. Seluruh jaringan internal dapat mengakses internet melalui Gendo.
2. Alamat IP internal hanya diterjemahkan ketika paket keluar menuju NAT1.
3. Komunikasi antar-LAN tetap menggunakan alamat IP asli pengirim.
4. Node internal dapat melakukan resolusi nama domain menggunakan DNS.
5. Koneksi internet dapat dibuktikan melalui pengujian ping ke `8.8.8.8` dan `deb.debian.org` dari Armisael dan Lilith.

## Konsep dan Cara Kerja

Pada topologi jaringan ini, Gendo berperan sebagai gateway utama yang menghubungkan seluruh jaringan internal dengan internet melalui NAT1.

Gendo memperoleh alamat IP pada interface `eth0` secara otomatis menggunakan DHCP. Karena alamat IP tersebut dapat berubah, digunakan metode MASQUERADE pada tabel NAT.

MASQUERADE merupakan metode NAT yang secara otomatis menggunakan alamat IP dari interface keluar. Dengan demikian, konfigurasi NAT tidak perlu diubah ketika alamat IP yang diperoleh dari NAT1 berubah.

Alur komunikasi menuju internet:

1. Node internal mengirimkan paket menuju alamat internet.
2. Paket diteruskan melalui gateway masing-masing jaringan dan router cabang.
3. Paket sampai ke Gendo.
4. Gendo meneruskan paket melalui interface `eth0`.
5. Rule MASQUERADE mengubah alamat IP sumber dari jaringan internal menjadi alamat IP `eth0` Gendo.
6. Paket diteruskan menuju NAT1 dan internet.
7. Paket balasan diterima kembali oleh Gendo.
8. Gendo mengembalikan alamat tujuan ke alamat IP asli node internal melalui mekanisme connection tracking.

Sementara itu, komunikasi antar-LAN tidak mengalami translasi alamat karena rule NAT hanya berlaku untuk paket yang keluar melalui interface `eth0`.

## Konfigurasi Router Gendo

### Konfigurasi Interface

Isi konfigurasi:

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
    up sysctl -w net.ipv4.ip_forward=1

auto eth1
iface eth1 inet static
    address 10.95.4.109
    netmask 255.255.255.252

auto eth2
iface eth2 inet static
    address 10.95.4.113
    netmask 255.255.255.252

auto eth3
iface eth3 inet static
    address 10.95.4.117
    netmask 255.255.255.252

auto eth4
iface eth4 inet static
    address 10.95.4.121
    netmask 255.255.255.252

auto eth5
iface eth5 inet static
    address 10.95.4.125
    netmask 255.255.255.252

auto eth6
iface eth6 inet static
    address 10.95.4.129
    netmask 255.255.255.252

auto eth7
iface eth7 inet static
    address 10.95.4.133
    netmask 255.255.255.252

auto eth8
iface eth8 inet static
    address 10.95.4.105
    netmask 255.255.255.252

    up sysctl -w net.ipv4.ip_forward=1

    # Static Routing
    up ip route replace 10.95.4.56/29 via 10.95.4.110
    up ip route replace 10.95.3.192/27 via 10.95.4.110
    up ip route replace 10.95.4.72/29 via 10.95.4.110

    up ip route replace 10.95.4.80/28 via 10.95.4.114

    up ip route replace 10.95.4.96/30 via 10.95.4.118
    up ip route replace 10.95.3.128/26 via 10.95.4.118
    up ip route replace 10.95.4.48/29 via 10.95.4.118

    up ip route replace 10.95.4.100/30 via 10.95.4.122
    up ip route replace 10.95.4.64/29 via 10.95.4.126

    up ip route replace 10.95.2.0/24 via 10.95.4.130
    up ip route replace 10.95.3.224/27 via 10.95.4.130

    up ip route replace 10.95.0.0/23 via 10.95.4.134
    up ip route replace 10.95.4.32/28 via 10.95.4.134
    up ip route replace 10.95.4.0/27 via 10.95.4.134
    up ip route replace 10.95.3.0/25 via 10.95.4.134
```

Interface `eth0` menggunakan DHCP karena terhubung langsung dengan NAT1. Sementara itu, interface `eth1` sampai `eth8` menggunakan alamat IP statis sesuai pembagian subnet pada tugas sebelumnya.

### Mengaktifkan IP Forwarding

IP forwarding digunakan agar Gendo dapat meneruskan paket dari satu interface ke interface lainnya.

Perintah untuk mengaktifkan IP forwarding:

```bash
up sysctl -w net.ipv4.ip_forward=1
```

```bash
sysctl net.ipv4.ip_forward
```

Hasil pemeriksaan:

```text
net.ipv4.ip_forward = 1
```

Hasil tersebut menunjukkan bahwa IP forwarding pada Gendo telah aktif.

### Konfigurasi NAT MASQUERADE

Konfigurasi NAT dilakukan pada Gendo menggunakan iptables.

Pertama, tambahkan rule MASQUERADE:

```bash
up iptables -t nat -A POSTROUTING -s 10.95.0.0/16 -o eth0 -j MASQUERADE
```

Dengan aturan tersebut, alamat IP internal akan diterjemahkan menjadi alamat IP yang diperoleh Gendo dari NAT1 ketika paket keluar menuju internet.

### Konfigurasi IP Forwarding pada Firewall

Selain NAT, diperlukan aturan forwarding agar paket dari jaringan internal dapat diteruskan menuju internet dan paket balasan dapat kembali ke jaringan internal.

Mengizinkan paket dari jaringan internal menuju internet:

```bash
up iptables -A FORWARD -s 10.95.0.0/16 -o eth0 -j ACCEPT
```

Mengizinkan paket balasan dari internet:

```bash
up iptables -A FORWARD -i eth0 -d 10.95.0.0/16 -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

```

Mengizinkan komunikasi antar-LAN:

```bash
up iptables -A FORWARD -s 10.95.0.0/16 -d 10.95.0.0/16 -j ACCEPT
```

Aturan terakhir digunakan agar komunikasi antar-LAN tetap berjalan tanpa mengubah alamat IP asli pengirim.

Dengan demikian, NAT hanya diterapkan pada paket yang keluar melalui interface `eth0`, sedangkan paket antar-LAN tidak mengalami translasi alamat.

## Konfigurasi DNS pada Node Internal

Agar node internal dapat mengakses alamat menggunakan nama domain, diperlukan konfigurasi DNS resolver.

Konfigurasi dilakukan pada node yang membutuhkan akses internet dan akan melakukan instalasi paket, termasuk Armisael dan Lilith.

File konfigurasi DNS berada di:

```bash
nano /etc/resolv.conf
```

Konfigurasi DNS:

```bash
nameserver 1.1.1.1
nameserver 8.8.8.8
```

Penjelasan:
- `1.1.1.1` merupakan DNS resolver Cloudflare.
- `8.8.8.8` merupakan DNS resolver Google.

DNS digunakan untuk menerjemahkan nama domain menjadi alamat IP sehingga node dapat mengakses layanan internet menggunakan nama domain.

## Pengujian Koneksi Internet

Pengujian dilakukan menggunakan dua node, yaitu Armisael dan Lilith. Pengujian mencakup koneksi internet menggunakan alamat IP publik dan resolusi nama domain.

### Pengujian dari Armisael

Pengujian koneksi ke internet menggunakan alamat IP publik:

```bash
ping -c 4 8.8.8.8
```

Pengujian menunjukkan bahwa Armisael berhasil berkomunikasi dengan alamat IP publik `8.8.8.8`.

Selanjutnya dilakukan pengujian resolusi nama domain:

```bash
ping -c 4 deb.debian.org
```

Setelah konfigurasi DNS diterapkan, pengujian berhasil. Hal tersebut menunjukkan bahwa Armisael telah dapat menerjemahkan nama domain menjadi alamat IP dan mengaksesnya melalui internet.

<img width="419" height="227" alt="4 - ping armisael" src="https://github.com/user-attachments/assets/37ddaa66-2053-4f93-bdda-b319dadb2833" />

### Pengujian dari Lilith

Pengujian koneksi ke internet:

```bash
ping -c 4 8.8.8.8
```

Pengujian resolusi nama domain:

```bash
ping -c 4 deb.debian.org
```

Kedua pengujian berhasil dilakukan. Hal tersebut menunjukkan bahwa Lilith dapat mengakses internet melalui jalur routing menuju Gendo.

<img width="444" height="225" alt="4 - ping lilith" src="https://github.com/user-attachments/assets/64078658-05eb-4ede-9822-2939a2aea7fd" />

## Pemeriksaan Counter Rule NAT

Pemeriksaan counter dilakukan pada Gendo untuk memastikan bahwa paket dari jaringan internal telah melewati aturan NAT MASQUERADE.

Perintah yang digunakan:

```bash
iptables -t nat -L POSTROUTING -n -v
```

Alternatif untuk menampilkan counter secara lebih detail:

```bash
iptables -t nat -nvxL POSTROUTING
```

<img width="512" height="138" alt="4 - iptables" src="https://github.com/user-attachments/assets/fc3d5e3f-ad35-4a9e-8b73-a026e93cf9ae" />

Nilai counter akan bertambah ketika paket dari jaringan internal melewati aturan NAT tersebut.

# Soal 5

Menerapkan keamanan jaringan pada router Gendo menggunakan firewall iptables. Gendo berperan sebagai gateway utama yang menghubungkan seluruh jaringan internal dengan NAT1 sebagai akses menuju internet.

Pada tugas ini, akses masuk ke Gendo dibatasi dengan mengubah policy INPUT dan FORWARD menjadi DROP. Meskipun demikian, beberapa jenis komunikasi tetap diizinkan agar jaringan tetap dapat beroperasi sebagaimana mestinya.

Konfigurasi firewall harus memenuhi beberapa ketentuan, yaitu:

1. Mengizinkan paket balasan dari koneksi yang sudah terbentuk.
2. Mengizinkan traffic dari jaringan internal menuju internet.
3. Mengizinkan komunikasi antar-LAN.
4. Mengizinkan node internal mengakses Gendo secara langsung.
5. Mengizinkan komunikasi melalui interface loopback.
6. Mengizinkan DHCP dari NAT1 agar Gendo tetap mendapatkan alamat IP secara otomatis.
7. Menolak koneksi baru yang berasal dari sisi NAT1.
8. Memastikan konfigurasi pada Tugas 2, 3, dan 4 tetap berjalan.

Seluruh konfigurasi firewall dibuat dalam satu file bernama `gendo.sh` agar lebih mudah dijalankan dan dikelola.

## Konsep dan Cara Kerja Firewall

Firewall merupakan mekanisme keamanan jaringan yang digunakan untuk mengatur paket data yang masuk, keluar, maupun melewati sebuah perangkat.

Pada tugas ini digunakan iptables dengan dua policy utama, yaitu INPUT dan FORWARD.

### INPUT

Chain INPUT digunakan untuk mengatur paket yang ditujukan langsung kepada router Gendo.

Policy INPUT diubah menjadi DROP:

```bash
iptables -P INPUT DROP
```

Artinya, seluruh paket yang masuk menuju Gendo akan ditolak secara default, kecuali paket yang secara khusus diizinkan melalui rule firewall.

Dengan demikian, koneksi baru dari sisi NAT1 tidak dapat masuk secara bebas ke Gendo.

### FORWARD

Chain FORWARD digunakan untuk mengatur paket yang melewati Gendo menuju jaringan lain.

Policy FORWARD diubah menjadi DROP:

```bash
iptables -P FORWARD DROP
```

Artinya, paket yang melewati Gendo akan ditolak secara default kecuali terdapat aturan yang mengizinkannya.

Beberapa pengecualian dibuat agar komunikasi internal, akses internet, dan paket balasan tetap dapat berjalan.

### OUTPUT

Chain OUTPUT digunakan untuk mengatur paket yang dikirimkan langsung oleh Gendo.

Policy OUTPUT tetap menggunakan ACCEPT:

```bash
iptables -P OUTPUT ACCEPT
```

Dengan demikian, Gendo tetap dapat mengirim paket keluar, misalnya untuk melakukan komunikasi dengan NAT1 dan layanan internet.

## Konfigurasi Firewall pada Gendo

### Membuat File gendo.sh

Seluruh konfigurasi firewall disimpan dalam satu file bernama `gendo.sh`.

File dibuat menggunakan perintah:

```bash
nano /root/gendo.sh
```

Kemudian dimasukkan konfigurasi berikut:

### 4.2 Isi Lengkap gendo.sh

```bash
#!/bin/bash

# ==========================================
# FIREWALL GENDO - TUGAS 5
# ==========================================

# Mengaktifkan IP forwarding
sysctl -w net.ipv4.ip_forward=1

# ==========================================
# 1. MEMBERSIHKAN RULE FIREWALL SEBELUMNYA
# ==========================================

iptables -F
iptables -X

# ==========================================
# 2. MENGATUR DEFAULT POLICY
# ==========================================

iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

# ==========================================
# 3. RULE INPUT
# ==========================================

# Mengizinkan loopback
iptables -A INPUT -i lo -j ACCEPT

# Mengizinkan balasan koneksi yang sudah ada
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# Mengizinkan balasan DHCP dari NAT1
iptables -A INPUT -i eth0 -p udp --sport 67 --dport 68 -j ACCEPT

# Mengizinkan node internal mengakses Gendo
iptables -A INPUT -s 10.95.0.0/16 ! -i eth0 -j ACCEPT

# ==========================================
# 4. RULE FORWARD
# ==========================================

# Mengizinkan balasan koneksi yang sudah ada
iptables -A FORWARD -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# Mengizinkan komunikasi antar-LAN
iptables -A FORWARD -s 10.95.0.0/16 -d 10.95.0.0/16 -j ACCEPT

# Mengizinkan jaringan internal menuju internet
iptables -A FORWARD -s 10.95.0.0/16 -o eth0 -j ACCEPT

# ==========================================
# 5. RULE NAT MASQUERADE
# ==========================================

# Menghapus rule MASQUERADE lama yang sama agar tidak duplikat
while iptables -t nat -C POSTROUTING \
-s 10.95.0.0/16 -o eth0 -j MASQUERADE 2>/dev/null
do
    iptables -t nat -D POSTROUTING \
    -s 10.95.0.0/16 -o eth0 -j MASQUERADE
done

# Menambahkan NAT MASQUERADE
iptables -t nat -A POSTROUTING \
-s 10.95.0.0/16 -o eth0 -j MASQUERADE

echo "Konfigurasi firewall Gendo berhasil diterapkan."
```

### Memberikan Izin Eksekusi

Setelah file dibuat, diberikan izin agar file dapat dijalankan sebagai script.

Perintah:

```bash
chmod +x /root/gendo.sh
```

Kemudian script dijalankan menggunakan:

```bash
bash /root/gendo.sh
```

Jika berhasil, akan muncul pesan:

```text
net.ipv4.ip_forward = 1
Konfigurasi firewall Gendo berhasil diterapkan.
```

<img width="309" height="59" alt="5 - bash gendo" src="https://github.com/user-attachments/assets/513359bb-e706-485c-8b25-6cc072fde5b7" />

Pesan tersebut menunjukkan bahwa IP forwarding telah diaktifkan dan konfigurasi firewall berhasil dijalankan.

## Penjelasan Setiap Rule Firewall

### Mengaktifkan IP Forwarding

```bash
sysctl -w net.ipv4.ip_forward=1
```

Perintah ini mengaktifkan kemampuan Gendo untuk meneruskan paket IPv4 dari satu interface ke interface lainnya.

IP forwarding diperlukan karena Gendo berperan sebagai router utama yang menghubungkan seluruh jaringan internal dengan internet.

### Membersihkan Rule Sebelumnya

```bash
iptables -F
iptables -X
```

Perintah `iptables -F` digunakan untuk menghapus seluruh rule pada chain tabel filter.

Perintah `iptables -X` digunakan untuk menghapus chain tambahan yang tidak lagi digunakan.

Langkah ini dilakukan agar aturan firewall yang diterapkan tidak bercampur dengan aturan filter sebelumnya.

Rule pada tabel NAT tidak dihapus menggunakan perintah tersebut, sehingga konfigurasi NAT dapat dipertahankan dan dikelola secara terpisah.

### Mengatur Default Policy

```bash
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT
```

Pengaturan ini menjadikan INPUT dan FORWARD menggunakan kebijakan DROP secara default.

Dengan demikian, paket yang tidak sesuai dengan aturan yang diizinkan akan ditolak.

Sementara itu, OUTPUT tetap ACCEPT agar Gendo tetap dapat mengirim paket keluar.

### Mengizinkan Loopback

```bash
iptables -A INPUT -i lo -j ACCEPT
```

Loopback merupakan interface internal perangkat yang menggunakan alamat `127.0.0.1`.

Rule ini diperlukan agar proses komunikasi internal pada Gendo tetap berjalan.

### Mengizinkan Balasan Koneksi

```bash
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

Rule ini mengizinkan paket yang merupakan bagian dari koneksi yang sudah terbentuk maupun paket yang berhubungan dengan koneksi tersebut.

Pada chain FORWARD juga diterapkan aturan yang sama:

```bash
iptables -A FORWARD -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

Aturan tersebut memungkinkan paket balasan dari internet diteruskan kembali menuju jaringan internal.

Dengan demikian, koneksi yang dimulai dari jaringan internal tetap dapat menerima respons dari internet meskipun policy INPUT dan FORWARD menggunakan DROP.

### Mengizinkan DHCP dari NAT1

```bash
iptables -A INPUT -i eth0 -p udp --sport 67 --dport 68 -j ACCEPT
```

Rule ini mengizinkan paket balasan DHCP dari NAT1 menuju Gendo melalui interface `eth0`.

DHCP menggunakan UDP port 67 pada server dan UDP port 68 pada client.

Aturan ini diperlukan karena Gendo mendapatkan alamat IP secara otomatis dari NAT1.

Tanpa aturan tersebut, proses penerimaan alamat IP DHCP dapat terganggu akibat policy INPUT DROP.

### Mengizinkan Jaringan Internal Mengakses Gendo

```bash
iptables -A INPUT -s 10.95.0.0/16 ! -i eth0 -j ACCEPT
```

Rule ini mengizinkan paket yang berasal dari prefix internal `10.95.0.0/16` dan masuk melalui interface selain `eth0`.

Dengan demikian, node internal dapat berkomunikasi langsung dengan Gendo.

Contohnya adalah ketika node internal melakukan ping ke alamat interface Gendo atau mengakses layanan yang berjalan pada Gendo.

### Mengizinkan Komunikasi Antar-LAN

```bash
iptables -A FORWARD -s 10.95.0.0/16 -d 10.95.0.0/16 -j ACCEPT
```

Rule ini mengizinkan komunikasi antarjaringan internal yang menggunakan prefix `10.95.0.0/16`.

Dengan adanya aturan ini, paket dari satu LAN dapat diteruskan menuju LAN lainnya melalui Gendo.

Komunikasi tersebut tidak mengalami translasi alamat karena NAT hanya diterapkan pada paket yang keluar melalui interface `eth0`.

### Mengizinkan Jaringan Internal Mengakses Internet

```bash
iptables -A FORWARD -s 10.95.0.0/16 -o eth0 -j ACCEPT
```

Rule ini mengizinkan paket yang berasal dari jaringan internal untuk diteruskan keluar melalui interface `eth0` menuju NAT1.

Aturan ini mempertahankan fungsi akses internet yang telah dibuat pada Tugas 4.

### Mempertahankan NAT MASQUERADE

```bash
iptables -t nat -A POSTROUTING \
-s 10.95.0.0/16 -o eth0 -j MASQUERADE
```

Rule ini mempertahankan konfigurasi NAT dari Tugas 4.

MASQUERADE mengubah alamat IP sumber dari jaringan internal menjadi alamat IP yang digunakan Gendo pada interface `eth0`.

Penggunaan MASQUERADE memungkinkan konfigurasi tetap berfungsi ketika alamat IP dari NAT1 berubah.

Sebelum menambahkan rule baru, script memeriksa dan menghapus rule MASQUERADE yang identik agar tidak terjadi duplikasi.

## Pengujian Konfigurasi

Setelah script `gendo.sh` dijalankan, dilakukan beberapa pengujian untuk memastikan firewall berfungsi dan konfigurasi Tugas 2 sampai 4 tetap berjalan.

### Memeriksa Alamat IP Gendo

Perintah:

```bash
ip -br addr
```

<img width="449" height="138" alt="5 - ip addr" src="https://github.com/user-attachments/assets/0cc185b5-b5dd-48d9-84a1-2dcdd37748e9" />

Pemeriksaan dilakukan untuk memastikan seluruh interface Gendo masih memiliki alamat IP sesuai konfigurasi sebelumnya.

Interface `eth0` harus memperoleh alamat IP melalui DHCP NAT1, sedangkan interface internal menggunakan alamat IP statis.

Alamat IP NAT1 yang digunakan pada saat pengujian adalah:

```text
192.168.122.124/24
```

### Memeriksa Default Route

Perintah:

```bash
ip route
```

<img width="440" height="306" alt="5 - ip route" src="https://github.com/user-attachments/assets/94ea86b9-eb85-4907-afbd-a59b94c9883f" />

Hasil tersebut menunjukkan bahwa Gendo masih memiliki jalur keluar menuju NAT1.

Static route menuju seluruh jaringan internal juga harus tetap tersedia.

### Memeriksa IP Forwarding

Perintah:

```bash
sysctl net.ipv4.ip_forward
```

<img width="274" height="29" alt="5 - sysctl" src="https://github.com/user-attachments/assets/d017ac44-2b37-40e6-890a-b4dbb562cfd3" />

Hasil tersebut menunjukkan bahwa IP forwarding tetap aktif sehingga Gendo dapat meneruskan paket antarjaringan.

### Memeriksa Policy dan Rule Firewall

Untuk menampilkan seluruh rule pada tabel filter digunakan:

```bash
iptables -S
```

<img width="401" height="130" alt="5 - -s" src="https://github.com/user-attachments/assets/2b6d6ba9-75c4-431d-865a-204a3eb264b2" />

Hasil tersebut digunakan untuk membuktikan bahwa policy INPUT dan FORWARD telah diubah menjadi DROP, sementara traffic yang diperlukan tetap diizinkan.

### Memeriksa Rule NAT

Untuk memastikan NAT dari Tugas 4 tetap berjalan, digunakan perintah:

```bash
iptables -t nat -S
```

<img width="354" height="75" alt="5 - -t" src="https://github.com/user-attachments/assets/8274da9a-342c-4a83-bc31-163215fb2fee" />

Dengan adanya rule tersebut, paket dari jaringan internal yang keluar melalui Gendo tetap dapat diterjemahkan alamatnya ketika menuju internet.

### Pengujian Ping Internet dari Armisael

Armisael digunakan sebagai salah satu node pengujian untuk memastikan akses internet dari jaringan internal tetap berjalan setelah firewall diterapkan.

Konfigurasi Armisael:

- IP Address: `10.95.4.83/29`
- Gateway: `10.95.4.81`

Perintah pengujian:

```bash
ping -c 4 8.8.8.8
```

Hasil pengujian menunjukkan bahwa Armisael berhasil menerima balasan dari alamat IP publik `8.8.8.8`.

<img width="398" height="118" alt="5 - ping 8" src="https://github.com/user-attachments/assets/c6305dcf-d161-45ae-ba05-dc73e12d38ec" />

Keberhasilan tersebut menunjukkan bahwa:

1. Paket dari Armisael dapat melewati router Shigeru dan Gendo.
2. Gendo mengizinkan paket internal menuju internet.
3. NAT MASQUERADE tetap berjalan.
4. Paket balasan dari internet dapat diteruskan kembali menuju Armisael.

Dengan demikian, firewall tidak menghalangi koneksi internet yang dimulai dari jaringan internal.

### Pengujian Komunikasi Antar-LAN

Untuk memastikan komunikasi antar-LAN tetap berjalan, pengujian dapat dilakukan dari Armisael menuju node internal lainnya.

Pengujian menuju Lilith:

```bash
ping -c 4 10.95.4.74
```

Pengujian menuju Sachiel:

```bash
ping -c 4 10.95.3.130
```

Pengujian menuju Comm-Net:

```bash
ping -c 4 10.95.2.2
```

<img width="424" height="339" alt="5 - ping" src="https://github.com/user-attachments/assets/a5f52585-2cdc-4fbd-9eb9-cfc05b9d5c36" />

Pengujian ini digunakan untuk memastikan bahwa rule FORWARD antar-LAN tetap mengizinkan komunikasi antara jaringan internal yang berbeda.

### Pengujian Resolusi DNS

Untuk memastikan DNS dari Tugas 4 tetap berjalan, dilakukan pengujian:

```bash
ping -c 4 deb.debian.org
```

<img width="440" height="125" alt="5 - ping deb" src="https://github.com/user-attachments/assets/679a69e1-a28a-4a01-8004-12b2b786a1e7" />

Keberhasilan pengujian menunjukkan bahwa node internal tetap dapat melakukan resolusi nama domain dan mengakses alamat tersebut melalui internet.

# Soal 6

Tugas ini bertujuan untuk memberikan alamat IP statis dan default gateway kepada seluruh node non-router pada topologi jaringan GNS3. Sebelumnya, jaringan sudah berhasil dibangun dan komunikasi antar-router telah berjalan. Namun, perangkat client dan server belum memiliki konfigurasi alamat jaringan permanen.

Oleh karena itu, konfigurasi dilakukan agar setiap node memiliki identitas alamat IP sendiri dan dapat berkomunikasi dengan perangkat lain, baik dalam satu jaringan maupun jaringan yang berbeda.

Adapun tujuan pengerjaan tugas ini adalah:

1. Memberikan IP address statis kepada seluruh node non-router.
2. Memberikan default gateway sesuai dengan subnet masing-masing.
3. Menggunakan alamat IP berdasarkan pembagian VLSM dan glosarium.
4. Menyimpan konfigurasi agar tetap tersedia setelah perangkat di-restart.
5. Melakukan pengujian alamat IP dan konektivitas gateway pada Unit-01.

# Dasar Konfigurasi

Konfigurasi menggunakan pembagian alamat IP dari tugas VLSM sebelumnya dengan prefix jaringan utama `10.95.0.0/16`.

Setiap node non-router menggunakan interface `eth0` untuk terhubung ke switch pada jaringan masing-masing.

Setiap konfigurasi juga diawali dengan konfigurasi loopback:

```bash
auto lo
iface lo inet loopback
```

Interface loopback merupakan interface internal yang digunakan sistem untuk komunikasi dengan dirinya sendiri.

## Daftar IP Address dan Default Gateway

Seluruh node non-router diberikan alamat IP sesuai subnet masing-masing.

| No. | Node | IP Address | Prefix | Default Gateway |
|---:|---|---|---:|---|
| 1 | Quarters | 10.95.0.2 | /23 | 10.95.0.1 |
| 2 | Comm-Net | 10.95.2.2 | /24 | 10.95.2.1 |
| 3 | Hangar-Crew | 10.95.3.2 | /25 | 10.95.3.1 |
| 4 | Sachiel | 10.95.3.130 | /26 | 10.95.3.129 |
| 5 | Pen-Pen | 10.95.3.194 | /27 | 10.95.3.193 |
| 6 | Medic-Bay | 10.95.3.195 | /27 | 10.95.3.193 |
| 7 | Relay-Node | 10.95.3.226 | /27 | 10.95.3.225 |
| 8 | Garden-Staff | 10.95.4.2 | /27 | 10.95.4.1 |
| 9 | Dock-Crew | 10.95.4.34 | /28 | 10.95.4.33 |
| 10 | Tokyo3-Core | 10.95.4.106 | /30 | 10.95.4.105 |
| 11 | Magi-Casper | 10.95.4.58 | /29 | 10.95.4.57 |
| 12 | Magi-Balthasar | 10.95.4.59 | /29 | 10.95.4.57 |
| 13 | Magi-Melchior | 10.95.4.60 | /29 | 10.95.4.57 |
| 14 | Entry-Plug | 10.95.4.50 | /29 | 10.95.4.49 |
| 15 | Dummy-Plug | 10.95.4.51 | /29 | 10.95.4.49 |
| 16 | Unit-01 | 10.95.4.66 | /29 | 10.95.4.65 |
| 17 | Unit-02 | 10.95.4.67 | /29 | 10.95.4.65 |
| 18 | Unit-00 | 10.95.4.68 | /29 | 10.95.4.65 |
| 19 | Adam | 10.95.4.75 | /29 | 10.95.4.73 |
| 20 | Lilith | 10.95.4.74 | /29 | 10.95.4.73 |
| 21 | Zeruel | 10.95.4.82 | /29 | 10.95.4.81 |
| 22 | Armisael | 10.95.4.83 | /29 | 10.95.4.81 |
| 23 | Radar-Array | 10.95.4.90 | /29 | 10.95.4.89 |
| 24 | Archive-Vault | 10.95.4.98 | /30 | 10.95.4.97 |
| 25 | Spy | 10.95.4.102 | /30 | 10.95.4.101 |

Jumlah keseluruhan perangkat yang dikonfigurasi adalah **25 node non-router**.

## Implementasi Konfigurasi IP Statis

Berikut konfigurasi lengkap masing-masing node.

### Quarters

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.0.2
    netmask 255.255.254.0
    gateway 10.95.0.1
```

### Comm-Net

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.2.2
    netmask 255.255.255.0
    gateway 10.95.2.1
```

### Hangar-Crew

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.3.2
    netmask 255.255.255.128
    gateway 10.95.3.1
```

### Sachiel

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.3.130
    netmask 255.255.255.192
    gateway 10.95.3.129
```

### Pen-Pen

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.3.194
    netmask 255.255.255.224
    gateway 10.95.3.193
```

### Medic-Bay

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.3.195
    netmask 255.255.255.224
    gateway 10.95.3.193
```

### Relay-Node

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.3.226
    netmask 255.255.255.224
    gateway 10.95.3.225
```

### Garden-Staff

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.2
    netmask 255.255.255.224
    gateway 10.95.4.1
```

### Dock-Crew

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.34
    netmask 255.255.255.240
    gateway 10.95.4.33
```

### Tokyo3-Core

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.106
    netmask 255.255.255.252
    gateway 10.95.4.105
```

### Magi-Casper

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.58
    netmask 255.255.255.248
    gateway 10.95.4.57
```

### Magi-Balthasar

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.59
    netmask 255.255.255.248
    gateway 10.95.4.57
```

### Magi-Melchior

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.60
    netmask 255.255.255.248
    gateway 10.95.4.57
```

### Entry-Plug

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.50
    netmask 255.255.255.248
    gateway 10.95.4.49
```

### Dummy-Plug

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.51
    netmask 255.255.255.248
    gateway 10.95.4.49
```

### Unit-01

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.66
    netmask 255.255.255.248
    gateway 10.95.4.65
```

### Unit-02

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.67
    netmask 255.255.255.248
    gateway 10.95.4.65
```

### Unit-00

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.68
    netmask 255.255.255.248
    gateway 10.95.4.65
```

### Adam

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.75
    netmask 255.255.255.248
    gateway 10.95.4.73
```

### Lilith

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.74
    netmask 255.255.255.248
    gateway 10.95.4.73
```

### Zeruel

```bash
auto lo
iface lo inet static

auto eth0
iface eth0 inet static
    address 10.95.4.82
    netmask 255.255.255.248
    gateway 10.95.4.81
```

### Armisael

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.83
    netmask 255.255.255.248
    gateway 10.95.4.81
```

### Radar-Array

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.90
    netmask 255.255.255.248
    gateway 10.95.4.89
```

### Archive-Vault

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.98
    netmask 255.255.255.252
    gateway 10.95.4.97
```

### Spy

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 10.95.4.102
    netmask 255.255.255.252
    gateway 10.95.4.101
```

## Pengujian Konfigurasi

Pengujian dilakukan untuk memastikan setiap perangkat telah memiliki alamat IP dan gateway sesuai dengan subnet masing-masing.

### Pemeriksaan IP Address

Perintah yang digunakan:

```bash
ip -br addr
```

Perintah tersebut digunakan untuk menampilkan seluruh interface jaringan beserta alamat IP yang terpasang dalam format ringkas.

Pada Unit-01, hasil yang diperoleh adalah:

<img width="446" height="92" alt="6 - ip addr" src="https://github.com/user-attachments/assets/2356073b-f65c-4411-a8b6-4900631cda18" />

Berdasarkan hasil tersebut, interface `eth0` pada Unit-01 telah memiliki alamat IP `10.95.4.66/29`, sesuai dengan konfigurasi yang ditentukan.

### Pemeriksaan Default Gateway

Perintah yang digunakan:

```bash
ip route
```

Hasil pada Unit-01:

<img width="397" height="70" alt="6 - ip route" src="https://github.com/user-attachments/assets/ac8ea61b-08e7-43e8-929d-31210747a0e5" />

Hasil tersebut menunjukkan bahwa default gateway Unit-01 telah diarahkan ke `10.95.4.65` melalui interface `eth0`.

Alamat tersebut merupakan alamat interface router Misato yang menjadi gateway untuk jaringan Unit.

### Pengujian Ping Gateway Unit-01

Pengujian konektivitas dilakukan menggunakan perintah:

```bash
ping -c 4 10.95.4.65
```

Hasil pengujian:

<img width="448" height="137" alt="6 - ping" src="https://github.com/user-attachments/assets/7c6a8103-8a9c-423f-9312-001887b80754" />

Hasil tersebut menunjukkan bahwa seluruh paket ICMP berhasil diterima oleh gateway. Tidak terdapat packet loss selama pengujian.

Dengan demikian, Unit-01 telah berhasil berkomunikasi dengan gateway pada jaringan yang sama.

### Pengujian Persistensi Setelah Restart

Pengujian persistensi dilakukan dengan me-restart node melalui GNS3.

Setelah perangkat dinyalakan kembali, pemeriksaan dilakukan menggunakan:

```bash
ip -br addr
ip route
ping -c 4 10.95.4.65
```

<img width="478" height="245" alt="6 - restart" src="https://github.com/user-attachments/assets/67524025-9877-48ef-beb3-e60f279c5038" />

Hasil pemeriksaan menunjukkan bahwa konfigurasi IP address dan default gateway tetap tersedia setelah restart.

# Soal 7

Bertujuan mengaktifkan tiga node MAGI, yaitu
Magi-Casper, Magi-Balthasar, dan Magi-Melchior, agar dapat menerima
pesan melalui layanan TCP menggunakan Netcat.

Pekerjaan yang dilakukan meliputi:

1.  Memasang paket `iptables` dan `netcat-traditional` pada ketiga node
    MAGI.
2.  Membuat script instalasi pada direktori `/root/`.
3.  Menjalankan listener TCP sesuai port pada glosarium.
4.  Mengirim pesan dari node Lilith menuju ketiga MAGI.
5.  Mengirim pesan khusus ke port TCP 5001 milik Magi-Balthasar.
6.  Memeriksa pesan yang diterima pada masing-masing node.

## Topologi dan Informasi IP

Ketiga node MAGI berada pada jaringan Terminal yang terhubung melalui
Switch-Terminal. Lilith berada pada jaringan lain dan mengirimkan pesan
melalui konfigurasi routing yang telah dibuat pada tahap sebelumnya.

| Node | IP Address | Prefix | Gateway | Port TCP |
|---|---|---|---|---|
| Magi-Casper | `10.95.4.58` | `/29` | `10.95.4.57` | 5000 |
| Magi-Balthasar | `10.95.4.59` | `/29` | `10.95.4.57` | 5000, 5001 |
| Magi-Melchior | `10.95.4.60` | `/29` | `10.95.4.57` | 5000 |
| Lilith | `10.95.4.74` | `/29` | `10.95.4.73` | - |

Alamat jaringan Terminal adalah `10.95.4.56/29`, dengan gateway
`10.95.4.57`. Berdasarkan glosarium, setiap MAGI menggunakan port TCP
5000, sedangkan Balthasar juga menyediakan port TCP 5001.

## Persiapan pada Setiap Node MAGI

Langkah ini dilakukan secara terpisah pada Magi-Casper, Magi-Balthasar,
dan Magi-Melchior.

### Memeriksa konfigurasi jaringan

Jalankan perintah berikut:

``` bash
ip -br addr
ip route
```

Pastikan alamat `eth0` sesuai dengan IP masing-masing node dan default
gateway mengarah ke `10.95.4.57`.

<img width="486" height="110" alt="7 - ip casper" src="https://github.com/user-attachments/assets/24a72641-9c13-4026-9cc4-626f3035921d" />

<img width="524" height="109" alt="7 - ip balthasar" src="https://github.com/user-attachments/assets/5278d0f8-9441-4b0c-8cb3-3368169a34b5" />

<img width="554" height="109" alt="7 - ip melchior" src="https://github.com/user-attachments/assets/8ef2e4d6-e0dc-4306-876f-c677ce6ca1b2" />

### Memeriksa DNS

DNS diatur menggunakan:

``` bash
printf "nameserver 1.1.1.1\nnameserver 8.8.8.8\n" > /etc/resolv.conf
```

Periksa resolusi DNS:

``` bash
ping -c 3 deb.debian.org
```

<img width="431" height="114" alt="7 - ping casper" src="https://github.com/user-attachments/assets/e88742eb-1a18-4352-9c5c-823296030c49" />

<img width="453" height="113" alt="7 - ping balthasar" src="https://github.com/user-attachments/assets/e48805f8-3e00-49f7-9a04-268d0b38e455" />

<img width="464" height="107" alt="7 - ping melchior" src="https://github.com/user-attachments/assets/6f3f8488-26ec-44fd-8895-a729b6570a25" />


Jika nama domain berhasil di resolve, proses pengambilan daftar paket
dapat dilanjutkan.

## Membuat Script Instalasi

Sesuai instruksi soal, instalasi dilakukan melalui script pada direktori
`/root/`. Setiap node memiliki script masing-masing.

### Script Magi-Casper

Pada Magi-Casper, buat file:

``` bash
nano /root/casper.sh
```

Isi file:

``` bash
#!/bin/bash

apt-get update
apt-get install -y iptables netcat-traditional

iptables -F
iptables -P INPUT ACCEPT
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT

echo "Magi-Casper siap menerima koneksi."
```

Simpan file, kemudian berikan izin eksekusi dan jalankan:

``` bash
chmod +x /root/casper.sh
/root/casper.sh
```

<img width="945" height="371" alt="7 - script casper" src="https://github.com/user-attachments/assets/b165750b-c7c1-4f2d-922f-1c182749c8dd" />

### Script Magi-Balthasar

Pada Magi-Balthasar, buat file:

``` bash
nano /root/balthasar.sh
```

Isi file:

``` bash
#!/bin/bash

apt-get update
apt-get install -y iptables netcat-traditional

iptables -F
iptables -P INPUT ACCEPT
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT

echo "Magi-Balthasar siap menerima koneksi."
```

Simpan, lalu jalankan:

``` bash
chmod +x /root/balthasar.sh
/root/balthasar.sh
```

<img width="951" height="371" alt="7 - script balthasar" src="https://github.com/user-attachments/assets/8271ef1f-e478-4440-bfe1-fa432d964332" />

### Script Magi-Melchior

Pada Magi-Melchior, buat file:

``` bash
nano /root/melchior.sh
```

Isi file:

``` bash
#!/bin/bash

apt-get update
apt-get install -y iptables netcat-traditional

iptables -F
iptables -P INPUT ACCEPT
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT

echo "Magi-Melchior siap menerima koneksi."
```

Simpan, lalu jalankan:

``` bash
chmod +x /root/melchior.sh
/root/melchior.sh
```

<img width="947" height="371" alt="7 - script melchior" src="https://github.com/user-attachments/assets/d82f3193-a744-4197-99d0-66f53783126a" />

### Penjelasan perintah pada script

| Perintah | Fungsi |
|---|---|
| `#!/bin/bash` | Menentukan interpreter Bash untuk menjalankan script. |
| `apt-get update` | Memperbarui daftar paket dari repository. |
| `apt-get install -y iptables netcat-traditional` | Memasang iptables dan netcat-traditional. |
| `iptables -F` | Menghapus seluruh aturan pada tabel filter. |
| `iptables -P INPUT ACCEPT` | Mengatur kebijakan INPUT menjadi ACCEPT. |
| `iptables -P OUTPUT ACCEPT` | Mengatur kebijakan OUTPUT menjadi ACCEPT. |
| `iptables -P FORWARD ACCEPT` | Mengatur kebijakan FORWARD menjadi ACCEPT. |
| `chmod +x` | Memberikan izin eksekusi pada file script. |

Kebijakan ACCEPT digunakan karena pada tahap ini MAGI diminta untuk
melayani koneksi terlebih dahulu dan pengamanan akan dibahas pada tahap
berikutnya. Perintah `iptables -F` menghapus aturan filter yang sudah
ada pada node tersebut, sehingga penggunaannya perlu dibatasi pada node
MAGI sesuai instruksi praktikum.

### Memastikan paket telah terpasang

Pada masing-masing node, jalankan:

``` bash
dpkg -l iptables netcat-traditional
```

Paket yang berhasil terpasang ditandai dengan status `ii` pada awal
baris.

<img width="623" height="101" alt="7 - paket casper" src="https://github.com/user-attachments/assets/9ee0f98f-49fd-4790-a1da-83e70857db45" />

<img width="602" height="99" alt="7 - paket balthasar" src="https://github.com/user-attachments/assets/95cbd944-752a-48f0-bb25-27a17446c79c" />

<img width="604" height="98" alt="7 - paket melchior" src="https://github.com/user-attachments/assets/15f6d959-e17c-4993-bb5c-d7b1834f3911" />

## Mengaktifkan Listener TCP

Setelah paket terpasang, setiap MAGI dijalankan sebagai server TCP
menggunakan Netcat. Pesan yang diterima diarahkan ke file log agar dapat
diperiksa setelah pengiriman.

### Listener Magi-Casper

Pada terminal Magi-Casper:

``` bash
nc -l -p 5000 > /tmp/casper.log &
nc.traditional -l -p 5000 > /tmp/casper.log &
```

Periksa apakah port 5000 sedang mendengarkan:

``` bash
ss -lntp
```

Port TCP `5000` harus terlihat dalam status `LISTEN`.

<img width="897" height="99" alt="7 - listen casper" src="https://github.com/user-attachments/assets/d05c9583-0d6c-42c3-ad13-6c38dfe98600" />

### Listener Magi-Balthasar

Magi-Balthasar harus membuka dua listener karena glosarium menetapkan
dua port, yaitu 5000 dan 5001.

Jalankan:

``` bash
nc -l -p 5000 > /tmp/balthasar-5000.log &
nc -l -p 5001 > /tmp/balthasar-5001.log &

nc.traditional -l -p 5000 > /tmp/balthasar-5000.log &
nc.traditional -l -p 5001 > /tmp/balthasar-5001.log &
```

Periksa:

``` bash
ss -lntp
```

Pastikan port `5000` dan `5001` sama-sama muncul dalam status `LISTEN`.

<img width="923" height="167" alt="7 - listen balthasar" src="https://github.com/user-attachments/assets/233eab84-8f57-4d5b-a1da-efb17101d399" />

### Listener Magi-Melchior

Pada terminal Magi-Melchior:

``` bash
nc -l -p 5000 > /tmp/melchior.log &

nc.traditional -l -p 5000 > /tmp/melchior.log &
```

Periksa:

``` bash
ss -lntp
```

Pastikan port `5000` muncul dalam status `LISTEN`.

<img width="590" height="126" alt="7 - listen melchior" src="https://github.com/user-attachments/assets/558ba594-2993-4396-92fa-81629c3b4748" />

### Penjelasan perintah listener

| Perintah | Fungsi |
|---|---|
| `nc.traditional` | Menjalankan implementasi Netcat Traditional. |
| `-l` | Menjalankan Netcat dalam mode listen/server. |
| `-p 5000` | Menentukan port TCP yang digunakan. |
| `> /tmp/nama.log` | Mengarahkan pesan yang diterima ke file log. |
| `&` | Menjalankan proses di background. |
| `ss -lntp` | Menampilkan socket TCP yang sedang listen beserta informasi prosesnya. |

Listener yang digunakan menerima satu koneksi, kemudian prosesnya berhenti. Oleh karena itu, listener harus dijalankan kembali sebelum pengujian pengiriman berikutnya jika proses sebelumnya sudah selesai.

## Mengirim Pesan dari Lilith

Setelah listener aktif, pengiriman pesan dilakukan dari node Lilith.

Pengiriman pesan menggunakan Netcat Traditional dengan perintah `nc.traditional`.

### Catatan instalasi Netcat Traditional pada Lilith

Instalasi  paket `netcat-traditional` pada Lilith menggunakan:

``` bash
printf "nameserver 1.1.1.1\nnameserver 8.8.8.8\n" > /etc/resolv.conf
```

```bash
apt-get update
apt-get install -y netcat-traditional
```

### Mengirim pesan ke Magi-Casper

```bash
echo "Halo MAGI Casper, pesan dari Lilith!" | nc.traditional -w 3 10.95.4.58 5000
```

Tujuan:
- IP tujuan: `10.95.4.58`
- Port TCP: `5000`

### Mengirim pesan ke Magi-Balthasar port 5000

```bash
echo "Halo MAGI Balthasar port 5000, pesan dari Lilith!" | nc.traditional -w 3 10.95.4.59 5000
```

Tujuan:
- IP tujuan: `10.95.4.59`
- Port TCP: `5000`

### Mengirim pesan ke Magi-Balthasar port 5001

```bash
echo "Halo MAGI Balthasar port 5001, pesan dari Lilith!" | nc.traditional -w 3 10.95.4.59 5001
```

Tujuan:
- IP tujuan: `10.95.4.59`
- Port TCP: `5001`

Pengujian port 5001 wajib dilakukan karena soal secara khusus meminta pengiriman pesan ke port tersebut.

### Mengirim pesan ke Magi-Melchior

```bash
echo "Halo MAGI Melchior, pesan dari Lilith!" | nc.traditional -w 3 10.95.4.60 5000
```

Tujuan:
- IP tujuan: `10.95.4.60`
- Port TCP: `5000`

Opsi `-w 3` digunakan untuk memberikan batas waktu tiga detik pada proses komunikasi.

## Memeriksa Pesan yang Diterima

Setelah pengiriman pesan dilakukan, file log diperiksa pada masing-masing node MAGI.

### Memeriksa Magi-Casper

Pada Magi-Casper:

```bash
cat /tmp/casper.log
```

<img width="457" height="68" alt="7 - pesan casper" src="https://github.com/user-attachments/assets/6fb67830-9190-4ccf-b7f0-0bcdfb285660" />

### Memeriksa Magi-Balthasar port 5000

Pada Magi-Balthasar:

```bash
cat /tmp/balthasar-5000.log
```

<img width="362" height="26" alt="7 - pesan balthasar 5000" src="https://github.com/user-attachments/assets/31db3fad-f1a8-4058-ab0c-4ed61b44a53c" />

### Memeriksa Magi-Balthasar port 5001

Masih pada Magi-Balthasar:

```bash
cat /tmp/balthasar-5001.log
```

<img width="332" height="29" alt="7 - pesan balthasar 5001" src="https://github.com/user-attachments/assets/abcdd4e4-0c73-4bbd-9fed-d37be3aa9431" />

### Memeriksa Magi-Melchior

Pada Magi-Melchior:

```bash
cat /tmp/melchior.log
```

<img width="502" height="39" alt="7 - pesan melchior" src="https://github.com/user-attachments/assets/0c51a01e-e863-4177-a1de-33613a9bccba" />


# Soal 8

Dilakukan konfigurasi layanan TCP pada dua node, yaitu Pen-Pen dan Tokyo3-Core. Kedua node harus dapat memberikan respons tertentu ketika menerima koneksi dari Lilith.

Tujuan pengerjaan ini adalah:
1. Mengaktifkan layanan TCP pada port 80 di Pen-Pen.
2. Mengaktifkan layanan TCP pada port 80 dan 8080 di Tokyo3-Core.
3. Memastikan setiap port memberikan respons sesuai ketentuan soal.
4. Menguji koneksi dari Lilith menggunakan Netcat (`nc`).
5. Memastikan port yang tidak memiliki layanan, seperti port 22, langsung menolak koneksi dan tidak menggantung.

## Topologi dan Informasi IP Address

Pengujian dilakukan menggunakan tiga node, yaitu Pen-Pen, Tokyo3-Core, dan Lilith.

| Node | IP Address | Gateway | Fungsi |
|---|---|---|---|
| Pen-Pen | 10.95.3.194/27 | 10.95.3.193 | Server port 80 |
| Tokyo3-Core | 10.95.4.106/30 | 10.95.4.105 | Server port 80 dan 8080 |
| Lilith | 10.95.4.74/29 | 10.95.4.73 | Client untuk pengujian |

## Ketentuan Layanan

Layanan TCP yang harus dijalankan adalah sebagai berikut.

| Node | Port TCP | Respons |
|---|---:|---|
| Pen-Pen | 80 | Welcome to Pen-Pen |
| Tokyo3-Core | 80 | Welcome to Tokyo3-Core |
| Tokyo3-Core | 8080 | syifa imutz |

Selain itu, port 22 digunakan sebagai contoh port yang tidak memiliki layanan. Koneksi ke port tersebut harus langsung gagal.

## Konfigurasi Pen-Pen

### Pemeriksaan hostname dan Netcat

Pertama, dilakukan pemeriksaan hostname dan ketersediaan perintah Netcat pada Pen-Pen.

Perintah:

```bash
hostname
command -v nc.traditional
command -v nc
```

Hasil pemeriksaan:

<img width="272" height="59" alt="8 - hostname pen" src="https://github.com/user-attachments/assets/21752668-5f35-44d4-8325-f1a47dc5c8e8" />

Berdasarkan hasil tersebut, hostname Pen-Pen sudah sesuai. Perintah `nc.traditional` tidak tersedia, tetapi Netcat biasa tersedia pada `/usr/bin/nc`. Oleh karena itu, layanan dijalankan menggunakan `nc`.

### Membuat script layanan

Dibuat file `/root/penpen.sh` untuk menjalankan layanan TCP pada port 80.

Perintah:

```bash
cat > /root/penpen.sh <<'EOF'
#!/bin/bash
while true; do
    printf "Welcome to Pen-Pen\n" | nc -l -p 80
done
EOF
```

Penjelasan:
- `#!/bin/bash` menentukan interpreter yang digunakan.
- `while true` membuat layanan berjalan terus-menerus.
- `printf` menyiapkan pesan respons.
- `nc -l -p 80` membuat Netcat mendengarkan koneksi TCP pada port 80.
- Setelah satu koneksi selesai, perulangan menjalankan listener kembali.

### Menjalankan layanan

Script diberikan izin eksekusi dan dijalankan di background.

```bash
chmod +x /root/penpen.sh
nohup /root/penpen.sh > /tmp/penpen-service.log 2>&1 &
```

<img width="360" height="39" alt="8 - layanan pen" src="https://github.com/user-attachments/assets/d68d7cb7-33e1-4eec-92c9-cfcbae5d1f96" />

Keterangan:
- `chmod +x` memberikan izin eksekusi.
- `nohup` menjalankan proses agar tetap berjalan setelah terminal ditutup.
- `&` menjalankan proses di background.
- Output dan error diarahkan ke `/tmp/penpen-service.log`.

### Memeriksa listener

Perintah:

```bash
ss -lntp | grep ':80'
```

<img width="490" height="36" alt="8 - listen pen" src="https://github.com/user-attachments/assets/ff2a91d4-4e94-43ff-b7e2-79fbcd1705d8" />

Hasil tersebut menunjukkan bahwa Pen-Pen sudah mendengarkan koneksi TCP pada port 80.

## Konfigurasi Tokyo3-Core

### Pemeriksaan hostname dan Netcat

Pemeriksaan dilakukan untuk memastikan hostname dan ketersediaan Netcat.

Perintah:

```bash
hostname
command -v nc.traditional
command -v nc
```

<img width="190" height="56" alt="8 - hostname tokyo" src="https://github.com/user-attachments/assets/9e05475d-86b9-475d-920a-a035490da79f" />

Berdasarkan hasil tersebut, hostname sudah sesuai dan Netcat biasa tersedia pada `/usr/bin/nc`. Dengan demikian, layanan dijalankan menggunakan `nc`.

### Membuat script layanan

Dibuat file `/root/tokyo3.sh` untuk menjalankan dua layanan sekaligus, yaitu port 80 dan 8080.

Perintah:

```bash
cat > /root/tokyo3.sh <<'EOF'
#!/bin/bash

while true; do
    printf "Welcome to Tokyo3-Core\n" | nc -l -p 80
done &

while true; do
    printf "syifa imutz\n" | nc -l -p 8080
done &

wait
EOF
```

Penjelasan:
- Perulangan pertama menjalankan listener TCP pada port 80.
- Respons yang diberikan adalah `Welcome to Tokyo3-Core`.
- Perulangan kedua menjalankan listener TCP pada port 8080.
- Respons yang diberikan adalah `syifa imutz`.
- `&` membuat kedua layanan berjalan secara paralel.
- `wait` menjaga proses utama tetap berjalan selama kedua layanan aktif.

### Menjalankan layanan

Perintah:

```bash
chmod +x /root/tokyo3.sh
nohup /root/tokyo3.sh > /tmp/tokyo3-service.log 2>&1 &
```

<img width="349" height="40" alt="8 - layanan tokyo" src="https://github.com/user-attachments/assets/a622f608-ef0d-43b3-b7b8-7d3dd567afdb" />

Script dijalankan di background agar kedua layanan dapat terus menerima koneksi.

### Memeriksa listener

Perintah:

```bash
ss -lntp | grep -E ':80|:8080'
```

<img width="506" height="63" alt="8 - listen tokyo" src="https://github.com/user-attachments/assets/aa4918bb-afaa-4bc1-9047-d6ce1a4ef2e0" />

Hasil tersebut membuktikan bahwa Tokyo3-Core sudah mendengarkan koneksi TCP pada port 80 dan 8080.


## Pengujian Koneksi dari Lilith

Setelah seluruh layanan aktif, dilakukan pengujian dari node Lilith menggunakan Netcat.

### Pengujian Pen-Pen port 80

Perintah:

```bash
echo | nc -w 3 10.95.3.194 80
```

<img width="292" height="24" alt="8 - tes pen" src="https://github.com/user-attachments/assets/288aeb8a-3a1f-4cc2-a00c-4441258341ac" />

Lilith berhasil terhubung ke Pen-Pen pada port 80. Pen-Pen memberikan respons `Welcome to Pen-Pen` sesuai ketentuan soal.

### Pengujian Tokyo3-Core port 80

Perintah:

```bash
echo | nc -w 3 10.95.4.106 80
```

<img width="284" height="29" alt="8 - tes tokyo 80" src="https://github.com/user-attachments/assets/548e235b-cc02-4e39-b5a4-6d54e9cf486e" />

Lilith berhasil terhubung ke Tokyo3-Core pada port 80. Respons yang diterima sesuai dengan hostname server.

### Pengujian Tokyo3-Core port 8080

Perintah:

```bash
echo | nc -w 3 10.95.4.106 8080
```

<img width="296" height="26" alt="8 - tes tokyo 8080" src="https://github.com/user-attachments/assets/7631f5ad-20d9-4371-abc1-6a8f535f0e08" />

Lilith berhasil terhubung ke Tokyo3-Core pada port 8080 dan menerima pesan `syifa imutz` sesuai ketentuan soal.

## Pengujian Port yang Tidak Dilayani

Selain menguji port yang aktif, dilakukan pengujian terhadap port 22 pada Pen-Pen dan Tokyo3-Core.

Pengujian ini bertujuan memastikan bahwa port yang tidak memiliki layanan langsung menolak koneksi dan tidak membuat client menunggu terlalu lama.

### Pengujian Pen-Pen port 22

Perintah:

```bash
nc -zvw2 10.95.3.194 22
```

<img width="409" height="26" alt="8 - tes pen 22" src="https://github.com/user-attachments/assets/b348e86d-9579-4d9c-83e0-6e92ab0da380" />

Koneksi ke port 22 Pen-Pen langsung ditolak karena tidak ada layanan yang mendengarkan pada port tersebut.

### Pengujian Tokyo3-Core port 22

Perintah:

```bash
nc -zvw2 10.95.4.106 22
```

<img width="410" height="27" alt="8 - tes tokyo 22" src="https://github.com/user-attachments/assets/ebbf7220-f774-4753-9692-d67266b660d5" />

Koneksi ke port 22 Tokyo3-Core juga langsung ditolak. Hal ini menunjukkan bahwa port tersebut tidak menyediakan layanan TCP.

# Soal 9

Pada tugas Nomor 9 dilakukan simulasi sabotase routing pada router Shigeru menggunakan script `break_routing.sh`.

Sabotase menyebabkan Lilith tidak dapat berkomunikasi dengan Armisael, meskipun Armisael masih dapat melakukan ping ke gatewaynya sendiri.

Tujuan pengerjaan ini adalah:

1. Menjalankan script sabotase `break_routing.sh` pada router Shigeru.
2. Mengidentifikasi seluruh perubahan konfigurasi yang menyebabkan gangguan routing.
3. Memperbaiki konfigurasi IP forwarding, routing table, dan policy routing.
4. Mengembalikan jalur komunikasi antarjaringan.
5. Membuktikan bahwa Lilith dapat melakukan ping ke Armisael setelah perbaikan.

## Informasi Topologi dan IP Address

Pengujian melibatkan tiga node utama, yaitu Shigeru, Lilith, dan Armisael.

| Node | IP Address | Gateway | Keterangan |
|---|---|---|---|
| Shigeru eth0 | 10.95.4.114/30 | 10.95.4.113 | Link menuju Gendo |
| Shigeru eth1 | 10.95.4.81/29 | - | Jaringan Monolith |
| Shigeru eth2 | 10.95.4.137/30 | - | Link menuju Makoto |
| Lilith | 10.95.4.74/29 | 10.95.4.73 | Client pengujian |
| Armisael | 10.95.4.83/29 | 10.95.4.81 | Host di jaringan Monolith |

Hubungan jaringan:

- Shigeru terhubung ke Gendo melalui `eth0`.
- Shigeru terhubung ke jaringan Monolith melalui `eth1`.
- Shigeru terhubung ke Makoto melalui `eth2`.
- Armisael berada di jaringan Monolith dan menggunakan Shigeru sebagai gateway.
- Lilith berada di jaringan Dogma dan mengakses Armisael melalui jaringan antarrouter.

## Kondisi Konfigurasi Sebelum Sabotase

Sebelum sabotase, konfigurasi Shigeru adalah sebagai berikut.

| Interface | IP Address | Fungsi |
|---|---|---|
| eth0 | 10.95.4.114/30 | Terhubung ke Gendo |
| eth1 | 10.95.4.81/29 | Jaringan Monolith |
| eth2 | 10.95.4.137/30 | Terhubung ke Makoto |

Konfigurasi routing normal Shigeru:

```bash
default via 10.95.4.113 dev eth0
10.95.4.80/29 dev eth1 proto kernel scope link src 10.95.4.81
10.95.4.88/29 via 10.95.4.138 dev eth2
```

IP forwarding seharusnya bernilai `1` agar Shigeru dapat meneruskan paket dari satu jaringan menuju jaringan lainnya.

## Pelaksanaan Script Sabotase

### Memastikan Node dan Hak Akses

Script sabotase hanya boleh dijalankan pada router Shigeru. Oleh karena itu, dilakukan pemeriksaan hostname dan hak akses root terlebih dahulu.

Perintah:

```bash
hostname
id -u
```

<img width="179" height="49" alt="9 - hostname" src="https://github.com/user-attachments/assets/b2170c65-e9b6-45b6-9b15-ae8eb1a3b587" />

- Hostname menunjukkan `Shigeru`, sesuai dengan node yang ditentukan.
- Nilai `id -u` adalah `0`, yang berarti perintah dijalankan menggunakan hak akses root.

### Menjalankan Script Sabotase

Script `break_routing.sh` dijalankan pada Shigeru.

Perintah:

```bash
chmod +x /root/break_routing.sh
sh /root/break_routing.sh
```

<img width="277" height="36" alt="9 - break" src="https://github.com/user-attachments/assets/47b061f7-b236-47aa-b278-31b6adef2802" />

Pesan tersebut menunjukkan bahwa script sabotase berhasil dijalankan.

## Identifikasi Kerusakan Setelah Sabotase

Setelah script berhasil dijalankan, dilakukan pemeriksaan terhadap interface, routing table, policy routing, dan IP forwarding.

### Memeriksa IP Address Interface

Perintah:

```bash
ip -br addr
```

<img width="461" height="77" alt="9 - ip addr after" src="https://github.com/user-attachments/assets/f9a00ded-d9b3-4387-b5b0-bdf53ebab7a1" />

IP address pada tiga interface utama Shigeru masih sesuai dengan konfigurasi awal. Tidak ditemukan perubahan alamat IP pada `eth0`, `eth1`, maupun `eth2`.

Dengan demikian, kerusakan utama bukan berasal dari perubahan IP address interface.

### Memeriksa Routing Table

Perintah:

```bash
ip route
```

<img width="439" height="86" alt="9 - ip route after" src="https://github.com/user-attachments/assets/0998e211-bcbd-4c6a-b79b-015dd9a358b3" />

Ditemukan dua kerusakan pada routing table.

**Kerusakan pertama: Default gateway diubah.**

Sebelum sabotase:

```bash
default via 10.95.4.113 dev eth0
```

Setelah sabotase:

```bash
default via 10.95.4.138 dev eth2
```

Default gateway seharusnya mengarah ke Gendo melalui `eth0`, yaitu `10.95.4.113`.

Namun, script mengubah default gateway menjadi `10.95.4.138` melalui `eth2`, yang merupakan alamat Makoto.

Perubahan tersebut menyebabkan jalur utama paket menuju jaringan di luar Shigeru menjadi salah.

**Kerusakan kedua: Blackhole route ditambahkan.**

Ditemukan konfigurasi:

```bash
blackhole 10.95.4.72/29
```

Jaringan `10.95.4.72/29` merupakan jaringan Dogma tempat Lilith berada.

Blackhole route menyebabkan seluruh paket yang memiliki tujuan ke jaringan tersebut langsung dibuang oleh router.

Akibatnya, paket balasan dari Armisael menuju Lilith tidak dapat diteruskan melalui Shigeru.

### Memeriksa Policy Routing

Perintah:

```bash
ip rule show
```

<img width="251" height="62" alt="9 - ip rule after" src="https://github.com/user-attachments/assets/3992ea41-3598-494b-aec9-fa1c17ba7b8b" />

Ditemukan policy routing tambahan:

```bash
90: from all iif eth1 lookup 100
```

Rule tersebut berarti setiap paket yang masuk melalui interface `eth1` akan menggunakan routing table 100.

Karena `eth1` merupakan interface jaringan Monolith tempat Armisael berada, paket balasan dari Armisael akan terkena aturan ini.

### Memeriksa Routing Table 100

Berdasarkan isi script sabotase, routing table 100 diisi dengan:

```bash
ip route add unreachable default table 100
```

Artinya, seluruh tujuan yang tidak memiliki rute lebih spesifik dalam tabel tersebut akan dianggap tidak dapat dijangkau.

Karena policy routing mengarahkan paket masuk dari `eth1` ke tabel 100, paket balasan dari Armisael akan ditolak oleh aturan `unreachable default`.

### Memeriksa IP Forwarding

Perintah:

```bash
sysctl net.ipv4.ip_forward
```

<img width="278" height="28" alt="9 - sysctl after" src="https://github.com/user-attachments/assets/a5f2abff-45a1-4d96-9fba-0e7befcad09d" />

Ditemukan kerusakan tambahan, yaitu IP forwarding dimatikan.

IP forwarding diperlukan agar router dapat meneruskan paket dari satu interface ke interface lainnya.

Ketika nilainya `0`, Shigeru tidak dapat meneruskan paket antarjaringan meskipun interface dan routing table memiliki konfigurasi tertentu.

### Ringkasan Penyebab Sabotase

Berdasarkan hasil pemeriksaan, ditemukan empat penyebab utama gangguan komunikasi.

| No. | Penyebab | Kondisi setelah sabotase | Dampak |
|---|---|---|---|
| 1 | IP forwarding dimatikan | `net.ipv4.ip_forward = 0` | Router tidak meneruskan paket antarjaringan |
| 2 | Default gateway diubah | Via 10.95.4.138 melalui eth2 | Jalur utama menuju Gendo menjadi salah |
| 3 | Blackhole route ditambahkan | `10.95.4.72/29` | Paket menuju jaringan Dogma dibuang |
| 4 | Policy routing ditambahkan | `iif eth1 lookup 100` | Paket dari Monolith diarahkan ke tabel routing yang bermasalah |

Keempat kerusakan tersebut saling memengaruhi dan menyebabkan Lilith tidak dapat berkomunikasi dengan Armisael.

## Proses Perbaikan Konfigurasi

Setelah seluruh penyebab diketahui, dilakukan perbaikan pada router Shigeru.

### Mengaktifkan Kembali IP Forwarding

Perintah:

```bash
sysctl -w net.ipv4.ip_forward=1
```

IP forwarding diaktifkan kembali agar Shigeru dapat meneruskan paket antarjaringan.

### Menghapus Blackhole Route

Perintah:

```bash
ip route del blackhole 10.95.4.72/29
```

Perintah tersebut menghapus blackhole route yang sebelumnya membuang paket menuju jaringan Dogma.

Setelah dihapus, paket menuju jaringan `10.95.4.72/29` tidak lagi dibuang oleh aturan tersebut.

### Menghapus Policy Routing Priority 90

Perintah:

```bash
ip rule del priority 90
```

Perintah tersebut menghapus aturan policy routing yang mengarahkan paket dari `eth1` ke routing table 100.

Dengan demikian, paket dari jaringan Monolith kembali menggunakan routing table utama.

### Membersihkan Routing Table 100

Perintah:

```bash
ip route flush table 100
```

Seluruh entri routing pada tabel 100 dihapus agar tidak ada lagi rute `unreachable default` yang tersisa.

### Mengembalikan Default Gateway

Perintah:

```bash
ip route replace default via 10.95.4.113 dev eth0
```

Default gateway dikembalikan menuju Gendo melalui `eth0`.

Alamat `10.95.4.113` merupakan alamat interface Gendo pada link Gendo–Shigeru.

### Memastikan Route Radar Tetap Ada

Perintah:

```bash
ip route replace 10.95.4.88/29 via 10.95.4.138 dev eth2
```

Jaringan Radar tetap dapat dijangkau melalui Makoto.

Alamat `10.95.4.88/29` merupakan jaringan Radar, sedangkan `10.95.4.138` merupakan alamat Makoto pada link Shigeru–Makoto.

## Verifikasi Setelah Perbaikan

Setelah seluruh perbaikan dilakukan, dilakukan pemeriksaan ulang terhadap konfigurasi Shigeru.

### Memeriksa IP Forwarding

Perintah:

```bash
sysctl net.ipv4.ip_forward
```

<img width="275" height="23" alt="9 - sysctl perbaikan" src="https://github.com/user-attachments/assets/00ffb82d-331d-441a-8e18-143ca8beb74e" />

IP forwarding sudah kembali aktif.

### Memeriksa Routing Table

Perintah:

```bash
ip route
```

<img width="410" height="77" alt="9 - ip route perbaikan" src="https://github.com/user-attachments/assets/4aac7236-6b93-40aa-9d31-d29290d79e2b" />

Keterangan:
- Default gateway sudah kembali menuju Gendo.
- Jaringan Monolith tetap terhubung langsung melalui `eth1`.
- Jaringan Radar tetap diarahkan melalui Makoto.
- Blackhole route menuju jaringan Dogma sudah tidak ditemukan.

### Memeriksa Policy Routing

Perintah:

```bash
ip rule show
```

<img width="206" height="47" alt="9 - ip rule perbaikan" src="https://github.com/user-attachments/assets/19564a6f-106d-4dac-9dae-7433fca5cc4d" />

Policy rule priority 90 sudah tidak ditemukan. Paket kembali menggunakan routing table utama.

### Memeriksa Routing Table 100

Perintah:

```bash
ip route show table 100
```

<img width="242" height="15" alt="9 - table 100" src="https://github.com/user-attachments/assets/298dc449-fd90-4cfa-ab89-d63e614734d2" />

Tidak ada output.

Routing table 100 sudah kosong dan tidak lagi memiliki aturan `unreachable default`.

## Pengujian Konektivitas Lilith ke Armisael

Setelah konfigurasi Shigeru kembali normal, dilakukan pengujian dari Lilith menuju Armisael.

IP address tujuan:

```text
Armisael = 10.95.4.83
```

Perintah yang dijalankan pada Lilith:

```bash
ping -c 4 10.95.4.83
```

<img width="395" height="121" alt="9 - ping" src="https://github.com/user-attachments/assets/265167fb-9e10-4720-b01b-07e4324dc274" />

Hasil pengujian menunjukkan bahwa:

- Lilith berhasil mengirimkan empat paket ICMP menuju Armisael.
- Armisael berhasil memberikan balasan terhadap seluruh paket.
- Tidak terdapat packet loss.
- Waktu rata-rata respons adalah 1,213 ms.

Dengan demikian, komunikasi dari Lilith menuju Armisael sudah kembali normal setelah konfigurasi routing pada Shigeru diperbaiki.

# Soal 10

Bertujuan untuk mengidentifikasi dan memperbaiki gangguan Network Address Translation (NAT) pada jaringan Cage yang menyebabkan Unit-01, Unit-02, dan Unit-00 tidak dapat mengakses internet.

Selain itu, ini bertujuan untuk:
1. Menjalankan script `break_nat.sh` pada router Misato dan Gendo.
2. Mengidentifikasi seluruh aturan NAT yang menyebabkan gangguan.
3. Menjelaskan alasan jaringan Cage terdampak, sedangkan jaringan Intel tetap dapat mengakses internet.
4. Memperbaiki aturan NAT yang mengalami sabotase.
5. Membuktikan bahwa Unit-01 dapat kembali melakukan ping ke `8.8.8.8`.
6. Menentukan router yang bertanggung jawab melakukan penerjemahan alamat sumber.

## Topologi dan Informasi Jaringan

Praktikum menggunakan dua jaringan yang menjadi objek pengujian, yaitu Cage dan Intel.

| Perangkat | Alamat IP | Subnet | Gateway |
|---|---|---|---|
| Unit-01 | 10.95.4.66 | 10.95.4.64/29 | 10.95.4.65 |
| Unit-02 | 10.95.4.67 | 10.95.4.64/29 | 10.95.4.65 |
| Unit-00 | 10.95.4.68 | 10.95.4.64/29 | 10.95.4.65 |
| Misato (Cage) | 10.95.4.65 | 10.95.4.64/29 | 10.95.4.125 |
| Spy | 10.95.4.102 | 10.95.4.100/30 | 10.95.4.101 |
| Gendo | 192.168.122.124 | NAT1 | 192.168.122.1 |

Keterangan:
- Cage menggunakan subnet `10.95.4.64/29` dan terhubung ke router Misato.
- Intel menggunakan subnet `10.95.4.100/30` dan terhubung melalui router Kaji.
- Misato terhubung ke Gendo melalui jaringan `10.95.4.124/30`.
- Gendo merupakan router utama yang terhubung ke NAT1 melalui interface `eth0`.
- Seluruh akses internet dari jaringan internal diteruskan melalui Gendo.

## Konfigurasi Awal dan Pelaksanaan Sabotase

Sesuai instruksi soal, script `break_nat.sh` dijalankan pada router Misato dan Gendo. Kedua router menggunakan file script yang sama.

### Menjalankan script pada Misato

Pertama, dilakukan pemeriksaan hostname dan hak akses root.

```bash
hostname
id -u
```

<img width="151" height="52" alt="10 - hostname misato" src="https://github.com/user-attachments/assets/e1b02ee7-d156-4e26-a36b-11bb4ecff3e9" />

Nilai `0` menunjukkan bahwa perintah dijalankan menggunakan hak akses root.

Selanjutnya, script diberikan izin eksekusi dan dijalankan.

```bash
chmod +x /root/break_nat.sh
sh /root/break_nat.sh
```

<img width="261" height="51" alt="10 - break misato" src="https://github.com/user-attachments/assets/e41d30f4-53e2-4a59-9c2a-8e24a3a67972" />


### Menjalankan script pada Gendou

Langkah yang sama dilakukan pada router Gendo.

```bash
hostname
id -u
```

<img width="152" height="53" alt="10 - hostname gendou" src="https://github.com/user-attachments/assets/c79b1a6a-1605-4ce1-9289-bdd66e8f820b" />

Kemudian script dijalankan.

```bash
chmod +x /root/break_nat.sh
sh /root/break_nat.sh
```

<img width="282" height="51" alt="10 - break gendou" src="https://github.com/user-attachments/assets/997dc0c8-cb48-40eb-8ef0-40f6d5849b56" />

Dengan demikian, script sabotase berhasil dijalankan pada kedua router.

## Identifikasi Penyebab Kerusakan

Setelah script dijalankan, dilakukan pemeriksaan terhadap IP forwarding, tabel NAT, dan routing pada masing-masing router.

### Pemeriksaan Misato

Pemeriksaan IP forwarding dilakukan menggunakan perintah:

```bash
sysctl net.ipv4.ip_forward
```

Hasil:
```text
net.ipv4.ip_forward = 1
```

Hasil tersebut menunjukkan bahwa IP forwarding masih aktif. Dengan demikian, gangguan bukan disebabkan oleh IP forwarding yang dinonaktifkan.

Selanjutnya, dilakukan pemeriksaan aturan NAT:

```bash
iptables -t nat -L POSTROUTING -n -v --line-numbers
```

Hasil:
```text
Chain POSTROUTING (policy ACCEPT 0 packets, 0 bytes)

num  pkts bytes target  prot opt in out source           destination
1    0    0     SNAT    all  --  *  eth0 10.95.4.64/29   !10.95.0.0/16
                                      to:172.31.99.1
```

Ditemukan aturan SNAT yang menerjemahkan alamat sumber jaringan Cage menjadi `172.31.99.1`.

Aturan tersebut memiliki fungsi:
- Sumber paket berasal dari `10.95.4.64/29`.
- Paket keluar melalui interface `eth0` pada Misato.
- Tujuan paket bukan bagian dari jaringan internal `10.95.0.0/16`.
- Alamat sumber paket diubah menjadi `172.31.99.1`.

Aturan tersebut merupakan penyebab kerusakan pertama.

Seharusnya, Misato hanya meneruskan paket dari Cage menuju Gendo tanpa melakukan penerjemahan alamat sumber. Penerjemahan alamat sumber seharusnya dilakukan di Gendo ketika paket keluar menuju NAT1.

Pemeriksaan routing dilakukan menggunakan:

```bash
ip route
```

Hasil:
```text
default via 10.95.4.125 dev eth0
10.95.4.64/29 dev eth1 proto kernel scope link src 10.95.4.65
10.95.4.124/30 dev eth0 proto kernel scope link src 10.95.4.126
```

Routing Misato masih sesuai:
- Default route mengarah ke Gendo melalui `10.95.4.125`.
- Jaringan Cage terhubung langsung melalui `eth1`.
- Tidak ditemukan kerusakan pada routing.

<img width="525" height="140" alt="10 - misato after" src="https://github.com/user-attachments/assets/237dd6bc-9cc2-4b58-ac15-7dfbdf8f783e" />

### Pemeriksaan Gendo

Pemeriksaan IP forwarding dilakukan menggunakan:

```bash
sysctl net.ipv4.ip_forward
```

Hasil:
```text
net.ipv4.ip_forward = 1
```

IP forwarding Gendo masih aktif.

Selanjutnya, dilakukan pemeriksaan tabel NAT:

```bash
iptables -t nat -L POSTROUTING -n -v --line-numbers
```

Hasil:
```text
Chain POSTROUTING (policy ACCEPT 9 packets, 1904 bytes)

num  pkts bytes target      prot opt in out source          destination
1    0    0     RETURN      all  --  *  eth0 10.95.4.64/29  0.0.0.0/0
2    48   3363  MASQUERADE  all  --  *  eth0 10.95.0.0/16   0.0.0.0/0
```

Ditemukan aturan RETURN pada urutan pertama:

```bash
iptables -t nat -I POSTROUTING 1 -s 10.95.4.64/29 -o eth0 -j RETURN
```

Aturan tersebut menyebabkan paket dari jaringan Cage yang keluar melalui `eth0` langsung melewati proses NAT berikutnya.

Padahal, Gendo memiliki aturan MASQUERADE:

```bash
iptables -t nat -A POSTROUTING -s 10.95.0.0/16 -o eth0 -j MASQUERADE
```

Aturan MASQUERADE tersebut seharusnya menerjemahkan alamat sumber seluruh jaringan internal ketika paket keluar menuju NAT1.

Karena aturan RETURN berada di urutan pertama dan cocok dengan paket dari Cage, aturan MASQUERADE tidak dijalankan untuk trafik tersebut.

Aturan RETURN merupakan penyebab kerusakan kedua.

Pemeriksaan routing dilakukan menggunakan:

```bash
ip route
```

Hasil menunjukkan bahwa Gendo masih memiliki default route:

```text
default via 192.168.122.1 dev eth0 metric 2184
```

Rute menuju jaringan Cage juga masih tersedia:

```text
10.95.4.64/29 via 10.95.4.126 dev eth5
```

Dengan demikian, routing pada Gendo masih benar. Gangguan berasal dari aturan NAT yang telah dimodifikasi.

<img width="591" height="407" alt="10 - gendou after" src="https://github.com/user-attachments/assets/175ae85b-f82c-4128-9880-0438b7f77ea0" />

## Analisis Mengapa Cage Terdampak tetapi Intel Tidak

Gangguan hanya terjadi pada jaringan Cage karena kedua aturan sabotase secara khusus menargetkan subnet:

```text
10.95.4.64/29
```

Subnet tersebut digunakan oleh Unit-01, Unit-02, dan Unit-00.

Sementara itu, jaringan Intel menggunakan subnet:

```text
10.95.4.100/30
```

Alamat sumber dari jaringan Intel tidak cocok dengan aturan SNAT di Misato maupun aturan RETURN di Gendo.

Akibatnya, trafik dari Intel tetap dapat melewati aturan MASQUERADE yang benar di Gendo.

Hal tersebut dibuktikan melalui pengujian dari perangkat Spy.

Perintah:

```bash
ping -c 4 8.8.8.8
```

<img width="403" height="118" alt="10 - ping spy after" src="https://github.com/user-attachments/assets/a2108990-28da-457e-955e-7dc064f7b758" />

Spy tetap berhasil mengakses internet karena alamat sumbernya tidak terkena aturan sabotase.

Selain itu, komunikasi internal antara Cage dan Lilith tetap berjalan karena aturan SNAT pada Misato memiliki pengecualian tujuan jaringan internal:

```text
! -d 10.95.0.0/16
```

Artinya, aturan SNAT hanya berlaku untuk trafik menuju luar jaringan internal. Ketika perangkat Cage berkomunikasi dengan Lilith, tujuan masih berada dalam jaringan `10.95.0.0/16`, sehingga aturan SNAT tidak cocok.

Dengan demikian, komunikasi antarjaringan internal tetap berjalan, tetapi akses Cage menuju internet terganggu.

## Perbaikan Konfigurasi NAT

Setelah seluruh penyebab ditemukan, dilakukan penghapusan terhadap dua aturan sabotase tanpa menghapus aturan NAT lainnya.

### Menghapus aturan SNAT pada Misato

Pada router Misato dijalankan:

```bash
iptables -t nat -D POSTROUTING -s 10.95.4.64/29 ! -d 10.95.0.0/16 -o eth0 -j SNAT --to-source 172.31.99.1
```

Perintah tersebut menghapus aturan SNAT yang mengubah alamat sumber Cage menjadi `172.31.99.1`.

Kemudian dilakukan pemeriksaan ulang:

```bash
iptables -t nat -L POSTROUTING -n -v --line-numbers
```

<img width="491" height="75" alt="10 - misato perbaikan" src="https://github.com/user-attachments/assets/29c0ab63-8f59-47bb-969b-e777c8da67dd" />

Aturan SNAT yang bermasalah sudah tidak digunakan.

### Menghapus aturan RETURN pada Gendo

Pada router Gendo dijalankan:

```bash
iptables -t nat -D POSTROUTING -s 10.95.4.64/29 -o eth0 -j RETURN
```

Perintah tersebut menghapus aturan RETURN yang menyebabkan trafik Cage melewati proses MASQUERADE.

Selanjutnya, dipastikan aturan MASQUERADE tetap tersedia:

```bash
iptables -t nat -C POSTROUTING -s 10.95.0.0/16 -o eth0 -j MASQUERADE 2>/dev/null || iptables -t nat -A POSTROUTING -s 10.95.0.0/16 -o eth0 -j MASQUERADE
```

Perintah tersebut memeriksa keberadaan aturan MASQUERADE. Jika belum tersedia, aturan akan ditambahkan.

Aturan yang dipertahankan adalah:

```bash
iptables -t nat -A POSTROUTING -s 10.95.0.0/16 -o eth0 -j MASQUERADE
```

Dengan konfigurasi ini, seluruh trafik dari jaringan internal yang keluar melalui Gendo menuju NAT1 akan diterjemahkan menggunakan alamat IP interface `eth0` Gendo.

<img width="554" height="215" alt="10 - gendou perbaikan" src="https://github.com/user-attachments/assets/e747178d-9624-4bbd-bf66-2e8f34ac9052" />

## Pengujian Setelah Perbaikan

Setelah kedua aturan sabotase dihapus, dilakukan pengujian kembali dari Unit-01.

### Pengujian koneksi Unit-01 ke gateway Cage dan ke internet sebelum perbaikan

Perintah:

```bash
ping -c 4 10.95.4.65
```

Hasil sebelum perbaikan:
```text
4 packets transmitted, 4 received, 0% packet loss
```

Unit-01 dapat berkomunikasi dengan gateway Cage. Hal ini menunjukkan bahwa koneksi lokal masih berjalan dengan baik.

Perintah:

```bash
ping -c 4 8.8.8.8
```

Hasil:
```text
4 packets transmitted, 0 received, 100% packet loss
```

Unit-01 belum dapat mengakses internet sebelum aturan sabotase diperbaiki.

<img width="416" height="176" alt="10 - ping unit after" src="https://github.com/user-attachments/assets/b97340d7-3bf8-42c0-91ce-8f02e98140c2" />

### Pengujian koneksi Unit-01 ke internet setelah perbaikan

Setelah aturan SNAT di Misato dan RETURN di Gendo dihapus, dilakukan pengujian kembali:

```bash
ping -c 4 8.8.8.8
```

<img width="433" height="230" alt="10 - ping unit perbaikan" src="https://github.com/user-attachments/assets/70005bb9-dec6-4f43-a4d1-4854c329901c" />

Hasil tersebut membuktikan bahwa Unit-01 sudah dapat mengakses internet setelah konfigurasi NAT diperbaiki.

### Pemeriksaan counter MASQUERADE pada Gendo

Untuk memastikan paket dari Cage benar-benar melewati proses NAT, dilakukan pemeriksaan:

```bash
iptables -t nat -L POSTROUTING -n -v --line-numbers
```

<img width="526" height="137" alt="10 - masquerade" src="https://github.com/user-attachments/assets/b414d11c-c050-42c6-8bfe-0d33d0eb479d" />

Hasil pengujian menunjukkan bahwa jumlah paket dan byte pada aturan MASQUERADE bertambah setelah Unit-01 melakukan ping ke `8.8.8.8`.

Hal tersebut membuktikan bahwa paket dari Unit-01 telah melewati aturan MASQUERADE pada Gendo.

## Lokasi Penerjemahan Alamat Sumber

Penerjemahan alamat sumber yang benar dilakukan pada router **Gendo**, tepatnya melalui interface `eth0` yang terhubung ke NAT1.

Aturan yang digunakan:

```bash
iptables -t nat -A POSTROUTING -s 10.95.0.0/16 -o eth0 -j MASQUERADE
```

MASQUERADE digunakan karena alamat IP interface Gendo yang terhubung ke NAT1 diperoleh secara dinamis melalui DHCP.

Dengan demikian, alamat sumber dari jaringan internal akan diterjemahkan menggunakan alamat IP terkini pada interface `eth0` Gendo.

Misato tidak seharusnya melakukan NAT karena tugasnya adalah meneruskan paket dari jaringan Cage menuju Gendo.

Alur komunikasi yang benar:

```text
Unit-01 (10.95.4.66)
        |
        v
Misato (10.95.4.65)
        |
        v
Gendo
NAT MASQUERADE pada eth0
        |
        v
NAT1
        |
        v
Internet (8.8.8.8)
```

# Soal 11

Bertujuan untuk mengamankan perangkat Magi-Casper agar tidak dapat diketahui melalui pengujian ping oleh perangkat lain, termasuk perangkat yang berada dalam satu jaringan lokal maupun perangkat dari jaringan berbeda.

Selain itu, praktikum ini bertujuan untuk:
1. Mengonfigurasi firewall menggunakan iptables pada Magi-Casper.
2. Memblokir seluruh permintaan ICMP Echo Request yang masuk ke Casper.
3. Memastikan Casper tetap dapat melakukan ping ke perangkat lain.
4. Memastikan layanan TCP port 5000 pada Casper tetap berjalan.
5. Membuktikan bahwa Balthasar dan Lilith tidak dapat melakukan ping ke Casper, sedangkan Casper tetap dapat melakukan ping ke keduanya.

## Topologi dan Informasi Jaringan

Praktikum menggunakan tiga perangkat, yaitu Magi-Casper, Magi-Balthasar, dan Lilith.

Berikut informasi alamat IP masing-masing perangkat:

| Perangkat | Alamat IP | Subnet | Gateway |
|---|---|---|---|
| Magi-Casper | 10.95.4.58 | 10.95.4.56/29 | 10.95.4.57 |
| Magi-Balthasar | 10.95.4.59 | 10.95.4.56/29 | 10.95.4.57 |
| Magi-Melchior | 10.95.4.60 | 10.95.4.56/29 | 10.95.4.57 |
| Lilith | 10.95.4.74 | 10.95.4.72/29 | 10.95.4.73 |

Keterangan:
- Magi-Casper dan Magi-Balthasar berada dalam satu subnet, yaitu `10.95.4.56/29`.
- Lilith berada pada subnet berbeda, yaitu `10.95.4.72/29`.
- Casper harus menolak seluruh permintaan ping dari perangkat lain.
- Casper tetap diperbolehkan mengirimkan paket ICMP ke perangkat lain.
- Layanan TCP port 5000 pada Casper harus tetap aktif.

## Pemeriksaan Kondisi Awal

Sebelum melakukan konfigurasi firewall, dilakukan pemeriksaan terhadap hostname, alamat IP, aturan firewall, dan layanan TCP pada Casper.

### Pemeriksaan hostname dan alamat IP Casper

Perintah yang digunakan:

```bash
hostname
ip -br addr
```

<img width="475" height="155" alt="image" src="https://github.com/user-attachments/assets/485389e8-437e-40ee-8795-63ac9dd113ec" />

Hasil:
```text
Magi-Casper

lo     UNKNOWN  127.0.0.1/8 ::1/128
eth0   UNKNOWN  10.95.4.58/29
eth1   UNKNOWN  fe80::42:78ff:fe6e:a101/64
eth2   UNKNOWN  fe80::42:78ff:fe6e:a102/64
eth3   UNKNOWN  fe80::42:78ff:fe6e:a103/64
```

Berdasarkan hasil tersebut, diketahui bahwa:
- Node yang sedang dikonfigurasi adalah Magi-Casper.
- Alamat IPv4 Casper adalah `10.95.4.58/29`.
- Interface `eth0` merupakan interface yang memiliki alamat IPv4 untuk jaringan MAGI.

### Pemeriksaan aturan firewall awal

Perintah:

```bash
iptables -L INPUT -n -v --line-numbers
```

<img width="475" height="155" alt="image" src="https://github.com/user-attachments/assets/485389e8-437e-40ee-8795-63ac9dd113ec" />

Hasil:
```text
Chain INPUT (policy ACCEPT 28 packets, 2055 bytes)

num  pkts bytes target  prot opt in out source      destination
```

Hasil pemeriksaan menunjukkan bahwa:
- Policy INPUT masih menggunakan ACCEPT.
- Belum terdapat aturan firewall untuk memblokir paket ICMP.
- Semua paket yang masuk masih diizinkan secara default.

Dengan kondisi tersebut, perangkat lain masih dapat melakukan ping ke Casper.

### Pemeriksaan layanan TCP port 5000

Perintah:

```bash
ss -lntp | grep ':5000'
```

<img width="475" height="155" alt="image" src="https://github.com/user-attachments/assets/485389e8-437e-40ee-8795-63ac9dd113ec" />

Pada pemeriksaan awal, tidak ditemukan output yang menunjukkan bahwa layanan TCP port 5000 sedang berjalan.

Oleh karena itu, layanan TCP port 5000 perlu diaktifkan kembali sebelum pengujian akhir.

## Pengujian Koneksi Sebelum Konfigurasi

Sebelum menerapkan firewall, dilakukan pengujian ping dari Balthasar dan Lilith menuju Casper.

### Pengujian dari Magi-Balthasar

Perintah:

```bash
ping -c 4 10.95.4.58
```

<img width="407" height="109" alt="image-1" src="https://github.com/user-attachments/assets/c9e24bb6-0cd1-4d12-b947-3e65aad4b995" />

Hasil:
```text
4 packets transmitted, 4 received, 0% packet loss
```

Hasil tersebut menunjukkan bahwa Balthasar masih dapat melakukan ping ke Casper.

### Pengujian dari Lilith

Perintah:

```bash
ping -c 4 10.95.4.58
```

<img width="415" height="117" alt="image-2" src="https://github.com/user-attachments/assets/0f0e43bc-d28b-47ef-9e37-e21c7611b913" />

Hasil:
```text
4 packets transmitted, 4 received, 0% packet loss
```

Hasil tersebut menunjukkan bahwa Lilith juga masih dapat melakukan ping ke Casper.

Dengan demikian, sebelum konfigurasi firewall diterapkan, Casper masih dapat ditemukan melalui pengujian ICMP dari jaringan lokal maupun jaringan berbeda.

## Konfigurasi Firewall pada Magi-Casper

Untuk memenuhi persyaratan soal, dilakukan konfigurasi firewall menggunakan iptables.

Aturan yang digunakan adalah:

```bash
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
```

<img width="518" height="92" alt="image-3" src="https://github.com/user-attachments/assets/b549196a-9512-423d-9e94-617eaf9f77df" />

Perintah tersebut dijalankan pada console Magi-Casper.

Penjelasan setiap bagian perintah:

| Bagian perintah | Fungsi |
|---|---|
| `iptables` | Mengelola aturan firewall Linux |
| `-A INPUT` | Menambahkan aturan pada chain INPUT |
| `-p icmp` | Memilih paket dengan protokol ICMP |
| `--icmp-type echo-request` | Memilih paket permintaan ping |
| `-j DROP` | Membuang paket yang cocok dengan aturan |

Aturan tersebut menyebabkan seluruh paket ICMP Echo Request yang masuk ke Casper dibuang.

Dengan demikian, perangkat lain tidak akan mendapatkan balasan ketika mencoba melakukan ping ke Casper.

Namun, aturan tersebut tidak memblokir:
- Paket ICMP Echo Request yang dikirim oleh Casper.
- Paket balasan ICMP Echo Reply yang diterima Casper.
- Koneksi TCP, termasuk layanan pada port 5000.

Hal ini karena aturan hanya diterapkan pada paket ICMP Echo Request yang masuk melalui chain INPUT.

## Pemeriksaan Aturan Firewall Setelah Konfigurasi

Setelah aturan ditambahkan, dilakukan pemeriksaan menggunakan:

```bash
iptables -L INPUT -n -v --line-numbers
```

<img width="518" height="92" alt="image-3" src="https://github.com/user-attachments/assets/b549196a-9512-423d-9e94-617eaf9f77df" />

Hasil:
```text
Chain INPUT (policy ACCEPT 36 packets, 2727 bytes)

num  pkts bytes target  prot opt in out source      destination
1    0    0     DROP    icmp -- *  *   0.0.0.0/0   0.0.0.0/0
                                      icmptype 8
```

Berdasarkan hasil tersebut, aturan DROP berhasil ditambahkan pada chain INPUT dengan nomor aturan 1.

Keterangan `icmptype 8` menunjukkan bahwa aturan tersebut berlaku untuk ICMP Echo Request, yaitu paket yang digunakan ketika perangkat melakukan ping.

Dengan konfigurasi tersebut, Casper tidak akan memberikan respons terhadap permintaan ping dari perangkat lain.

## Mengaktifkan Layanan TCP Port 5000

Selain mengamankan Casper dari ping masuk, soal juga mensyaratkan bahwa layanan TCP port 5000 harus tetap hidup.

Untuk mengaktifkan layanan tersebut, digunakan perintah:

```bash
nc.traditional -l -p 5000 &
```

<img width="455" height="64" alt="image-4" src="https://github.com/user-attachments/assets/b2f2d521-79e7-4849-840d-9009e45662a5" />

Keterangan:
- `nc.traditional` digunakan untuk menjalankan layanan menggunakan Netcat Traditional.
- `-l` mengaktifkan mode listener atau menunggu koneksi masuk.
- `-p 5000` menentukan port yang digunakan, yaitu port 5000.
- `&` menjalankan proses di background sehingga console dapat digunakan kembali.

Setelah perintah dijalankan, dilakukan pemeriksaan menggunakan:

```bash
ss -lntp | grep ':5000'
```

Hasil:
```text
LISTEN 0 1 0.0.0.0:5000 0.0.0.0:* users:(("nc.traditional",pid=187,fd=3))
```

<img width="455" height="64" alt="image-4" src="https://github.com/user-attachments/assets/b2f2d521-79e7-4849-840d-9009e45662a5" />

Hasil tersebut menunjukkan bahwa:
- Port TCP 5000 berada dalam kondisi LISTEN.
- Layanan mendengarkan koneksi pada seluruh alamat IPv4 (`0.0.0.0`).
- Proses Netcat Traditional berhasil berjalan dengan PID 187.

Dengan demikian, layanan TCP port 5000 tetap aktif meskipun firewall telah dikonfigurasi untuk memblokir ping masuk.

## Pengujian Setelah Konfigurasi Firewall

Setelah konfigurasi selesai, dilakukan pengujian dari kedua arah untuk memastikan bahwa firewall bekerja sesuai persyaratan.

### Pengujian ping dari Magi-Balthasar ke Casper

Pada console Magi-Balthasar dijalankan:

```bash
ping -c 4 10.95.4.58
```

<img width="395" height="72" alt="image-5" src="https://github.com/user-attachments/assets/c2d842e6-54ce-4bfe-9ac5-8a86213dc8f0" />

Hasil:
```text
4 packets transmitted, 0 received, 100% packet loss
```

Hasil tersebut menunjukkan bahwa Balthasar tidak dapat melakukan ping ke Casper.

Paket ICMP Echo Request yang dikirimkan Balthasar berhasil diblokir oleh aturan DROP pada chain INPUT Casper.

### Pengujian ping dari Lilith ke Casper

Pada console Lilith dijalankan:

```bash
ping -c 4 10.95.4.58
```

<img width="399" height="71" alt="image-6" src="https://github.com/user-attachments/assets/38a8ffd0-c7e9-4742-8823-1378e9a3d03b" />

Hasil:
```text
4 packets transmitted, 0 received, 100% packet loss
```

Hasil tersebut menunjukkan bahwa Lilith juga tidak dapat melakukan ping ke Casper.

Walaupun Lilith berada pada jaringan berbeda, paket ICMP Echo Request yang sampai ke Casper tetap diblokir oleh aturan firewall yang sama.

### Pengujian ping dari Casper ke Balthasar

Pada console Magi-Casper dijalankan:

```bash
ping -c 4 10.95.4.59
```

<img width="440" height="229" alt="image-7" src="https://github.com/user-attachments/assets/c63b14f7-dde9-4324-800d-b18a3737f743" />

Hasil:
```text
4 packets transmitted, 4 received, 0% packet loss
```

Hasil tersebut membuktikan bahwa Casper tetap dapat melakukan ping ke Balthasar.

Hal ini terjadi karena aturan firewall hanya memblokir paket ICMP Echo Request yang masuk ke Casper, bukan paket yang dikirimkan oleh Casper.

### Pengujian ping dari Casper ke Lilith

Pada console Magi-Casper dijalankan:

```bash
ping -c 4 10.95.4.74
```

<img width="440" height="229" alt="image-8" src="https://github.com/user-attachments/assets/b068ab63-36c5-46b1-901d-a492c740d96c" />

Hasil:
```text
4 packets transmitted, 4 received, 0% packet loss
```

Hasil tersebut membuktikan bahwa Casper tetap dapat melakukan ping ke Lilith meskipun Lilith berada pada jaringan berbeda.

Dengan demikian, Casper tetap dapat melakukan komunikasi keluar ke perangkat lain.

### Pengujian layanan TCP port 5000

Setelah seluruh pengujian ping dilakukan, layanan TCP port 5000 diperiksa kembali menggunakan:

```bash
ss -lntp | grep ':5000'
```

<img width="494" height="46" alt="image-9" src="https://github.com/user-attachments/assets/f4b9647e-4b3d-4bd6-b55b-6efbe92c1ee1" />

Hasil:
```text
LISTEN 0 1 0.0.0.0:5000 0.0.0.0:* users:(("nc.traditional",pid=187,fd=3))
```

Hasil tersebut menunjukkan bahwa layanan TCP port 5000 masih berada dalam kondisi LISTEN.

Dengan demikian, penerapan firewall ICMP tidak mengganggu layanan TCP port 5000 pada Casper.

## Rekapitulasi Hasil Pengujian

Berikut rekapitulasi seluruh pengujian yang telah dilakukan:

| No. | Pengujian | Hasil | Keterangan |
|---|---|---|---|
| 1 | Balthasar → Casper | 100% packet loss | Ping diblokir |
| 2 | Lilith → Casper | 100% packet loss | Ping diblokir |
| 3 | Casper → Balthasar | 4/4 berhasil | Ping diizinkan |
| 4 | Casper → Lilith | 4/4 berhasil | Ping diizinkan |
| 5 | TCP port 5000 Casper | LISTEN | Layanan aktif |


