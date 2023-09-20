### How To Setup App

1. Copy .env-example to .env
2. Change DB{HOST, DATABASE, USERNAME, PASSWORD}
3. Build App
```bash
docker-compose build app
```
4. Run Docker-compose
```bash
docker-compose up -d
```
5. Check Container
```bash
docker-compose ps
docker-compose exec app ls -l
```
6. Reset App
```bash
docker-compose exec app rm -rf vendor composer.lock
docker compose exec app composer install
```
7. Generate Key Laravel
```bash
docker compose exec app php artisan key:generate
```
8. Migration, Seeder, Database
```bash
docker compose exec app php artisan migrate:refresh --seed
```



