# SDD-008 - Módulo de Notificaciones

## 1. Información General

| Campo | Valor |
|--------|-------|
| **Código** | SDD-NOTIFICATIONS-008 |
| **Módulo** | Notifications |
| **Versión** | 1.0.0 |
| **Estado** | Draft |
| **Prioridad** | Alta |

### Objetivo

Diseñar e implementar el sistema de notificaciones in-app y por correo electrónico.

---

## 2. Alcance

### Incluye

- Notificaciones dentro de la plataforma
- Notificaciones por correo electrónico
- Marcar como leídas
- Historial de notificaciones

---

## 3. Requerimientos Asociados

| ID | Descripción |
|----|-------------|
| RF-042 | Mostrar notificaciones dentro de la plataforma |
| RF-043 | Enviar notificaciones por correo electrónico |
| RF-044 | Marcar notificaciones como leídas |
| RF-045 | Consultar historial de notificaciones |

---

## 4. Casos de Uso

### CU-001 Recibir Notificación

**Actor:** Todos  
**Flujo:**

1. Sistema genera evento (login, pago, visa, etc.)
2. Se crea notificación in-app
3. Se envía email (si aplica)
4. Usuario ve notificación en tiempo real

---

### CU-002 Marcar como Leída

**Actor:** Todos  
**Flujo:**

1. Usuario hace click en notificación
2. Se marca como leída
3. Se actualiza contador de no leídas

---

### CU-003 Consultar Historial

**Actor:** Todos  
**Flujo:**

1. Usuario accede a notificaciones
2. Ve historial completo
3. Puede filtrar por tipo, fecha, estado

---

## 5. Modelo de Base de Datos

### notifications

| Campo | Tipo | Constraints |
|--------|------|-------------|
| id | UUID | PK |
| user_id | UUID | FK → users.id |
| type | VARCHAR(50) | NOT NULL |
| title | VARCHAR(255) | NOT NULL |
| message | TEXT | NOT NULL |
| reference_type | VARCHAR(50) | |
| reference_id | UUID | |
| read | BOOLEAN | DEFAULT false |
| email_sent | BOOLEAN | DEFAULT false |
| created_at | TIMESTAMP | DEFAULT NOW() |

---

## 6. API REST

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| GET | /notifications | Listar notificaciones | ALL |
| GET | /notifications/unread | Conteo no leídas | ALL |
| PATCH | /notifications/:id/read | Marcar leída | ALL |
| PATCH | /notifications/read-all | Marcar todas leídas | ALL |

---

## 7. Eventos Kafka

| Evento | Descripción |
|--------|-------------|
| notification.create | Crear notificación |
| notification.email | Enviar email |

---

## 8. Casos de Prueba

| Código | Escenario | Resultado Esperado |
|---------|-----------|--------------------|
| TP-001 | Crear notificación | Notificación creada |
| TP-002 | Marcar leída | Estado actualizado |
| TP-003 | Contar no leídas | Conteo correcto |

---

## 9. Dependencias

- PostgreSQL
- Redis (real-time)
- AWS SES (email)
- Kafka

---

## 10. Criterios de Aceptación

- Las notificaciones aparecen en tiempo real
- Los emails se envían correctamente
- El historial se mantiene completo

---

> *Última actualización: 2026-07-27*
