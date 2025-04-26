# Pendefinisian Data di MySQL

Pada bagian ini, kita akan mempelajari cara mendefinisikan dan mengatur struktur data di MySQL. Ini adalah langkah pertama yang penting sebelum kita mulai menyimpan dan mengelola data.

---

## DDL (Data Definition Language)

DDL adalah bahasa yang digunakan untuk **mendefinisikan dan mengubah struktur database**. Dengan DDL, kita bisa membuat, mengubah, dan menghapus objek-objek dalam database seperti tabel, index, dan schema.

### Perintah Dasar DDL

1. **`CREATE`**: Digunakan untuk membuat objek baru dalam database

   ```sql
   -- Membuat tabel baru bernama Mahasiswa
   CREATE TABLE Mahasiswa (
       NIM INT PRIMARY KEY,
       Nama VARCHAR(50),
       Jurusan VARCHAR(30)
   );
   ```

2. **`ALTER`**: Digunakan untuk mengubah struktur tabel yang sudah ada

   ```sql
   -- Menambahkan kolom baru ke tabel Mahasiswa
   ALTER TABLE Mahasiswa ADD COLUMN Alamat VARCHAR(100);
   
   -- Mengubah tipe data kolom yang sudah ada
   ALTER TABLE Mahasiswa MODIFY COLUMN Nama VARCHAR(100);
   ```

3. **`DROP`**: Digunakan untuk menghapus objek dari database

   ```sql
   -- Menghapus tabel Mahasiswa
   DROP TABLE Mahasiswa;
   ```

### Contoh kasus: Sistem Informasi Akademik

Mari kita bayangkan kita sedang membuat sistem informasi akademik untuk sebuah universitas. Kita perlu menyimpan data mahasiswa, mata kuliah, dan nilai. Berikut adalah contoh penggunaan DDL untuk kasus ini:

```sql
-- Membuat database untuk sistem akademik
CREATE DATABASE sistem_akademik;

-- Menggunakan database yang baru dibuat
USE sistem_akademik;

-- Membuat tabel untuk menyimpan data mahasiswa
CREATE TABLE mahasiswa (
    nim VARCHAR(10) PRIMARY KEY,
    nama VARCHAR(100),
    alamat TEXT,
    tanggal_lahir DATE,
    program_studi VARCHAR(50)
);

-- Membuat tabel untuk menyimpan data mata kuliah
CREATE TABLE mata_kuliah (
    kode_mk VARCHAR(10) PRIMARY KEY,
    nama_mk VARCHAR(100),
    sks INT,
    semester INT
);

-- Membuat tabel untuk menyimpan nilai mahasiswa
CREATE TABLE nilai (
    id_nilai INT AUTO_INCREMENT PRIMARY KEY,
    nim VARCHAR(10),
    kode_mk VARCHAR(10),
    nilai_angka DECIMAL(4,2),
    nilai_huruf CHAR(2),
    FOREIGN KEY (nim) REFERENCES mahasiswa(nim),
    FOREIGN KEY (kode_mk) REFERENCES mata_kuliah(kode_mk)
);
```

---

## Tipe Data di MySQL

### Untuk apa mengerti tipe data?

Memahami tipe data sangat penting karena:

1. **Efisiensi Penyimpanan**: Tipe data yang tepat menghemat ruang penyimpanan
2. **Validasi Data**: Memastikan data yang dimasukkan sesuai dengan yang diharapkan
3. **Kinerja**: Tipe data yang tepat dapat meningkatkan kecepatan query
4. **Integritas Data**: Mencegah kesalahan dalam penyimpanan data

Tipe data menentukan jenis nilai yang bisa disimpan dalam kolom tabel. Berikut adalah tipe data yang sering digunakan:

### Tipe Data Numerik

- **`INT`**: Untuk menyimpan bilangan bulat

  ```sql
  -- Contoh: Menyimpan jumlah mahasiswa dalam kelas
  jumlah_mahasiswa INT
  ```

- **`FLOAT`/`DOUBLE`**: Untuk menyimpan bilangan desimal

  ```sql
  -- Contoh: Menyimpan IPK mahasiswa
  ipk FLOAT(3,2)  -- 3 digit total, 2 digit di belakang koma
  ```

### Tipe Data Teks

- **`VARCHAR(n)`**: Untuk menyimpan teks dengan panjang maksimum n karakter

  ```sql
  -- Contoh: Menyimpan nama mahasiswa
  nama VARCHAR(100)
  ```

- **`TEXT`**: Untuk menyimpan teks panjang

  ```sql
  -- Contoh: Menyimpan deskripsi mata kuliah
  deskripsi TEXT
  ```

### Tipe Data Tanggal dan Waktu

- **`DATE`**: Untuk menyimpan tanggal (YYYY-MM-DD)

  ```sql
  -- Contoh: Menyimpan tanggal lahir mahasiswa
  tanggal_lahir DATE
  ```

