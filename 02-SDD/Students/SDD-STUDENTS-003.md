# SDD-003 - Módulo de Gestión de Estudiantes

## 1. Información General

| Campo | Valor |
|--------|-------|
| **Código** | SDD-STUDENTS-003 |
| **Módulo** | Students |
| **Versión** | 1.0.0 |
| **Estado** | Draft |
| **Prioridad** | Alta |

### Objetivo

Diseñar e implementar el módulo encargado de gestionar la información de los estudiantes en el sistema **DigiDoc Travel**.

---

## 2. Alcance

### Incluye

- Registro de estudiantes
- Edición de información del estudiante
- Consulta de información del estudiante
- Asociar estudiante a asesor
- Registrar observaciones del estudiante

### No Incluye

- Gestión documental (ver SDD-004)
- Seguimiento de visas (ver SDD-005)

---

## 3. Requerimientos Asociados

| ID | Descripción |
|----|-------------|
| RF-012 | Registrar estudiantes |
| RF-013 | Editar información del estudiante |
| RF-014 | Consultar información del estudiante |
| RF-015 | Asociar un estudiante a un asesor |
| RF-016 | Registrar observaciones del estudiante |

---

## 4. Actores

| Actor | Descripción |
|--------|-------------|
| Administrador | Control total |
| Supervisor | Gestión operativa |
| Consultor | Gestión de estudiantes asignados |

---

## 5. Casos de Uso

### CU-001 Registrar Estudiante

**Actor:** Consultor, Supervisor, Administrador  
**Precondiciones:** Rol válido autenticado  
**Postcondiciones:** Estudiante registrado

**Flujo Principal:**

1. El usuario accede a gestión de estudiantes
2. Selecciona "Crear estudiante"
3. Ingresa datos personales (nombre, email, teléfono, país de origen)
4. Ingresa datos académicos (universidad, carrera, semestre)
5. El sistema valida los datos
6. Se crea el registro
7. Se registra auditoría

---

### CU-002 Editar Estudiante

**Actor:** Consultor, Supervisor, Administrador  
**Precondiciones:** Estudiante existente  
**Postcondiciones:** Información actualizada

**Flujo Principal:**

1. El usuario selecciona un estudiante
2. Selecciona "Editar"
3. Modifica los campos permitidos
4. Guarda los cambios
5. Se registra auditoría

---

### CU-003 Consultar Estudiante

**Actor:** Consultor, Supervisor, Administrador  
**Precondiciones:** Rol válido  
**Postcondiciones:** Información del estudiante

**Flujo Principal:**

1. El usuario busca un estudiante
2. Puede filtrar por: nombre, email, país, estado
3. Selecciona un estudiante
4. El sistema muestra la información completa

---

### CU-004 Asociar Asesor

**Actor:** Supervisor, Administrador  
**Precondiciones:** Estudiante y asesor existentes  
**Postcondiciones:** Asociación creada

**Flujo Principal:**

1. El usuario selecciona un estudiante
2. Selecciona "Asignar asesor"
3. Selecciona el asesor
4. Guarda la asociación
5. Se notifica al asesor

---

### CU-005 Registrar Observaciones

**Actor:** Consultor, Supervisor  
**Precondiciones:** Estudiante existente  
**Postcondiciones:** Observación registrada

**Flujo Principal:**

1. El usuario selecciona un estudiante
2. Selecciona "Agregar observación"
3. Ingresa el texto de la observación
4. Guarda la observación
5. Se registra con fecha y autor

---

## 6. Modelo de Base de Datos

### students

| Campo | Tipo | Constraints |
|--------|------|-------------|
| id | UUID | PK |
| user_id | UUID | FK → users.id |
| first_name | VARCHAR(100) | NOT NULL |
| last_name | VARCHAR(100) | NOT NULL |
| email | VARCHAR(255) | UNIQUE, NOT NULL |
| phone | VARCHAR(20) | |
| country_origin | VARCHAR(100) | NOT NULL |
| city_origin | VARCHAR(100) | |
| university | VARCHAR(200) | |
| career | VARCHAR(200) | |
| semester | INTEGER | |
| status | BOOLEAN | DEFAULT true |
| advisor_id | UUID | FK → users.id |
| created_at | TIMESTAMP | DEFAULT NOW() |
| updated_at | TIMESTAMP | DEFAULT NOW() |

### student_observations

| Campo | Tipo | Constraints |
|--------|------|-------------|
| id | UUID | PK |
| student_id | UUID | FK → students.id |
| user_id | UUID | FK → users.id (autor) |
| observation | TEXT | NOT NULL |
| created_at | TIMESTAMP | DEFAULT NOW() |

---

## 7. API REST

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| POST | /students | Crear estudiante | CONS, SUP, ADMIN |
| GET | /students | Listar estudiantes | CONS, SUP, ADMIN |
| GET | /students/:id | Obtener estudiante | CONS, SUP, ADMIN |
| PATCH | /students/:id | Actualizar estudiante | CONS, SUP, ADMIN |
| DELETE | /students/:id | Desactivar estudiante | SUP, ADMIN |
| POST | /students/:id/advisor | Asignar asesor | SUP, ADMIN |
| POST | /students/:id/observations | Agregar observación | CONS, SUP |
| GET | /students/:id/observations | Listar observaciones | CONS, SUP, ADMIN |

---

## 8. Casos de Prueba

| Código | Escenario | Resultado Esperado |
|---------|-----------|--------------------|
| TP-001 | Crear estudiante válido | Estudiante creado |
| TP-002 | Editar información | Datos actualizados |
| TP-003 | Asociar asesor | Asociación creada |
| TP-004 | Agregar observación | Observación registrada |
| TP-005 | Consultar con filtros | Lista filtrada |

---

## 9. Dependencias

- SDD-001 (Authentication)
- SDD-002 (Users)
- PostgreSQL

---

## 10. Criterios de Aceptación

- Los estudiantes se registran con toda la información requerida
- La asociación estudiante-asesor funciona correctamente
- Las observaciones quedan registradas con fecha y autor
- La búsqueda y filtrado funcionan correctamente

---

> *Última actualización: 2026-07-27*
