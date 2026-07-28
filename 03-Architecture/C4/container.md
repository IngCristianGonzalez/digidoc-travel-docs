# Diagrama de Contenedores C4

## Descripción

Diagrama de nivel 2 que muestra los contenedores principales del sistema.

## Contenedores

| Contenedor | Tecnología | Responsabilidad |
|------------|------------|-----------------|
| Frontend | Angular | UI/UX |
| API | NestJS | Lógica de negocio |
| Database | PostgreSQL | Almacenamiento |
| Cache | Redis | Sesiones y cache |
| Messages | Kafka | Eventos asíncronos |
| Storage | AWS S3 | Archivos |

## Diagrama

```text
┌─────────────────────────────────────────────────────────────┐
│                      Frontend                                │
│                    Angular App                               │
└──────────────────────────┬──────────────────────────────────┘
                           │ HTTPS
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                    API Backend                               │
│                    NestJS API                                │
│                                                              │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐       │
│  │   Auth   │ │ Students │ │Documents │ │  Visa    │       │
│  │ Module   │ │  Module  │ │  Module  │ │ Module   │       │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘       │
└──────────────────────────┬──────────────────────────────────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
┌─────────────────┐ ┌───────────┐ ┌───────────┐
│   PostgreSQL    │ │   Redis   │ │   Kafka   │
└─────────────────┘ └───────────┘ └───────────┘
```

---

> *Última actualización: 2026-07-27*