- **`DATETIME`**: Untuk menyimpan tanggal dan waktu

  ```sql
  -- Contoh: Menyimpan waktu pendaftaran mata kuliah
  waktu_daftar DATETIME
  ```

### Tipe Data Lainnya

- **`BOOLEAN`**: Untuk menyimpan nilai benar/salah

  ```sql
  -- Contoh: Menandai status aktif mahasiswa
  status_aktif BOOLEAN
  ```

---

## Primary Key dan Foreign Key

### Primary Key

- Merupakan kolom yang menjadi **identitas unik** untuk setiap baris data
- Tidak boleh kosong (NULL) dan harus unik
- Biasanya digunakan untuk kolom seperti NIM, ID, atau nomor unik lainnya

#### Contoh kasus: Identifikasi Mahasiswa

Dalam sistem akademik, setiap mahasiswa harus memiliki identitas unik. NIM (Nomor Induk Mahasiswa) adalah pilihan yang tepat untuk primary key karena:

1. Setiap mahasiswa memiliki NIM yang berbeda
2. NIM tidak boleh kosong
3. NIM digunakan untuk mengidentifikasi mahasiswa dalam berbagai proses akademik

Contoh perintah:

```sql
CREATE TABLE mahasiswa (
    nim VARCHAR(10) PRIMARY KEY,
    nama VARCHAR(100),
    program_studi VARCHAR(50)
);
```

### Foreign Key

- Digunakan untuk **menghubungkan** satu tabel dengan tabel lainnya
- Memastikan data yang dimasukkan valid dan sesuai dengan data di tabel referensi

#### Contoh kasus: Relasi Mata Kuliah dan Nilai

Dalam sistem akademik, kita perlu menghubungkan data nilai dengan data mahasiswa dan mata kuliah. Foreign key memastikan bahwa:

1. Nilai hanya bisa dimasukkan untuk mahasiswa yang terdaftar
2. Nilai hanya bisa dimasukkan untuk mata kuliah yang ada
3. Data tetap konsisten antar tabel

Contoh perintah:

```sql
-- Tabel mata kuliah
CREATE TABLE mata_kuliah (
    kode_mk VARCHAR(10) PRIMARY KEY,
    nama_mk VARCHAR(100),
    sks INT
);

-- Tabel nilai dengan foreign key
CREATE TABLE nilai (
    id_nilai INT AUTO_INCREMENT PRIMARY KEY,
    nim VARCHAR(10),
    kode_mk VARCHAR(10),
    nilai_angka DECIMAL(4,2),
    FOREIGN KEY (nim) REFERENCES mahasiswa(nim),
    FOREIGN KEY (kode_mk) REFERENCES mata_kuliah(kode_mk)
);
```

---

## Indexing

### Contoh kasus: Pencarian Data Mahasiswa

Dalam sistem akademik, seringkali kita perlu mencari data mahasiswa berdasarkan nama atau NIM. Tanpa index, pencarian ini akan lambat terutama jika data mahasiswa sudah banyak (ribuan atau puluhan ribu).

Index membantu mempercepat pencarian dengan cara:

1. Membuat struktur data khusus untuk pencarian
2. Mengurangi jumlah data yang perlu diperiksa
3. Mempercepat operasi JOIN antar tabel

### Cara Membuat Index

```sql
-- Membuat index untuk pencarian berdasarkan nama
CREATE INDEX idx_nama_mahasiswa ON mahasiswa(nama);

-- Membuat index untuk pencarian berdasarkan NIM dan nama
CREATE INDEX idx_nim_nama ON mahasiswa(nim, nama);

-- Membuat index untuk pencarian nilai berdasarkan NIM dan kode mata kuliah
CREATE INDEX idx_nilai_mahasiswa ON nilai(nim, kode_mk);
```

### Index Otomatis

- Index otomatis dibuat ketika kita mendefinisikan:
  - `PRIMARY KEY`
  - `UNIQUE` constraint

### Kapan Menggunakan Index?

- Gunakan index untuk kolom yang sering digunakan dalam:
  - Pencarian (WHERE clause)
  - Pengurutan (ORDER BY)
  - Penggabungan tabel (JOIN)

---

## Best Practices

1. **Pemilihan Tipe Data**
   - Pilih tipe data yang paling sesuai dengan kebutuhan
   - Jangan menggunakan VARCHAR(255) untuk semua kolom teks
   - Gunakan INT untuk ID, bukan VARCHAR

2. **Penamaan**
   - Gunakan nama yang deskriptif dan konsisten
   - Hindari penggunaan spasi dalam nama tabel/kolom
   - Gunakan huruf kecil dan underscore untuk pemisah kata

3. **Primary Key**
   - Selalu gunakan primary key untuk setiap tabel
   - Gunakan tipe data yang sesuai (biasanya INT atau BIGINT)
   - Pertimbangkan menggunakan AUTO_INCREMENT untuk ID

4. **Foreign Key**
   - Selalu gunakan foreign key untuk menjaga integritas data
   - Pastikan tipe data foreign key sama dengan primary key yang direferensikan
