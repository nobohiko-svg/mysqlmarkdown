# Pendahuluan

## Apa itu MySQL?

MySQL adalah sistem manajemen basis data (database management system) yang sangat populer di dunia. MySQL menggunakan bahasa SQL (Structured Query Language) untuk mengelola data. MySQL bersifat open-source, artinya bisa digunakan secara gratis dan memiliki komunitas yang besar.

Beberapa keunggulan MySQL:
- Mudah digunakan dan dipelajari
- Cepat dan efisien
- Bisa menangani data dalam jumlah besar
- Banyak digunakan di berbagai aplikasi web
- Mendukung berbagai sistem operasi (Windows, Linux, macOS)

## Tentang SQL

SQL (Structured Query Language) adalah bahasa pemrograman yang digunakan untuk mengelola dan memanipulasi data dalam database. SQL memungkinkan kita untuk:
- Membuat database dan tabel
- Menyimpan data
- Mengambil data
- Mengubah data
- Menghapus data

SQL menggunakan perintah-perintah yang mudah dipahami karena mirip dengan bahasa Inggris sehari-hari. Misalnya:
- `SELECT` untuk memilih data
- `INSERT` untuk menambah data
- `UPDATE` untuk mengubah data
- `DELETE` untuk menghapus data

## Apa itu DDL (Data Definition Language)?

DDL adalah bagian dari SQL yang digunakan untuk mendefinisikan struktur database. DDL digunakan untuk membuat, mengubah, dan menghapus objek-objek dalam database seperti tabel, indeks, dan view.

Contoh perintah DDL:

1. Membuat database:
```sql
CREATE DATABASE nama_database;
```

2. Membuat tabel:
```sql
CREATE TABLE mahasiswa (
    id INT PRIMARY KEY,
    nama VARCHAR(100),
    nim VARCHAR(20),
    jurusan VARCHAR(50)
);
```

3. Mengubah struktur tabel:
```sql
ALTER TABLE mahasiswa ADD COLUMN email VARCHAR(100);
```

4. Menghapus tabel:
```sql
DROP TABLE mahasiswa;
```

## Apa itu DML (Data Manipulation Language)?

DML adalah bagian dari SQL yang digunakan untuk memanipulasi data dalam tabel. DML memungkinkan kita untuk menambah, mengubah, mengambil, dan menghapus data.

Contoh perintah DML:

1. Menambah data:
```sql
INSERT INTO mahasiswa (id, nama, nim, jurusan)
VALUES (1, 'Budi Santoso', '2023001', 'Teknik Informatika');
```

2. Mengambil data:
```sql
SELECT * FROM mahasiswa;
SELECT nama, jurusan FROM mahasiswa WHERE id = 1;
```

3. Mengubah data:
```sql
UPDATE mahasiswa 
SET jurusan = 'Sistem Informasi' 
WHERE id = 1;
```

4. Menghapus data:
```sql
DELETE FROM mahasiswa WHERE id = 1;
```

Dengan memahami DDL dan DML, kita sudah memiliki dasar yang kuat untuk mulai bekerja dengan database MySQL. Pada bab-bab selanjutnya, kita akan mempelajari lebih detail tentang setiap perintah SQL dan cara menggunakannya secara efektif.