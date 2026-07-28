# Índices de Base de Datos

## users

```sql
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_status ON users(status);
CREATE INDEX idx_users_created_at ON users(created_at);
```

## roles

```sql
CREATE INDEX idx_roles_name ON roles(name);
```

## permissions

```sql
CREATE INDEX idx_permissions_module ON permissions(module);
CREATE INDEX idx_permissions_action ON permissions(action);
CREATE INDEX idx_permissions_module_action ON permissions(module, action);
```

## audit_logs

```sql
CREATE INDEX idx_audit_logs_user_id ON audit_logs(user_id);
CREATE INDEX idx_audit_logs_action ON audit_logs(action);
CREATE INDEX idx_audit_logs_module ON audit_logs(module);
CREATE INDEX idx_audit_logs_created_at ON audit_logs(created_at);
CREATE INDEX idx_audit_logs_user_action ON audit_logs(user_id, action);
```

## user_roles

```sql
CREATE INDEX idx_user_roles_user_id ON user_roles(user_id);
CREATE INDEX idx_user_roles_role_id ON user_roles(role_id);
```

## role_permissions

```sql
CREATE INDEX idx_role_permissions_role_id ON role_permissions(role_id);
CREATE INDEX idx_role_permissions_permission_id ON role_permissions(permission_id);
```

---

> *Última actualización: 2026-07-27*
