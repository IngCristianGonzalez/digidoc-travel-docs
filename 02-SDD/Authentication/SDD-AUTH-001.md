# SDD-001 - Módulo de Autenticación y Autorización

## 1. Información General

| Campo | Valor |
|--------|-------|
| **Código** | SDD-AUTH-001 |
| **Módulo** | Authentication |
| **Versión** | 1.0.0 |
| **Estado** | Draft |
| **Prioridad** | Alta |

### Objetivo

Diseñar e implementar el módulo encargado de autenticar usuarios, administrar sesiones y controlar el acceso a los diferentes módulos del sistema **DigiDoc Travel**, mediante autenticación basada en JWT y autorización basada en Roles y Permisos.

---

## 2. Alcance

### Incluye

- Inicio de sesión
- Cierre de sesión
- Refresh Token
- Recuperación de contraseña
- Cambio de contraseña
- Gestión de sesiones
- Gestión de Roles
- Gestión de Permisos
- Registro de Auditoría
- Control de acceso

### No Incluye

- Registro público de usuarios
- Login con Google
- Login con Facebook
- Login con Microsoft

---

## 3. Tecnologías

| Tecnología | Implementación |
|------------|----------------|
| Frontend | Angular |
| Backend | NestJS |
| Lenguaje | TypeScript |
| Base de Datos | PostgreSQL |
| Cache | Redis |
| Broker | Kafka |
| ORM | TypeORM |
| Storage | AWS S3 |
| Cloud | AWS / Supabase |
| Autenticación | JWT |
| Hash | bcrypt |

---

## 4. Arquitectura

```text
Angular

        │

        ▼

NestJS API

        │

        ▼

Authentication Module

        │

 ┌──────┴─────────┐

 ▼                ▼

Redis        PostgreSQL

 │

 ▼

Kafka

 │

 ▼

Notification Module
```

---

## 5. Actores

| Actor | Descripción |
|--------|-------------|
| Administrador | Control total del sistema |
| Supervisor | Gestión operativa |
| Consultor | Gestión de estudiantes |
| Asesor | Seguimiento documental |
| Sistema | Procesos automáticos |

---

## 6. Casos de Uso

### CU-001 Iniciar Sesión

**Actor:** Usuario

**Flujo Principal:**

1. El usuario ingresa correo electrónico.
2. Ingresa contraseña.
3. El sistema valida las credenciales.
4. Se genera un Access Token.
5. Se genera un Refresh Token.
6. El Refresh Token se almacena en Redis.
7. Se registra la auditoría.
8. Se retorna el perfil del usuario.

---

### CU-002 Cerrar Sesión

**Flujo:**

1. Invalidar Refresh Token.
2. Eliminar sesión de Redis.
3. Registrar auditoría.
4. Retornar respuesta exitosa.

---

### CU-003 Recuperar Contraseña

**Flujo:**

1. Usuario ingresa correo.
2. Sistema genera Token temporal.
3. Publica evento en Kafka.
4. Notification Service envía correo.
5. Usuario restablece contraseña.

---

### CU-004 Cambiar Contraseña

**Flujo:**

1. Validar contraseña actual.
2. Validar nueva contraseña.
3. Actualizar hash.
4. Invalidar sesiones activas.
5. Registrar auditoría.

---

## 7. Requerimientos Funcionales

| Código | Descripción | Prioridad |
|---------|-------------|-----------|
| RF-001 | Iniciar sesión mediante correo y contraseña | Alta |
| RF-002 | Generar Access Token JWT | Alta |
| RF-003 | Generar Refresh Token | Alta |
| RF-004 | Renovar Access Token | Alta |
| RF-005 | Cerrar sesión | Alta |
| RF-006 | Recuperar contraseña | Alta |
| RF-007 | Cambiar contraseña | Alta |
| RF-008 | Administrar Roles | Alta |
| RF-009 | Administrar Permisos | Alta |
| RF-010 | Registrar Auditoría | Alta |

---

## 8. Requerimientos No Funcionales

