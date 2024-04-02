# Jarkom-Modul-1-IT09-2024

| Nama | NRP |
|---------|---------|
| Gavriel Pramuda Kurniaadi | 5027221031  |
| Stephanie Hebrina Mabunbun Simatupang | 5027221069  | 

## Daftar isi
- [Jarkom-Modul-1-IT09-2024](#jarkom-modul-1-it09-2024)
  - [1. Creds](#1-creds)
  - [2. Evidence](#2-evidence)
  - [3. Fuzz](#3-fuzz)
  - [4. ATM or ATP or FTP](#4-atm-or-atp-or-ftp)
  - [5. How Many Packets?](#5-how-many-packets)
  - [6. Trace Him](#6-trace-him)
  - [7. Malwaew](#7-malwaew)
  - [8. Malwleowleo](#8-malwleowleo)
  - [9. Whoami](#9-whoami)
  - [10. Secret](#10-secret)

## 1. Creds
<img width="495" alt="creds1" src="https://github.com/GavrielAdi/Jarkom-Modul-1-IT09-2024/assets/51376746/6c741474-fa73-4556-b06a-09bc39d8d7b9">

<br/>
File : evidence.pcap
<br/>
Maksud soal : Kita diminta untuk mencari Username FTP yang digunakan oleh attacker & Password FTP yang digunakan oleh attacker. 
<br />
**Cara pengerjaan:**
1. Memfilter ftp && frame contains " Login " artinya untuk mencari yang Login saja, kemudian resultnya hanya keluar 1 yang succesfull
<img width="1008" alt="creds2" src="https://github.com/GavrielAdi/Jarkom-Modul-1-IT09-2024/assets/51376746/ffc4f891-821f-4381-bcd3-61dd7d2b4d98">
2. Kemudian klik Follow > TCP Stream, akan muncul seperti ini 
<img width="1008" alt="creds3" src="https://github.com/GavrielAdi/Jarkom-Modul-1-IT09-2024/assets/51376746/3db32c17-c3c4-49ba-a240-cc13742ee6ff">
3. Kemudian akan muncul USER dan PASS nya
<img width="1008" alt="creds4" src="https://github.com/GavrielAdi/Jarkom-Modul-1-IT09-2024/assets/51376746/cbbd9201-6b53-4aa6-b73a-6060c64ec6b4">

**Jika dimasukan ke netcat maka akan ketemu flagnya**
<img width="549" alt="creds5" src="https://github.com/GavrielAdi/Jarkom-Modul-1-IT09-2024/assets/51376746/3f395ff9-7ff2-4007-8f63-82b0a779f6a6">

## 2. Evidence
<img width="495" alt="ev" src="https://github.com/GavrielAdi/Jarkom-Modul-1-IT09-2024/assets/51376746/eab5deeb-627a-4524-9737-b6e16c7dab61">
<br/>
File : challenge.pcapng
<br/>
Maksud soal : Kita diminta untuk mencari informasi tentang cara pelaku bisa masuk ke dalam perusahaan nanomate.
<br />
**Cara pengerjaan:**

1. Melakukan follow pada salah satu stream TCP dan didapatkan informasi mengenai domain dan web server korban.
![ev1](https://github.com/GavrielAdi/Jarkom-Modul-1-IT09-2024/assets/51376746/794b1951-8887-4de4-a7c7-3b5bc505dcd1)
2. Kemudian, dilakukan pencarian endpoint yang digunakan untuk login sebagai user biasa dengan melakukan filter http. Ditemukan ada banyak sekali endpoint ```/app/includes/process_login.php```, kemudian dicoba untuk submit dan jawabannya benar.
![ev2](https://github.com/GavrielAdi/Jarkom-Modul-1-IT09-2024/assets/51376746/4be32273-9c95-4c72-978e-611016cc8d4b)
3. Terakhir, dilakukan pencarian email dan password yang berhasil digunakan untuk login sebagai user biasa. Dilakukan sorting dengan menekan kata "Info" untuk mempermudah pencarian email dan password pada "302 Found". Ditemukan juga ada kalimat menarik, yaitu Invalid Username or Password.
![ev3](https://github.com/GavrielAdi/Jarkom-Modul-1-IT09-2024/assets/51376746/426f820f-5127-45ad-89d8-932b35c49635)
4. Dilakukan follow HTTP dan ditemukan ada kalimat Login Successful pada ```tcp.stream eq 1240``` sehingga berhasil ditemukan email dan passwordnya.
![ev4](https://github.com/GavrielAdi/Jarkom-Modul-1-IT09-2024/assets/51376746/a1bf55c4-3339-43a1-985d-6aff3319f0a0)

**Jika dimasukan ke netcat maka akan ketemu flagnya**
![ev5](https://github.com/GavrielAdi/Jarkom-Modul-1-IT09-2024/assets/51376746/63653046-3131-4146-865d-08fb6849fb80)

## 3. Fuzz
<img width="495" alt="fuzz" src="https://github.com/GavrielAdi/Jarkom-Modul-1-IT09-2024/assets/51376746/f57fc05c-53a0-498f-b62a-6b5114f2b47c">
<br/>
File : capture.pcap
<br/>
Maksud soal : Kita diminta untuk menganalisis network traffic ini untuk melacak attackernya
<br />
**Cara pengerjaan:**

1. Terlihat bahwa terdapat POST request dari IP 10.33.1.154 kepada IP 172.20.0.2, maka dapat disimpulkan bahwa IP attacker adalah 10.33.1.154 dan IP korban adalah 172.20.0.2.
![fuzz1](https://github.com/GavrielAdi/Jarkom-Modul-1-IT09-2024/assets/51376746/9afa2a0b-ec75-4db8-b48f-a814512b01bf)
2. Kemudian, dilakukan pencarian port dari web server korban dengan mengecek detail packet dari IP korban ke IP attacker. Ditemukan terdapat pengiriman data dari port 80 ke port 1264 sehingga port dari web server korban adalah 80.
![f2](gambar/fuzz2.png)
3. Dilakukan follow pada salah satu packet yang berisi POST request dan ditemukan bahwa attacker melakukan POST pada endpoint /. Ditemukan juga tool yang digunakan, yaitu Fuzz Faster U Fool v2.0.0-dev atau disingkat ffuf-v2.0.0-dev.
![f3](gambar/fuzz3.png)
4. Untuk mencari username dan password yang berhasil ditemukan attacker, dilakukan pencarian menggunakan fitur "Find a Packet" dengan icon kaca pembesar dan memasukkan string 302 Found.
![f4](gambar/fuzz4.png)
5. Dilakukan follow terhadap packet tersebut, dicari string 302 Found, dan ditemukan kredensial user yang berhasil digunakan attacker.
![f5](gambar/fuzz5.png)

**Jika dimasukan ke netcat maka akan ketemu flagnya**
![f6](gambar/fuzz6.png)

## 4. ATM or ATP or FTP
![atm](gambar/atm1.png)
<br/>
File : ftp.pcap
<br/>
Maksud soal : Kita diminta untuk mencari password yang berhasil didapatkan oleh hacker setelah melakukan bruteforce login ftp
<br />
**Cara pengerjaan:**
1. Memfilter ftp && frame contains " Login " artinya untuk mencari yang Login saja, kemudian resultnya hanya keluar 1 yang successful
![Atmm](gambar/atm2.png)
2. Kemudian klik Follow > TCP Stream, akan muncul seperti ini 
![atmmm](gambar/atm3.png)

**Jika dimasukan ke netcat maka akan ketemu flagnya**
![atmmm](gambar/atm4.png)

## 5. How Many Packets?
![many](gambar/many1.png)
<br/>
File : ftp.pcap
<br/>
Maksud soal : Kita diminta untuk menghitung total attempt login(bruteforce) yang dilakukan oleh hacker
<br />
**Cara pengerjaan:**
1. Memfilter ftp && frame contains " Login " artinya untuk mencari data yang pernah Login
![Atmm](gambar/atm2.png)
2. Kemudian di kanan bawah ada tulisan "Displayed : 934", artinya yang total attemp login adalah 934 kali
![manyy](gambar/many2.png)

**Jika dimasukan ke netcat maka akan ketemu flagnya**
![manyyy](gambar/many3.png)

## 6. Trace Him
![trace](gambar/trace.png)
<br/>
File : ftp.pcap
<br/>
Maksud soal : Kita diminta untuk mencari alamat IP Attacker
<br />
**Cara pengerjaan:**
1. Langsung dapat terlihat IP dari attackernya, yaitu 10.30.3.4, dibuktikan dengan permintaan untuk mengakses user adminJarkom kepada IP 10.15.40.20.
![trace1](gambar/trace1.png)

**Jika dimasukan ke netcat maka akan ketemu flagnya:**
![trace2](gambar/trace2.png)

## 7. Malwaew
![malwaew](gambar/malwaew.png)
<br/>
File : infected.zip
<br/>
Maksud soal : Diminta untuk menganalisis network traffic salah satu komputer yang terkena malware dan menemukannya
<br/>
**Cara pengerjaan:**
1. Pada folder infected, diberikan file keylog.txt. Kemudian membuka Edit -> Preferences -> Protocols -> TLS dan memasukkan file tadi ke dalam (Pre)-Master-Secret log filename.
![malwaew1](gambar/malwaew1.png)
2. Melakukan filter http dan ditemukan file mencurigakan, yaitu invest_20.dll
![malwaew2](gambar/malwaew2.png)
3. Download file dengan membuka File -> Export Objects -> HTTP
![malwaew3](gambar/malwaew3.png)
4. Mengecek informasi tentang file tersebut dengan command ```file invest_20.dll``` dan ditemukan bahwa file tersebut merupakan file executable
![malwaew4](gambar/malwaew4.png)
5. Mengecek hash SHA256 dari file tersebut
![malwaew5](gambar/malwaew5.png)

**Jika dimasukan ke netcat maka akan ketemu flagnya**
![malwaew6](gambar/malwaew6.png)

## 8. Malwleowleo
![wle](gambar/wleo.png)
<br/>
File : evidence.pcap
<br/>
Maksud soal : Kita diminta untuk mencari nama malware yang dikirim oleh attacker melalui ftp
<br />
**Cara pengerjaan:**
1. Memfilter ftp && saat scroll akan ada Request: STOR m4L1c10us_W4re.c
![wlee](gambar/wleo2.png)

**Jika dimasukan ke netcat maka akan ketemu flagnya**
![wleee](gambar/wleo1.png)

## 9. Whoami
![wh](gambar/wh.png)
<br/>
File : evidence.pcap
<br/>
Maksud soal : Kita diminta untuk menemukan identitas attacker
<br />
**Cara pengerjaan:**
1. Melakukan filter pada tcp dan ditemukan sebuah string unik pada stream ke-7.
![wh1](gambar/wh1.png)
2. Dilakukan decode pada string tersebut dalam base64 dan ditemukan nama seseorang.
![wh2](gambar/wh2.png)

**Jika dimasukan ke netcat maka akan ketemu flagnya:**
![wh3](gambar/wh3.png)

## 10. Secret
![6](gambar/secret1.png)
<br/>
File : evidence.pcap
<br/>
Maksud soal : Kita diminta untuk mencari file lainnya selain dari file malware
<br />
**Cara pengerjaan:**
1. Memfilter ftp-data
![7](gambar/secret2.png)
2. Klik yang STOR Mirza.jpg > File > Export Object > FTP-Data
![wkwkwk](gambar/secret5.png)
3. Kemudian Save gambarnya ke file
 ![8](gambar/secret3.png)
4. Saat dibuka gambarnya, akan muncul jawabannya :D
![wow](gambar/secret6.png)

**Jika dimasukan ke netcat maka akan ketemu flagnya:**
![4](gambar/secret4.png)
