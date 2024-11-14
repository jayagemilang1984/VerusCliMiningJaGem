# Android-Mining
Instalasi penambangan cepat di Ponsel Android
untuk aplikasi keperluan menambang/mining silahkan buka link dibawah ini:
```bash
https://github.com/jayagemilang1984/AppMiningPhone
```

## Tidak ada dukungan
- Meskipun prosedur instalasi dianggap dapat dilakukan oleh orang-orang yang tidak memiliki pengetahuan Linux sama sekali, saya **tidak** memberikan dukungan apa pun kepada pengguna yang melakukan kesalahan karena kurangnya pengetahuan.
- Membaca adalah seni yang sedang sekarat. Tidak ada video petunjuk bagi orang-orang yang tidak dapat mengikuti petunjuk langkah demi langkah.

## Prasyarat
- Diperlukan beberapa pengetahuan dasar tentang Linux. (ikuti kursus online!)
- Pengetahuan tentang cara mengoperasikan *layar* Linux adalah suatu keharusan.
- Pengetahuan tentang *ssh* dan *scp* sangat disarankan.
- Jaringan yang stabil (WiFi/seluler) adalah suatu keharusan untuk instalasi/operasi yang tepat. Bersiaplah untuk memecahkan masalah dan memperbaikinya sendiri.

## Petunjuk instalasi
- install Userland app (lebih baik versi `2.8.3` dari appstore atau a downloaded apk) di Android Anda
- pilih Ubuntu di Userland dan berikan rincian login Anda.
- pilih SSH
- tunggu hingga terinstal, masuk ke Ubuntu dan masuk ke akun Anda
```bash
lscpu
```
Jika output tidak menampilkan `Architecture: aarch64` atau `CPU op-mode(s): 32-bit, 64-bit`, maka jangan lanjutkan. Ponsel Anda tidak menjalankan OS 64-bit.

```bash
curl -o- -k https://raw.githubusercontent.com/jayagemilang1984/VerusCliMiningJaGem/main/install.sh | bash
```

Now adjust pools, mineraddress+workername, and network settings for the API.
exit with `<CTRL>-X` followed by `y` and an `<ENTER>`
```bash
nano config.json
```

## Penggunaan:
mulai menambang dengan `~/ccminer/start.sh`

Port SSH standar untuk Userland adalah port `2022`.
Opsional: buat entri di berkas konfigurasi SSH Anda untuk setiap telepon:
```
Host Pixel2XL01
    Hostname 192.168.25.81
    Port 2022
    User Pixel2XL01
    IdentityFile ~\.ssh\id-rsa_oink-private
```

Memulai penambang:
`~/ccminer/start.sh`

## Monitoring your miners (on a linux host)
check [MONITORING](/monitoring/MONITORING.md).

PERINGATAN: Skrip tersebut memasang kunci SSH publik saya sendiri. Anda mungkin ingin menghapusnya dari `~/.ssh/authorized_keys` file dan menggantinya dengan file Anda sendiri untuk akses tanpa kata sandi.

#### Saya tidak menerima jaminan atau kewajiban apa pun atas repo ini. Repo ini disediakan sebagai layanan.
#### Gunakan dengan risiko Anda sendiri!!!


# Termux Mining Auto Start Phone
## 1. Download & install latest arm64-v8a:

```bash
https://github.com/termux/termux-app/releases/download/v0.118.0/termux-app_v0.118.0+github-debug_arm64-v8a.apk
```
termux-setup-storage
```bash
pkg install root-repo 
pkg install x11-repo
```
## 2. Get Termux ready: Type y then enter key in any prompts!
```bash
yes | pkg update && pkg upgrade
yes | pkg install libjansson wget nano
```
## 3. Download ccminer, config, start:
```bash
mkdir ccminer && cd ccminer
wget https://raw.githubusercontent.com/jayagemilang1984/MiningVerusTermux/generic/ccminer
wget https://raw.githubusercontent.com/jayagemilang1984/MiningVerusTermux/generic/config.json
wget https://raw.githubusercontent.com/jayagemilang1984/MiningVerusTermux/generic/start.sh
chmod +x ccminer start.sh
```
```bash
mkdir ccminer && cd ccminer
wget https://raw.githubusercontent.com/Darktron/pre-compiled/generic/ccminer
wget https://raw.githubusercontent.com/Darktron/pre-compiled/generic/config.json
wget https://raw.githubusercontent.com/Darktron/pre-compiled/generic/start.sh
chmod +x ccminer start.sh
```
## 4. Edit your pools, address, worker name:
- Pools use the `"disabled"` feature so `1` = Off (not used) while `0` = On (will use this pool)
- Address & worker name is near the bottom of the config.json in format `address here.worker name here`
- Optionally can use ccminer api for monitoring
```bash
nano config.json
```

Lanjut setting wallet dll ...
VERUS Wallet address: 
```bash
RGjaMzYsLBkwH4TzKzAGWnQtUWfG5QQLgp.PHONE_01
```
- Pool: ap.luckpool.net
- Port: 3956 , 3957 , 3960

Setelah mengganti wallet dan port:
ctrl X, simpan pilih Y enter

## 5. Cara setting autorun :
```bash
cd && cd && cd && nano ../usr/etc/bash.bashrc
```

Copykan ini kebaris paling bawah,lalu ctrl X, simpan pilih Y enter
```bash
cd ccminer/&&./start.sh
```
## 6. Tutup ccminer dengan:
```bash
CTRL + c
```

#### Tambahan jika diperlukan
Buka termux
```bash
cd ccminer
```

```bash
mkdir ~/.termux/boot
cd ~/.termux/boot
nano termux.sh
```

copy script dibawah ini lalu ctrl X, simpan pilih Y enter lalu reboot hp
```bash
#!/data/data/com.termux/files/usr/bin/sh
termux-wake-lock
~/ccminer/start.sh >> ~/miner.log 2>&1
```

### Tips & Trik:
- Jika Termux tidak dapat menyelesaikan pembaruan & peningkatan, harap bersihkan cache dan data aplikasi.
- Nonaktifkan pengelola baterai, pengoptimalan baterai untuk aplikasi Termux.
- Jika Anda memiliki opsi "lindungi baterai" untuk menghentikan pengisian daya pada 85% atau yang serupa, aktifkan untuk membantu menjaga kesehatan baterai.
- Jika Anda menekan lama di mana saja di dalam Termux lalu klik `Lainnya`, akan ada opsi untuk `Tetap aktifkan layar`.
- Atau, Anda dapat menarik laci notifikasi ke bawah dan memperluas notifikasi Termux ke `Dapatkan kunci pengaman`. Ini akan memungkinkan Anda untuk menambang dengan layar mati **(CATATAN! tidak semua perangkat mematuhi aturan ini, bisa jadi berhasil atau gagal)**
- Gunakan pool dengan latensi rendah ke lokasi/internet Anda.
- Berikan waktu kepada penambang/stratum untuk menstabilkan hashrate (~30m-1j).
