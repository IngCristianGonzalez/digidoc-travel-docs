# Roles de Usuario

## Lista de Roles

| Rol | Código | Descripción | Nivel |
|-----|--------|-------------|-------|
| Administrador | ADMIN | Control total del sistema | 1 |
| Supervisor | SUP | Gestión operativa | 2 |
| Consultor | CONS | Gestión de estudiantes | 3 |
| Asesor | ASES | Seguimiento documental | 4 |
| Estudiante | EST | Consulta y documentos | 5 |

## Matriz de Permisos

| Módulo | ADMIN | SUP | CONS | ASES | EST |
|--------|-------|-----|------|------|-----|
| **Users** | CRUD | R | - | - | - |
| **Students** | CRUD | CRUD | CRUD | R | R* |
| **Documents** | CRUD | CRUD | CRUD | R | CRUD* |
| **Visa** | CRUD | CRUD | R | R | R* |
| **Payments** | CRUD | CRUD | R | - | R* |
| **Events** | CRUD | CRUD | CRUD | R | R |
| **Notifications** | CRUD | CRUD | R | R | R |
| **Dashboard** | Full | Full | Partial | Partial | Basic |
| **Reports** | Full | Full | R | - | - |
| **Settings** | CRUD | R | - | - | - |

**Leyenda:**
- CRUD: Crear, Leer, Actualizar, Eliminar
- R: Solo lectura
- R*: Solo registros propios
- -: Sin acceso

## Descripción por Rol

### Administrador (ADMIN)
- Acceso total al sistema
- Gestión de usuarios y roles
- Configuración del sistema
- Reportes completos
- Auditoría

### Supervisor (SUP)
- Gestión operativa diaria
- Supervisión de consultores
- Aprobación de documentos
- Reportes de su área

### Consultor (CONS)
- Gestión de estudiantes asignados
- Carga y validación de documentos
- Seguimiento de visas
- Comunicación con asesores

### Asesor (ASES)
- Seguimiento documental
- Consulta de información
- Notificaciones
- Reportes básicos

### Estudiante (EST)
- Consulta de su información
- Carga de documentos propios
- Seguimiento de su visa
- Historial de pagos

---

> *Última actualización: 2026-07-27*
