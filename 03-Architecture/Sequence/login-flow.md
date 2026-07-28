# Diagrama de Secuencia: Login Flow

## Descripción

Flujo completo de inicio de sesión del usuario.

## Participantes

- User (Actor)
- Angular (Frontend)
- NestJS API (Backend)
- Auth Module
- Redis (Cache)
- PostgreSQL (Database)
- Kafka (Events)

## Secuencia

```text
User          Angular       NestJS API      Auth Module     Redis         PostgreSQL    Kafka
 │               │               │               │            │               │            │
 │  1. Login     │               │               │            │               │            │
 │──────────────▶│               │               │            │               │            │
 │               │  2. POST /auth/login          │            │               │            │
 │               │──────────────▶│               │            │               │            │
 │               │               │  3. validate()│            │               │            │
 │               │               │──────────────▶│            │               │            │
 │               │               │               │  4. find user               │            │
 │               │               │               │───────────────────────────▶│            │
 │               │               │               │  5. user data              │            │
 │               │               │               │◀───────────────────────────│            │
 │               │               │               │            │               │            │
 │               │               │               │  6. compare password       │            │
 │               │               │               │────────────│               │            │
 │               │               │               │  7. valid   │               │            │
 │               │               │               │◀───────────│               │            │
 │               │               │               │            │               │            │
 │               │               │               │  8. generate tokens        │            │
 │               │               │               │────────────│               │            │
 │               │               │               │  9. tokens  │               │            │
 │               │               │               │◀───────────│               │            │
 │               │               │               │            │               │            │
 │               │               │               │  10. store refresh token   │            │
 │               │               │               │──────────────────────────▶│            │
 │               │               │               │            │               │            │
 │               │               │               │  11. publish event         │            │
 │               │               │               │────────────────────────────────────────▶│
 │               │               │               │            │               │            │
 │               │               │  12. return tokens          │               │            │
 │               │               │◀──────────────│            │               │            │
 │               │  13. tokens   │               │            │               │            │
 │               │◀──────────────│               │            │               │            │
 │  14. success  │               │               │            │               │            │
 │◀──────────────│               │               │            │               │            │
```

---

> *Última actualización: 2026-07-27*
