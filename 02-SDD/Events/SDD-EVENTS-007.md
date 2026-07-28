# SDD-007 - Módulo de Gestión de Eventos

## 1. Información General

| Campo | Valor |
|--------|-------|
| **Código** | SDD-EVENTS-007 |
| **Módulo** | Events |
| **Versión** | 1.0.0 |
| **Estado** | Draft |
| **Prioridad** | Media |

### Objetivo

Diseñar e implementar el módulo de gestión de eventos con generación de QR y enlaces únicos.

---

## 2. Alcance

### Incluye

- Crear eventos
- Editar eventos
- Generar código QR
- Generar enlace único
- Enviar recordatorios

---

## 3. Requerimientos Asociados

| ID | Descripción |
|----|-------------|
| RF-037 | Crear eventos |
| RF-038 | Editar eventos |
| RF-039 | Generar código QR para cada evento |
| RF-040 | Generar enlace único para compartir el evento |
| RF-041 | Enviar recordatorios antes de la realización del evento |

---

## 4. Casos de Uso

### CU-001 Crear Evento

**Actor:** Consultor, Administrador  
**Flujo:**

1. Ingresa datos del evento:
   - Título
   - Descripción
   - Fecha y hora
   - Ubicación
   - Participantes
2. Sistema genera código QR
3. Sistema genera enlace único
4. Se guarda el evento

---

### CU-002 Compartir Evento

**Actor:** Todos  
**Flujo:**

1. Selecciona evento
2. Copia enlace único
3. Comparte vía email/mensajería
4. Receptor accede al enlace
5. Ve detalles del evento

---

### CU-003 Recordatorio

**Actor:** Sistema (automático)  
**Flujo:**

1. Cron job verifica eventos próximos
2. 24 horas antes del evento:
   - Envía email a participantes
   - Crea notificación in-app

---

## 5. Modelo de Base de Datos

### events

| Campo | Tipo | Constraints |
|--------|------|-------------|
| id | UUID | PK |
| title | VARCHAR(255) | NOT NULL |
| description | TEXT | |
| event_date | TIMESTAMP | NOT NULL |
| location | VARCHAR(255) | |
| qr_code | TEXT | |
| unique_link | VARCHAR(255) | UNIQUE |
| reminder_sent | BOOLEAN | DEFAULT false |
| created_by | UUID | FK → users.id |
| created_at | TIMESTAMP | DEFAULT NOW() |
| updated_at | TIMESTAMP | DEFAULT NOW() |

### event_participants

| Campo | Tipo | Constraints |
|--------|------|-------------|
| id | UUID | PK |
| event_id | UUID | FK → events.id |
| student_id | UUID | FK → students.id |
| status | VARCHAR(50) | DEFAULT 'invited' |

---

## 6. API REST

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| POST | /events | Crear evento | CONS, ADMIN |
| GET | /events | Listar eventos | ALL |
| GET | /events/:id | Obtener evento | ALL |
| PATCH | /events/:id | Actualizar evento | CONS, ADMIN |
| GET | /events/:id/qr | Obtener QR | ALL |
| GET | /events/:link | Acceder por enlace | PUBLIC |

---

## 7. Servicios Externos

| Servicio | Uso |
|----------|-----|
| QR Code Generator | Generar código QR |
| AWS SES | Enviar recordatorios |

---

## 8. Casos de Prueba

| Código | Escenario | Resultado Esperado |
|---------|-----------|--------------------|
| TP-001 | Crear evento | Evento con QR y enlace |
| TP-002 | Acceder por enlace | Detalles visibles |
| TP-003 | Evento en 24h | Recordatorio enviado |

---

## 9. Dependencias

- SDD-003 (Students)
- SDD-008 (Notifications)
- PostgreSQL
- AWS SES

---

## 10. Criterios de Aceptación

- Cada evento tiene código QR y enlace único
- Los enlaces son accesibles públicamente
- Los recordatorios se envían 24h antes

---

> *Última actualización: 2026-07-27*
