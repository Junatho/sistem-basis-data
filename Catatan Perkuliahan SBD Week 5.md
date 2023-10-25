## 📘 SISTEM BASIS DATA

### 🗓️ Week 5: Intermediate to SQL (1)
### Asynchronous Class: 
- Pelajari slide untuk topik hari ini
- Kerjakan Discussion 5.1 dan Discussion 5.2

#### 📍 Discussion 5.1 
1. What is the difference between Natural Join and Inner Join? Give an example
of a case.
Secara hasil kedua teknik ini menghasilkan output yang sama, namun
hanya saja berbeda pada penulisan syntax, sehingga perbedaan utama dari
Natural Join dan Inner Join adalah dalam penggunaan Inner Join kita harus
bisa menentukan secara spesifik kolom dan kondisi, sedangkan Natural Join
akan menggabungkan dua tabel sesuai dengan nama attribute dan datatype
yang sama. Ada beberapa hal yang bisa membedakan Natural Join dan Inner
Join, seperti:
- Returned Records:
Pada Natural Join, apabila tidak ada kondisi yang ditentukan,
maka akan secara otomatis mencari atribut yang memiliki value yang
sama di kedua tabel. Sedangkan pada Inner Join, value yang dihasilkan
adalah value yang exist dan sama dalam kedua tabel sesuai dengan
kondisi pengecekannya.
- Syntax:
Natural Join = SELECT * FROM tabel1 NATURAL JOIN tabel2
Inner Join = SELECT * FROM tabel1 INNER JOIN tabel2 ON
tabel1.Nama_Kolom = tabel2.Nama_Kolom

- Left Join:
Teknik Left Join akan digunakan ketika kita ingin
menggabungkan tabel1 dengan kolom yang cocok di tabel2. Dengan
kata lain, tabel1 akan menjadi patokan dan akan memberi output yang
dicocokkan dengan tabel2. Sebagai contoh dibawah, kolom order_id
dan item di tabel orders akan menjadi output yang urutannya tidak
berubah, kemudian untuk mendapatkan kolom status, akan di cocokan
kolom customer_id di tabel orders dengan kolom customer di tabel
shippings.

- Right Join:
Teknik Right Join akan digunakan ketika kita ingin
menggabungkan tabel2 yang valuenya di cocokan dengan kolom di
tabel1. Dengan syntax ‘from orders right join shippings’ itu sama saja
dengan ‘from shippings left join orders’. Dengan contoh dibawah ini,
dikarenakan pada situs programmiz online compiler tidak menyediakan
fitur Right Join maka kita bisa menggunakan alternatif Left Join.
hasilnya tentu saja berbeda dengan hasil left join yang ada diatas,
karena kali ini yang menjadi patokan adalah tabel shippings sehingga
urutan pada kolom status tidak akan berubah. Bagian yang kosong
dikarenakan pada tabel shippings terpadat customer_id = 5 sedangkan
pada tabel orders tidak ada data mengenai customer_id yang bernilai 5.

- Full Join:
Teknik Full Join akan digunakan untuk menggabungkan semua
baris di kolom yang telah dipilih dengan SELECT yang kemudian akan
di cek kondisinya dengan ON. Dalam contoh di bawah, kolom
CustomerName pada tabel Customers memiliki 3 baris yang akan
digabungkan dengan semua baris yang ada pada kolom OrderID di
tabel Orders. OrderID = 10309 dengan CustomerID = 37 tidak ada
yang cocok dengan CustomerID di tabel Customers sehingga
outputnya akan NULL di kolom CustomerName. Begitu juga
sebaliknya dengan CustomerName = ‘Alfreds Futterkiste’
CustomerID = 1 di tabel Customers tidak ada yang cocok dengan
CustomerID di tabel Orders sehingga outputnya akan NULL di
kolom OrderID

#### 📍 Discussion 5.2
1. Views in SQL
- View definition and use. Definisi dan kegunaan View dalam sebuah SQL adalah hasil dari
sebuah query SQL yang disimpan dalam basis data sebagai objek yang
bersifat virtual. View adalah sebuah tabel virtual yang bisa digunakan
sama seperti tabel sebenarnya. View digunakan untuk
menyederhanakan sebuah kompleksitas pada sebuah query,
mengamankan sebuah data, dan bertujuan agar mempermudah
pengguna untuk memahami

- View expansion tidak biasa digunakan dalam konteks database
SQL. Tetapi, View Expansion ini dapat merujuk pada proses dimana
tampilan diperluas atau dipecah menjadi elemen penyusunnya saat
membuat kueri atau memanipulasi data. Hal ini biasanya
mempengaruhi perubahan sebuah kueri yang mempengaruhi tampilan
menjadi kueri secara eksplisit mereferensikan tabel dan kolom dasar
yang secara efektif dalam memperluas view.

- Update of view adalah sebuah pembaruan view, apakah view
bersifat updatable atau tidak. Tetapi update of view dapat melakukan
pembaharuan hanya pada view yang sederhana, seperti:
  Klausa from hanya memiliki satu relasi database
● Klausa select hanya berisi nama atribut relasi dan tidak memiliki
expressions atau pembeda apapun
● Setiap attribute yang tidak di list dalam klausa select akan di set
jadi null
● Query tidak memiliki group by atau having clause

2. Benefit of using views:
- Simplicity
Melalui views seseorang dapat mengambil data dari berbagai
tabel dan semuanya ditunjukkan lewat satu tabel saja.

- Readability
Sama halnya seperti yang di atas, seseorang dapat menggunakan
views untuk menunjukkan data dari berbagai tabel dengan hanya satu
tabel saja. Ini membuat orang lain yang membacanya dapat lebih paham
dengan satu tabel dibandingkan berbagai tabel sekaligus.

- Security and Maintainability
Views tergolong aman karena user dapat menentukan siapa yang
dapat menggunakan views dan siapa yang tidak. Orang yang diberikan
akses pada views juga tidak bisa mengubah data tabel asli, hanya user
yang dapat mengubahnya. Views juga dapat di-maintain dengan cukup
mudah tetapi apabila query yang ada terlalu banyak ataupun ketika
suatu query mengambil data dari banyak tabel maka maintainabilitynya tidak akan terjaga.

3. Limitation of using views
Meskipun views tergolong aman, masih ada resiko seperti terlihatnya
data yang bisa saja sensitif kepada orang yang diberikan akses. Orang tersebut
tidak bisa mengubah data tersebut tapi orang masih bisa melihat data yang
ditampilkan lewat views. Apabila data merupakan data sensitif maka orang
lain dapat melihat data tabel, meskipun tidak bisa mengubahnya. Karena itu
jika user tidak benar-benar mengamankan data yang ditampilkan lewat views
sehingga cukup rentan. Selain itu penggunaan INSERT, UPDATE, DELETE,
GROUP BY, dan sebagainya tidak selalu bisa dipakai. Contohnya; seseorang
tidak bisa menggunakan INSERT, UPDATE, dan DELETE jika views berada
dalam opsi read-only. Views memiliki keunggulannya sendiri tetapi masih
ada beberapa batasan yang perlu diketahui supaya views dapat digunakan
secara optimal oleh user
