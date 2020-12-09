<ul>
<li>mount img file ubuntu</li>
<pre>
parted Armbian_5.30_Orangepizero_Ubuntu_xenial_default_3.4.113.img
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) unit
Unit?  [compact]? B
(parted) print
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags:

Number  Start     End          Size         Type     File system  Flags
 1      4194304B  1484783615B  1480589312B  primary  ext4

(parted) ^C
mount -o loop, offset=4194304 Armbian_5.30_Orangepizero_Ubuntu_xenial_default_3.4.113.img /root/mount/

</pre>
<li>step by step install lede luci dan uboot</li>
<pre>
1.install firmware
tanpa password
kita download dulu firmware untuk device anda 
http://felexindo.mooo.com:81
saya pake local
192.168.1.20:81
kita sudah dapat firmwarenya
selanjutnya kita upload ke router
biar mudah menggunakan winscp
saya sudah ada win scp nya 
simpan firmware di folder /tmp
flash firmware clean
mtd -e firmware -r write fw.bin firmware
tunggu sabar
oke install firmware berhasil
kita coba ping 
ping suksess kita masuk ke langkah selanjutnya
setting internet cli wifi 
sebutsaja fdi wifi ap-sta
setelah firmware berhasil kita tidak di tanyakan password 
maka kita buat password dulu terserah anda
ketik 
passwd
2. setting fdi wifi ap-sta
ketik fdi
karakter sensitif perhatikan dengan jelas sebalum menulis
saya pakai FryzilliaZaqhira SSID nya
pilih nomer 3
ketik di router
block info -- untuk melihat terdeteksinya partisi
tunggu sampai connected
suksess
ping facebook.com
ping google.com
ping 8.8.8.8
jika ping domain dan ip berhasil kita bisa langsung tahap exroot
3. exroot
colok flash disk...
buat partisi
EXT4 dan LINUX SWAP
saya sudah buat partisi nya biar singkat waktu
colok kembali ke router flashdisk nya
kita akan membuat exroot di /dev/sda1 dengan partisi ext4
mulain exrootcara clean
mount /dev/sda1 /overlay  <-- putty
rm -rf /overlay/* <-- putty
umount /overlay  <-- putty
fdi  <-- putty
option 1
selesai exroot tapi jangan dulu install apapun kita cek dulu
jika sudah yakin exroot berhasilkita reboot router nya
ketik 
reboot
exroot suksessss
3. install luci
kita lanjut tahap install luci 
agar tidak ada masalah kita cek tahap2 ini
perhatikan
jika sesuai sama dengan di tampilkan kita bisa install luci
option 4
selesai install luci
kita buka browser
luci sudah muncul
suksess
4. wifi web setting cgi html
alternatif setting wifi lewat web
kita test dengan SSID yang sama
masih dalam tahap pengembangan maaf ada banyak bug di sini
mungkin kita kledepannya bikin webui biar lebih kumplit
harap sabar
sudah terkoneksi
skarang kita coba uboot mod pepe2k
5.uboot mod pepe2k
download binary uboot nya
hahaha inggrisnya ngaco
belsambung
semoga berkah amiiin
TEST UBOOT
sambunglan nya belum hehehe
uboot berhasil
terimakasih
</pre>
<li>
<a>important sed script</a>
</li>
<pre>
sed -e '/sip/ s/^#*/# /' -i test.txt
sed -E 's/( )+$//'

-------------------------------------------------- ----------------------- 
SITUS SATU-LINE BERGUNA UNTUK SED (editor arus Unix) 29 Desember 2005 
Disusun oleh Eric Pement - pemente di northpark [dot] edu versi 5.5 Versi 

terbaru dari berkas ini (dalam bahasa Inggris) biasanya di: 
   http://sed.sourceforge.net/sed1line.txt 
   http://www.pement.org/sed/sed1line.txt 

Berkas ini akan juga tersedia dalam bahasa lain: 
  Cina - http://sed.sourceforge.net/sed1line_zh-CN.html 
  Ceko - http://sed.sourceforge.net/sed1line_cz.html 
  Belanda - http://sed.sourceforge.net/ sed1line_nl.html  
  bahasa Prancis - http://sed.sourceforge.net/sed1line_fr.html
  bahasa Jerman - http://sed.sourceforge.net/sed1line_de.html 
  bahasa Italia - (tertunda)
  Portugis - http://sed.sourceforge.net/sed1line_pt-BR.html 
  Spanyol - (tertunda) 


