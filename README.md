# Microservicios Gym - Guía de Instalación

## Prerrequisitos
- Node.js y npm
- Docker y Docker Compose
- Git

## Pasos de Instalación

### 1. Clonar el Repositorio

```bash
git clone --recurse-submodules https://github.com/MSProyectoWeb/MS_Gym.git
```

### 2. Instalar Dependencias

En cada directorio de microservicio, ejecutar:
```bash
npm install
```

**Nota**: Si encuentras errores, intenta:
```bash
npm install --legacy-peer-deps
```

### 3. Configurar Variables de Entorno

#### API Gateway
No requiere variables de entorno.

#### Servicio de Chat
Crear archivo `.env`:
```env
RABBITMQ_USER=user
RABBITMQ_PASS=password
RABBITMQ_HOST=localhost
RABBITMQ_QUEUE=chat_queue
```

#### Servicio de Users
Crear archivo `.env`:
```env
DATABASE_URL="postgresql://users_admin:users_password@localhost:5433/users_db?schema=public"
MAIL_USER="gymappgestion@gmail.com"
MAIL_PASS="vuzp sguz kkxh ufub"
RABBITMQ_USER=user
RABBITMQ_PASS=password
RABBITMQ_HOST=localhost
RABBITMQ_QUEUE=users_queue
```

### 4. Iniciar Servicios con Docker

Levantar base de datos y RabbitMQ:
```bash
docker-compose up -d
```

### 5. Configurar Prisma

Ejecutar en orden:

1. Generar cliente Prisma:
```bash
npx prisma generate
```

2. Ejecutar migraciones:
```bash
npx prisma migrate dev
```

### 6. Iniciar los Microservicios

Para cada servicio:
```bash
npm run start:dev
```

**Orden recomendado de inicio**:
1. Servicio de Chat
2. Servicio de Users
3. API Gateway

## Notas Adicionales
- Asegúrate de que los servicios de Docker estén funcionando antes de iniciar los microservicios
- Verifica que los puertos necesarios estén disponibles
- Mantén el orden recomendado de inicio para evitar problemas de conectividad
