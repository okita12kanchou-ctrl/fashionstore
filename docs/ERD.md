# ERD - FashionStore E-commerce

## Daftar Tabel

### 1. Tabel `users`
| Kolom | Tipe | Keterangan |
|-------|------|-------------|
| id | BIGINT (PK) | Auto increment |
| name | VARCHAR(255) | Nama lengkap |
| email | VARCHAR(255) | Email (unique) |
| password | VARCHAR(255) | Password terenkripsi |
| role | ENUM('admin','customer') | Peran pengguna |
| address | TEXT | Alamat pengiriman |
| phone | VARCHAR(20) | Nomor telepon |
| created_at | TIMESTAMP | Waktu dibuat |
| updated_at | TIMESTAMP | Waktu diupdate |

### 2. Tabel `products`
| Kolom | Tipe | Keterangan |
|-------|------|-------------|
| id | BIGINT (PK) | Auto increment |
| name | VARCHAR(255) | Nama produk/baju |
| description | TEXT | Deskripsi produk |
| price | DECIMAL(10,2) | Harga |
| stock | INT | Stok tersedia |
| category | VARCHAR(100) | Kategori (atasan/bawahan/outer) |
| size | VARCHAR(10) | Ukuran (S/M/L/XL) |
| color | VARCHAR(50) | Warna |
| image_url | VARCHAR(255) | Link gambar |
| created_at | TIMESTAMP | Waktu dibuat |
| updated_at | TIMESTAMP | Waktu diupdate |

### 3. Tabel `carts`
| Kolom | Tipe | Keterangan |
|-------|------|-------------|
| id | BIGINT (PK) | Auto increment |
| user_id | BIGINT (FK) | Foreign key ke users |
| product_id | BIGINT (FK) | Foreign key ke products |
| quantity | INT | Jumlah item |
| created_at | TIMESTAMP | Waktu dibuat |
| updated_at | TIMESTAMP | Waktu diupdate |

### 4. Tabel `orders`
| Kolom | Tipe | Keterangan |
|-------|------|-------------|
| id | BIGINT (PK) | Auto increment |
| user_id | BIGINT (FK) | Foreign key ke users |
| order_number | VARCHAR(50) | Nomor pesanan unik |
| total_price | DECIMAL(10,2) | Total harga |
| status | ENUM(...) | pending/paid/shipped/delivered/canceled |
| shipping_address | TEXT | Alamat pengiriman |
| payment_method | VARCHAR(50) | Metode pembayaran |
| payment_status | ENUM(...) | pending/success/failed |
| created_at | TIMESTAMP | Waktu dibuat |
| updated_at | TIMESTAMP | Waktu diupdate |

### 5. Tabel `order_items`
| Kolom | Tipe | Keterangan |
|-------|------|-------------|
| id | BIGINT (PK) | Auto increment |
| order_id | BIGINT (FK) | Foreign key ke orders |
| product_id | BIGINT (FK) | Foreign key ke products |
| quantity | INT | Jumlah item |
| price | DECIMAL(10,2) | Harga saat checkout |

### 6. Tabel `payments`
| Kolom | Tipe | Keterangan |
|-------|------|-------------|
| id | BIGINT (PK) | Auto increment |
| order_id | BIGINT (FK) | Foreign key ke orders |
| transaction_id | VARCHAR(100) | ID transaksi dari payment gateway |
| amount | DECIMAL(10,2) | Jumlah dibayar |
| payment_date | TIMESTAMP | Tanggal pembayaran |
| status | ENUM(...) | pending/success/failed |

## Relasi Antar Tabel
users ──┬── carts ── products
└── orders ── order_items ── products
└── payments

### Jenis Relasi:
- users → carts: **One to Many** (1 user punya banyak cart item)
- users → orders: **One to Many** (1 user punya banyak order)
- products → carts: **One to Many** (1 produk bisa di banyak cart)
- orders → order_items: **One to Many** (1 order punya banyak item)
- orders → payments: **One to One** (1 order punya 1 payment)