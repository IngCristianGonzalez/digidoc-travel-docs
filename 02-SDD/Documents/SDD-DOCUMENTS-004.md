# SDD-004 - Módulo de Gestión Documental

## 1. Información General

| Campo | Valor |
|--------|-------|
| **Código** | SDD-DOCUMENTS-004 |
| **Módulo** | Documents |
| **Versión** | 1.0.0 |
| **Estado** | Draft |
| **Prioridad** | Alta |

### Objetivo

Diseñar e implementar el módulo encargado de gestionar los documentos digitales en el sistema **DigiDoc Travel**.

---

## 2. Alcance

### Incluye

- Registro de documentos
- Carga de archivos digitales
- Edición de información documental
- Eliminación de documentos
- Descarga de documentos
- Búsqueda por filtros
- Clasificación por categoría
- Historial de modificaciones

---

## 3. Requerimientos Asociados

| ID | Descripción |
|----|-------------|
| RF-017 | Registrar documentos |
| RF-018 | Cargar archivos digitales |
| RF-019 | Editar información documental |
| RF-020 | Eliminar documentos |
| RF-021 | Descargar documentos |
| RF-022 | Buscar documentos por filtros |
| RF-023 | Clasificar documentos por categoría |
| RF-024 | Mantener historial de modificaciones |

---

## 4. Casos de Uso

### CU-001 Registrar Documento

**Actor:** Consultor, Administrador  
**Flujo:**

1. Selecciona tipo de documento
2. Ingresa metadatos (nombre, descripción, estudiante asociado)
3. Selecciona archivo
4. Sistema valida formato y tamaño
5. Archivo se almacena en S3
6. Se crea registro en BD
7. Se registra auditoría

---

### CU-002 Cargar Archivo

**Actor:** Consultor, Administrador  
**Flujo:**

1. Selecciona archivo local
2. Sistema valida:
   - Formato: PDF, JPG, PNG
   - Tamaño: máximo 10MB
3. Archivo se sube a S3
4. Se retorna URL del archivo

---

### CU-003 Descargar Documento

**Actor:** Consultor, Asesor, Administrador  
**Flujo:**

1. Selecciona documento
2. Selecciona "Descargar"
3. Sistema genera URL temporal (expira en 1 hora)
4. Se descarga el archivo

---

### CU-004 Buscar Documentos

**Actor:** Todos los roles  
**Flujo:**

1. Accede a búsqueda
2. Aplica filtros:
   - Tipo de documento
   - Estudiante
   - Fecha de carga
   - Categoría
   - Estado
3. Sistema retorna resultados paginados

---

### CU-005 Clasificar Documento

**Actor:** Consultor, Administrador  
**Flujo:**

1. Selecciona documento
2. Asigna categoría
3. Se guarda la clasificación

---

### CU-006 Ver Historial

**Actor:** Consultor, Administrador  
**Flujo:**

1. Selecciona documento
2. Selecciona "Historial"
3. Sistema muestra:
   - Fecha de creación
   - Modificaciones
   - Autor de cada cambio

---

## 5. Modelo de Base de Datos

### documents

| Campo | Tipo | Constraints |
|--------|------|-------------|
| id | UUID | PK |
| student_id | UUID | FK → students.id |
| type | VARCHAR(100) | NOT NULL |
| name | VARCHAR(255) | NOT NULL |
| description | TEXT | |
| category | VARCHAR(100) | |
| file_url | TEXT | NOT NULL |
| file_size | INTEGER | |
| file_type | VARCHAR(10) | |
| status | VARCHAR(50) | DEFAULT 'active' |
| uploaded_by | UUID | FK → users.id |
| created_at | TIMESTAMP | DEFAULT NOW() |
| updated_at | TIMESTAMP | DEFAULT NOW() |

### document_history

| Campo | Tipo | Constraints |
|--------|------|-------------|
| id | UUID | PK |
| document_id | UUID | FK → documents.id |
| user_id | UUID | FK → users.id |
| action | VARCHAR(50) | NOT NULL |
| changes | JSONB | |
| created_at | TIMESTAMP | DEFAULT NOW() |

---

## 6. API REST

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| POST | /documents | Crear documento | CONS, ADMIN |
| GET | /documents | Listar documentos | ALL |
| GET | /documents/:id | Obtener documento | ALL |
| PATCH | /documents/:id | Actualizar documento | CONS, ADMIN |
| DELETE | /documents/:id | Eliminar documento | CONS, ADMIN |
| GET | /documents/:id/download | Descargar | ALL |
| GET | /documents/:id/history | Ver historial | CONS, ADMIN |
| POST | /documents/upload | Subir archivo | CONS, ADMIN |

---

## 7. Servicios AWS

| Servicio | Uso |
|----------|-----|
| S3 | Almacenamiento de archivos |
| CloudFront | CDN para descargas |

---

## 8. Casos de Prueba

| Código | Escenario | Resultado Esperado |
|---------|-----------|--------------------|
| TP-001 | Subir PDF válido | Archivo almacenado |
| TP-002 | Subir archivo > 10MB | Error 400 |
| TP-003 | Subir formato no válido | Error 400 |
| TP-004 | Descargar documento | URL temporal generada |
| TP-005 | Buscar con filtros | Resultados filtrados |
| TP-006 | Clasificar documento | Categoría asignada |
| TP-007 | Ver historial | Historial completo |

---

## 9. Dependencias

- SDD-001 (Authentication)
- SDD-003 (Students)
- PostgreSQL
- AWS S3

---

## 10. Criterios de Aceptación

- Los archivos se almacenan correctamente en S3
- La validación de formato y tamaño funciona
- La búsqueda con filtros retorna resultados correctos
- El historial de modificaciones se registra
- Las descargas generan URLs temporales seguras

---

> *Última actualización: 2026-07-27*
