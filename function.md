# Manipulasi Data MySQL

Pada bagian ini, kita akan mempelajari cara mengelola data dalam database MySQL. Manipulasi data adalah kegiatan dasar yang sering dilakukan dalam pengelolaan database, seperti menambah, membaca, mengubah, dan menghapus data.

## Dasar-dasar Manipulasi Data (DML)

DML (Data Manipulation Language) adalah perintah-perintah SQL yang digunakan untuk mengelola data dalam tabel. Ada 4 operasi dasar yang dikenal dengan istilah CRUD:

1. **Create** (Membuat) - Menambahkan data baru
2. **Read** (Membaca) - Mengambil data
3. **Update** (Memperbarui) - Mengubah data
4. **Delete** (Menghapus) - Menghapus data

Mari kita pelajari satu per satu:

### 1. Menambahkan Data (INSERT)

Perintah `INSERT` digunakan untuk menambahkan data baru ke dalam tabel.

**Contoh Dasar:**

```sql
INSERT INTO Mahasiswa (NIM, Nama, Jurusan, IPK) 
VALUES (12345, 'Budi Santoso', 'Teknik Informatika', 3.75);
```

**Penjelasan:**

- `INSERT INTO` diikuti nama tabel
- Dalam kurung, sebutkan kolom-kolom yang akan diisi
- `VALUES` diikuti data yang akan dimasukkan

**Tips:**

- Pastikan urutan data sesuai dengan urutan kolom
- Data harus sesuai dengan tipe data kolom
- Jika kolom memiliki `NOT NULL`, data harus diisi

### 2. Membaca Data (SELECT)

Perintah `SELECT` digunakan untuk mengambil data dari tabel.

**Contoh Dasar:**

```sql
-- Mengambil semua kolom
SELECT * FROM Mahasiswa;

-- Mengambil kolom tertentu
SELECT Nama, IPK FROM Mahasiswa;

-- Mengambil dengan kondisi
SELECT * FROM Mahasiswa WHERE IPK > 3.5;
```

**Fitur Lanjutan SELECT:**

#### a. Filtering Data (WHERE)

```sql
-- Contoh sederhana
SELECT * FROM Mahasiswa WHERE Jurusan = 'Teknik Informatika';

-- Contoh dengan multiple kondisi
SELECT * FROM Mahasiswa 
WHERE IPK > 3.5 AND Jurusan = 'Sistem Informasi';
```

#### b. Pengurutan Data (ORDER BY)

```sql
-- Urutkan dari IPK tertinggi
SELECT * FROM Mahasiswa ORDER BY IPK DESC;

-- Urutkan berdasarkan multiple kolom
SELECT * FROM Mahasiswa 
ORDER BY Jurusan ASC, Nama ASC;
```

#### c. Membatasi Jumlah Data (LIMIT)

```sql
-- Ambil 5 data teratas
SELECT * FROM Mahasiswa ORDER BY IPK DESC LIMIT 5;

-- Untuk pagination (melewati 10 data, ambil 5 berikutnya)
SELECT * FROM Mahasiswa 
ORDER BY Nama LIMIT 5 OFFSET 10;
```

#### d. Pencarian dengan Pola (LIKE)

```sql
-- Cari nama yang diawali 'A'
SELECT * FROM Mahasiswa WHERE Nama LIKE 'A%';

-- Cari nama yang diakhiri 'i'
SELECT * FROM Mahasiswa WHERE Nama LIKE '%i';

-- Cari nama dengan 5 huruf, huruf ketiga 'd'
SELECT * FROM Mahasiswa WHERE Nama LIKE '__d__';
```

### 3. Memperbarui Data (UPDATE)

Perintah `UPDATE` digunakan untuk mengubah data yang sudah ada.

**Contoh:**

```sql
UPDATE Mahasiswa 
SET IPK = 3.85 
WHERE NIM = 12345;
```

**Penting:**

- Selalu gunakan `WHERE` untuk menentukan data mana yang akan diubah
- Tanpa `WHERE`, semua data dalam tabel akan diubah

### 4. Menghapus Data (DELETE)

Perintah `DELETE` digunakan untuk menghapus data dari tabel.

**Contoh:**

```sql
-- Hapus data spesifik
DELETE FROM Mahasiswa WHERE NIM = 12345;

-- Hapus semua data (hati-hati!)
DELETE FROM Mahasiswa;
```

**Catatan Penting:**

- `DELETE` tanpa `WHERE` akan menghapus semua data dalam tabel
- Untuk menghapus semua data dengan lebih cepat, bisa menggunakan `TRUNCATE TABLE`
- Data yang dihapus tidak bisa dikembalikan

## Best Practices dalam Manipulasi Data

1. **Backup Data**
   - Selalu backup data sebelum melakukan operasi besar
   - Gunakan `SELECT` untuk memeriksa data sebelum `DELETE` atau `UPDATE`

2. **Gunakan WHERE dengan Hati-hati**
   - Pastikan kondisi `WHERE` tepat
   - Uji dulu dengan `SELECT` sebelum `UPDATE` atau `DELETE`

3. **Perhatikan Tipe Data**
   - Pastikan data yang dimasukkan sesuai tipe data kolom
   - Gunakan tanda kutip untuk data string

4. **Optimalkan Query**
   - Gunakan `LIMIT` untuk membatasi jumlah data
   - Pilih kolom yang diperlukan saja, hindari `SELECT *`

## Latihan Praktis

Sebelum memulai latihan, buatlah tabel berikut terlebih dahulu:

```sql
CREATE TABLE Mahasiswa (
    NIM VARCHAR(10) PRIMARY KEY,
    Nama VARCHAR(100) NOT NULL,
    Jurusan VARCHAR(50) NOT NULL,
    IPK DECIMAL(3,2),
    Tanggal_Masuk DATE,
    Alamat TEXT
);
```

Coba praktikkan perintah-perintah berikut:

1. Tambahkan 3 data mahasiswa baru
2. Cari mahasiswa dengan IPK di atas 3.5
3. Update IPK mahasiswa tertentu
4. Hapus data mahasiswa yang sudah lulus

Ingat: Selalu backup data sebelum melakukan operasi yang berisiko!
