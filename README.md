# Jarkom-modul-1-C13-2021

## Crimping dan Wireshark

## Soal 1

Sebutkan webserver yang digunakan pada "ichimarumaru.tech"!

## Soal 2

Temukan paket dari web-web yang menggunakan basic authentication method!

**Filter** : `http.authbasic`

**Cara** :
1. Gunakan filter diatas untuk mencari paket
![image](https://user-images.githubusercontent.com/40484843/134595307-5b181014-e56e-4c29-b5ce-1d4103ecc368.png)
2. Ditemukan bahwa [basic.ichimarumaru.tech](http://basic.ichimarumaru.tech) menggunakan basic authentication

## Soal 3

Ikuti perintah di basic.ichimarumaru.tech! Username dan password bisa didapatkan dari file .pcapng!

**Filter** : `http.host contains "basic.ichimarumaru.tech"`

**Cara** :
1. Gunakan filter diatas untuk mencari paket
![image](https://user-images.githubusercontent.com/40484843/134595541-26bc7cfa-06d2-4be4-9fb2-13ffb100aa73.png)
2. Ditemukan ```username``` dan ```password``` untuk login ke [basic.ichimarumaru.tech](http://basic.ichimarumaru.tech)
3. Pada web tersebut ada perintah untuk menyebutkan urutan dari pengkalbelan ```T568A```
![image](https://user-images.githubusercontent.com/40484843/134596338-c4dd472b-73b5-4fb4-8a2a-e684e0c3d4a7.png)

```
Pengkabelan T568A :
Urutan ke 1 : Putih Hijau
Urutan ke 2 : Hijau
Urutan ke 3 : Putih Orange
Urutan ke 4 : Biru
Urutan ke 5 : Putih Biru
Urutan ke 6 : Orange
Urutan ke 7 : Putih Coklat
Urutan ke 8 : Coklat
```

**Note**:
- Sebenarnya paket yang ditemukan pada soal nomer 2 sudah mengandung ```username``` dan ```password``` pada bagian ```Authorization > credentials```

## Soal 4

Temukan paket mysql yang mengandung perintah query select!

## Soal 5

Login ke portal.ichimarumaru.tech kemudian ikuti perintahnya! Username dan password bisa didapat dari query insert pada table users dari file .pcap!.

**Filter** : `mysql.query contains "users"`

**Cara** :
1. Gunakan filter diatas untuk mencari paket
![image](https://user-images.githubusercontent.com/40484843/134596115-761a6302-3107-4d8c-8052-de0b6db4c8cb.png)
2. Ditemukan ```username``` dan ```password``` untuk login ke [portal.ichimarumaru.tech](http://portal.ichimarumaru.tech)
3. Pada web tersebut ada perintah untuk menyebutkan urutan dari pengkalbelan ```T568B```
![image](https://user-images.githubusercontent.com/40484843/134597047-d5d9f6fb-6ce4-4816-9c5d-03ec626d20c3.png)

```
Pengkabelan T568B :
Urutan ke 1 : Putih Orange
Urutan ke 2 : Orange
Urutan ke 3 : Putih Hijau
Urutan ke 4 : Biru
Urutan ke 5 : Putih Biru
Urutan ke 6 : Hijau
Urutan ke 7 : Putih Coklat
Urutan ke 8 : Coklat
```

## Soal 6

Cari username dan password ketika melakukan login ke FTP Server!

## Soal 7

Ada 500 file zip yang disimpan ke FTP Server dengan nama 0.zip, 1.zip, 2.zip, ..., 499.zip. Simpan dan Buka file pdf tersebut. (Hint = nama pdf-nya "Real.pdf")

## Soal 8

Cari paket yang menunjukan pengambilan file dari FTP tersebut!

## Soal 9

Dari paket-paket yang menuju FTP terdapat inidkasi penyimpanan beberapa file. Salah satunya adalah sebuah file berisi data rahasia dengan nama "secret.zip". Simpan dan buka file tersebut!

**Filter 1** : `ftp-data contains "secret.zip"`

**Filter 2** : `ftp-data contains "Wanted.zip"`

**Cara** :
1. Gunakan filter 1 diatas untuk mencari paket
![image](https://user-images.githubusercontent.com/40484843/134597382-2041012e-015c-42ba-b985-cb786bb3302e.png)
2. Memang pada awalnya memang belum ditemmukan paket yang berisi file `secret.zip` dan hanya ditemukan paket dengan file `history.txt`. Tapi didalamnya terdapat riwayat file yang di zip dan file itu bernama `Wanted.pdf`
![image](https://user-images.githubusercontent.com/40484843/134597759-eb9f5283-50f1-4809-887f-01732da07fb8.png)
3. Selanjutnya mencari dengan filter 2, dengan filter yang kedua ditemukan paket yang berisi `secret.zip`
![image](https://user-images.githubusercontent.com/40484843/134598058-1079484b-4718-4316-a316-8fca2e1a87ce.png)
4. Paket tersebut dapat tersimpan, tapi untuk meng-*extract* file didalamnya membutuhkan password
![image](https://user-images.githubusercontent.com/40484843/134598266-ad9df7dc-dcda-43f7-9bbf-daccbd45813c.png)

## Soal 10

Selain itu terdapat "history.txt" yang kemungkinan berisi history bash server tersebut! Gunakan isi dari "history.txt" untuk menemukan password untuk membuka file rahasia yang ada di "secret.zip"!

**Filter 1** : `frame contains "history.txt"`

**Filter 2** : `ftp-data`

**Cara** :
1. Gunakan filter 1 diatas untuk mencari paket berisi `history.txt`, walaupun file ini sudah ditemukan pada soal 9 sebelumnya
![image](https://user-images.githubusercontent.com/40484843/134598830-f3c8ce1d-c24f-4196-bb5a-7a0ae2572cd4.png)
2. Pada file ini dapat kita lihat bahwa password dari `secret.zip` adalah baris terakhir dari file `bukanapaapa.txt` dari perintah `key=$(tail -1 bukanapaapa.txt)`. Karena dengan filter yang spesifik file `bukanapaapa.txt` belum ditemukan, maka dari itu digunakan filter yang umum seperti pada filter 2 dan paket yang berisi file tersebut ditemukan.
![image](https://user-images.githubusercontent.com/40484843/134599157-912769a1-4053-4517-8ab1-34ece6aef936.png)
3. Dapat dilihat isi dari file `bukanapaapa.txt` yang merupakan password dari `secret.zip` adalah `d1b1langbukanapaapajugagapercaya`
4. Dan file `secret.zip` dapat di *extract* dan tampilan dari isinya sebagai berikut
![image](https://user-images.githubusercontent.com/40484843/134599513-f1345d31-2654-4901-a21f-ac82458d5520.png)


## Soal 11

Filter sehingga wireshark hanya mengambil paket yang berasal dari port 80!

## Soal 12

Filter sehingga wireshark hanya mengambil paket yang mengandung port 21!

## Soal 13

Filter sehingga wireshark hanya menampilkan paket yang menuju port 443!

## Soal 14

Filter sehingga wireshark hanya mengambil paket yang tujuannya ke kemenag.go.id!

## Soal 15

Filter sehingga wireshark hanya mengambil paket yang berasal dari ip kalian!