FILE SPACE: 

 spasi ganda sebuah file 
 sed G 

 double space sebuah file yang sudah memiliki baris kosong di dalamnya. File keluaran 
 harus berisi tidak lebih dari satu baris kosong di antara baris teks. 
 Sed * / ^ $ / d; G ' 

 tiga spasi sebuah file 
 sed' G; G ' 

 undo double-spacing (anggap garis genap selalu kosong) 
 sed' n; d ' 

 masukkan baris kosong di atas setiap baris yang cocok dengan "regex" 
 sed '/ regex / {x; p; x;}' 
 sed '/ regex / {x; p ; x; G;} '

 sed '/ regex / G' 

 masukkan baris kosong di atas dan di bawah setiap baris yang sesuai dengan "regex" 


 nomor setiap baris file (simple left alignment). Dengan menggunakan tab (lihat 
 catatan pada '\ t' pada akhir file), bukan spasi yang akan menghemat margin. 
 sed = filename | sed 'N; s / \ n / \ t /' 

 nomor setiap baris dari sebuah file (angka di sebelah kiri, kanan-kanan) 
 sed = filename | sed 'N; s / ^ / /; s / * \ (. \ {6, \} \) \ n / \ 1 / ' 

 nomor setiap baris file, tapi hanya mencetak angka jika baris tidak kosong 
 sed' /./= 'filename | sed '/./N; s / \ n / / ' 

 count lines (mengemulasi "wc -l") 
 sed -n' $ = ' 
 
 echo 'first=url1, second=url2, third=url3' | sed 's/.*first=\([^ ]*\),.*/\1/'

