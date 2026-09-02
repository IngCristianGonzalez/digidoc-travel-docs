# Requerimientos No Funcionales

## RNF-001: Rendimiento

| Código | Descripción | Métrica |
|--------|-------------|---------|
| RNF-001-01 | Tiempo de respuesta API | < 2 segundos |
| RNF-001-02 | Tiempo de carga inicial | < 3 segundos |
| RNF-001-03 | Concurrentes simultáneos | > 1000 |

## RNF-002: Disponibilidad

| Código | Descripción | Métrica |
|--------|-------------|---------|
| RNF-002-01 | Uptime del sistema | 99.9% |
| RNF-002-02 | Ventana de mantenimiento | < 4 horas/mes |
| RNF-002-03 | Recovery Time Objective | < 1 hora |
| RNF-002-04 | Recovery Point Objective | < 5 minutos |

## RNF-003: Seguridad

| Código | Descripción | Estándar |
|--------|-------------|----------|
| RNF-003-01 | Cifrado de contraseñas | bcrypt |
| RNF-003-02 | Autenticación | JWT RS256 |
| RNF-003-03 | HTTPS | Obligatorio |
| RNF-003-04 | Rate Limiting | 100 req/min |
| RNF-003-05 | Auditoría | Todas las acciones críticas |

## RNF-004: Escalabilidad

| Código | Descripción | Métrica |
|--------|-------------|---------|
| RNF-004-01 | Horizontal scaling | Auto-scaling |
| RNF-004-02 | Base de datos | Read replicas |
| RNF-004-03 | Cache | Redis cluster |

## RNF-005: Mantenibilidad

| Código | Descripción | Métrica |
|--------|-------------|---------|
| RNF-005-01 | Cobertura de tests | > 80% |
| RNF-005-02 | Documentación | Actualizada |
| RNF-005-03 | Code review | Obligatorio |

## RNF-006: Compatibilidad

| Código | Descripción | Versión |
|--------|-------------|---------|
| RNF-006-01 | Navegadores | Chrome, Firefox, Safari, Edge |
| RNF-006-02 | Responsive | Desktop, Tablet, Mobile |
| RNF-006-03 | API | RESTful, versionada |

---

> *Última actualización: 2026-07-27*
