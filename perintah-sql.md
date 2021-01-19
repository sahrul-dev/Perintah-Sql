# Perintah-Sql

========================================================================
Writer   : Lois-Chan     (`3`)/
code     : 1015_CH       (@.@)?
contributor : Lois Christian & Mohammad Sahrullah
username Github :
JackN1ght 
sahrl-dev
========================================================================
for your information "//" itu adalah filed komentar dan saya gunakan untuk memberi penjelasa pada setiap baris
========================================================================
Cd\
Cd\xampp\mysql\bin
mysql -u root
========================================================================
ERD(Entity Relationship Diagram)
========================================================================
Suatu model untuk menjalaskan hubungan antar data basus data berdasarkan objek-objek
dasar data yang mempunyai antar relasi

Ada 3 komponen:
1. Entitas
    merupakan objek yang mewakili sesuatu yang nyata dan dapat dibedakan dari
sesuatu yang lain.(simbol persegi panjang)
2. Atribut
    merupakan element yang berada di dalam atribut yang mendeskripsikan 
karakteristik entitas tersebut.(lambang elips)
3. Relasi/hubungan
    hubungan antara sejumlah entitas yang berasal dari himpunan entitas yang berbeda
========================================================================
Struktur Database
========================================================================
[COMMING SOON]'-')b
========================================================================
PERINTAH pada BASIS DATA
menggunakan CMD atau SQLyog
========================================================================
==>DDl (Data Definition Lenguage)
========================================================================
`CREATE DATABASE db_uks; //membuat database db_uks`

`SHOW DATABASES; //untuk menampilkan semua database`

`USE db_uks;` //untuk menggunakan database yang di pilih

`CREATE TABLE tb_pasien (nik INT NOT NULL,
	nama VARCHAR(100) NOT NULL,
	tgl_masuk DATE); //membuat tabel tb_pasien`

`SHOW TABLES;` //untuk menampilkan semua table di dalam database yang di pilih

`ALTER TABLE tb_pasien CHANGE nik id INT AUTO_INCREMENT;` //untuk mengubah nama, type, dan lainnya di field yang di pilih

`ALTER TABLE tb_pasien DROP tgl_masuk;` //untuk menghapus field dari tabel

`ALTER TABLE tb_pasien ADD tgl_masuk DATE;` //untuk menambah field  pada tabel

`DESC tb_pasien;` //untuk menampilkan bagian lebih detail dari table yang di pilih
========================================================================
==>yang (biasa) di isi setelah type data saat pembuatan tabel
========================================================================
`NOT NULL` //data wajib di isi dan tidak boleh kosong
`PRIMARY KEY` //kunci utama di tabel
`FOREIGN KEY` //kunci asing pada tabel yang di gunakan untuk menciptakan hubungan (relasi)
`AUTO_INCREMENT` //pembuatan angka unik yang di buat secara otomatis
========================================================================
==>DML (Data Manipulation Lenguage)
========================================================================
`INSERT INTO  tb_pasien VALUES ('','lois','2019/09/26');` //untuk memasukkan data ke dalam table yang di pilih

`SELECT * FROM tb_pasien;` //menampilkan semua data dari table yang di pilih

`UPDATE tb_pasien SET tgl_masuk='2019\03\13' where id=1;` //untuk mengubah data tgl masuk dengan id yang di tentukan

`DELETE FROM tb_pasien WHERE id=1;` //menghapus data dimana id yang bernama 1
========================================================================
==>WHERE
========================================================================
`SELECT nama,tgl_masuk` //memilih field
`FROM tb_pasien` //nama tabel
`WHERE nama LIKE 'a%'` //mencari nama
ORDER BY tgl_masuk //mengurutkan dari yang paling kecil
;
========================================================================
SELECT id,nama,tgl_masuk //memilih field
FROM tb_pasien  //nama tabel
WHERE id //memilih data id
BETWEEN '1' AND '20' //menampilkan data yang memiliki id di antara 1 dan 20
; 
========================================================================
==>Value
========================================================================
SELECT LEFT(alamat,5) //membaca dari sebelah kiri dengan banyak value 5
AS lokasi, //data sebelum di namai lokasi
nama,email,tgl_masuk //memilih field lainnya
FROM tb_pasieen; //nama tabel
========================================================================
SELECT RIGHT(alamat,5) //membaca dari sebelah kanan dengan banyak value 5
AS lokasi, //data sebelum dinamai lokasi
nama,email,tgl_masuk //memilih field lainnya
FROM tb_pasieen; //nama tabel
========================================================================
SELECT id, nama, //memilih
MID(alamat,1,4) AS jalan, //mengambil data alamat di kalimat ke 1 dengan banyak value 4 dan dinamai jalan
email,tgl_masuk //memilih field lain
FROM tb_pasieen; //nama tabel
========================================================================
==>penggabungan field
========================================================================
SELECT id,nama,email, //memilih field
CONCAT(alamat,", ",tgl_masuk) //menggabungkan field alamat dengan tgl_masuk dengan di beri jarak ", "
AS ttl //memberi nama concat dengan ttl
FROM tb_pasieen; //nama tabel
========================================================================
==>data tipe DATE
========================================================================
SELECT id,nama,email,alamat, //memilih field lainnya
DATE_FORMAT(tgl_masuk, '%d %M %Y') //mengubah format data tgl_masukkan menjadi lebih detail
AS tgl_masuk //data sebelum dinamai tgl_masuk
FROM tb_pasieen; //nama tabel
========================================================================
SELECT id,nama,email,alamat, //memilih field lainnya
YEAR(tgl_masuk)  //menampilkan data date dengan tahun nya saja
AS tgl_masuk //data sebelum dinamai tgl_masuk
FROM tb_pasieen; //nama tabel
========================================================================
==>COUNT
========================================================================
SELECT COUNT(*) //menghitung semua data
FROM tb_pasieen; //nama tabel
		//atau menghitung semua data yang berada di tabel tb_pasieen
