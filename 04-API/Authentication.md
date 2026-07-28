# API Authentication

## Endpoints

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| POST | /auth/login | Inicio de sesión | No |
| POST | /auth/logout | Cerrar sesión | Sí |
| POST | /auth/refresh | Renovar token | No |
| POST | /auth/forgot-password | Recuperar contraseña | No |
| POST | /auth/reset-password | Restablecer contraseña | No |
| GET | /auth/profile | Perfil del usuario | Sí |

## Request/Response

### POST /auth/login

**Request:**
```json
{
  "email": "user@email.com",
  "password": "password123"
}
```

**Response 200:**
```json
{
  "accessToken": "eyJhbGciOiJSUzI1NiIs...",
  "refreshToken": "abc123...",
  "user": {
    "id": "uuid",
    "email": "user@email.com",
    "roles": ["admin"]
  }
}
```

### POST /auth/refresh

**Request:**
```json
{
  "refreshToken": "abc123..."
}
```

**Response 200:**
```json
{
  "accessToken": "eyJhbGciOiJSUzI1NiIs..."
}
```

---

> *Última actualización: 2026-07-27*
