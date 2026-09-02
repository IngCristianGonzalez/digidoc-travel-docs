# SDD-006 - Módulo de Plan de Pagos

## 1. Información General

| Campo | Valor |
|--------|-------|
| **Código** | SDD-PAYMENTS-006 |
| **Módulo** | Payments |
| **Versión** | 1.0.0 |
| **Estado** | Draft |
| **Prioridad** | Alta |

### Objetivo

Diseñar e implementar el módulo de gestión de planes de pago y cuotas.

---

## 2. Alcance

### Incluye

- Crear planes de pago
- Registrar cuotas
- Registrar pagos realizados
- Consultar estado del plan
- Notificaciones antes del vencimiento
- Alertas en dashboard

---

## 3. Requerimientos Asociados

| ID | Descripción |
|----|-------------|
| RF-031 | Crear planes de pago |
| RF-032 | Registrar cuotas |
| RF-033 | Registrar pagos realizados |
| RF-034 | Consultar estado del plan de pagos |
| RF-035 | Notificar automáticamente antes del vencimiento |
| RF-036 | Mostrar alertas de pagos pendientes en el panel principal |

---

## 4. Casos de Uso

### CU-001 Crear Plan de Pago

**Actor:** Consultor, Administrador  
**Flujo:**

1. Selecciona estudiante
2. Ingresa datos del plan:
   - Concepto
   - Monto total
   - Número de cuotas
   - Fecha de inicio
3. Sistema genera cuotas automáticamente
4. Se crea el plan

---

### CU-002 Registrar Pago

**Actor:** Consultor, Administrador  
**Flujo:**

1. Selecciona plan de pago
2. Selecciona cuota
3. Ingresa datos del pago:
   - Monto pagado
   - Fecha de pago
   - Método de pago
   - Referencia/Comprobante
4. Se actualiza estado de cuota

---

### CU-003 Notificar Vencimiento

**Actor:** Sistema (automático)  
**Flujo:**

1. Cron job diario verifica cuotas
2. Si faltan ≤ 7 días para vencimiento:
   - Crea notificación
   - Envía email

---

## 5. Modelo de Base de Datos

### payment_plans

| Campo | Tipo | Constraints |
|--------|------|-------------|
| id | UUID | PK |
| student_id | UUID | FK → students.id |
| concept | VARCHAR(255) | NOT NULL |
| total_amount | DECIMAL(10,2) | NOT NULL |
| installments | INTEGER | NOT NULL |
| start_date | DATE | NOT NULL |
| status | VARCHAR(50) | DEFAULT 'active' |
| created_by | UUID | FK → users.id |
| created_at | TIMESTAMP | DEFAULT NOW() |

### installments

| Campo | Tipo | Constraints |
|--------|------|-------------|
| id | UUID | PK |
| plan_id | UUID | FK → payment_plans.id |
| number | INTEGER | NOT NULL |
| amount | DECIMAL(10,2) | NOT NULL |
| due_date | DATE | NOT NULL |
| status | VARCHAR(50) | DEFAULT 'pending' |
| paid_at | TIMESTAMP | |
| created_at | TIMESTAMP | DEFAULT NOW() |

### payments

| Campo | Tipo | Constraints |
|--------|------|-------------|
| id | UUID | PK |
| installment_id | UUID | FK → installments.id |
| amount | DECIMAL(10,2) | NOT NULL |
| payment_date | DATE | NOT NULL |
| method | VARCHAR(50) | |
| reference | VARCHAR(255) | |
| receipt_url | TEXT | |
| created_by | UUID | FK → users.id |
| created_at | TIMESTAMP | DEFAULT NOW() |

---

## 6. API REST

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| POST | /payment-plans | Crear plan | CONS, ADMIN |
| GET | /payment-plans | Listar planes | ALL |
| GET | /payment-plans/:id | Obtener plan | ALL |
| GET | /payment-plans/:id/installments | Ver cuotas | ALL |
| POST | /installments/:id/pay | Registrar pago | CONS, ADMIN |
| GET | /payment-plans/pending | Pagos pendientes | ALL |

---

## 7. Casos de Prueba

| Código | Escenario | Resultado Esperado |
|---------|-----------|--------------------|
| TP-001 | Crear plan con 3 cuotas | 3 cuotas generadas |
| TP-002 | Registrar pago completo | Cuota pagada |
| TP-003 | Cuota a 7 días | Notificación enviada |
| TP-004 | Consultar pendientes | Lista de pendientes |

---

## 8. Dependencias

- SDD-003 (Students)
- SDD-008 (Notifications)
- PostgreSQL
- Kafka

---

## 9. Criterios de Aceptación

- Los planes se crean con cuotas calculadas correctamente
- Los pagos se registran y actualizan estados
- Las notificaciones se envían antes del vencimiento
- El dashboard muestra alertas de pendientes

---

> *Última actualización: 2026-07-27*
