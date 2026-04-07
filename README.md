# tesloshop-app
📌 TesloShop - Sistema Web con Docker

TesloShop es una aplicación web basada en arquitectura de microservicios que integra un backend en NestJS, un frontend en Angular y una base de datos PostgreSQL, todo orquestado mediante Docker Compose.

Arquitectura del sistema

El sistema está compuesto por tres servicios principales:

Frontend: Angular servido con Nginx
Backend: API REST con NestJS
Base de datos: PostgreSQL
[ Angular (Nginx) ] → [ NestJS API ] → [ PostgreSQL ]

📁 Estructura del proyecto
tesloshop/
│
├── docker-compose.yml
├── .env
├── .env.example
├── start.sh
├── stop.sh
│
├── teslo-shop/
│   ├── Dockerfile
│   ├── package.json
│   └── src/
│
├── angular-tesloshop/
│   ├── Dockerfile
│   ├── nginx.conf
│   └── src/

Variables de entorno

El archivo .env contiene la configuración sensible del sistema.

Ejemplo (.env.example):

# Base de datos
POSTGRES_DB=tesloshop
POSTGRES_USER=admin
POSTGRES_PASSWORD=admin123

# Backend
PORT=3000
DB_HOST=database
DB_PORT=5432
DB_USER=admin
DB_PASSWORD=admin123
DB_NAME=tesloshop

Importante:
El archivo .env NO debe subirse al repositorio.

Fase 2 – Construcción de imágenes
Backend (NestJS)
Imagen multi-stage (build + producción)
Optimizada para menor tamaño
Frontend (Angular + Nginx)
Build de Angular
Servido con Nginx
Configuración personalizada (nginx.conf)
Construcción manual
docker build -t tesloshop-backend ./teslo-shop
docker build -t tesloshop-frontend ./angular-tesloshop

Fase 3 – Docker Compose

El archivo docker-compose.yml define:

Servicios:
frontend
backend
database
Configuraciones:
Variables de entorno desde .env
Red compartida automática
Volúmenes para persistencia
depends_on para control de arranque
Ejecución del sistema
Usando script:
./start.sh
Manual:
docker compose up --build -d

Detener servicios
./stop.sh

o

docker compose down

Fase 4 – Validación
Verificar contenedores
docker ps
Acceso a servicios
Frontend: http://localhost
Backend API: http://localhost:3000
Base de datos:
PostgreSQL en puerto 5432
Comunicación entre servicios
El frontend consume la API del backend
El backend se conecta a PostgreSQL mediante variables de entorno

Datos de prueba (Seed)

Si está configurado:

docker exec -it backend npm run seed

Fase 5 – Evidencias requeridas

El repositorio debe incluir:

✔ Contenedores corriendo (docker ps)
✔ Frontend en funcionamiento
✔ Respuestas del backend
✔ Conexión a base de datos

Scripts de automatización
start.sh

Levanta todos los servicios:

docker compose up --build -d
stop.sh

Detiene y elimina contenedores:

docker compose down

Tecnologías utilizadas
NestJS
Angular
PostgreSQL
Docker
Docker Compose
Nginx