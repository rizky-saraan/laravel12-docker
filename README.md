# Laravel 12 Docker Template Docker

## Struktur Folder

```
laravel-app/
├── app/
├── bootstrap/
├── config/
├── database/
├── public/
├── resources/
├── routes/
├── storage/
├── tests/
├── docker/
│   ├── php/
│   │   ├── Dockerfile
│   │   ├── php.ini
│   ├── supervisor/
│   │   ├── laravel-worker.conf
│   ├── redis/
│       ├── redis.conf
├── docker-compose.yml
├── .env
├── .gitignore
├── artisan
├── composer.json
├── package.json
├── README.md
```

---

## Cara Penggunaan

### 1. Clone Repo atau Extract Zip

Download zip atau clone dari repo yang disediakan.

### 2. Pastikan struktur folder yang diclone sudah sesuai


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
