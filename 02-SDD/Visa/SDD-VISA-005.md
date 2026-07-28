# SDD-005 - Módulo de Gestión de Visas

## 1. Información General

| Campo | Valor |
|--------|-------|
| **Código** | SDD-VISA-005 |
| **Módulo** | Visa |
| **Versión** | 1.0.0 |
| **Estado** | Draft |
| **Prioridad** | Alta |

### Objetivo

Diseñar e implementar el módulo de seguimiento de visas con alertas automáticas de vencimiento.

---

## 2. Alcance

### Incluye

- Registro de información de visas
- Registro de fechas (expedición, vencimiento)
- Consulta de estado
- Alertas automáticas 3 meses antes del vencimiento
- Notificación al equipo responsable

---

## 3. Requerimientos Asociados

| ID | Descripción |
|----|-------------|
| RF-025 | Registrar información de visas |
| RF-026 | Registrar fecha de expedición |
| RF-027 | Registrar fecha de vencimiento |
| RF-028 | Consultar estado de la visa |
| RF-029 | Generar alerta automática tres meses antes del vencimiento |
| RF-030 | Notificar automáticamente a todo el equipo responsable |

---

## 4. Casos de Uso

### CU-001 Registrar Visa

**Actor:** Consultor, Administrador  
**Flujo:**

1. Selecciona estudiante
2. Ingresa datos de visa:
   - Tipo de visa
   - Número de visa
   - País de emisión
   - Fecha de expedición
   - Fecha de vencimiento
3. Sistema valida fechas
4. Se crea el registro
5. Se programa alerta de vencimiento

---

### CU-002 Consultar Estado

**Actor:** Todos  
**Flujo:**

1. Busca visa por estudiante o número
2. Sistema muestra:
   - Datos de la visa
   - Estado (vigente, por vencer, vencida)
   - Días restantes

---

### CU-003 Alerta de Vencimiento

**Actor:** Sistema (automático)  
**Flujo:**

1. Cron job diario verifica visas
2. Si faltan ≤ 90 días para vencimiento:
   - Crea notificación in-app
   - Envía email al equipo
   - Registra en dashboard

---

## 5. Modelo de Base de Datos

### visas

| Campo | Tipo | Constraints |
|--------|------|-------------|
| id | UUID | PK |
| student_id | UUID | FK → students.id |
| visa_type | VARCHAR(100) | NOT NULL |
| visa_number | VARCHAR(100) | UNIQUE |
| country | VARCHAR(100) | NOT NULL |
| issue_date | DATE | NOT NULL |
| expiry_date | DATE | NOT NULL |
| status | VARCHAR(50) | DEFAULT 'active' |
| alert_sent | BOOLEAN | DEFAULT false |
| created_by | UUID | FK → users.id |
| created_at | TIMESTAMP | DEFAULT NOW() |
| updated_at | TIMESTAMP | DEFAULT NOW() |

---

## 6. API REST

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| POST | /visas | Crear visa | CONS, ADMIN |
| GET | /visas | Listar visas | ALL |
| GET | /visas/:id | Obtener visa | ALL |
| PATCH | /visas/:id | Actualizar visa | CONS, ADMIN |
| GET | /visas/expiring | Visas por vencer | ALL |

---

## 7. Eventos Kafka

| Evento | Payload |
|--------|---------|
| visa.expiring | `{studentId, visaId, expiryDate, daysLeft}` |
| visa.expired | `{studentId, visaId}` |

---

## 8. Casos de Prueba

| Código | Escenario | Resultado Esperado |
|---------|-----------|--------------------|
| TP-001 | Crear visa válida | Visa creada |
| TP-002 | Fecha vencimiento < expedición | Error 400 |
| TP-003 | Visa a 90 días | Alerta generada |
| TP-004 | Visa vencida | Estado "expired" |

---

## 9. Dependencias

- SDD-003 (Students)
- SDD-008 (Notifications)
- PostgreSQL
- Kafka

---

## 10. Criterios de Aceptación

- Las visas se registran con fechas válidas
- Las alertas se generan 3 meses antes del vencimiento
- El equipo recibe notificación automática
- El estado se calcula correctamente

---

> *Última actualización: 2026-07-27*