========================================================================
SELECT COUNT(alamat)AS alamat //menghitung jumlah data alamat dan di beri nama alamat
FROM tb_pasieen //nama tabel
		//menghitung semua data alamat yang berada di tabel tb_pasieen
========================================================================
SELECT alamat, //memilih field
COUNT(alamat)AS alamat //menghitung jumlah data alamat dan di beri nama alamat
FROM tb_pasieen //nama tabel
GROUP BY alamat; //di filter berdasarkan nama alamat
		//menampilkan data alamat dari tabel tb_pasieen berdasarkan nama alamat nya
========================================================================
SELECT COUNT(DISTINCT alamat) AS alamat //menghitung beda nama alamat
FROM tb_pasieen; //nama tabel
		//menampilkan jumlah beda nama alamat yang ada di tabel tb_pasieen
========================================================================
UPDATE tb_pasieen //memilih nama tabel 
SET nama='lois' //mengubah isi field nama menjadi lois
WHERE nip IN (1,5,10) //memilih nip yang bernama 1, 5, dan 10
		//mengubah isi field nama menjadi lois dengan nip bernama 1, 5, dan 10 secara bersamaan
========================================================================
SELECT YEAR(CURDATE())-YEAR(tgl_masuk) AS tahun //menampilkan hasil dari pengurangan tahun sekarang dikurangi tgl_masuk
FROM tb_pasieen //nama tabel
========================================================================
SELECT tb_pasieen.`nip`,tb_pasieen.`nama`,tb_pasieen.`email`,tb_pasieen.`alamat`,DATE_FORMAT(tb_pasieen.`tgl_masuk`,'%d %M %Y') AS tanggal,
tb_orang_tua.`nama` AS nama_ortu,LEFT(tb_orang_tua.`no_hp`,12) AS no_ortu,tb_pembina.`nama` AS pembina
FROM tb_pasieen,tb_orang_tua,tb_pembina
WHERE tb_pasieen.`id`=tb_orang_tua.`id` AND tb_orang_tua.`peg_id`=tb_pembina.`peg_id`
ORDER BY tb_pasieen.`id`

SELECT tb_pasieen.`nip`,tb_pasieen.`nama`,tb_pasieen.`email`,tb_pasieen.`alamat`,DATE_FORMAT(tb_pasieen.`tgl_masuk`,'%d %M %Y') AS tanggal,
tb_orang_tua.`nama` AS nama_ortu,tb_orang_tua.`no_hp`
FROM tb_pasieen,tb_orang_tua
WHERE tb_pasieen.`id`=tb_orang_tua.`id`
AND tb_pasieen.`tgl_masuk`
BETWEEN '2001-01-01' AND '2003-01-01'
ORDER BY tb_pasieen.`nama`

SELECT tb_pasieen.`nip`,tb_pasieen.`nama`,tb_pasieen.`email`,tb_pasieen.`alamat`,DATE_FORMAT(tb_pasieen.`tgl_masuk`,'%d %M %Y') AS tanggal,
tb_orang_tua.`nama` AS nama_ortu,LEFT(tb_orang_tua.`no_hp`,12) AS no_ortu,tb_pembina.`nama` AS pembina,tb_pmr.`nama`AS perawat
FROM tb_pasieen,tb_orang_tua,tb_pembina,tb_pmr
WHERE tb_pasieen.`id`=tb_orang_tua.`id` AND tb_orang_tua.`peg_id`=tb_pembina.`peg_id` AND tb_pasieen.`nisn`=tb_pmr.`nisn`
ORDER BY tb_pasieen.`id`

