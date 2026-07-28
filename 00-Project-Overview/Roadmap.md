# Roadmap del Proyecto

## Fase 1: Fundamentos (Semanas 1-4)

### Semana 1-2: Infraestructura
- [ ] Configurar repositorios
- [ ] Setup de Angular y NestJS
- [ ] Configurar Docker
- [ ] Configurar CI/CD
- [ ] Setup de bases de datos

### Semana 3-4: Módulo de Autenticación
- [ ] Implementar JWT
- [ ] Login / Logout
- [ ] Gestión de sesiones
- [ ] Roles y permisos
- [ ] Auditoría

---

## Fase 2: Módulos Core (Semanas 5-10)

### Semana 5-6: Módulo de Usuarios
- [ ] CRUD de usuarios
- [ ] Perfiles
- [ ] Asignación de roles

### Semana 7-8: Módulo de Estudiantes
- [ ] Registro de estudiantes
- [ ] Documentos personales
- [ ] Historial

### Semana 9-10: Módulo de Documentos
- [ ] Carga de archivos
- [ ] Validación
- [ ] Versionado
- [ ] Almacenamiento S3

---

## Fase 3: Módulos Secundarios (Semanas 11-14)

### Semana 11-12: Módulo de Visa
- [ ] Seguimiento de solicitudes
- [ ] Estados
- [ ] Notificaciones

### Semana 13-14: Módulo de Pagos
- [ ] Registro de pagos
- [ ] Estados
- [ ] Historial

---

## Fase 4: Integraciones (Semanas 15-16)

### Semana 15: Notificaciones
- [ ] Email (SES)
- [ ] Push notifications
- [ ] Eventos Kafka

### Semana 16: Dashboard y Reportes
- [ ] Panel administrativo
- [ ] Reportes básicos
- [ ] Métricas

---

## Fase 5: QA y Deploy (Semanas 17-18)

### Semana 17: Testing
- [ ] Unit tests
- [ ] Integration tests
- [ ] E2E tests

### Semana 18: Deploy
- [ ] Deploy a staging
- [ ] Pruebas de aceptación
- [ ] Deploy a producción

---

## Cronograma Visual

```
Fase 1: ████░░░░░░░░░░░░░░░░  (Semanas 1-4)
Fase 2: ░░░░████████░░░░░░░░  (Semanas 5-10)
Fase 3: ░░░░░░░░░░░░████░░░░  (Semanas 11-14)
Fase 4: ░░░░░░░░░░░░░░░░██░░  (Semanas 15-16)
Fase 5: ░░░░░░░░░░░░░░░░░░██  (Semanas 17-18)
```

---

## Hitos Principales

| Hito | Fecha Estimada | Dependencias |
|------|----------------|--------------|
| MVP Auth | Semana 4 | Ninguna |
| MVP Users | Semana 6 | Auth |
| MVP Students | Semana 8 | Users |
| MVP Documents | Semana 10 | Students |
| Beta | Semana 16 | Todos |
| Producción | Semana 18 | Beta |

---

> *Última actualización: 2026-07-27*
