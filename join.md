# Penggabungan Tabel (JOIN) di MySQL

## 🎯 Pengenalan

Dalam database relasional seperti MySQL, data seringkali tersebar di beberapa tabel yang saling berhubungan. JOIN adalah salah satu fitur terpenting dalam SQL yang memungkinkan kita untuk menggabungkan data dari beberapa tabel berdasarkan hubungan (relasi) antar tabel tersebut.

### Mengapa Perlu JOIN?

1. **Efisiensi Penyimpanan**: Data disimpan secara terpisah untuk menghindari duplikasi
2. **Integritas Data**: Memastikan data tetap konsisten antar tabel
3. **Fleksibilitas**: Memungkinkan pengambilan data dari berbagai tabel sekaligus

---

## 🔗 Konsep Dasar Relasi Tabel

### Primary Key dan Foreign Key

- **Primary Key (PK)**: Kolom unik yang menjadi identitas utama sebuah tabel
- **Foreign Key (FK)**: Kolom yang merujuk ke Primary Key tabel lain

### Contoh Relasi Sederhana

```shell
Tabel Mahasiswa
+--------+--------+-------------+
| NIM (PK)| Nama   | KodeJurusan |
+--------+--------+-------------+
| 123    | Budi   | IF         |
| 124    | Ani    | SI         |
+--------+--------+-------------+

Tabel Jurusan
+-------------+-------------+
| KodeJurusan | NamaJurusan |
+-------------+-------------+
| IF         | Informatika |
| SI         | Sistem Info |
+-------------+-------------+
```

## 📊 Jenis-Jenis JOIN

### Overview JOIN Types

Diagram di bawah ini menunjukkan perbedaan utama antara berbagai jenis JOIN dalam MySQL. Setiap jenis JOIN memiliki cara yang berbeda dalam menggabungkan data dari dua tabel:

- **INNER JOIN**: Hanya mengambil data yang cocok di kedua tabel
- **LEFT JOIN**: Mengambil semua data dari tabel kiri dan data yang cocok dari tabel kanan
- **RIGHT JOIN**: Mengambil semua data dari tabel kanan dan data yang cocok dari tabel kiri
- **FULL JOIN**: Mengambil semua data dari kedua tabel (tidak langsung didukung di MySQL)

![Diagram JOIN Types](https://bigtechinterviews.com/wp-content/uploads/2024/03/image-7-1024x824.png)

### 1. INNER JOIN

- **Penjelasan**: Mengambil data yang memiliki kecocokan di kedua tabel
- **Kapan Digunakan**: Ketika kita hanya membutuhkan data yang memiliki relasi di kedua tabel
- **Contoh Query**:

  ```sql
  SELECT Mahasiswa.Nama, Jurusan.NamaJurusan 
  FROM Mahasiswa 
  INNER JOIN Jurusan 
  ON Mahasiswa.KodeJurusan = Jurusan.KodeJurusan;
  ```

### 2. LEFT JOIN (LEFT OUTER JOIN)

- **Penjelasan**: Mengambil semua data dari tabel kiri, dan data yang cocok dari tabel kanan
- **Kapan Digunakan**: Ketika kita ingin melihat semua data dari tabel utama, meskipun tidak ada relasi di tabel kedua
- **Contoh Query**:

  ```sql
  SELECT Mahasiswa.Nama, Jurusan.NamaJurusan 
  FROM Mahasiswa 
  LEFT JOIN Jurusan 
  ON Mahasiswa.KodeJurusan = Jurusan.KodeJurusan;
  ```

### 3. RIGHT JOIN (RIGHT OUTER JOIN)

- **Penjelasan**: Mengambil semua data dari tabel kanan, dan data yang cocok dari tabel kiri
- **Kapan Digunakan**: Ketika kita ingin melihat semua data dari tabel referensi
- **Contoh Query**:

  ```sql
  SELECT Mahasiswa.Nama, Jurusan.NamaJurusan 
  FROM Mahasiswa 
  RIGHT JOIN Jurusan 
  ON Mahasiswa.KodeJurusan = Jurusan.KodeJurusan;
  ```

### 4. FULL JOIN (FULL OUTER JOIN)

- **Penjelasan**: Mengambil semua data dari kedua tabel, baik yang memiliki relasi maupun tidak
- **Kapan Digunakan**: Ketika kita ingin melihat semua data dari kedua tabel
- **Catatan**: MySQL tidak mendukung FULL JOIN secara langsung, bisa menggunakan kombinasi LEFT JOIN dan RIGHT JOIN dengan UNION:

  ```sql
  SELECT Mahasiswa.Nama, Jurusan.NamaJurusan 
  FROM Mahasiswa 
  LEFT JOIN Jurusan 
  ON Mahasiswa.KodeJurusan = Jurusan.KodeJurusan
  UNION
  SELECT Mahasiswa.Nama, Jurusan.NamaJurusan 
  FROM Mahasiswa 
  RIGHT JOIN Jurusan 
  ON Mahasiswa.KodeJurusan = Jurusan.KodeJurusan;
  ```

---

## 💡 Tips dan Best Practices

1. **Gunakan Alias**: Berikan alias pada tabel untuk memudahkan penulisan query

   ```sql
   SELECT m.Nama, j.NamaJurusan 
   FROM Mahasiswa m 
   INNER JOIN Jurusan j 
   ON m.KodeJurusan = j.KodeJurusan;
   ```

2. **Perhatikan Performa**: JOIN bisa mempengaruhi performa query, pastikan kolom yang di-join sudah terindeks

3. **Hindari JOIN yang Tidak Perlu**: Gunakan JOIN hanya ketika benar-benar diperlukan

4. **Gunakan WHERE dengan Bijak**: Filter data setelah JOIN untuk hasil yang lebih efisien

---

## 🎓 Latihan Praktis

### Contoh Kasus 1: Menampilkan Data Mahasiswa dengan Jurusannya

```sql
SELECT m.NIM, m.Nama, j.NamaJurusan
FROM Mahasiswa m
INNER JOIN Jurusan j
ON m.KodeJurusan = j.KodeJurusan;
```

### Contoh Kasus 2: Menemukan Mahasiswa yang Belum Memiliki Jurusan

```sql
SELECT m.NIM, m.Nama
FROM Mahasiswa m
LEFT JOIN Jurusan j
ON m.KodeJurusan = j.KodeJurusan
WHERE j.KodeJurusan IS NULL;
```
