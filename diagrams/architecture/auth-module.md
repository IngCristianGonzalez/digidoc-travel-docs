# Prompt: Diagrama de Arquitectura del Módulo Auth

## Instrucciones

Usa este prompt con una herramienta de generación de diagramas (Mermaid, PlantUML, draw.io, etc.)

## Prompt

```
Genera un diagrama de arquitectura para el módulo de autenticación de DigiDoc Travel con los siguientes componentes:

1. Frontend (Angular)
   - Componente de Login
   - Componente de Profile
   - Service de Auth

2. Backend (NestJS API)
   - AuthController
   - AuthService
   - JwtService
   - RedisService
   - AuditService

3. Base de Datos
   - PostgreSQL (Supabase)
   - Redis

4. Mensajería
   - Kafka

5. AWS Services
   - S3 (Storage)
   - SES (Email)

Conexiones:
- Frontend → API Gateway → NestJS API
- NestJS API → PostgreSQL (lectura/escritura)
- NestJS API → Redis (cache, sesiones)
- NestJS API → Kafka (eventos)
- Kafka → Notification Module
- NestJS API → S3 (archivos)
- NestJS API → SES (emails)

Estilo: Arquitectura de capas con colores por dominio
```

## Salida Esperada

Un diagrama visual que muestre:
- Capa de presentación (Angular)
- Capa de API (NestJS)
- Capa de datos (PostgreSQL, Redis)
- Capa de mensajería (Kafka)
- Servicios AWS

---

> *Última actualización: 2026-07-27*
