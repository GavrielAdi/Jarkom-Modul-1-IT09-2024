# Jarkom-Modul-1-IT09-2024

| Nama | NRP |
|---------|---------|
| Gavriel Pramuda Kurniaadi | 5027221031  |
| Stephanie Hebrina Mabunbun Simatupang | 5027221069  | 

## 1. Creds

![1](gambar/creds1.png)
<br/>
Maksud soal : Kita diminta untuk mencari Username FTP yang digunakan oleh attacker & Password FTP yang digunakan oleh attacker
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

## 3. Fuzz
![f](gambar/fuzz.png)

## 4. ATM or ATP or FTP
![atm](gambar/atm1.png)
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
Maksud soal : Kita diminta untuk mencari alamat IP Attacker
<br />

## 7. Malwaew

## 8. Malwleo
![wle](gambar/wleo.png)
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

## 10. Secret
![6](gambar/secret1.png)
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