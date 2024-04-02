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
![1](gambar/creds1.png)
<br/>
File : evidence.pcap
<br/>
Maksud soal : Kita diminta untuk mencari Username FTP yang digunakan oleh attacker & Password FTP yang digunakan oleh attacker. 
<br />
**Cara pengerjaan:**
1. Memfilter ftp && frame contains " Login " artinya untuk mencari yang Login saja, kemudian resultnya hanya keluar 1 yang succesfull
![dwa](gambar/creds2.png)
2. Kemudian klik Follow > TCP Stream, akan muncul seperti ini 
![hehe](gambar/creds3.png)
3. Kemudian akan muncul USER dan PASS nya
![hwhw](gambar/creds4.png)

**Jika dimasukan ke netcat maka akan ketemu flagnya**
![aokwaow](gambar/creds5.png)

## 2. Evidence
![ev](gambar/ev.png)
<br/>
File : challenge.pcapng
<br/>
Maksud soal : Kita diminta untuk mencari informasi tentang cara pelaku bisa masuk ke dalam perusahaan nanomate.
<br />
**Cara pengerjaan:**
1. Melakukan follow pada salah satu stream TCP dan didapatkan informasi mengenai domain dan web server korban.
![ev1](gambar/ev1.png)
2. Kemudian, dilakukan pencarian endpoint yang digunakan untuk login sebagai user biasa dengan melakukan filter http. Ditemukan ada banyak sekali endpoint ```/app/includes/process_login.php```, kemudian dicoba untuk submit dan jawabannya benar.
![ev2](gambar/ev2.png)
3. Terakhir, dilakukan pencarian email dan password yang berhasil digunakan untuk login sebagai user biasa. Dilakukan sorting dengan menekan kata "Info" untuk mempermudah pencarian email dan password pada "302 Found". Ditemukan juga ada kalimat menarik, yaitu Invalid Username or Password.
![ev3](gambar/ev3.png)
4. Dilakukan follow HTTP dan ditemukan ada kalimat Login Successful pada ```tcp.stream eq 1240``` sehingga berhasil ditemukan email dan passwordnya.
![ev4](gambar/ev4.png)

**Jika dimasukan ke netcat maka akan ketemu flagnya**
![ev5](gambar/ev5.png)

## 3. Fuzz
![f](gambar/fuzz.png)
<br/>
File : capture.pcap
<br/>
Maksud soal : Kita diminta untuk menganalisis network traffic ini untuk melacak attackernya
<br />
**Cara pengerjaan:**
1. 

## 4. ATM or ATP or FTP
![atm](gambar/atm1.png)
<br/>
File : ftp.pcap
<br/>
Maksud soal : Kita diminta untuk mencari password yang berhasil didapatkan oleh hacker setelah melakukan bruteforce login ftp
<br />
**Cara pengerjaan:**
1. Memfilter ftp && frame contains " Login " artinya untuk mencari yang Login saja, kemudian resultnya hanya keluar 1 yang succesfull
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
2. Download mirza.jpg
 ![8](gambar/secret3.png)

**Jika dimasukan ke netcat maka akan ketemu flagnya:**
![4](gambar/secret4.png)