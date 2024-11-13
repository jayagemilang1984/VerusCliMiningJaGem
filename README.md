# Android-Mining
Instalasi penambangan cepat di Ponsel Android

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


## Github cloning and customizing
1. clone this repo to your own github account
2. change the URL on line 14 of the README.md to reflect your own account
3. change the SSH key on line 10 of `install.sh` to reflect your own SSH key
4. change lines 15+16 to reflect your own github link (especially line 13!!!)
5. adjust the `config.json` to your address and mining details.
6. optional: change the lines 20-21 of your `config.json` to your own LAN IP range.

## Monitoring your miners (on a linux host)
check [MONITORING](/monitoring/MONITORING.md).

WARNING: The scripts installs my own public SSH key. You may want to remove that from your `~/.ssh/authorized_keys` file and replace it with your own for passwordless access.

### I accept no warranties or liabilities on this repo. It is supplied as a service.
### Use at your own risk!!!
