# Prompt: Diagrama ERD - Tablas de Auth

## Instrucciones

Usa este prompt con una herramienta de generación de diagramas ERD (Mermaid, dbdiagram.io, etc.)

## Prompt

```
Genera un diagrama entidad-relación para el módulo de autenticación de DigiDoc Travel con las siguientes tablas:

Tabla: users
- id: UUID (PK)
- email: VARCHAR(255) UNIQUE NOT NULL
- password: VARCHAR(255) NOT NULL
- status: BOOLEAN DEFAULT true
- last_login: TIMESTAMP
- created_at: TIMESTAMP
- updated_at: TIMESTAMP

Tabla: roles
- id: UUID (PK)
- name: VARCHAR(100) UNIQUE NOT NULL
- description: TEXT
- created_at: TIMESTAMP
- updated_at: TIMESTAMP

Tabla: permissions
- id: UUID (PK)
- module: VARCHAR(100) NOT NULL
- action: VARCHAR(100) NOT NULL
- description: TEXT
- created_at: TIMESTAMP
- updated_at: TIMESTAMP

Tabla: user_roles (junction)
- user_id: UUID (FK → users.id)
- role_id: UUID (FK → roles.id)
- PRIMARY KEY (user_id, role_id)

Tabla: role_permissions (junction)
- role_id: UUID (FK → roles.id)
- permission_id: UUID (FK → permissions.id)
- PRIMARY KEY (role_id, permission_id)

Tabla: audit_logs
- id: UUID (PK)
- user_id: UUID (FK → users.id)
- action: VARCHAR(100) NOT NULL
- module: VARCHAR(100) NOT NULL
- ip: VARCHAR(45)
- device: TEXT
- created_at: TIMESTAMP

Relaciones:
- users 1:N user_roles
- roles 1:N user_roles
- roles 1:N role_permissions
- permissions 1:N role_permissions
- users 1:N audit_logs

Estilo: Diagrama ERD con colores por dominio, cardinalidad clara
```

## Salida Esperada

Un diagrama que muestre:
- Todas las tablas con sus campos
- Relaciones 1:N y N:N
- Cardinalidad
- Índices principales

---

> *Última actualización: 2026-07-27*
