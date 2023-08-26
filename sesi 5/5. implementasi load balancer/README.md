# Sesi 5 - Implementasi Load Balancer

1. Jalankan aplikasi laravel dengan
     ```
     docker run --name laravel-app -p 7000:80 -d <username_docker_hub>/laravel-app:v1
     ```
2. Jalankan aplikasi laravel kedua dengan
     ```
     docker run --name laravel-app -p 8000:80 -d <username_docker_hub>/laravel-app:v1
     ```
3. Jalankan aplikasi laravel kedua dengan
     ```
     docker run --name laravel-app -p 9000:80 -d <username_docker_hub>/laravel-app:v1
     ```
4. Buat Load balancer dengan settingan berikut.

   ```
     upstream loadBalancer {
     server 127.0.0.1:7000;
     server 127.0.0.1:8000;
     server 127.0.0.1:9000;

     server {
     listen 80;
     listen [::]80;
     server_name lb.vandyrazy.online;

     location / {
     proxy_set_header Host $host:$server_port;
     proxy_pass http://loadbalancer/;
   }
   
   }

   }
   ```

