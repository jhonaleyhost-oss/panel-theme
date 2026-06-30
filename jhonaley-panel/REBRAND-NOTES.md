# Jhonaley Store Panel — Rebrand Notes

Fork dari `alxzy-group/alxzen` (Pterodactyl modified), di-rebrand jadi **Jhonaley Store**.

## Yang Sudah Diubah

| File | Perubahan |
|------|-----------|
| `config/app.php` | `name` → `jhonaley-store`, `author` → `Jhonaley Store` |
| `tailwind.config.js` | `black: '#131a20'` → `'#000000'` (pure black) |
| `app/Services/Helpers/SoftwareVersionService.php` | donation link → `https://jhonaley.store` |
| Semua file teks (`.php`, `.tsx`, `.blade.php`, `.md`, `.sh`, `.json`, `.yml`) | replace `Alxzen/alxzen/AlxZen` → `Jhonaley Store/jhonaley-store` |

## Theme Color

Theme dasar Alxzen **sudah blue** (`primary: colors.blue` di tailwind.config.js). Hanya `black` yang di-pure-kan ke `#000000`.

Kalau mau lebih biru elektrik, edit `tailwind.config.js`:
```js
primary: {
  500: '#3b82f6',  // blue-500
  600: '#2563eb',  // blue-600
  700: '#1d4ed8',  // blue-700
},
```

## Yang HARUS Kamu Lakukan di VPS

Folder ini hanya **source code** — belum di-install. Untuk jalan:

```bash
# 1. Download folder ini ke VPS
scp -r jhonaley-panel/ root@VPS_IP:/var/www/pterodactyl

# 2. Di VPS, install dependencies
cd /var/www/pterodactyl
composer install --no-dev --optimize-autoloader
yarn install

# 3. Setup env + database (lihat panduan instalasi Pterodactyl)
cp .env.example .env
php artisan key:generate --force
php artisan p:environment:setup
php artisan p:environment:database
php artisan migrate --seed --force
php artisan p:user:make  # buat admin pertama

# 4. Build frontend assets dengan branding baru
yarn build:production

# 5. Set permissions + restart
chown -R www-data:www-data /var/www/pterodactyl/*
systemctl restart nginx php8.1-fpm
```

## Logo & Favicon (Manual)

Folder ini **belum** include logo Jhonaley Store. Ganti manual:
- `public/favicons/` — replace semua icon dengan favicon kamu
- `resources/scripts/assets/images/pterodactyl.svg` — replace dengan logo kamu

Generate favicon di https://realfavicongenerator.net lalu replace file-nya.

## ⚠️ Reminder

Lovable **tidak menjalankan** code ini — ini PHP/Laravel, butuh VPS Linux + PHP + MySQL + Redis + Nginx. Folder ini cuma "staging" sebelum kamu upload ke server hosting.
