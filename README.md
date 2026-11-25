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

