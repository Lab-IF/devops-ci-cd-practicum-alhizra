# LAPORAN PRAKTIKUM DEVOPS – PERTEMUAN 02  
## Praktikum Docker Dasar, Dockerfile, dan Docker Compose  
Nama:Al Hizra 
NIM:105841101523

# TASK 1 – Eksplorasi Docker Dasar
## Tujuan
Memahami lifecycle container Docker:
- Pull image
- Menjalankan container
- Melihat logs
- Masuk ke container
- Stop dan menghapus container

## Langkah-Langkah
### Pull Image
bash
docker pull nginx:alpine
### Menjalankan Container
bash
docker run -d --name web-praktikum -p 8080:80 nginx:alpine
Cek container berjalan:
bash
docker ps
### Mengakses Aplikasi
Buka browser:
http://localhost:8080
Hasil: Halaman default nginx berhasil ditampilkan.
### Melihat Logs
bash
docker logs web-praktikum
### Masuk ke Dalam Container
bash
docker exec -it web-praktikum sh
Eksplorasi:
bash
ls -la /usr/share/nginx/html
cat /etc/nginx/nginx.conf
exit
### Stop dan Hapus Container
bash
docker stop web-praktikum
docker rm web-praktikum

## Kesimpulan Task 1
Lifecycle container Docker:
create → run → stop → remove
Container lebih ringan dibanding Virtual Machine karena tidak memerlukan sistem operasi terpisah.

# TASK 2 – Membuat Custom Docker Image
## Tujuan
Membuat image Docker sendiri menggunakan Dockerfile.
## Struktur Project
praktikum-docker/
│
├── Dockerfile
└── app/
    └── index.html
## Isi Dockerfile
dockerfile
FROM nginx:alpine
COPY app/index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
### Penjelasan
- FROM → menggunakan base image nginx alpine
- COPY → menyalin file HTML ke direktori nginx
- EXPOSE → mendeklarasikan port 80
- CMD → menjalankan nginx di foreground

## Build Image
bash
docker build -t praktikum-docker:v1 .
Cek image:
bash
docker images
## Menjalankan Container
bash
docker run -d -p 8080:80 --name praktikum-web praktikum-docker:v1
Akses:
http://localhost:8080
Hasil: Website custom dengan nama dan NIM berhasil ditampilkan.
## Kesimpulan Task 2
Saya berhasil:
- Membuat Dockerfile
- Build image
- Menjalankan container dari image custom
Dockerfile memungkinkan pembuatan environment aplikasi yang konsisten dan portable.

# TASK 3 – Docker Compose Multi-Container
## Tujuan
Menjalankan beberapa container sekaligus dalam satu konfigurasi menggunakan Docker Compose.
## Services yang Digunakan
- Web → nginx
- API → httpd
- Database → postgres
## 🔹 Menjalankan Docker Compose
bash
docker compose up -d
Cek status:
bash
docker compose ps
Melihat logs:
bash
docker compose logs -f
## Pengujian
Web:
http://localhost:8080
API:
http://localhost:8081
Kedua service berhasil berjalan dengan baik.
## Cleanup
bash
docker compose down -v

# Perbedaan Container vs Virtual Machine
| Container | Virtual Machine |
|------------|----------------|
| Ringan | Lebih berat |
| Startup cepat | Startup lebih lama |
| Share kernel OS | Memiliki OS sendiri |
| Cocok untuk microservices | Cocok untuk isolasi penuh |

# Screenshot
Screenshot yang dilampirkan dalam folder `screenshots/`:
1. Output docker ps  
2. Tampilan nginx di browser  
3. Output docker build  
4. Image berhasil dibuat  
5. Docker compose ps  
6. Tampilan web & api service  

# Kesimpulan Akhir
Pada praktikum ini saya telah:
✅ Memahami lifecycle container Docker  
✅ Menjalankan dan mengelola container  
✅ Membuat custom Docker image menggunakan Dockerfile  
✅ Menjalankan multi-container menggunakan Docker Compose  
Docker membantu proses deployment aplikasi menjadi lebih cepat, ringan, dan konsisten.
