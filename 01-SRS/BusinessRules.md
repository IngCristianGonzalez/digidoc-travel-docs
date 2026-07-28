# Reglas de Negocio

## RN-001: Autenticación

| Código | Regla | Excepción |
|--------|-------|-----------|
| RN-001-01 | Un usuario debe tener email único | Ninguna |
| RN-001-02 | La contraseña debe tener mínimo 8 caracteres | Ninguna |
| RN-001-03 | Intentos fallidos máximos: 5 | Bloqueo temporal |
| RN-001-04 | Token de acceso expira en 15 minutos | Refresh token válido |
| RN-001-05 | Refresh token expira en 7 días | Ninguna |

## RN-002: Usuarios

| Código | Regla | Excepción |
|--------|-------|-----------|
| RN-002-01 | Un usuario debe tener al menos un rol | Administrador |
| RN-002-02 | Un usuario puede tener múltiples roles | Ninguna |
| RN-002-03 | Un usuario desactivado no puede iniciar sesión | Administrador |
| RN-002-04 | Solo administradores pueden crear usuarios | Ninguna |

## RN-003: Roles y Permisos

| Código | Regla | Excepción |
|--------|-------|-----------|
| RN-003-01 | Un rol debe tener al menos un permiso | Ninguna |
| RN-003-02 | Los permisos son por módulo y acción | Ninguna |
| RN-003-03 | Un usuario hereda permisos de todos sus roles | Ninguna |
| RN-003-04 | No se pueden eliminar roles en uso | Reasignar primero |

## RN-004: Documentos

| Código | Regla | Excepción |
|--------|-------|-----------|
| RN-004-01 | Tamaño máximo de archivo: 10MB | Administrador |
| RN-004-02 | Formatos permitidos: PDF, JPG, PNG | Ninguna |
| RN-004-03 | Un documento debe estar asociado a un estudiante | Ninguna |
| RN-004-04 | Los documentos requieren validación | Ninguna |

## RN-005: Visa

| Código | Regla | Excepción |
|--------|-------|-----------|
| RN-005-01 | Una solicitud debe tener todos los documentos | Ninguna |
| RN-005-02 | El estado solo puede avanzar | Administrador |
| RN-005-03 | No se puede crear solicitud duplicada | Ninguna |

## RN-006: Pagos

| Código | Regla | Excepción |
|--------|-------|-----------|
| RN-006-01 | Un pago debe estar asociado a un servicio | Ninguna |
| RN-006-02 | El monto no puede ser negativo | Ninguna |
| RN-006-03 | Los pagos requieren verificación | Ninguna |

---

> *Última actualización: 2026-07-27*
