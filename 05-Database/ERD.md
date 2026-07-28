# Modelo de Datos - ERD

## Diagrama Entidad-Relación

```text
┌─────────────────┐       ┌─────────────────┐
│      users      │       │      roles      │
├─────────────────┤       ├─────────────────┤
│ id (UUID) PK    │       │ id (UUID) PK    │
│ email           │       │ name            │
│ password        │       │ description     │
│ status          │       │ created_at      │
│ last_login      │       │ updated_at      │
│ created_at      │       └────────┬────────┘
│ updated_at      │                │
└────────┬────────┘                │
         │                         │
         │    ┌────────────────────┤
         │    │                    │
         ▼    ▼                    ▼
┌─────────────────┐       ┌─────────────────┐
│   user_roles    │       │role_permissions │
├─────────────────┤       ├─────────────────┤
│ user_id (FK)    │       │ role_id (FK)    │
│ role_id (FK)    │       │ permission_id   │
└─────────────────┘       └────────┬────────┘
                                   │
                                   ▼
                          ┌─────────────────┐
                          │   permissions   │
                          ├─────────────────┤
                          │ id (UUID) PK    │
                          │ module          │
                          │ action          │
                          │ description     │
                          │ created_at      │
                          │ updated_at      │
                          └─────────────────┘

┌─────────────────┐
│   audit_logs    │
├─────────────────┤
│ id (UUID) PK    │
│ user_id (FK)    │
│ action          │
│ module          │
│ ip              │
│ device          │
│ created_at      │
└─────────────────┘
```

## Relaciones

| Relación | Tipo | Descripción |
|----------|------|-------------|
| users → user_roles | 1:N | Un usuario tiene muchos roles |
| roles → user_roles | 1:N | Un rol tiene muchos usuarios |
| roles → role_permissions | 1:N | Un rol tiene muchos permisos |
| permissions → role_permissions | 1:N | Un permiso está en muchos roles |
| users → audit_logs | 1:N | Un usuario tiene muchos logs |

---

> *Última actualización: 2026-07-27*
