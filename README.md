# Kali Linux didalam Termux (proot-distro Debian)

Perbarui repository Termux dan instal paket yang diperlukan dengan menjalankan perintah berikut:

```
pkg update && pkg upgrade
pkg install proot-distro
pd install debian 
```

Masuk ke Debian dengan perintah:

```
pd login debian
```

Perbarui repository Debian dan instal paket yang diperlukan dengan menjalankan perintah berikut:

```
apt-get update && apt-get upgrade
apt-get install wget
apt-get install gpg
```

Tambahkan repository Kali Linux ke dalam sistem dengan menjalankan perintah berikut:

```
echo "deb [signed-by=/usr/share/keyrings/kali-archive-keyring.asc] http://http.kali.org/kali kali-rolling main non-free contrib" | tee /etc/apt/sources.list.d/kali.list
wget -qO - https://archive.kali.org/archive-key.asc | tee /usr/share/keyrings/kali-archive-keyring.asc
```

Buka file repository Debian:

```
nano /etc/apt/sources.list
```

Ubah isinya menjadi seperti berikut:

```
deb [signed-by=/usr/share/keyrings/debian-archive-keyring.gpg] http://deb.debian.org/debian bookworm main contrib non-free non-free-firmware
deb [signed-by=/usr/share/keyrings/debian-archive-keyring.gpg] http://deb.debian.org/debian bookworm-updates main contrib non-free non-free-firmware
deb [signed-by=/usr/share/keyrings/debian-archive-keyring.gpg] http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
```

Buat file APT Pinning untuk Debian.

```
nano /etc/apt/preferences.d/debian-pin
```

Tambahkan konfigurasi berikut:

```
Package: *
Pin: release a=bookworm
Pin-Priority: 1000
```

Buat file APT Pinning untuk Kali Linux:

```
nano /etc/apt/preferences.d/kali-pin
```

Tambahkan konfigurasi berikut:

```
Package: *
Pin: release a=kali-rolling
Pin-Priority: 500
```

Perbarui repository:

```
apt-get update
```

Perintah ini akan memperbarui repository Debian dan Kali Linux secara bersamaan.

Jika hanya ingin memperbarui repository Kali Linux, jalankan:

```
apt-get -t kali-rolling update 
```

## Instal Paket 

Untuk menginstal paket, gunakan perintah:

```
apt-get install [nama_paket]
```

Secara default, paket akan diinstal dari repository yang memiliki nilai Pin-Priority lebih tinggi dalam konfigurasi APT Pinning.

Jika ingin menginstal paket dari repository Kali Linux, gunakan:

```
apt-get install -t kali-rolling [nama_paket]
```

Jika ingin menginstal paket dari repository Debian, gunakan:

```
apt-get install -t bookworm [nama_paket]
```

Jika tidak ingin menggunakan opsi `-t kali-rolling` atau `-t bookworm`, Anda bisa mengubah nilai Pin-Priority di file APT Pinning agar repository yang diinginkan menjadi prioritas utama.

## Catatan 

- Perintah `apt-get install [nama_paket]` akan menginstal paket dari repository yang memiliki Pin-Priority lebih tinggi.
- Jika ingin memastikan paket diinstal dari repository tertentu, gunakan opsi `-t [repo]` sesuai kebutuhan.
