# Redirection pada Linux
Command-line tools biasanya membaca input dari keyboard dan menampilkan output di layar — tetapi hal itu tidak selalu terjadi. Dengan rederection, kita dapat mengubah aliran data, sehingga command dan file dapat membaca data dari source yang berbeda atau menuliskannya ke tujuan lain.

<h3>Memahami Aliran Data Linux</h3>
Di Linux, aliran data merujuk pada tiga channel I/O standar yang dikenal sebagai standard input (stdin), standard output (stdout), dan standard error (stderr). Channel-channel ini mewakili cara data masuk atau keluar dari suatu program:


⦁ Stdin (Standard inut) adalah source input default untuk command dan memiliki deskriptor file 0. Ini mewakili data yang diterima command sebagai input, dan secara default, stdin terhubung dengan keyboard.

⦁ Stdout (Standard output) adalah tujuan output default untuk command dan memiliki deskriptor file 1. Ini mewakili output yang dihasilkan command yang ditampilkan di layar.

⦁ Stderr (Standard error) adalah channel untuk pesan error yang dihasilkan oleh command atau shell dan memiliki deskriptor file 2. Ia juga menampilkan pesan error di layar.

<h3> Menggunakan Redirection </h3>
Shell mengontrol input dan output command yang dijalankan dari atau ke file menggunakan simbol khusus. kita dapat menggunakan simbol kurang dari `<` dan simbol lebih besar dari `>` untuk memindahkan data antara command dan file. Simbol `>` mengirimkan output command ke file sebagai input, sementara `<` mengirimkan isi file ke program sebagai input.

Setiap simbol ini merupakan blok data yang memiliki dua deskriptor file, satu untuk membaca dan satu untuk menulis. Misalnya:

⦁ > : Sisi kiri membaca > sisi kanan menulis

⦁ < : Sisi kiri menulis < sisi kanan membaca

Bayangkan simbol < atau > sebagai penunjuk yang menunjukkan arah data dari file ke command, atau sebaliknya.

Saat berurusan dengan redirection secara interaktif dengan shell, selalu ingat syntax berikut:

⦁ command < file-input : membaca dari file-input

⦁ command > file-output : membuat/menimpa file-output

⦁ command >> file-output : menambahkan ke file-output


# Redricting Output
Pada bagian ini, kita akan melihat berbagai contoh redirecting standard output suatu proses ke dalam file

<h3>Menggunakan Operator Pengalihan Keluaran</h3>
Pertama kita buka Terminal. Setelah masuk, ketik perintah berikut:

```
$ echo “Why so serious?”
Why so serious?
```

Menampilkan teks sebagai output
Secara alami, output perintah echo ditampilkan di layar. Mengimplementasikan apa yang telah kita pelajari, kita gunakan simbol lebih besar (`>`) untuk redirect standard output ke file baru alih-alih layar:
```
$ echo “Why so serious?” > joker
```
Mengalihkan output echo ke “joker”
Command ini menggunakan simbol `>` agar shell menulis output langsung ke file `joker` tanpa mengisi layar Anda. pastikan dan periksa isi file baru ini:
```
$ cat joker
Why so serious?
```
Output yang diharapkan telah tersimpan dalam file. Hal lain yang perlu diingat adalah saat menggunakan output redirection operator, shell akan membuat file baru dengan nama file yang Anda tentukan. Namun, jika file sudah ada, shell akan menimpa file tersebut:
```
$ echo “Where is everyone?” > joker
```
Sekarang kita periksa isinya:
```
$ cat joker
Where is everyone?
```
Shell menghapus isi sebelumnya untuk menulis output baru. Ini adalah hal yang harus selalu di waspadai agar tidak secara tidak sengaja kehilangan data penting.

Salah satu trik hebat untuk membuat file adalah menggunakan output redirection tanpa command di operand kiri:
```
$ > batman
$ ls
```
Mengosongkan file, menampilkan daftar direktori
Command ini membuat file kosong karena tidak ada data yang perlu redirect.

Perlu diingat bahwa operator > sama dengan 1>, yang secara eksplisit menentukan deskriptor file stdout.

<h3>Menggunakan Append Rederiection Operator</h3>

Linux juga menyediakan operator untuk menghindari penghapusan isi file yang sudah ada saat redirecr output ke file tersebut. Dengan menggunakan simbol ganda lebih besar dari `>>` alih-alih satu simbol, shell akan menambahkan output ke file yang sudah ada tanpa menggantikannya.

Kita buat file quotes seperti berikut berikut:
```
$ echo " There's nothing you can't do if you try - Ishigami Senku." > quotes.txt
```
Selanjutnya, kita redirect output ke file tanpa kehilangan data sebelumnya:
```
$ echo “Science is Elegant. - Dr. X” >> quotes.txt 
$ cat quotes.txt 
There's nothing you can't do if you try - Ishigami Senku.
Science is Elegant. - Dr. X
```
Shell mempertahankan teks sebelumnya dan menambahkan teks baru. Operator ini juga akan membuat file baru jika tidak ada file dengan nama yang sama.

Kita bisa menggunakan append redirection (atau output redirection) untuk menulis langsung ke file tanpa menggunakan text editor. Untuk melakukan trik ini, Anda dapat menggunakan perintah cat dan operator `>>` seperti berikut:
```
$ cat >> quotes.txt
A good book is always good, no matter hpw many yu've already read it - Osamu Dazai.
```
Setelah selesai mengetik, tekan `ctrl+d` untuk keluar dari mode dan menyimpan file. 
```
$ cat quotes.txt
```
```
There's nothing you can't do if you try - Ishigami Senku.
Science is Elegant. - Dr. X
A good book is always good, no matter hpw many yu've already read it - Osamu Dazai.
```
Ini akan redirect standard output dari keyboard langsung ke file daripada ke layar.
