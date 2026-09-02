# Arquitectura del Proyecto

## Arquitectura General

```text
┌─────────────────────────────────────────────────────────────┐
│                      CLIENTE                                │
│                    Angular App                               │
└──────────────────────────┬──────────────────────────────────┘
                           │ HTTPS
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                    API GATEWAY                               │
│                   AWS API Gateway                            │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                    BACKEND                                   │
│                    NestJS API                                │
│                                                              │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐       │
│  │   Auth   │ │  Users   │ │ Students │ │Documents │       │
│  │ Module   │ │  Module  │ │  Module  │ │  Module  │       │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘       │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐       │
│  │  Visa    │ │ Payments │ │ Events   │ │Notif.    │       │
│  │ Module   │ │  Module  │ │  Module  │ │ Module   │       │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘       │
└──────────────────────────┬──────────────────────────────────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
┌─────────────────┐ ┌───────────┐ ┌───────────┐
│   PostgreSQL    │ │   Redis   │ │   Kafka   │
│   (Supabase)    │ │  (Cache)  │ │ (Events)  │
└─────────────────┘ └───────────┘ └───────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                    AWS SERVICES                              │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐       │
│  │    S3    │ │   SES    │ │   SQS    │ │CloudWatch│       │
│  │ Storage  │ │  Email   │ │  Queue   │ │Monitoring│       │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘       │
└─────────────────────────────────────────────────────────────┘
```

## Capas de Arquitectura

### 1. Capa de Presentación
- **Tecnología:** Angular 17+
- **Responsabilidad:** UI/UX, validaciones client-side

### 2. Capa de API
- **Tecnología:** NestJS
- **Responsabilidad:** Lógica de negocio, validaciones server-side

### 3. Capa de Datos
- **Base de Datos:** PostgreSQL (Supabase)
- **Cache:** Redis
- **Eventos:** Kafka

### 4. Capa de Servicios
- **Almacenamiento:** AWS S3
- **Email:** AWS SES
- **Monitoreo:** AWS CloudWatch

## Patrones Arquitectónicos

| Patrón | Implementación |
|--------|----------------|
| Microservicios | Modular por dominio |
| CQRS | Lectura/Escritura separados |
| Event Sourcing | Kafka para eventos |
| API REST | Endpoints estandarizados |
| JWT | Autenticación stateless |

---

> *Última actualización: 2026-07-27*
