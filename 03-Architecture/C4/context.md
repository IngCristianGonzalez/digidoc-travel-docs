# Diagrama de Contexto C4

## Descripción

Diagrama de nivel 1 que muestra el sistema DigiDoc Travel y sus interactores principales.

## Actores

| Actor | Tipo | Descripción |
|-------|------|-------------|
| Estudiante | Persona | Usuario principal del sistema |
| Consultor | Persona | Gestiona estudiantes |
| Administrador | Persona | Control total del sistema |
| Supabase | Sistema | Base de datos y autenticación |
| AWS | Sistema | Servicios cloud |

## Diagrama

```text
┌─────────────────────────────────────────────────────────┐
│                    DigiDoc Travel                        │
│                                                          │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐   │
│  │   Auth   │ │ Students │ │Documents │ │  Visa    │   │
│  │ Module   │ │  Module  │ │  Module  │ │ Module   │   │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘   │
│                                                          │
└─────────────────────────────────────────────────────────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
┌─────────────────┐ ┌───────────┐ ┌───────────┐
│   Supabase      │ │   AWS     │ │   Kafka   │
│   PostgreSQL    │ │   S3      │ │  Events   │
└─────────────────┘ └───────────┘ └───────────┘
```

---

> *Última actualización: 2026-07-27*
