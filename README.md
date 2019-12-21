# Menggunakan driver database bawaan pada PHP7

## Awalan

Fungsi ```mysql_connect``` tidak bisa digunakan dimulai dari PHP7, PHP7 menyediakan `mysqli_connect` atau `PDO` untuk mengkoneksikan ke database mysql.
Sebelum memakai driver mysql menggunakan PDO anda harus mengaktifkan ekstensi `pdo_mysql` pada konfigurasi `php.ini`, lokasi file tersebut ada di dalam folder software PHP yang diinstall & digunakan.
Jika anda menggunakan hosting salah satunya seperti 000webhost, bisa langsung menuju langkah selanjutnya.

## Cara membuat koneksi database mysql menggunakan driver PDO

```php
  // konfigurasi database
  $host = 'localhost';
  $db = 'nama database';
  $user = 'user database';
  $password = 'password database';

  $db = new PDO("mysql:host=${host};dbname=${db}", $user, $password);
```

## Cara mengambil data menggunakan driver PDO

Untuk mengambil data, harus menggunakan prepared statement untuk menghindari [SQL Injection](https://socs.binus.ac.id/2018/12/13/pengenalan-sql-injection/), prepared statement bisa digunakan dengan koneksi PDO dengan nama metode `prepare` 

```php
  $statement = $db->prepare('SELECT username, password, nama FROM pengguna WHERE username = :username');
  $statement->bindParam(':username', $username);
  $statement->execute();

  // contoh mengambil satu data
  $row = $statement->fetch(PDO::FETCH_ASSOC);
  $row['nama'] // mengambil data nama dari user

  // contoh mengambil semua data sekaligus
  $rows = $statement->fetchAll(PDO::FETCH_ASSOC);
  $rows[0]['nama'] // mengambil nama dari data pertama 

```
Untuk parameter dari metode fetch / fetchAll bisa dilihat di [dokumentasi fetch](https://www.php.net/manual/en/pdostatement.fetch.php)
