# Laravel Starter + Wasmer

This example shows how to deploy a standard **Laravel** application on **Wasmer Edge**.

## Demo

`https://<your-subdomain>.wasmer.app/` (deploy to get your own Laravel instance)

## How it Works

The project comes from `composer create-project laravel/laravel` with light tweaks:

* `routes/web.php` defines the default route that returns the `welcome` Blade view.
* `public/index.php` is Laravel’s front controller; Wasmer points traffic here.
* Cached configuration under `bootstrap/cache/` may contain absolute paths—update them to `/app/...` during deployment so they match Wasmer’s filesystem layout.

Add controllers, middleware, and Blade templates as you would in any Laravel app.

## Running Locally

```bash
composer install
php artisan serve --host 127.0.0.1 --port 8000
```

Visit `http://127.0.0.1:8000/` to confirm the welcome page. For parity with Wasmer, you can also run:

```bash
php -S 127.0.0.1:8000 -t public
```

## Deploying to Wasmer (Overview)

1. Run `composer install --no-dev --optimize-autoloader` and (optionally) `php artisan config:cache route:cache`.
2. Rewrite cached paths to `/app` if necessary (`sed -i '' "s|$PWD|/app|g" bootstrap/cache/*.php` on macOS).
3. Deploy to Wasmer Edge with a start command like `php -S 0.0.0.0:$PORT -t public`.