SELECT tb_pasieen.`nip`,tb_pasieen.`nama`,tb_pasieen.`email`,tb_pasieen.`alamat`,DATE_FORMAT(tb_pasieen.`tgl_masuk`,'%d %M %Y') AS tanggal,
tb_orang_tua.`nama` AS nama_ortu,LEFT(tb_orang_tua.`no_hp`,12) AS no_ortu,tb_pembina.`nama` AS pembina,tb_pmr.`nama`AS perawat,tb_uks.`nama` AS UKS
FROM tb_pasieen,tb_orang_tua,tb_pembina,tb_pmr,tb_uks
WHERE tb_pasieen.`id`=tb_orang_tua.`id` AND tb_orang_tua.`peg_id`=tb_pembina.`peg_id` AND tb_pasieen.`nisn`=tb_pmr.`nisn` AND tb_pasieen.`k_uks`=tb_uks.`k_uks`
ORDER BY tb_pasieen.`id`

`SELECT tb_pasieen.`nip`,tb_pasieen.`nama`,tb_pasieen.`email`,tb_pasieen.`alamat`,DATE_FORMAT(tb_pasieen.`tgl_masuk`,'%d %M %Y') AS tanggal,
tb_orang_tua.`nama` AS nama_ortu,LEFT(tb_orang_tua.`no_hp`,12) AS no_ortu,tb_pembina.`nama` AS pembina,tb_pmr.`nama`AS perawat,tb_uks.`nama` AS UKS,tb_sekolah.`nama_sekolah` AS sekolah
FROM tb_pasieen,tb_orang_tua,tb_pembina,tb_pmr,tb_uks,tb_sekolah
WHERE tb_pasieen.`id`=tb_orang_tua.`id` AND tb_orang_tua.`peg_id`=tb_pembina.`peg_id` AND tb_pasieen.`nisn`=tb_pmr.`nisn` AND tb_pasieen.`k_uks`=tb_uks.`k_uks` AND tb_uks.`npsn`=tb_sekolah.`npsn`
ORDER BY tb_pasieen.`id``

========================================================================
==>penjelasan
========================================================================
LIKE atau '=' ???

LIKE dapat gunakan tanda '%' di variable nya
sedangkan
'=' tidak dapat menggunakan tanda '%' di variable nya
========================================================================
LIKE 'a' atau ='a' //mencari nama a
LIKE 'a%' //nama depan a
LIKE '%a' //nama belakang a
LIKE '%a%' //semua nama yang terdapat huruf a
========================================================================
ORDER BY nama //mengurutkan dari a ke z atau dari terbesar ke terkecil
ORDER BY nama ASC //mengurutkan dari a ke z atau dari terbesar ke terkecil
ORDER BY nama DESC //mengurutkan dari z ke a atau dari terkecil ke terbesar
========================================================================
BETWEEN 'A%' AND 'C%' //menampilkan data dari di awal A dan di akhiri data sebelum c
BETWEEN '1' AND '20' //menampilkan data yang memiliki id di antara 1 dan 20
========================================================================
COUNT digunakan untuk menghitung data yang ada di dalam tabel
macam macam count:
COUNT(....) = menghitung jumlah semua data
COUNT(DISTINCT .....) = menghitung beda nama data
for your information = "....." bisa diisi apa saja tergantung nama field anda
======================================================================== 
CURDATE() = tanggal, bulan, tahun saat ini
NOW() = date + time skrg
year() = memanggil tahun saja
month() = memanggil bulan saja
day() = memanggil hari saja
========================================================================
DUPLICATE
========================================================================
INSERT INTO siswa(id_siswa,nis,nama) VALUES(9,777,'soleh')
ON DUPLICATE KEY UPDATE nama='eh sudah ada'; //insert yang akan mengisi data jika data primary key tidak sama, dan akan mengupdate data jika data primaty key nya sama

========================================================================
view
========================================================================
CREATE VIEW joko AS SELECT nis,nama from siswa where nama like 'j%'; //membuat tabel view joko dengan query tabel siswa

SELECT * FROM joko; // memanggil tabel view joko

//table view jika melakukan query insert update dan delete table yang akan berubah adalah tabel utama nya (siswa jika di contoh)

========================================================================
union
========================================================================
select nis from siswa union select nama from siswa; //menampilkan row nis dan siswa dalam satu kolom

========================================================================
procedure
========================================================================
delimiter $$
create procedure isi_siswa(isi_nis int,isi_nama varchar(50))
begin
	insert into siswa set nis=isi_nis,nama=isi_nama;
end $$
delimiter ; //membuat procedure insert

call isi_siswa(1,'wulung'); //memanggil procedure

drop procedure isi_siswa //menghapus procedure isi_siswa
