# Laravel Interview Project

Please complete the setup below **before the interview**.

## What you need

1. **Docker Desktop**
   - macOS / Windows: https://www.docker.com/products/docker-desktop/
   - Windows users: please use **WSL2** and clone the project **inside the WSL filesystem** (e.g. `~/projects`), not on `C:\`. Otherwise performance will be very poor.
2. **Git**
3. **Your preferred IDE/editor** (PhpStorm, VS Code, …) set up the way you like to work

You do **not** need PHP, Composer or MySQL installed locally. Everything runs inside Docker through Laravel Sail.

## Project setup

Inside the cloned project, run:

```bash
cp .env.example .env

docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v "$(pwd):/var/www/html" \
    -w /var/www/html \
    laravelsail/php84-composer:latest \
    composer install --ignore-platform-reqs

./vendor/bin/sail up -d
./vendor/bin/sail artisan key:generate
./vendor/bin/sail artisan migrate
./vendor/bin/sail artisan test
```

The first `sail up` builds the Docker image, which takes a few minutes. If `migrate` fails with a database connection error, MySQL is still starting. Wait a few seconds and try again.
