# Docker + Nginx

# 🐳

![container_docker](/container_docker.png)

## En Windows Docker Desktop de estar corriendo

# 🚀
## Run Container 

```bash
 docker-compose up -d
```

## Stop Container

```bash
docker-compose down
```

## Stop and Run Container

```bash
docker-compose down && docker-compose up -d
```

---

## Estructura del proyecto

![container_docker](estructura.png)

---

## docker-compose.yml

```yml

version: '3.8'

services:
nginx:
image: nginx:alpine
container_name: nginx-container
ports: - "8081:80"
volumes: - ./nginx.conf:/etc/nginx/nginx.conf - ./html:/usr/share/nginx/html
restart: unless-stopped

networks:
default:
name: nginx-network

```

---

## nginx.conf

```conf

events {
    worker_connections 1024;
}

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    sendfile on;
    keepalive_timeout 65;

    server {
        listen 80;
        server_name localhost;
        root /usr/share/nginx/html;
        index index.html;

        location / {
            try_files $uri $uri/ /index.html;
        }

        error_page 404 /404.html;
        error_page 500 502 503 504 /50x.html;
        
        location = /50x.html {
            root /usr/share/nginx/html;
        }
    }
}


```

---

# 🐧 Instalar Docker en Windows sin Docker Desktop, usando 

## ✅ Requisitos previos
Windows 10/11 actualizado

WSL2 activado

Ubuntu instalado desde Microsoft Store

¿Ya tienes WSL2 y Ubuntu instalado? Si no, te lo explico abajo. Si sí, pasa a la instalación de Docker.

## 🔧 PASO 1: Instalar WSL2 y Ubuntu
1.1 Instala WSL con Ubuntu desde CMD o PowerShell:
 ```
wsl --install -d Ubuntu
 ```

Esto instala Ubuntu y configura WSL2 automáticamente. Luego reinicia tu PC si se te solicita.

## 🐳 PASO 2: Instalar Docker en Ubuntu (WSL2)
## <font color="#ff0000">Abre Ubuntu desde el menú Inicio.</font>

 

Ejecuta estos comandos dentro de Ubuntu:
 
```
# Actualizar el sistema
sudo apt update && sudo apt upgrade -y


# Instalar Docker
 
sudo apt install docker.io -y
 

# Habilitar el servicio de Docker
sudo service docker start

# Añadir tu usuario al grupo docker (para evitar usar sudo cada vez)
 
sudo usermod -aG docker $USER
```

Sal del terminal con exit, cierra Ubuntu y vuelve a abrirlo para aplicar los cambios de grupo.

## ✅ Verifica que Docker funciona
Dentro de Ubuntu:

 ```
docker --version
docker run hello-world
 ```

Si ves un mensaje de bienvenida, Docker está funcionando sin Docker Desktop 🎉

---
## 🧠 Opcional: Ejecutar Docker automáticamente al abrir Ubuntu
Cada vez que abras Ubuntu, ejecuta:
```
sudo service docker start
```

Para automatizarlo:
 ```
echo "sudo service docker start" >> ~/.bashrc
 ```

---
## 🎁 Beneficios

Mucho menos uso de CPU y RAM.

Cero uso de Docker Desktop.

Mejor integración con Linux-based dev tools.






