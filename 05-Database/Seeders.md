# Seeders

## Datos Iniciales

### Roles

```sql
INSERT INTO roles (id, name, description) VALUES
    ('uuid-1', 'ADMIN', 'Administrador del sistema'),
    ('uuid-2', 'SUP', 'Supervisor operativo'),
    ('uuid-3', 'CONS', 'Consultor de estudiantes'),
    ('uuid-4', 'ASES', 'Asesor documental'),
    ('uuid-5', 'EST', 'Estudiante');
```

### Permisos

```sql
INSERT INTO permissions (id, module, action, description) VALUES
    ('uuid-p1', 'users', 'create', 'Crear usuarios'),
    ('uuid-p2', 'users', 'read', 'Leer usuarios'),
    ('uuid-p3', 'users', 'update', 'Actualizar usuarios'),
    ('uuid-p4', 'users', 'delete', 'Eliminar usuarios'),
    -- ... más permisos
```

## Comandos

```bash
# Ejecutar seeds
npm run seed

# Seed específico
npm run seed -- --module=auth
```

---

> *Última actualización: 2026-07-27*
