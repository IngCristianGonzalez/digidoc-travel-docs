# Diagrama de Secuencia: Refresh Token

## Descripción

Flujo de renovación del Access Token usando el Refresh Token.

## Participantes

- User (Actor)
- Angular (Frontend)
- NestJS API (Backend)
- Auth Module
- Redis (Cache)

## Secuencia

```text
User          Angular       NestJS API      Auth Module     Redis
 │               │               │               │            │
 │  1. Refresh   │               │               │            │
 │──────────────▶│               │               │            │
 │               │  2. POST /auth/refresh        │            │
 │               │──────────────▶│               │            │
 │               │               │  3. validate refresh token  │
 │               │               │──────────────▶│            │
 │               │               │               │  4. get token             │
 │               │               │               │───────────────────────▶│
 │               │               │               │  5. token data          │
 │               │               │               │◀───────────────────────│
 │               │               │               │            │            │
 │               │               │               │  6. validate JWT        │
 │               │               │               │────────────│            │
 │               │               │               │  7. valid   │            │
 │               │               │               │◀───────────│            │
 │               │               │               │            │            │
 │               │               │               │  8. generate new access token
 │               │               │               │────────────│            │
 │               │               │               │  9. token   │            │
 │               │               │               │◀───────────│            │
 │               │               │               │            │            │
 │               │               │  10. return new token       │            │
 │               │               │◀──────────────│            │            │
 │               │  11. token    │               │            │            │
 │               │◀──────────────│               │            │            │
 │  12. success  │               │               │            │            │
 │◀──────────────│               │               │            │            │
```

---

> *Última actualización: 2026-07-27*
