# Laravel 12 Docker Template

## Struktur Folder

```
laravel-docker-template/
├── docker-compose.yml
├── Dockerfile
├── .env.example
├── supervisor/
│   └── laravel-worker.conf
├── src/ (kosong, nanti Laravel 12 akan di-copy ke sini)
└── README.md
```

---

## Cara Penggunaan

### 1. Clone Repo atau Extract Zip

Download zip atau clone dari repo yang disediakan.

### 2. Copy Laravel Project

Masukkan semua file Laravel 12 kamu ke folder `src/`.

### 3. Update .env

Pastikan `.env` sudah disesuaikan terutama:

- Database: host = `db`
- Redis: host = `redis`

### 4. Jalankan Docker Compose

```bash
docker-compose up -d --build
```

### 5. Migrasi & Setup

Masuk ke container app:

```bash
docker-compose exec app bash
```

Jalankan:

```bash
php artisan migrate
php artisan config:cache
php artisan queue:restart
```

### 6. Cek Supervisor

Supervisor config sudah ada di:

```
/etc/supervisor/conf.d/laravel-worker.conf
```

Pastikan worker jalan:

```bash
supervisorctl reread
supervisorctl update
supervisorctl start laravel-worker:*
```

---

## Komponen

- **PHP 8.2 (bisa disesuaikan di Dockerfile)**
- **MySQL 8**
- **Redis (cache & queue)**
- **Supervisor (queue worker)**
- **nginx (proxy ke php-fpm)**
