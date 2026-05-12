# 🐕 Tienda de Alimentos para Perritos

> Aplicación web fullstack con arquitectura de 3 capas, containerizada con Docker y lista para desplegar en AWS.

![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat-square&logo=docker)
![Node.js](https://img.shields.io/badge/Node.js-Express-339933?style=flat-square&logo=node.js)
![MySQL](https://img.shields.io/badge/MySQL-8-4479A1?style=flat-square&logo=mysql)
![Status](https://img.shields.io/badge/Status-Active-success?style=flat-square)

---

## 📋 Descripción

Sistema completo de **gestión de productos** para una tienda de alimentos para perros. Implementa un CRUD funcional con arquitectura moderna basada en microservicios usando Docker.

### 🎯 Características Principales

✅ **Gestión de Productos CRUD**
- Listar productos
- Crear nuevos productos
- Editar productos existentes
- Eliminar productos

✅ **Arquitectura de 3 Capas**
- Frontend responsivo
- Backend con API REST
- Base de datos persistente

✅ **Containerización Completa**
- Docker & Docker Compose
- Volúmenes persistentes
- Configuración de variables de entorno

---

## 🏗️ Arquitectura

```
┌─────────────────────────────────────┐
│         INTERNET / Cliente           │
└──────────────┬──────────────────────┘
               │
        ┌──────▼───────┐
        │   Frontend    │
        │   (Nginx)     │
        │   Port 8080   │
        └──────┬───────┘
               │
        ┌──────▼───────┐
        │   Backend     │
        │   (Node.js)   │
        │   Port 3001   │
        └──────┬───────┘
               │
        ┌──────▼───────┐
        │   MySQL 8     │
        │   Port 3306   │
        └───────────────┘
```

| Capa | Servicio | Tecnología | Puerto |
|------|----------|-----------|--------|
| 🎨 **Presentación** | Frontend | HTML, JavaScript, Nginx | 8080 |
| ⚙️ **Aplicación** | Backend API | Node.js, Express | 3001 |
| 💾 **Datos** | Base de Datos | MySQL 8 | 3306 |

---

## 📁 Estructura del Proyecto

```
tienda-perritos/
│
├── 📄 docker-compose.yml         ← Orquestación de servicios
├── 📄 README.md                  ← Este archivo
│
├── 📂 frontend/
│   ├── Dockerfile                ← Imagen Nginx
│   ├── index.html                ← Interfaz HTML
│   ├── app.js                    ← Lógica JavaScript
│   └── .dockerignore
│
├── 📂 backend/
│   ├── Dockerfile                ← Imagen Node.js
│   ├── package.json              ← Dependencias
│   ├── server.js                 ← API Express
│   └── .dockerignore
│
└── 📂 db/
    └── init.sql                  ← Script de inicialización
```

---

## 🛠️ Requisitos

- **Docker Desktop** instalado y ejecutándose
- **Git** (opcional, para clonar el repositorio)
- Al menos **2GB de RAM** disponible

> Descarga Docker desde: https://www.docker.com/products/docker-desktop

---

## 🚀 Inicio Rápido

### 1️⃣ Clonar o descargar el proyecto
```bash
git clone <repositorio>
cd tienda-perritos_LOCAL
```

### 2️⃣ Construir las imágenes Docker
```bash
docker compose build
```

### 3️⃣ Iniciar los servicios
```bash
docker compose up -d
```

### 4️⃣ Acceder a la aplicación
- **Frontend:** http://localhost:8080
- **Backend API:** http://localhost:3001/api/productos

---

## 📊 Endpoints de la API

```
GET    /api/productos          ← Obtener todos los productos
POST   /api/productos          ← Crear nuevo producto
PUT    /api/productos/:id      ← Actualizar producto
DELETE /api/productos/:id      ← Eliminar producto
```

### Ejemplo de producto:
```json
{
  "id": 1,
  "nombre": "Alimento Cachorro Premium",
  "descripcion": "Sabor pollo, razas pequeñas",
  "precio": 19990,
  "stock": 15
}
```

---

## 🗄️ Base de Datos

**Base de datos:** `tienda_perritos`

**Tabla:** `productos`
| Campo | Tipo | Descripción |
|-------|------|-------------|
| `id` | INT (PK) | Identificador único |
| `nombre` | VARCHAR(100) | Nombre del producto |
| `descripcion` | VARCHAR(255) | Descripción breve |
| `precio` | DECIMAL(10,2) | Precio en CLP |
| `stock` | INT | Cantidad en inventario |

---

## 🔧 Configuración

### Variables de Entorno (Backend)
```env
DB_HOST=db              # Host de la BD
DB_USER=root            # Usuario MySQL
DB_PASSWORD=admin123    # Contraseña MySQL
DB_NAME=tienda_perritos # Base de datos
DB_PORT=3306            # Puerto MySQL
```

---

## 📚 Dependencias del Backend

```json
{
  "express": "^4.19.0",      // Framework web
  "cors": "^2.8.5",          // Manejo de CORS
  "mysql2": "^3.9.0"         // Driver MySQL con promesas
}
```

---

## ⚙️ Comandos Útiles

```bash
# Iniciar servicios en background
docker compose up -d

# Ver logs de los servicios
docker compose logs -f

# Detener servicios (conserva datos)
docker compose stop

# Reiniciar servicios
docker compose restart

# Eliminar contenedores y volúmenes (CUIDADO: Elimina datos)
docker compose down -v

# Ver estado de los contenedores
docker compose ps
```

---

## 🐛 Solución de Problemas

### ❌ "No se pueden conectar a los servicios"
```bash
# Verificar que los contenedores estén corriendo
docker compose ps

# Ver logs detallados
docker compose logs backend
docker compose logs db
```

### ❌ "Puerto 8080 o 3001 ya está en uso"
Cambiar los puertos en `docker-compose.yml`:
```yaml
ports:
  - "8081:80"    # Frontend en 8081
  - "3002:3001"  # Backend en 3002
```

### ❌ "Base de datos no se inicializa"
Eliminar volumen y recrear:
```bash
docker compose down -v
docker compose up -d
```

---

## 📝 Notas Importantes

- 🔐 Las credenciales de la BD son de **desarrollo**. Para producción, usar variables de entorno seguras.
- 💾 Los datos se persisten en el volumen `dbdata`.
- 🔄 Los cambios en código requieren reconstruir las imágenes.
- 🌐 La aplicación está lista para desplegar en AWS EC2.

---

## 📄 Licencia

Este proyecto es de ejemplo educativo.

---

## 👤 Autor

Desarrollado como práctica de DevOps y contenedorización.

**¡Última actualización:** Mayo 2026
('Alimento Cachorro Premium', 'Sabor pollo, razas pequeñas', 19990, 15),
('Alimento Adulto Light', 'Control de peso, razas medianas', 17990, 8),
('Snacks Dentales', 'Ayuda a la limpieza dental', 5990, 30);
Dockerfile Backend

El backend utiliza Node.js Alpine y aplica buenas prácticas de contenedorización:

Imagen base liviana.
Instalación solo de dependencias de producción.
Construcción multi-stage.
Usuario no root.
Exposición del puerto 3001.
Separación entre dependencias y código fuente.

Dockerfile:

# Etapa 1: instalación de dependencias
FROM node:18-alpine AS deps

WORKDIR /app

COPY package*.json ./

RUN npm install --omit=dev


# Etapa 2: imagen final liviana y segura
FROM node:18-alpine

WORKDIR /app

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

COPY --from=deps /app/node_modules ./node_modules

COPY package*.json ./
COPY server.js ./

RUN chown -R appuser:appgroup /app

USER appuser

EXPOSE 3001

CMD ["npm", "start"]
Dockerfile Frontend

El frontend utiliza Nginx Alpine para servir archivos estáticos y actuar como proxy reverso hacia el backend privado.

Características:

Imagen liviana.
Eliminación del contenido por defecto de Nginx.
Copia de archivos estáticos.
Configuración personalizada de Nginx.
Redirección de /api hacia el backend privado.

Dockerfile:

FROM nginx:alpine

RUN rm -rf /usr/share/nginx/html/*

COPY index.html /usr/share/nginx/html/index.html
COPY app.js /usr/share/nginx/html/app.js

COPY default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
Configuración Nginx Frontend

Archivo:

frontend/default.conf

Configuración usada:

server {
    listen 80;
    server_name _;

    root /usr/share/nginx/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location /api/ {
        proxy_pass http://10.0.141.193:3001/api/;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

Esta configuración permite que el navegador acceda solo a la instancia WEB, mientras que Nginx reenvía internamente las solicitudes /api hacia la instancia APP privada.

Persistencia de datos

La base de datos MySQL utiliza un volumen Docker llamado dbdata.

volumes:
  - dbdata:/var/lib/mysql

Este volumen permite que los datos no se pierdan si el contenedor de MySQL se reinicia o se vuelve a crear.

Se utiliza un named volume porque:

Docker administra su ubicación.
Es más portable.
Facilita la persistencia de datos.
Es adecuado para almacenar información crítica de MySQL.
Docker Compose local

El archivo docker-compose.local.yml permite levantar el stack completo localmente:

services:
  db:
    image: mysql:8
    container_name: tienda-db-local
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: admin123
      MYSQL_DATABASE: tienda_perritos
    volumes:
      - dbdata_local:/var/lib/mysql
      - ./db/init.sql:/docker-entrypoint-initdb.d/init.sql
    ports:
      - "3306:3306"

  backend:
    build:
      context: ./backend
    container_name: tienda-backend-local
    restart: always
    environment:
      DB_HOST: db
      DB_USER: root
      DB_PASSWORD: admin123
      DB_NAME: tienda_perritos
      DB_PORT: 3306
    ports:
      - "3001:3001"
    depends_on:
      - db

  frontend:
    build:
      context: ./frontend
    container_name: tienda-frontend-local
    restart: always
    ports:
      - "8080:80"
    depends_on:
      - backend

volumes:
  dbdata_local:

Comandos:

docker compose -f docker-compose.local.yml build
docker compose -f docker-compose.local.yml up -d

Acceso local:

Frontend: http://localhost:8080
Backend: http://localhost:3001/api/productos

Para detener:

docker compose -f docker-compose.local.yml down
Docker Compose para DATA

Archivo:

docker-compose.db.yml

Uso:

sudo docker compose -f docker-compose.db.yml up -d

Contenido:

services:
  db:
    image: mysql:8
    container_name: tienda-db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: admin123
      MYSQL_DATABASE: tienda_perritos
    ports:
      - "3306:3306"
    volumes:
      - dbdata:/var/lib/mysql
      - ./db/init.sql:/docker-entrypoint-initdb.d/init.sql

volumes:
  dbdata:
Docker Compose para APP

Archivo:

docker-compose.backend.yml

Uso:

sudo docker compose -f docker-compose.backend.yml up -d

Contenido:

services:
  backend:
    build:
      context: ./backend
    container_name: tienda-backend
    restart: always
    environment:
      DB_HOST: 10.0.152.47
      DB_USER: root
      DB_PASSWORD: admin123
      DB_NAME: tienda_perritos
      DB_PORT: 3306
    ports:
      - "3001:3001"
Docker Compose para WEB

Archivo:

docker-compose.frontend.yml

Uso:

sudo docker compose -f docker-compose.frontend.yml up -d

Contenido:

services:
  frontend:
    build:
      context: ./frontend
    container_name: tienda-frontend
    restart: always
    ports:
      - "80:80"
Despliegue en AWS
EC2 DATA

La instancia DATA ejecuta MySQL en Docker.

Comandos usados:

mkdir tienda-db
cd tienda-db
nano init.sql
nano docker-compose.yml
sudo docker compose up -d

Verificación:

sudo docker ps
sudo docker logs tienda-db
sudo docker exec -it tienda-db mysql -u root -p

Consulta de prueba:

USE tienda_perritos;
SELECT * FROM productos;
EC2 APP

La instancia APP ejecuta el backend Node.js en Docker.

Construcción:

sudo docker build -t tienda-backend .

Ejecución:

sudo docker run -d \
  --name tienda-backend \
  -p 3001:3001 \
  -e DB_HOST=10.0.152.47 \
  -e DB_USER=root \
  -e DB_PASSWORD=admin123 \
  -e DB_NAME=tienda_perritos \
  -e DB_PORT=3306 \
  tienda-backend

Verificación:

sudo docker ps
sudo docker logs tienda-backend
curl http://localhost:3001/api/health
curl http://localhost:3001/api/productos
EC2 WEB

La instancia WEB ejecuta el frontend en Docker con Nginx.

Construcción:

sudo docker build -t tienda-frontend .

Ejecución:

sudo docker run -d \
  --name tienda-frontend \
  -p 80:80 \
  tienda-frontend

Verificación:

sudo docker ps
curl http://localhost
curl http://localhost/api/productos

Acceso desde navegador:

http://IP_PUBLICA_WEB
Seguridad aplicada

La arquitectura utiliza Security Groups por capa.

Comunicación	Estado
Internet → WEB	Permitido
WEB → APP	Permitido
WEB → DATA	Bloqueado
APP → DATA	Permitido
APP → Internet	Permitido mediante NAT
DATA → Internet	Bloqueado
DATA → APP	Permitido

Solo la instancia WEB está expuesta a internet.
APP y DATA permanecen en subredes privadas.

Reglas principales de Security Groups
SG-WEB

Entrada:

HTTP 80 desde Internet.
SSH 22 desde mi IP.
ICMP desde Internet para pruebas de ping.

Salida:

Todo el tráfico permitido.
SG-APP

Entrada:

SSH desde SG-WEB.
ICMP desde SG-WEB.
TCP 3001 desde SG-WEB.

Salida:

Todo el tráfico permitido.
SG-DATA

Entrada:

SSH desde SG-APP.
ICMP desde SG-APP.
MySQL 3306 desde SG-APP.

Salida:

Restringida para evitar acceso directo a Internet.
Pruebas de conectividad

Pruebas realizadas:

Prueba	Resultado esperado
WEB recibe ping desde Internet	Correcto
WEB → APP	Correcto
WEB → DATA	Bloqueado
APP → Google	Correcto
APP → DATA	Correcto
DATA → Google	Bloqueado
DATA → WEB	Bloqueado
DATA → APP	Correcto
Pruebas funcionales

Se verificó:

El frontend carga correctamente desde la IP pública de WEB.
El botón “Cargar productos” muestra los productos de MySQL.
El backend responde desde APP.
El backend consulta correctamente a DATA.
MySQL mantiene los datos mediante volumen Docker.
La ruta /api/productos funciona correctamente.
La ruta /api/health responde correctamente.
Comandos útiles

Ver contenedores:

sudo docker ps

Ver logs del backend:

sudo docker logs tienda-backend

Ver logs del frontend:

sudo docker logs tienda-frontend

Ver logs de la base de datos:

sudo docker logs tienda-db

Probar backend en APP:

curl http://localhost:3001/api/health
curl http://localhost:3001/api/productos

Probar backend desde WEB:

curl http://10.0.141.193:3001/api/productos

Probar proxy frontend desde WEB:

curl http://localhost/api/productos
Prácticas DevOps aplicadas
Contenedorización con Docker.
Separación de servicios por capa.
Uso de Docker Compose.
Uso de variables de entorno.
Persistencia con volúmenes Docker.
Despliegue en AWS EC2.
Seguridad mediante Security Groups.
Separación entre red pública y privada.
Preparación para CI/CD con GitHub Actions.
Control de versiones mediante Git.
CI/CD propuesto

El flujo CI/CD considerado para el proyecto es:

Push a rama deploy
   ↓
GitHub Actions
   ↓
Build imagen Docker
   ↓
Push a Docker Hub
   ↓
SSH hacia EC2
   ↓
Pull de nueva imagen
   ↓
Stop + Remove contenedor anterior
   ↓
Run nuevo contenedor
GitHub Secrets necesarios

Para automatizar el despliegue se consideran los siguientes secrets:

Secret	Uso
DOCKER_USERNAME	Usuario de Docker Hub
DOCKER_PASSWORD	Token o contraseña de Docker Hub
EC2_HOST_WEB	IP pública de la instancia WEB
EC2_HOST_APP	IP o acceso SSH hacia APP
EC2_KEY	Llave privada SSH
DB_HOST	IP privada de DATA
DB_USER	Usuario MySQL
DB_PASSWORD	Contraseña MySQL
DB_NAME	Nombre de la base de datos
Justificación técnica

La arquitectura se diseñó en tres capas para separar responsabilidades:

WEB expone únicamente el frontend hacia Internet.
APP procesa la lógica de negocio y permanece en una subred privada.
DATA almacena la información crítica y no tiene acceso directo a Internet.

Esta separación permite aplicar el principio de mínimo privilegio, mejorar la seguridad y facilitar la escalabilidad futura.

Docker permite que cada componente se ejecute de forma portable, controlada y reproducible.
El uso de volúmenes en MySQL asegura persistencia de datos.
La automatización con CI/CD permite reducir errores manuales y acelerar futuras entregas.

Estado actual del proyecto
Frontend: funcionando en contenedor Docker en EC2 WEB.
Backend: funcionando en contenedor Docker en EC2 APP.
Base de datos: funcionando en contenedor Docker en EC2 DATA.
Integración Frontend → Backend → Data: funcionando correctamente.
Persistencia: implementada con volumen Docker.
Seguridad: aplicada mediante Security Groups.
CI/CD: preparado para implementación con GitHub Actions.
Próximas mejoras
Publicar imágenes en Docker Hub o Amazon ECR.
Automatizar despliegue con GitHub Actions.
Implementar monitoreo con CloudWatch.
Externalizar credenciales usando AWS Secrets Manager o GitHub Secrets.
Agregar HTTPS mediante certificado SSL.