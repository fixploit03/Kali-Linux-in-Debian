# Caranya

Update repo Termux dan instal paket yang diperlukan.

```
pkg update && pkg upgrade
pkg install proot-distro
pd install debian
pd login debian
apt-get update && apt-get upgrade
apt-get install wget
apt-get install gpg
wget -qO - https://archive.kali.org/archive-key.asc | sudo tee /usr/share/keyrings/kali-archive-keyring.asc
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

Buat file APT Pinning Debian.

```
nano /etc/apt/preferences.d/debian-pin
```

Tambahkan konfigurasi seperti ini:

```
Package: *
Pin: release a=bookworm
Pin-Priority: 1000
```

Buat file APT Pinning Kali Linux 

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

## Instal Paket 

untuk menginstal paket ketikkan perintah `apt-get install [nama_paket]`.

Menginstal paket tergantung pada nilai Pin-Priority pada file APT Pinning, jika nilai Pin-Priority Debian lebih besar dari Pin-Priority Kali Linux maka secara default akan menginstal paket dari repositori Debian.

Pada kasus ini untuk menginstal paket dari repositori Kali Linux gunakan perintah dibawah ini:

```
apt-get install -t kali-rolling [nama_paket]
```

Jika tidak mau menggunakan `-t kali-rolling` hanya `apt-get install [nama_paket]` ubah nilai Pin-Priority pada file APT Pinning Kali menjadi lebih besar dari nilai Pin-Priority pada file APT Pinning Debian.

## Kesimpulan 

Instal paket dari repositori Debian

```
apt-get install -t bookworm [nama_paket]
```

Instal paket dari repositori Kali Linux

```
apt-get install -t kali-rolling [nama_paket]
```

Kalo `apt-get install [nama_paket]` tergantung pada nilai Pin-Priority.
