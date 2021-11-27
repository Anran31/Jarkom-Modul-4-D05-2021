# Jarkom-Modul-4-D05-2021

## Anggota Kelompok D05

| Nama                          | NRP            |
| ----------------------------- | -------------- |
| Andika Nugrahanto             | 05111940000031 |
| Muhammad Rayhan Raffi Pratama | 05111940000110 |
| Fadhil Dimas Sucahyo          | 05111940000212 |

## VLSM (Variable Length Subnet Masking) - CPT

### Perhitungan Subnet

#### Langkah 1

Pertama-tama jumlah alamat IP yang dibutuhkan ditentukan untuk tiap subnet dan dilakukan labelling netmask berdasarkan jumlah IP yang dibutuhkan.

| Subnet | Jumlah IP | Netmask |
| :----: | :-------: | :-----: |
|   A1   |   2021    |   /21   |
|   A2   |    101    |   /25   |
|   A3   |     2     |   /30   |
|   A4   |    701    |   /22   |
|   A5   |     2     |   /30   |
|   A6   |   1001    |   /22   |
|   A7   |     2     |   /30   |
|   A8   |    521    |   /22   |
|   A9   |     2     |   /30   |
|  A10   |    252    |   /24   |
|  A11   |    721    |   /22   |
|  A12   |    502    |   /23   |
|  A13   |    13     |   /28   |
| total  |   5845    |   /19   |

Berdasarkan total IP dan netmask yang dibutuhkan, maka kita dapat menggunakan netmask /19 untuk memberikan pengalamatan IP pada subnet.

#### Langkah 2

Kemudian membuat pohon pembagian subnet seperti ini:

![VLSM-Tree](./imgs/vlsm-tree.PNG)

#### Langkah 3

Dilakukan pembaagian IP sehingga didapati tabel dibawah ini:
![VLSM-table](./imgs/vlsm-table.PNG)

Berikut merupakan gambar topologi yang telah disubnetting:
![VLSM-topologi](./imgs/vlsm-topologi.PNG)

### Routing

#### Subnetting

Pertama-tama, topologi dibuat dalam CPT.

![VLSM-cpt](./imgs/vlsm-cpt.PNG)

![VLSM-foosha](./imgs/vlsm-foosha.PNG)
Misal, karena disini `FastEthernet0/1` mengarah ke `Blueno (1000 Host)`, maka kita menggunakan subnet A12 dengan NID `10.19.8.0`. Pada konfigurasi `Foosha`, address untuk `FastEthernet0/1`-nya ditambahi 1 dari NID subnet A12 hingga menjadi `10.19.8.1`.

![VLSM-blueno](./imgs/vlsm-blueno.PNG)
Untuk kliennya, yaitu `Blueno (1000 Host)`, untuk config IP-nya ditambahi 1 lagi dari IP Foosha sehingga menjadi `10.19.8.2`. Untuk netmasknya mengikuti tabel yang telah dibuat sebelumnya. Gateway hanya digunakan untuk klien dan server dan mengarah ke IP router terdekat, jadi gateway untuk klien `Blueno (1000 Host)` adalah `10.19.8.1`.

Hal ini dilakukan pada semua node dan subnetting pun selesai.

#### Routing

Untuk routing pada CPT, diberikan static route pada semua router yang ada dengan route sebagai berikut untuk setiap router:

##### Foosha

```
192.194.27.0/25 via 192.194.27.146
192.194.0.0/21 via 192.194.27.146
192.194.27.156/30 via 192.194.27.146
192.194.16.0/22 via 192.194.27.146
192.194.12.0/22 via 192.194.27.150
192.194.26.0/24 via 192.194.27.150
192.194.27.128/28 via 192.194.27.150
192.194.24.0/23 via 192.194.27.150
192.194.20.0/22 via 192.194.27.150
192.194.27.152/30 via 192.194.27.150
192.194.27.164/30 via 192.194.27.150
```

##### Water7

```
0.0.0.0/0 via 192.194.27.145
192.194.27.0/25 via 192.194.27.158
192.194.0.0/21 via 192.194.27.158
```

##### Pucci

```
0.0.0.0/0 via 192.194.27.157
```

##### Guanhao

```
0.0.0.0/0 via 192.194.27.149
192.194.12.0/22 via 192.194.27.154
192.194.26.0/24 via 192.194.27.154
192.194.27.164/30 via 192.194.27.154
192.194.27.128/28 via 192.194.24.3

```

##### Alabasta

```
0.0.0.0/0 via 192.194.24.1
```

##### Oimo

```
0.0.0.0/0 via 192.194.27.153
192.194.12.0/22 via 192.194.26.3
```

##### Seastone

```
0.0.0.0/0 via 192.194.26.1
```
