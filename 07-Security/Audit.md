# Auditoría

## Eventos Registrados

| Evento | Descripción | Severidad |
|--------|-------------|-----------|
| auth.login | Inicio de sesión | INFO |
| auth.logout | Cierre de sesión | INFO |
| auth.login.failed | Login fallido | WARN |
| auth.password.changed | Contraseña cambiada | INFO |
| auth.password.reset | Contraseña restablecida | INFO |
| user.created | Usuario creado | INFO |
| user.updated | Usuario actualizado | INFO |
| user.deleted | Usuario eliminado | WARN |
| document.uploaded | Documento subido | INFO |
| document.deleted | Documento eliminado | WARN |

## Campos de Auditoría

| Campo | Descripción |
|-------|-------------|
| id | UUID único |
| user_id | ID del usuario |
| action | Acción realizada |
| module | Módulo afectado |
| ip | Dirección IP |
| device | Dispositivo/Agent |
| timestamp | Fecha y hora |

## Retención

| Tipo | Retención |
|------|-----------|
| Logs de auditoría | 1 año |
| Logs de aplicación | 30 días |
| Logs de error | 90 días |

## Consulta

```sql
-- Últimas acciones de un usuario
SELECT * FROM audit_logs 
WHERE user_id = 'uuid' 
ORDER BY created_at DESC 
LIMIT 100;
```

---

> *Última actualización: 2026-07-27*
