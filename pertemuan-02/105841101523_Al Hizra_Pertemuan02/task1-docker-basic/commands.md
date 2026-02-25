# Daftar Command Praktikum Docker

## Docker Basic
docker pull nginx:alpine
docker run -d --name web-praktikum -p 8080:80 nginx:alpine
docker logs web-praktikum
docker exec -it web-praktikum sh
docker stop web-praktikum
docker rm web-praktikum

## Dockerfile
Dockerfile dibuat menggunakan base image nginx:alpine dan menyalin file
index.html ke direktori /usr/share/nginx/html.

## Build dan Run Image
docker build -t praktikum-docker:v1 .
docker run -d -p 8080:80 --name praktikum-web praktikum-docker:v1

## Docker Compose
docker compose up -d
docker compose ps
docker compose logs -f
docker compose down -v
