# SDD-002 - Módulo de Gestión de Usuarios

## 1. Información General

| Campo | Valor |
|--------|-------|
| **Código** | SDD-USERS-002 |
| **Módulo** | Users |
| **Versión** | 1.0.0 |
| **Estado** | Draft |
| **Prioridad** | Alta |

### Objetivo

Diseñar e implementar el módulo encargado de gestionar los usuarios del sistema **DigiDoc Travel**, incluyendo registro, edición, desactivación y asignación de roles.

---

## 2. Alcance

### Incluye

- Registro de usuarios
- Edición de información de usuarios
- Desactivación de usuarios
- Consulta de usuarios
- Asignación de roles a usuarios

### No Incluye

- Autenticación (ver SDD-001)
- Gestión de permisos (ver SDD-001)
- Perfil de usuario (ver SDD-001)

---

## 3. Requerimientos Asociados

| ID | Descripción |
|----|-------------|
| RF-007 | Registrar usuarios |
| RF-008 | Editar información de usuarios |
| RF-009 | Desactivar usuarios |
| RF-010 | Consultar usuarios |
| RF-011 | Asignar roles a usuarios |

---

## 4. Actores

| Actor | Descripción |
|--------|-------------|
| Administrador | Control total del sistema |
| Supervisor | Gestión operativa |

---

## 5. Casos de Uso

### CU-001 Registrar Usuario

**Actor:** Administrador  
**Precondiciones:** Rol ADMIN autenticado  
**Postcondiciones:** Usuario creado

**Flujo Principal:**

1. El administrador accede a gestión de usuarios
2. Selecciona "Crear usuario"
3. Ingresa email, nombre y contraseña
4. Selecciona rol(es)
5. El sistema valida los datos
6. Se crea el usuario
7. Se registra auditoría

**Flujo Alternativo:**

- 5a. Email ya existe → Error 409

---

### CU-002 Editar Usuario

**Actor:** Administrador  
**Precondiciones:** Usuario existente  
**Postcondiciones:** Usuario actualizado

**Flujo Principal:**

1. El administrador selecciona un usuario
2. Selecciona "Editar"
3. Modifica los campos permitidos
4. Guarda los cambios
5. Se registra auditoría

---

### CU-003 Desactivar Usuario

**Actor:** Administrador  
**Precondiciones:** Usuario activo  
**Postcondiciones:** Usuario desactivado

**Flujo Principal:**

1. El administrador selecciona un usuario
2. Selecciona "Desactivar"
3. Confirma la acción
4. El usuario queda desactivado
5. Se invalidan sesiones activas
6. Se registra auditoría

**Flujo Alternativo:**

- 3a. Usuario es el último admin → Error 400

---

### CU-004 Consultar Usuarios

**Actor:** Administrador, Supervisor  
**Precondiciones:** Rol válido  
**Postcondiciones:** Lista de usuarios

**Flujo Principal:**

1. El usuario accede a gestión de usuarios
2. El sistema muestra la lista
3. Puede filtrar por: email, rol, estado
4. Puede paginar resultados

---

### CU-005 Asignar Roles

**Actor:** Administrador  
**Precondiciones:** Usuario y roles existentes  
**Postcondiciones:** Roles asignados

**Flujo Principal:**

1. El administrador selecciona un usuario
2. Selecciona "Asignar roles"
3. Marca los roles a asignar
4. Guarda los cambios
5. Se registra auditoría

---

## 6. Modelo de Base de Datos

### users

| Campo | Tipo | Constraints |
|--------|------|-------------|
| id | UUID | PK |
| email | VARCHAR(255) | UNIQUE, NOT NULL |
| password | VARCHAR(255) | NOT NULL |
| first_name | VARCHAR(100) | NOT NULL |
| last_name | VARCHAR(100) | NOT NULL |
| phone | VARCHAR(20) | |
| status | BOOLEAN | DEFAULT true |
| last_login | TIMESTAMP | |
| created_at | TIMESTAMP | DEFAULT NOW() |
| updated_at | TIMESTAMP | DEFAULT NOW() |

---

## 7. API REST

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| POST | /users | Crear usuario | ADMIN |
| GET | /users | Listar usuarios | ADMIN, SUP |
| GET | /users/:id | Obtener usuario | ADMIN, SUP |
| PATCH | /users/:id | Actualizar usuario | ADMIN |
| DELETE | /users/:id | Desactivar usuario | ADMIN |
| POST | /users/:id/roles | Asignar roles | ADMIN |

---

## 8. Requerimientos No Funcionales

| Código | Descripción |
|---------|-------------|
| RNF-001 | Tiempo de respuesta menor a 2 segundos |
| RNF-002 | Contraseñas cifradas con bcrypt |
| RNF-003 | Paginación obligatoria en listados |
| RNF-004 | Búsqueda con filtros y ordenamiento |
| RNF-005 | Registro de auditoría en todas las operaciones |

---

## 9. Casos de Prueba

| Código | Escenario | Resultado Esperado |
|---------|-----------|--------------------|
| TP-001 | Crear usuario válido | Usuario creado |
| TP-002 | Crear usuario con email duplicado | Error 409 |
| TP-003 | Editar usuario | Datos actualizados |
| TP-004 | Desactivar usuario | Usuario inactivo |
| TP-005 | Desactivar último admin | Error 400 |
| TP-006 | Asignar roles | Roles asignados |
| TP-007 | Listar usuarios con filtros | Lista filtrada |

---

## 10. Dependencias

- SDD-001 (Authentication)
- PostgreSQL
- Redis (sesiones)

---

## 11. Criterios de Aceptación

- El administrador puede crear usuarios correctamente
- Los roles se asignan y validan correctamente
- Los usuarios desactivados no pueden iniciar sesión
- Todas las operaciones quedan registradas en auditoría
- La búsqueda y filtrado funcionan correctamente

---

> *Última actualización: 2026-07-27*