| Código | Descripción |
|---------|-------------|
| RNF-001 | Tiempo de respuesta menor a 2 segundos |
| RNF-002 | Contraseñas cifradas con bcrypt |
| RNF-003 | JWT firmado mediante RS256 |
| RNF-004 | Refresh Token almacenado únicamente en Redis |
| RNF-005 | HTTPS obligatorio |
| RNF-006 | Rate Limit para Login |
| RNF-007 | Registro centralizado de Logs |
| RNF-008 | Disponibilidad mínima del 99% |

---

## 9. Modelo de Base de Datos

### users

| Campo | Tipo |
|--------|------|
| id | UUID |
| email | varchar |
| password | varchar |
| status | boolean |
| last_login | timestamp |
| created_at | timestamp |
| updated_at | timestamp |

### roles

| Campo | Tipo |
|--------|------|
| id | UUID |
| name | varchar |
| description | text |

### permissions

| Campo | Tipo |
|--------|------|
| id | UUID |
| module | varchar |
| action | varchar |
| description | text |

### role_permissions

| Campo | Tipo |
|--------|------|
| role_id | UUID |
| permission_id | UUID |

### user_roles

| Campo | Tipo |
|--------|------|
| user_id | UUID |
| role_id | UUID |

### audit_logs

| Campo | Tipo |
|--------|------|
| id | UUID |
| user_id | UUID |
| action | varchar |
| module | varchar |
| ip | varchar |
| device | varchar |
| created_at | timestamp |

---

## 10. Eventos Kafka

### auth.login

```json
{
  "userId": "uuid",
  "email": "user@email.com",
  "date": "2026-07-27T10:00:00Z"
}
```

### auth.logout

```json
{
  "userId": "uuid"
}
```

### auth.password.reset

```json
{
  "userId": "uuid",
  "email": "user@email.com"
}
```

---

## 11. Redis

| Key | Descripción |
|------|-------------|
| refresh:{userId} | Refresh Token |
| session:{userId} | Sesión activa |
| login_attempts:{ip} | Control de intentos |
| blacklist:{token} | Tokens inválidos |

---

## 12. API REST

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| POST | /auth/login | Inicio de sesión |
| POST | /auth/logout | Cerrar sesión |
| POST | /auth/refresh | Renovar token |
| POST | /auth/forgot-password | Recuperar contraseña |
| POST | /auth/reset-password | Restablecer contraseña |
| GET | /auth/profile | Perfil del usuario |

---

## 13. Guards

- JWT Guard
- Roles Guard
- Permissions Guard

---

## 14. Interceptores

- LoggingInterceptor
- ResponseInterceptor
- AuditInterceptor

---

## 15. Excepciones

- UnauthorizedException
- ForbiddenException
- BadRequestException
- ConflictException
- TooManyRequestsException

---

## 16. Casos de Prueba

| Código | Escenario | Resultado Esperado |
|---------|-----------|--------------------|
| TP-001 | Login correcto | Token generado |
| TP-002 | Contraseña incorrecta | Error 401 |
| TP-003 | Token expirado | Solicitar Refresh |
| TP-004 | Refresh válido | Nuevo Access Token |
| TP-005 | Refresh inválido | Error 401 |
| TP-006 | Cambio de contraseña | Actualización exitosa |
| TP-007 | Recuperación de contraseña | Correo enviado |
| TP-008 | Rate Limit | Error 429 |
| TP-009 | Acceso sin permisos | Error 403 |
| TP-010 | Auditoría | Registro almacenado |

---

## 17. Dependencias

- PostgreSQL
- Redis
- Kafka
- Notification Module
- User Module
- Roles Module

---

## 18. Criterios de Aceptación

- El usuario puede autenticarse correctamente.
- Solo usuarios autorizados acceden al sistema.
- Los Refresh Tokens son almacenados en Redis.
- Todas las acciones quedan registradas en auditoría.
- Los permisos son evaluados antes de acceder a cualquier recurso.
- Los eventos de autenticación son publicados en Kafka.
- El módulo cumple con los estándares de seguridad definidos para DigiDoc Travel.

---

> *Última actualización: 2026-07-27*
