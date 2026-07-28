# Autorización

## RBAC (Role-Based Access Control)

### Roles

| Rol | Nivel | Descripción |
|-----|-------|-------------|
| ADMIN | 1 | Control total |
| SUP | 2 | Gestión operativa |
| CONS | 3 | Gestión de estudiantes |
| ASES | 4 | Seguimiento documental |
| EST | 5 | Consulta propia |

### Permisos

| Formato | Ejemplo |
|---------|---------|
| `module:action` | `users:create` |
| `module:action:*` | `students:*` (todas las acciones) |
| `*:*` | Acceso total |

## Guards

| Guard | Responsabilidad |
|-------|-----------------|
| JwtGuard | Validar token |
| RolesGuard | Validar roles |
| PermissionsGuard | Validar permisos |

## Implementación

```typescript
@UseGuards(JwtGuard, RolesGuard)
@Roles('ADMIN', 'SUP')
@Controller('users')
export class UsersController {}
```

---

> *Última actualización: 2026-07-27*
