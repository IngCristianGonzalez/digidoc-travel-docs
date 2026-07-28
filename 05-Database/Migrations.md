# Migraciones

## Estrategia

- Usar TypeORM migrations
- Migraciones en carpetas por módulo
- Naming convention: `Timestamp-Description.ts`

## Estructura

```
src/
├── database/
│   ├── migrations/
│   │   ├── 1690000000000-CreateUsers.ts
│   │   ├── 1690000001000-CreateRoles.ts
│   │   ├── 1690000002000-CreatePermissions.ts
│   │   ├── 1690000003000-CreateUserRoles.ts
│   │   ├── 1690000004000-CreateRolePermissions.ts
│   │   └── 1690000005000-CreateAuditLogs.ts
│   └── seeds/
```

## Comandos

```bash
# Generar migración
npm run migration:generate -- src/database/migrations/MigrationName

# Ejecutar migraciones
npm run migration:run

# Revertir migración
npm run migration:revert
```

---

> *Última actualización: 2026-07-27*
