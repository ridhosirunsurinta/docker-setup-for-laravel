# Laravel dengan Docker Compose

Setup Laravel menggunakan Docker Compose (PHP-FPM, Nginx, MySQL, Redis).

---

## 🚀 Persiapan

Pastikan sudah ter-install:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

Struktur folder:

```bash
laravel-app/
├─ docker/
│ ├─ nginx/
│ │ └─ default.conf
│ └─ php/
│ └─ Dockerfile
├─ docker-compose.yml
└─ (kode Laravel)
```

---

## 🔧 Setup Project

### 1. Build & Up Container

```bash
docker compose up -d --build
```

### 2. Install Dependencies PHP di dalam Container

```bash
docker compose exec app composer install
```

### 3. Generate App Key

```bash
docker compose exec app php artisan key:generate
```

### 4. Symlink Storage

```bash
docker compose exec app php artisan storage:link
```

### 5. Jalankan Migrasi Database

```bash
docker compose exec app php artisan migrate
```

## 🌐 Akses Aplikasi

Aplikasi akan tersedia di:

http://localhost:8000

## ⚙️ Service yang tersedia

app → PHP-FPM (Laravel)

web → Nginx

db → MySQL 8

redis → Redis

queue → Worker Queue Laravel

## 🛠 Perintah Tambahan

Masuk ke dalam container app:

```bash
docker compose exec app bash
```

Jalankan artisan command:

```bash
docker compose exec app php artisan tinker
```

Jalankan test:

```bash
docker compose exec app php artisan test
```

## 📦 Catatan

- Ubah konfigurasi database & redis di file .env agar sesuai dengan docker-compose.yml.

- Untuk development frontend dengan Vite, jalankan container node (opsional).
