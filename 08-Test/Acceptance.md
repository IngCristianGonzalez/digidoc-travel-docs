# Tests de Aceptación

## Criterios de Aceptación

### Auth Module

| ID | Criterio | Estado |
|----|----------|--------|
| CA-001 | Usuario puede iniciar sesión | Pendiente |
| CA-002 | Credenciales incorrectas rechazadas | Pendiente |
| CA-003 | Token expirado solicita refresh | Pendiente |
| CA-004 | Refresh token válido renueva access | Pendiente |
| CA-005 | Cerrar sesión invalida tokens | Pendiente |
| CA-006 | Recuperar contraseña envía email | Pendiente |
| CA-007 | Cambiar contraseña actualiza hash | Pendiente |
| CA-008 | Rate limiting funciona | Pendiente |
| CA-009 | Auditoría registra acciones | Pendiente |
| CA-010 | Roles y permisos funcionan | Pendiente |

## Flujo de Validación

```text
1. Ejecutar tests automatizados
2. Revisión manual de UI
3. Validación con stakeholder
4. Documentar resultados
5. Aprobar o rechazar
```

## Checklist

- [ ] Login funciona correctamente
- [ ] Logout invalida sesión
- [ ] Refresh token renueva access
- [ ] Permisos bloquean acceso no autorizado
- [ ] Auditoría registra todas las acciones
- [ ] Rate limiting previene abuso
- [ ] Errores son descriptivos
- [ ] UI es responsiva

---

> *Última actualización: 2026-07-27*
