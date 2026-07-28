# Diagrama de Componentes C4

## Descripción

Diagrama de nivel 3 que muestra los componentes internos de cada contenedor.

## Componentes del Módulo Auth

| Componente | Responsabilidad |
|------------|-----------------|
| AuthController | Endpoints REST |
| AuthService | Lógica de autenticación |
| JwtService | Generación y validación JWT |
| RedisService | Gestión de sesiones |
| UserRepository | Acceso a datos de usuarios |
| RoleRepository | Acceso a datos de roles |
| AuditService | Registro de auditoría |

## Diagrama

```text
┌─────────────────────────────────────────────────────────────┐
│                    Auth Module                               │
│                                                              │
│  ┌──────────────────┐    ┌──────────────────┐               │
│  │  AuthController  │───▶│   AuthService    │               │
│  └──────────────────┘    └────────┬─────────┘               │
│                                   │                          │
│              ┌────────────────────┼────────────────────┐     │
│              ▼                    ▼                    ▼     │
│  ┌──────────────────┐  ┌──────────────────┐  ┌───────────┐ │
│  │   JwtService     │  │  RedisService    │  │AuditService│ │
│  └──────────────────┘  └──────────────────┘  └───────────┘ │
│              │                    │                          │
│              ▼                    ▼                          │
│  ┌──────────────────┐  ┌──────────────────┐                │
│  │ UserRepository   │  │  RoleRepository  │                │
│  └──────────────────┘  └──────────────────┘                │
└─────────────────────────────────────────────────────────────┘
```

---

> *Última actualización: 2026-07-27*
