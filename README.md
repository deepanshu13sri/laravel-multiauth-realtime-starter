# Laravel Multi-Auth + Realtime + Push + Queue Starter

This repo is a **starter skeleton** aligned with your assessment requirements:

- Separate **Admin** and **Customer** guards
- Product CRUD + **bulk import** (CSV/Excel) via **queues & chunking**
- Orders with **status updates**
- **Websockets** broadcasting (Pusher/Echo) for real-time order status + presence
- **Web Push** notifications via OneSignal channel
- **Tests**: feature + unit examples
- Includes `products_sample_import.csv`

> You still need to run `composer install`, set up `.env`, and run migrations. Code is production-lean but simplified for readability.

## Quick Start

```bash
composer install
cp .env.example .env
php artisan key:generate

# configure DB + Pusher/OneSignal in .env

php artisan migrate
php artisan queue:table && php artisan migrate

# build assets
npm install
npm run dev

# run servers
php artisan serve
php artisan queue:work
```

### Multi-Auth

- Guards: `admin`, `customer`
- Providers: `admins`, `customers`
- Middleware examples: `auth:admin`, `auth:customer`

### Realtime (Websockets)

- Broadcasting via **Pusher** (default). Configure keys in `.env`.
- Presence channel: `presence-online`
- Event: `OrderStatusUpdated`
- Echo setup in `resources/js/bootstrap.js`

### Push Notifications

- Using **OneSignal** channel package. Add your keys in `.env`.
- Notification: `OrderStatusPush`

### Bulk Import

- Upload CSV/Excel in Admin panel.
- Job: `ImportProductsJob` uses chunked reads via `Maatwebsite\Excel` or native CSV fallbacks.
- Validates rows; missing image -> defaults.

### Tests

- `tests/Feature/ProductImportTest.php`
- `tests/Feature/OrderPlacementTest.php`
- `tests/Unit/ImportRowValidatorTest.php`

## Notes

- Minimal Blade UI to demonstrate flows.
- Presence status also persisted to DB (`user_presences` table).