KONVERSI TEKS DAN SUBSTITUSI: 

 DI LINGKUNGAN UNIX:
 sed 's /.$//' # mengasumsikan bahwa semua baris diakhiri dengan CR / LF 
 sed di bash / tcsh, tekan Ctrl-V lalu Ctrl-M
 Sed / \ x0D $ // '# bekerja pada ssed, gsed 3.02.80 atau lebih tinggi 

 IN UNIX ENVIRONMENT: convert Unix newlines (LF) ke format DOS. 
 sed "s / $ /` echo -e \\\ r` / "# baris perintah di bawah ksh 
 sed's / $ '" / `echo \\\ r` /" # baris perintah di bawah bash 
 sed "s / $ / `echo \\\ r` /" # baris perintah di bawah zsh 
 sed's / $ / \ r / '# gsed 3.02.80 atau lebih tinggi 

 DI LINGKUNGAN DOS: ubah format baris baru Unix (LF) ke format DOS. 
 sed "s / $ //" # method 1 
 sed -np # method 2 

 IN LINGKUNGAN DOS: ubah baris baru DOS (CR / LF) ke format Unix. 
 Hanya bisa dilakukan dengan UnxUtils sed, versi 4.0. 7 atau lebih tinggi. Itu 
 UnxUtils dapat diidentifikasi dengan tombol ubah "--text" ubah ubah menjadi 
 yang muncul saat Anda menggunakan tombol "--help". Jika tidak, mengubah 
 baris baru DOS ke baris baru Unix tidak dapat dilakukan dengan sed di lingkungan DOS 
 Gunakan "tr" sebagai gantinya. 
 sed "s / \ r //" infile> outfile # UnxUtils sed v4.0.7 atau lebih tinggi 
 tr -d \ r <infile> outfile # GNU tr versi 1.22 atau lebih tinggi 

 hapus spasi utama (spasi, tab) dari depan setiap baris 
 aligns all text flush left 
 seds / ^ [\ t] * // '# lihat catatan di' \ t 'pada akhir file 

 hapus spasi tambahan (spasi,
 sed / [\ t] * $ // '# lihat catatan di' \ t 'di akhir file 

 sed / ^ [\ t] * //; s / [\ t] * $ //' 

 masukkan 5 spasi kosong pada awal setiap baris (buat halaman offset) 
 sed / ^ / / ' 

 align all text flush right pada lebar 79 kolom 
 sed -e: a -e \ ^. \ {1, 78 \} $ / & /; ta '# set di 78 ditambah 1 spasi 

 pusatkan semua teks di tengah lebar 79 kolom. Dalam metode 1, 
 spasi pada awal baris adalah signifikan, dan trailing 
 spasi ditambahkan pada akhir baris. Dalam metode 2, spasi di 
 awal baris dibuang dalam memusatkan garis, dan 
 tidak ada spasi tambahan yang muncul di akhir baris. 
 sed -e: a -e \ ^. \ {1,77 \} $ / & /; ta '
 sed -e: a-^ / \. \ {1,77 \} $ / & /; ta '-e's / \ (* \) \ 1 / \ 1 /' # method 2 

 pengganti (temukan dan ganti) "foo" 
 sed's / foo / bar / '# menggantikan hanya 1 contoh di baris 
 sed' s / foo / bar / 4 '# menggantikan hanya instance ke 4 di baris 
 sed's / foo / bar / g' # menggantikan SEMUA contoh dalam baris 
 sed ' s / \ (. * \) foo \ (. * foo \) / \ 1bar \ 2 / '# ganti huruf berikutnya ke huruf terakhir 
 sed / \ (. * \) foo / \ 1bar /' # replace hanya kasus terakhir 

 ganti "foo" dengan "bar" HANYA untuk baris yang berisi "baz" 
 sed '/ baz / s / foo / bar / g' 

 substitute "foo" dengan "bar" KECUALI untuk baris yang berisi "baz " 
 sed '/ baz /! s / foo / bar / g'

 ganti "merah" atau "ruby" atau "puce" menjadi "merah" 
 sed / scarlet / red / g; s / ruby ​​/ red / g; s / puce / red / g '# paling seds 
 gsed 's / scarlet \ | ruby ​​\ | puce / red / g '# GNU sed only 

 urutan terbalik baris (mengemulasi "tac")
 bug / fitur di HHsed v1.5 menyebabkan baris kosong untuk dihapus 
 sed '1! G; h; $! d' # method 1 
 sed -n '1! G; h; $ p' # method 2 

 membalikkan setiap karakter di telepon (emulates "rev") 
 sed '/\n/!G;s/\(.\)\(.*\n\)/&\2\1/;//D;s/.// ' 

 Bergabunglah dengan pasangan baris berdampingan (seperti "tempel") 
 sed' $! N; s / \ n / / ' 

 jika sebuah garis berakhir dengan garis miring terbalik, tambahkan baris berikutnya ke dalamnya 
 sed -e: a -e '/ \\ $ / N; s / \\\ n //; ta ' 

 jika sebuah baris dimulai dengan tanda yang sama, tambahkan ke baris sebelumnya 
 dan ganti "=" dengan spasi tunggal 
 sed -e: a -e' $! N; s / \ n = / /; ta '-e' P; D ' 

 menambahkan koma ke string numerik, mengubah " 
 gsed ': a; s / \ B [0-9] \ {3 \} \> /, & /; ta' # GNU sed 
 sed -e: a / \ (. * [0-9] \) \ ([0-9] \ {3 \} \) / \ 1, \ 2 /; ta '# other seds 

 tambahkan koma ke angka dengan titik desimal dan tanda minus (GNU sed) 
 gsed -r ': a; s / (^ | [^ 0-9.]) ([0-9] +) ([0-9] {3}) / \ 1 \ 2, \ 3 / g; ta ' 

 tambahkan baris kosong setiap 5 baris (setelah baris 5, 10, 15, 20, dll.) 
 Gsed' 0 ~ 5G '# GNU sed only 
 sed' n; n; n; n; G; ' # other seds 

SELECTIVE PRINTING OF CERTAIN LINES: 

print first 10 lines of file (emulasikan perilaku "kepala") 
 sed 10q 

cetak baris pertama file (mengemulasikan "head -1"

cetak 10 baris terakhir dari sebuah file (mengemulasi "ekor") 

cetak 2 baris terakhir dari sebuah file (mengemulasikan "tail -2") 
 sed '$! N; $! D' 

cetak baris terakhir dari sebuah file (meniru 
 metode "tail -1") sed '$! d' # 1 metode 
 sed-n '$ p' # 2 

cetak baris berikutnya dari file 
 sed -e '$! {h; d;} '-ex # untuk file 1 baris, cetak baris kosong 
 sed -e' 1 {$ q;} '-e' $! {h; d;} '-ex # untuk file 1-baris, cetak line 
 sed -e '1 {$ d;}' -e '$! {h; d;}' -ex # untuk file 1-baris, tidak mencetak apa-apa 

hanya mencetak baris yang sesuai dengan ekspresi reguler (mengemulasi "grep") 
 sed -n '/ regexp / p'# metode 1 
 sed '/ regexp /! d' # method 2

 print only lines yang TIDAK cocok dengan regexp (mengemulasi 
 metode "grep -v") sed -n '/ regexp /! p' # 1, sesuai dengan metode 
 sed '/ regexp / d' # 2 di atas, sintaks sederhana 

 print baris segera sebelum regexp, tapi bukan baris 
 yang berisi regexp 
 sed -n '/ regexp / {g; 1! p;}; h' 

 cetak baris segera setelah regexp, tapi tidak baris 
 yang mengandung regexp 
 sed -n '/ regexp / {n; p;}' 

 print 1 baris konteks sebelum dan sesudah regexp, dengan nomor baris 
 menunjukkan di mana regexp terjadi (mirip dengan "grep -A1 -B1") 
 sed -n -e ' / regexp / {=; x; 1; p; g; $! N; p; D;} '-eh 

 grep untuk AAA dan BBB dan CCC (dalam urutan apapun) 
 sed' / AAA /! d; / BBB /! D; / CCC /! D ' 

 grep untuk AAA dan BBB dan CCC (dalam urutan itu) 
 sed' /AAA.*BBB.*CCC/!
 
 grep untuk AAA atau BBB atau CCC (mengemulasi "egrep") 
 sed -e '/ AAA / b' -e '/ BBB / b' -e '/ CCC / b' -ed # paling seds 
 gsed '/ AAA \ | BBB \ | CCC /! D' # GNU sed only 

 print paragraf jika berisi AAA (baris kosong paragraf terpisah) 
 HHsed v1.5 harus memasukkan 'G;' setelah 'x;' dalam 3 skrip berikutnya di bawah 
 sed -e '/./{H;$!d;}' -e 'x; / AAA /! d;' 

 paragraf cetak jika berisi AAA dan BBB dan CCC (dalam urutan apapun) 
 sed -e '/./{H;$!d;}' -e 'x; / AAA /! d; / BBB /! d; / CCC /! D '

 sed -e '/./{H;$!d;}' -e 'x; / AAA / b' -e '/ BBB / b' -e '/ CCC / b' -ed 
 gsed '/./ { H; $! D;}; x; / AAA \ | BBB \ | CCC / b; d '# GNU sed only 

 hanya mencetak baris dari 65 karakter atau lebih lama 
 sed -n' /^.\{65\}/p ' 

 sed -n' /^.\{65\}/!p '# method 1, sesuai dengan di atas 
 sed' /^.\{65\}/d '# method 2, sintaks sederhana 

 bagian cetak file dari biasanya ekspresi ke akhir file 
 sed -n '/ regexp /, $ p' 

 print bagian dari file berdasarkan nomor baris (baris 8-12, inklusif) 
 sed -n '8,12p' # method 1 
 sed '8,12! d '# method 2 

 print line number 52 
 sed -n' 52p '# metode 1 
 sed '52! d '# method 2 
 sed' 52q; d '# method 3, efisien pada file besar 

 mulai dari baris 3, cetak setiap baris ke 7 
 gsed -n' 3 ~ 7p ' # GNU sed hanya 
 sed-n '3, $ {p; n; n; n; n; n; n;}' # lainnya seds
 
 bagian cetak file antara dua ekspresi reguler (inklusif) 
 sed - n '/ Iowa /, / Montana / p' # case sensitive 

SELECTIVE DELETION OF CERTAIN LINES: 

 print semua file EXCEPT section antara 2 regular expressions 
 sed '/ Iowa /, / Montana / d' 

 hapus duplikat, baris berturut-turut dari file (mengemulasi "uniq"). 
 Baris pertama dalam satu set garis duplikat dijaga, sisanya akan dihapus. 
 sed '$! N; /^\(.*\)\n\1$/!P; D ' 

 menghapus duplikat, baris yang tidak berurutan dari sebuah file. Berhati-hatilah untuk tidak melakukannya
 meluap ukuran buffer dari ruang hold, atau menggunakan GNU sed. 
 sed -n 'G; s / \ n / && /; / ^ \ ([- ~] * \ n \). * \ n \ 1 / d; s / \ n //; h; P '

 sed '$! N; s / ^ \ (. * \) \ n \ 1 $ / \ 1 /; t; D ' 

 hapus 10 baris pertama dari file 
 sed' 1.10d ' 

 hapus baris terakhir dari file 
 sed' $ d ' 

 hapus 2 baris terakhir dari file 
 sed' N; $! P; $! D ; $ d ' 

 hapus 10 baris terakhir dari file 
 sed -e: a -e' $ d; N; 2,10ba '-e' P; D '# method 1 
 sed -n -e: a -e' 1.10! {P; N; D;}; N; ba '# method 2 

 hapus setiap baris 8 
 gsed' 0 ~ 8d '# GNU sed only 
 sed' n; n; n; n; n; n; n ; d; ' # other seds 


 hapus semua baris kosong dari sebuah file (sama seperti "grep '.'") 
 sed '/ ^ $ / d' # method 1 
 sed '/./!

 hapus semua baris kosong CONSECUTIVE dari file kecuali yang pertama; juga 
 menghapus semua baris kosong dari atas dan akhir file (mengemulasikan "cat -s") 
 sed '/./,/^$/!d' # method 1, memungkinkan 0 kosong di atas, 1 di EOF 
 sed '/ ^ $ / N; / \ n $ / D '# method 2, 

 beri 1 kosong di atas, 0 di EOF # hapus semua baris kosong CONSECUTIVE dari file kecuali yang pertama 2: 
 sed' / ^ $ / N; / \ n $ / N; // D ' 

 hapus semua baris kosong terkemuka di atas file 
 sed' /./,$!d ' 

 hapus semua baris kosong di akhir file  
 sed -e: a -e' / ^ \ n * $ / {$ d; N; ba '-e'} '
 sed -e: a -e' / ^ \ n * $ / N; / \ n $ / ba '# ditto, kecuali gsed 3.02. * 

 Hapus baris terakhir dari setiap paragraf 
 sed -n' /^$/{p;h;};/./{x;/. / p;} '


 remove nroff overstrikes (char, backspace) dari halaman manual. Perintah 'echo' 
 mungkin memerlukan switch -e jika Anda menggunakan Unix System V atau bash shell. 
 Sed "s /. `echo \\\ b` // g" # tanda kutip ganda yang dibutuhkan untuk lingkungan Unix 
 sed's /. ^ H // g '# di bash / tcsh, tekan Ctrl-V dan kemudian Ctrl-H 
 sed 's /. \ x08 // g' # hex expression untuk sed 1.5, GNU sed, ssed 

 dapatkan header pesan Usenet / e-mail 
 sed '/ ^ $ / q' # menghapus semuanya setelah baris kosong pertama 
 
 hapus # dapatkan Usenet / e -mail message body
 sed '1, / ^ $ / d '# menghapus semuanya sampai baris kosong pertama 

 mendapatkan header Subjek, tapi hapus "Subject:" bagian awal 
 sed' / ^ Subject: * /! d; s ///; q ' 

 mendapatkan header alamat pengirim
 sed '/ ^ Balas-Untuk: / q; / ^ Dari: / h; /./d;g;q ' 

 parse keluar alamat yang tepat. Menarik keluar alamat e-mail dengan sendirinya 
 dari header alamat 1-baris kembali (lihat skrip sebelumnya) 
 sed's / * (. *) //; s ^.*//; s /.* [: <] * // ' 

 tambahkan braket dan ruang sudut terkemuka ke setiap baris (kutip sebuah pesan) 
 sed / ^ /> /' 

 hapus braket dan ruang sudut terkemuka dari setiap baris (tanpa tanda kutip pesan) 
 sed / e> // ' 
 ekstrak binari uuencoded multi-bagian, hapus header asing 
 info, sehingga hanya bagian uuencoded yang tersisa. File yang dilewatkan ke 
 sed harus dilalui dengan urutan yang benar. Versi 1 bisa dimasukkan

 sed -e: a -e / <[^>] *> // g; / </ N; // ba '

 dari baris perintah; versi 2 bisa dibuat menjadi 
 skrip shell Unix yang dapat dieksekusi . (Diubah dari naskah oleh Rahul Dhesi.) Sed 
 '/ ^ end /, / ^ begin / d' file1 file2 ... fileX | uudecode # vers. 1 
 sed '/ ^ end /, / ^ begin / d' "$ @" | uudecode # vers. 2 

 sort paragraf dari abjad. Paragraf dipisahkan dengan 
 baris # kosong . GNU sed menggunakan \ v untuk tab vertikal, atau char unik apa pun yang akan dilakukan. 
 sed '/./{H;d;};x;s/\n/={NL}=/g' file | semacam | sed '1s / = {NL} = //; s / = {NL} = / \ n / g' 
 gsed '/./{H;d};x;y/\n/\v/' file | semacam | Sekarang kita 

 ganti file source dan 
 setting nama masing-masing file .ZIP ke basename dari file .TXT secara terpisah, hapus file source dan # setting masing-masing file .ZIP ke basename. 
 (di bawah DOS: "dir / b" switch mengembalikan nama file kosong di semua tutup). 
 echo @echo off> zipup.bat 
 dir / b * .txt | Jika 

menggunakan satu atau beberapa perintah pengeditan dan menerapkan semuanya 
, secara berurutan, ke setiap baris input Setelah semua perintah telah 
diterapkan ke jalur input pertama, baris tersebut adalah output dan 
jalur masukan kedua diambil untuk pemrosesan, dan siklus berulang. The 
contoh sebelumnya mengasumsikan bahwa masukan berasal dari standar input 
device (yaitu, konsol, biasanya ini akan disalurkan input). Satu atau
lebih banyak nama file bisa ditambahkan ke command line jika inputnya 
tidak berasal dari stdin. Output dikirim ke stdout (layar). Jadi: 

 nama file kucing | Sed '10q' # menggunakan input 
 penyisipan sed '10q' filename # efek yang sama, hindari file "cat" 
 sed '10q' filename> newfile # pengalihan output ke disk 
awk, 2nd Edition," oleh Dale Dougherty dan Arnold Robbins (O'Reilly, 
1997; http://www.ora.com), "UNIX Text Processing," oleh Dale Dougherty 
dan Tim O'Reilly (Hayden Books, 1987) atau tutorial oleh Mike Arst

Untuk petunjuk sintaks tambahan, termasuk cara untuk menerapkan 
perintah pengeditan dari file disk dan bukan baris perintah, berkonsultasilah "sed & 
distributed di U-SEDIT2.ZIP (banyak situs). Untuk memanfaatkan sepenuhnya kekuatan 
sed, seseorang harus mengerti" ekspresi reguler "Untuk ini, lihat 
" Menguasai Pernyataan Reguler "oleh Jeffrey Friedl (O'Reilly, 1997). 
Halaman manual (" man ") pada sistem Unix dapat membantu (coba" man 
sed "," man regexp " atau sub bagian pada ekspresi reguler dalam "man 
ed"), namun halaman manual sangat sulit, tidak ditulis untuk 
mengajarkan penggunaan atau regexps kepada pengguna pertama, namun sebagai teks referensi 
bagi mereka yang sudah mengenal alat ini.

QUOTING SYNTAX: Contoh sebelumnya menggunakan tanda kutip tunggal ('...')  
bukan tanda kutip ganda ("...") untuk menyertakan perintah pengeditan, karena
sed biasanya digunakan pada platform Unix. Tanda kutip tunggal mencegah 
shell Unix dari intrepreting tanda dolar ($) dan backquotes 
(`...`), yang diperluas oleh shell jika disertakan dalam 
tanda kutip ganda. Pengguna shell "csh" dan turunannya juga perlu 
mengutip tanda seru (!) Dengan tanda garis miring terbalik (yaitu, \!) Untuk 
menjalankan contoh-contoh yang tercantum di atas dengan benar, bahkan dalam tanda kutip tunggal. 
Versi sed ditulis untuk DOS selalu memerlukan tanda kutip ganda 
("...") bukan tanda kutip tunggal untuk melampirkan perintah pengeditan. 

PENGGUNAAN '\ t' DALAM SED SCRIPTS: Untuk kejelasan dalam dokumentasi, kami telah menggunakan
ekspresi '\ t' untuk menunjukkan karakter tab (0x09) pada skrip. 
Namun, sebagian besar versi sed tidak mengenali singkatan '\ t'
Jadi saat mengetik skrip ini dari command line, Anda harus menekan 
tombol TAB sebagai gantinya. '\ t' didukung sebagai ekspresi reguler 
metacharacter di awk, perl, dan HHsed, sedmod, dan GNU sed v3.02.80. 

VERSIONS OF SED: Versi sed berbeda, dan beberapa 
variasi sintaksis sedikit yang diharapkan. Secara khusus, sebagian besar tidak mendukung 
penggunaan label (: nama) atau instruksi cabang (b, t) dalam 
perintah pengeditan , kecuali pada akhir perintah tersebut. Kami telah menggunakan sintaks 
yang akan portabel untuk sebagian besar pengguna sed, meskipun 
versi GNU yang populer memungkinkan sintaks yang lebih ringkas. Saat pembaca melihat 
perintah yang cukup panjang seperti ini: 

   sed -e '/ AAA / b' -e '/ BBB / b' -e '/ CCC / b' -sini 

menggembirakan untuk mengetahui bahwa GNU sed akan membiarkan Anda menguranginya menjadi: 

   sed '/ AAA / b; / BBB / b; / CCC / b; d' # atau bahkan 
   sed '
 
Selain itu, ingatlah bahwa meski banyak versi sed menerima perintah 
seperti "/ one / s / RE1 / RE2 /", beberapa TIDAK mengizinkan "/ one /! s / RE1 / RE2 /", yang 
berisi spasi sebelum 's'. Abaikan ruang saat mengetik perintah. 

OPTIMIZING FOR SPEED: Jika kecepatan eksekusi perlu ditingkatkan (karena 
file input besar atau prosesor lambat atau hard disk), substitusi akan 
dieksekusi lebih cepat jika "find" 
ekspresi ditentukan sebelum memberikan instruksi "s / .../.../". Demikian:

   Sed 's / foo / bar / g' filename # standard ganti perintah 
   sed '/ foo / s / foo / bar / g' filename # mengeksekusi lebih cepat 
   sed '/ foo / s // bar / g' filename # shorthand sed syntax 

Pada seleksi atau penghapusan garis di mana Anda hanya perlu mengeluarkan baris 
dari bagian pertama file, perintah "berhenti" (q) dalam skrip 
akan mengurangi waktu pemrosesan file besar secara drastis. Jadi: 

   sed -n '45, 50p 'filename # print line nos. 45-50 dari file 
   sed -n '51q; 45,50p' filename # sama, tapi dijalankan lebih cepat 
-------------------------------------------------- -----------------------
</pre>
<li>
<a>makefile compile</a>
</li>
<pre>
compile:
	CC="$(CC)" CFLAGS="-Os -pipe -mips32r2 -mtune=mips32r2" shc -r -B -f fdi.sh
	CC="$(CC)" CFLAGS="-Os -pipe -mips32r2 -mtune=mips32r2" shc -r -B -f html

	mv fdi.sh.x fdi && mv html.x html && rm *.x.c

clean:

	rm -rf *.x *.c *.o *.c fdi html
</pre>
<li>
<a>compile bash script makefile<>	
</li>
<pre>
include $(TOPDIR)/rules.mk

PKG_NAME:=fdi
PKG_RELEASE:=1.0.2

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)
PKG_INSTALL_DIR:=$(PKG_BUILD_DIR)/ipkg-install

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define Package/fdi
  SECTION:=shcbash
  CATEGORY:=shc bash
  SUBMENU :=fdi
  TITLE:=shc script
  DEPENDS :=
endef

define Package/fdi/description
	shc bash compile
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS)
endef

define Package/fdi/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/www/cgi-bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/fdi $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/html $(1)/www/cgi-bin/
endef

$(eval $(call BuildPackage,fdi))
</pre>
<li>
<a>makefile include lib and cmake</a>
</li>
<pre>
include $(TOPDIR)/rules.mk

PKG_NAME:=tun2socks
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)
PKG_INSTALL_DIR:=$(PKG_BUILD_DIR)/ipkg-install

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define Package/tun2socks
	SECTION:=tun2socks
	CATEGORY:=WRTnode
	SUBMENU :=opencv_script
	TITLE:=opencv socket
	DEPENDS :=
endef

define Package/tun2socks/description
	opencv trough TCP/IP program for opencv lib
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)/build
	mkdir -p $(PKG_BUILD_DIR)/build
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	cd $(PKG_BUILD_DIR)/build
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		CFLAGS="$(TARGET_CFLAGS)"
endef

define Package/tun2socks/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/build/tun2socks $(1)/usr/bin/
endef

$(eval $(call BuildPackage,tun2socks))
</pre>
<li>
<a>default /etc/hosts</a>
</li>
<pre>
127.0.0.1 localhost
::1       localhost localhost6 ip6-localhost
#
# Some programs look for these and nice to have in logs
#
fe00::    ip6-localnet
ff00::    ip6-mcastprefix
ff02::1   ip6-allnodes
ff02::2   ip6-allrouters
ff02::3   ip6-allhosts
</pre>
</ul>
