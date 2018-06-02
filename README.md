# untungtanujaya.github.io

## GIFCompression
Graphics Interchange Format (GIF) adalah format grafis yang sering digunakan untuk keperluan desain situs web. GIF memiliki kombinasi warna lebih sedikit dibanding JPEG, tetapi mampu menyimpan grafis dengan latar belakang (background) transparan ataupun dalam bentuk animasi sederhana.

## Bagaimana GIF Dikompresi ?
GIF diformat dengan kompresi algoritme LZW (Lempel Zev Welch) yang dimiliki oleh Unisys. Pemegang hak cipta GIF kini dipegang oleh CompuServe Incorporated. Awalnya GIF bebas royalti bagi semua pengguna namun tahun 1995. Unisys memutuskan menarik royalti pada vendor pengguna GIF.

## Penjelasan algoritma Lempel–Ziv–Welch
### Definisi
Algoritma LZW dikembangkan dari metode kompresi yang dibuat oleh Ziv dan Lempel pada tahun 1977. Algoritma ini melakukan kompresi dengan menggunakan dictionary, di mana fragmen-fragmen teks digantikan dengan indeks yang diperoleh dari sebuah “kamus”. Prinsip sejenis juga digunakan dalam kode Braille, di mana kode-kode khusus digunakan untuk merepresentasikan kata-kata yang ada. Pendekatan ini bersifat adaptif dan efektif karena banyak karakter dapat dikodekan dengan mengacu pada string yang telah muncul sebelumnya dalam teks. Prinsip kompresi tercapai jika referensi dalam bentuk pointer dapat disimpan dalam jumlah bit yang lebih sedikit dibandingkan string aslinya.

### Algoritma
Algoritma Lempel-Ziv-Welch untuk melakukan kompresi adalah sebagai berikut:

1. Dictionary diinisialisasi dengan semua karakter dasar yang ada, dan P adalah kosong. 
2. C diisi dengan karakter selanjutnya di dalam teks
3. Apakah string P+C terdapat dalam dictionary ?
  •	Jika ada, maka P = P+C
  •	Jika tidak, maka :
    i. output P ke stream karakter
    ii. Tambahkan string P+C ke dalam dictionary
    iii. P diisi dengan C
4. Apakah terdapat kode lagi di stream kode ?
  •	Jika ya, maka kembali ke langkah 2.
  •	Jika tidak, maka terminasi proses (stop).

Tentunya algoritma ini juga memiliki cara untuk melakukan decoding suatu string yang telah dikompresi. Berikut adalah algoritma untuk decoding:

1. Dictionary diinisialisasi dengan semua karakter dasar yang ada
2. cW diisi dengan kode kata pertama
3. output string.cW ke stream karakter
4. pW = cW
5. cW = kode kata selanjutnya
6. Apakah string.cW ada di dalam dictionary?
  • Jika ada:
    i. output string.cW ke stream karakter
    ii. P = string.pW
    iii. C = karakter pertama dari string.cW
    iv. tambahkan string P+C ke dalam dictionary
  • Jika tidak:
    i. P = string.pW
    ii. C = karakter pertama string.pW
    iii. output string P+C ke stream karakter dan tambahkan ke dictionary (berkorespondensi dengan cW)
7. Apakah masih ada kode kata dalam stream kode?
  • Jika masih ada, ulangi langkah 4
  • Jika tidak, STOP.

## Contoh Algoritma
Algoritma ini akan lebih dipahami bila disertai dengan contoh. Sebagai contoh, akan dilakukan kompresi terhadap string *wabbawabba*. Misalkan hanya terdapat tiga huruf pada komputer ini yaitu a, b, dan w dan setiap huruf berkorespondensi dengan indeks pada dictionary berikut.

Indeks | Dictionary
-------|-----------
1 | a
2 | b
3 | w

Selanjutnya P tidak berisi apa-apa, dan C diisi dengan karakter pertama pada string yaitu w. Karena P+C = w ada di dalam kamus, maka P diisi dengan w. Selanjutnya C diisi dengan karakter kedua yaitu a, dan P+C = wa tidak ada dalam Dictionary, sehingga wa ditambahkan ke dalam dictionary dan dilakukan output ke stream karakter dengan indeks yang berpasangan dengan kata P pada dictionary tersebut. Berikut adalah tabel untuk setiap iterasi yang dilakukan dengan algoritma kompresi LZW ini.

No | P | C | P+C | output | Dictionary (Index) Baru
---|---|---|-----|--------|------------------------
1 | - | w | w | - | -
2 | w | a | wa | 3 | wa (4)
3 | a | b | ab | 1 | ab (5)
4 | b | b | bb | 2 | bb (6)
5 | b | a | ba | 2 | ba (7)
6 | a | w | aw | 1 | aw (8)
7 | w | a | wa | - | -
8 | wa | b | wab | 4 | wab (9)
9 | b | b | bb | - | -
10 | bb | a | bba | 6 | bba (10)
11 | a | - | a | 1 | -

Maka kode tersebut terkompresi menjadi kode 31221461 dengan dictionary yang dihasilkan adalah sebagai berikut:

Indeks | Dictionary
-------|-----------
1 | a
2 | b
3 | w
4 | wa
5 | ab
6 | bb
7 | ba
8 | aw
9 | wab
10 | bba

Selanjutnya untuk melakukan decoding dari 31221461 menjadi kata wabbawabba adalah sebagai berikut:
Pertama dictionary akan dinisiasi dengan huruf-huruf yang ada pada karakter yang masih dalam batasan.

Indeks | Dictionary
-------|-----------
1 | a
2 | b
3 | w

pW awalnya kosong, dan cW diisi dengan 3. string.cW akan berisi w sehingga dilakukan output ke stream karakter dengan w. Kemudian pW diisi dengan cW, dan cW diisi dengan kode selanjutnya yaitu 1, ... (akan dilanjutkan)

Umumnya indeks yang ditambahkan pada dictionary yang merupakan kombinasi dari dua atau lebih karakter adalah di atas range bit pada karakter yang ada. Misalkan untuk string yang memiliki karakter 8-bit, maka indeks untuk kombinasi dua atau lebih karakter akan dimulai dari 256, karena bit 0 – 255 sudah dipakai untuk melambangkan karakter yang sudah ada.

## Daftar Pustaka
https://www.w3.org/Graphics/GIF/spec-gif87.txt

https://www.youtube.com/watch?v=rZ-JRCPv_O8

Bonnie Soeherman (2008). *Photoshop for Abusement*. Elex Media Komputindo. ISBN 978-979-27-3058-6.

Pupung Budi Purnama (2004). *Kiat Praktis Menjadi Desainer Web Profesional*. Elex Media Komputindo. ISBN 979-20-5763-3.

-------
Dibuat oleh:

**13516133** Teresa (Algoritma LZW, Membuat Laporan)

**13516135** Untung Tanujaya (GIF, Membuat Github Pages)
