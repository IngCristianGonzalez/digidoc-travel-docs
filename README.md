# DigiDoc Travel Docs

Documentación técnica del proyecto **DigiDoc Travel** - Plataforma de gestión documental para estudiantes internacionales.

## Stack Tecnológico

| Capa | Tecnología |
|------|------------|
| Frontend | Angular 17+ |
| Backend | NestJS |
| Lenguaje | TypeScript |
| Base de Datos | PostgreSQL (Supabase) |
| Cache | Redis |
| Mensajería | Apache Kafka |
| ORM | TypeORM |
| Almacenamiento | AWS S3 |
| Autenticación | JWT (RS256) |

---

## Estructura del Proyecto

```
digidoc-travel-docs/
│
├── README.md                    # Este archivo
├── CONTRIBUTING.md              # Guía de contribución
├── CHANGELOG.md                 # Historial de cambios
│
├── 00-Project-Overview/         # Visión general del proyecto
├── 01-SRS/                      # Especificación de Requerimientos
├── 02-SDD/                      # Documentos de Diseño de Software
├── 03-Architecture/             # Diagramas de arquitectura
├── 04-API/                      # Documentación de endpoints
├── 05-Database/                 # Modelo de datos
├── 06-DevOps/                   # Infraestructura y despliegue
├── 07-Security/                 # Seguridad y auditoría
├── 08-Test/                     # Estrategia de pruebas
└── diagrams/                    # Prompts para generación de diagramas
```

---

## 00-Project-Overview

Visión general y dirección del proyecto.

| Archivo | Descripción |
|---------|-------------|
| `Vision.md` | Visión y objetivos del proyecto |
| `Scope.md` | Alcance incluido y excluido |
| `Architecture.md` | Arquitectura general del sistema |
| `TechStack.md` | Stack tecnológico detallado |
| `Roadmap.md` | Cronograma y fases de desarrollo |

---

## 01-SRS (Software Requirements Specification)

Especificación de requerimientos del sistema.

| Archivo | Descripción |
|---------|-------------|
| `FunctionalRequirements.md` | Requerimientos funcionales por módulo |
| `NonFunctionalRequirements.md` | Rendimiento, disponibilidad, seguridad |
| `BusinessRules.md` | Reglas de negocio del dominio |
| `UserRoles.md` | Roles y matriz de permisos |
| `UseCases.md` | Casos de uso principales |
| `Glossary.md` | Glosario de términos |

---

## 02-SDD (Software Design Document)

Documentos de diseño por módulo.

| Módulo | Descripción |
|--------|-------------|
| `Authentication/` | SDD-001: Autenticación y autorización |
| `Users/` | Gestión de usuarios |
| `Students/` | Gestión de estudiantes |
| `Documents/` | Gestión documental |
| `Visa/` | Seguimiento de visas |
| `Payments/` | Gestión de pagos |
| `Events/` | Gestión de eventos |
| `Notifications/` | Sistema de notificaciones |
| `Dashboard/` | Panel administrativo |
| `Reports/` | Generación de reportes |

### Módulo Auth (SDD-001)

Documento completo en [`02-SDD/Authentication/SDD-AUTH-001.md`](./02-SDD/Authentication/SDD-AUTH-001.md)

---

## 03-Architecture

Diagramas de arquitectura del sistema.

| Carpeta | Contenido |
|---------|-----------|
| `C4/` | Diagramas de contexto, contenedor y componentes |
| `Sequence/` | Diagramas de secuencia (login, refresh token) |
| `Deployment/` | Diagrama de despliegue |
| `Database/` | Diagrama de entidad-relación |
| `Integrations/` | Integraciones con servicios externos |

---

## 04-API

Documentación de la API REST.

| Archivo | Descripción |
|---------|-------------|
| `OpenAPI.yaml` | Especificación OpenAPI 3.0 |
| `Authentication.md` | Endpoints de autenticación |
| `Students.md` | Endpoints de estudiantes |
| `Documents.md` | Endpoints de documentos |
| `Visa.md` | Endpoints de visa |
| `Payments.md` | Endpoints de pagos |
| `Events.md` | Endpoints de eventos |

### Endpoints Principales

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/auth/login` | Inicio de sesión |
| POST | `/auth/logout` | Cerrar sesión |
| POST | `/auth/refresh` | Renovar token |
| GET | `/auth/profile` | Perfil del usuario |

---

## 05-Database

Modelo de datos y estrategia de base de datos.

| Archivo | Descripción |
|---------|-------------|
| `ERD.md` | Diagrama entidad-relación |
| `Tables.md` | Script de creación de tablas |
| `Indexes.md` | Índices para optimización |
| `Migrations.md` | Estrategia de migraciones |
| `Seeders.md` | Datos iniciales |

### Tablas Principales

| Tabla | Descripción |
|-------|-------------|
| `users` | Usuarios del sistema |
| `roles` | Roles disponibles |
| `permissions` | Permisos por módulo |
| `user_roles` | Relación usuario-rol |
| `role_permissions` | Relación rol-permiso |
| `audit_logs` | Registro de auditoría |

---

## 06-DevOps

Infraestructura, despliegue y operaciones.

| Archivo | Descripción |
|---------|-------------|
| `AWS.md` | Servicios AWS utilizados |
| `Docker.md` | Configuración de contenedores |
| `CI-CD.md` | Pipeline de integración continua |
| `Monitoring.md` | Monitoreo y alertas |
| `Backup.md` | Estrategia de respaldos |

---

## 07-Security

Seguridad, autenticación y auditoría.

| Archivo | Descripción |
|---------|-------------|
| `Authentication.md` | Configuración JWT y bcrypt |
| `Authorization.md` | RBAC y control de acceso |
| `Encryption.md` | Cifrado de datos |
| `Audit.md` | Registro de auditoría |
| `OWASP.md` | Mitigaciones OWASP Top 10 |

---

## 08-Test

Estrategia de pruebas del sistema.

| Archivo | Descripción |
|---------|-------------|
| `Unit.md` | Tests unitarios |
| `Integration.md` | Tests de integración |
| `E2E.md` | Tests end-to-end |
| `Acceptance.md` | Criterios de aceptación |

---

## diagrams/

Prompts listos para generar diagramas con herramientas externas (Mermaid, PlantUML, draw.io).

| Prompt | Descripción |
|--------|-------------|
| `architecture/auth-module.md` | Arquitectura del módulo Auth |
| `sequence/login-flow.md` | Secuencia de login |
| `sequence/refresh-token.md` | Secuencia de refresh token |
| `erd/auth-tables.md` | Diagrama ERD de tablas Auth |

### Uso

1. Copia el contenido del prompt
2. Pégalo en tu herramienta de generación de diagramas
3. Genera el diagrama
4. Guarda la imagen en la carpeta correspondiente

---

## Commits

Este proyecto sigue [Conventional Commits](https://www.conventionalcommits.org/).

```
feat: add new feature
fix: bug fix
docs: documentation update
style: formatting changes
refactor: code refactoring
test: add or update tests
chore: maintenance tasks
```

---

## Licencia

Propietario - DigiDoc Travel

---

> *Última actualización: 2026-07-27*
