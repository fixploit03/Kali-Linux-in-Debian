# Kali Linux didalam Termux (proot-distro Debian)

Update repository Termux dan instal paket-paket yang diperlukan dengan mengetikkan perintah berikut:

```
pkg update && pkg upgrade
pkg install proot-distro
pd install debian 
```

Masuk ke Debian dengan perintah:

```
pd login debian
```

Update repository Debian dan instal paket-paket yang diperlukan dengan mengetikkan perintah berikut:

```
apt-get update && apt-get upgrade
apt-get install wget
apt-get install gpg
echo "deb [signed-by=/usr/share/keyrings/kali-archive-keyring.asc] http://http.kali.org/kali kali-rolling main non-free contrib" | tee /etc/apt/sources.list.d/kali.list
wget -qO - https://archive.kali.org/archive-key.asc | tee /usr/share/keyrings/kali-archive-keyring.asc
```

Buka file repositori Debian.

```
nano /etc/apt/sources.list
```

Ubah konfigurasinya menjadi seperti ini:

```
deb [signed-by=/usr/share/keyrings/debian-archive-keyring.gpg] http://deb.debian.org/debian bookworm main contrib non-free non-free-firmware
deb [signed-by=/usr/share/keyrings/debian-archive-keyring.gpg] http://deb.debian.org/debian bookworm-updates main contrib non-free non-free-firmware
deb [signed-by=/usr/share/keyrings/debian-archive-keyring.gpg] http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
```

Buat file APT Pinning untuk Debian.

```
nano /etc/apt/preferences.d/debian-pin
```

Tambahkan konfigurasi seperti ini:

```
Package: *
Pin: release a=bookworm
Pin-Priority: 1000
```

Buat file APT Pinning untuk Kali Linux 

```
nano /etc/apt/preferences.d/kali-pin
```

Tambahkan konfigurasi seperti ini:

```
Package: *
Pin: release a=kali-rolling
Pin-Priority: 500
```

Update repositori

```
apt-get update
```

Ini akan mengupdate repositori Debian dan Kali Linux secara bersamaan.

Kalau hanya mau mengupdate repositori Kali Linux ketikkan:

```
apt-get -t kali-rolling update 
```

## Instal Paket 

untuk menginstal paket ketikkan perintah `apt-get install [nama_paket]`.

Menginstal paket tergantung pada nilai Pin-Priority pada file APT Pinning, jika nilai Pin-Priority Debian lebih besar dari Pin-Priority Kali Linux maka secara default akan menginstal paket dari repositori Debian.

Pada kasus ini untuk menginstal paket dari repositori Kali Linux gunakan perintah dibawah ini:

```
apt-get install -t kali-rolling [nama_paket]
```

Jika tidak mau menggunakan `-t kali-rolling` hanya `apt-get install [nama_paket]` ubah nilai Pin-Priority pada file APT Pinning Kali menjadi lebih besar dari nilai Pin-Priority pada file APT Pinning Debian.

## Catatan 

Instal paket dari repositori Debian

```
apt-get install -t bookworm [nama_paket]
```

Instal paket dari repositori Kali Linux

```
apt-get install -t kali-rolling [nama_paket]
```

Kalo `apt-get install [nama_paket]` tergantung pada nilai Pin-Priority.
