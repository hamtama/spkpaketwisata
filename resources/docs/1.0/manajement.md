## 📊 Struktur Tabel - Sistem Pendukung Keputusan Pemilihan Paket Wisata

### 🗺️ Tabel: `destinations`

| Field            | Tipe Data        | Keterangan                                 |
|------------------|------------------|--------------------------------------------|
| id               | BIGINT (auto)    | Primary Key                                |
| name             | VARCHAR(255)     | Nama paket wisata                          |
| location         | VARCHAR(255)     | Lokasi paket wisata                        |
| price            | DECIMAL(12,2)    | Harga paket                                |
| duration_days    | INT              | Durasi dalam hari                          |
| type             | VARCHAR(100)     | Jenis wisata (Alam, Budaya, Sejarah, dll.) |
| facilities       | TEXT             | Daftar fasilitas                           |
| participants_min | INT              | Jumlah minimal peserta                     |
| participants_max | INT              | Jumlah maksimal peserta                    |
| description      | TEXT             | Deskripsi paket                            |
| created_at       | TIMESTAMP        | Timestamp                                  |
| updated_at       | TIMESTAMP        | Timestamp                                  |

---

### 🧮 Tabel: `criteria`

| Field      | Tipe Data            | Keterangan                                              |
|------------|----------------------|----------------------------------------------------------|
| id         | BIGINT (auto)        | Primary Key                                             |
| name       | VARCHAR(255)         | Nama kriteria (Harga, Durasi, Fasilitas, dll.)          |
| weight     | FLOAT                | Bobot kriteria                                          |
| type       | ENUM('benefit','cost') | Tipe kriteria (`benefit` = makin tinggi makin bagus)     |
| created_at | TIMESTAMP            | Timestamp                                               |
| updated_at | TIMESTAMP            | Timestamp                                               |

---

### 🔄 Tabel: `alternatives`

| Field         | Tipe Data     | Keterangan                                              |
|---------------|---------------|----------------------------------------------------------|
| id            | BIGINT (auto) | Primary Key                                             |
| destination_id| BIGINT        | Foreign Key ke `destinations.id`                        |
| criterion_id  | BIGINT        | Foreign Key ke `criteria.id`                            |
| value         | FLOAT         | Nilai alternatif (misal: skor fasilitas, nilai harga)   |
| created_at    | TIMESTAMP     | Timestamp                                               |
| updated_at    | TIMESTAMP     | Timestamp                                               |

---

### 👤 Tabel: `users` *(opsional)*

| Field      | Tipe Data        | Keterangan                    |
|------------|------------------|--------------------------------|
| id         | BIGINT (auto)    | Primary Key                   |
| name       | VARCHAR(255)     | Nama pengguna                 |
| email      | VARCHAR(255)     | Email                         |
| password   | VARCHAR(255)     | Password (hashed)             |
| created_at | TIMESTAMP        | Timestamp                     |
| updated_at | TIMESTAMP        | Timestamp                     |

---

### ✅ Tabel: `recommendations`

| Field            | Tipe Data     | Keterangan                                          |
|------------------|---------------|------------------------------------------------------|
| id               | BIGINT (auto) | Primary Key                                         |
| user_id          | BIGINT        | Foreign Key ke `users.id` *(opsional)*              |
| recommended_id   | BIGINT        | Foreign Key ke `destinations.id`                    |
| score            | FLOAT         | Skor hasil perhitungan rekomendasi                  |
| created_at       | TIMESTAMP     | Timestamp                                           |

---

### 🔗 Relasi Antar Tabel

[destinations] ---< [alternatives] >--- [criteria]

[users] ---< [recommendations] >--- [destinations]