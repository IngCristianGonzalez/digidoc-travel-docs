# SDD-010 - Módulo de Dashboard

## 1. Información General

| Campo | Valor |
|--------|-------|
| **Código** | SDD-DASHBOARD-010 |
| **Módulo** | Dashboard |
| **Versión** | 1.0.0 |
| **Estado** | Draft |
| **Prioridad** | Alta |

### Objetivo

Diseñar e implementar el panel principal con indicadores clave del sistema.

---

## 2. Alcance

### Incluye

- Indicadores generales del sistema
- Estudiantes activos
- Documentos pendientes
- Visas próximas a vencer
- Pagos pendientes
- Próximos eventos

---

## 3. Requerimientos Asociados

| ID | Descripción |
|----|-------------|
| RF-051 | Mostrar indicadores generales del sistema |
| RF-052 | Mostrar estudiantes activos |
| RF-053 | Mostrar documentos pendientes |
| RF-054 | Mostrar visas próximas a vencer |
| RF-055 | Mostrar pagos pendientes |
| RF-056 | Mostrar próximos eventos programados |

---

## 4. Casos de Uso

### CU-001 Ver Dashboard

**Actor:** Todos  
**Flujo:**

1. Usuario inicia sesión
2. Accede al dashboard
3. Sistema carga indicadores
4. Muestra datos en tiempo real

---

## 5. Indicadores

| Indicador | Fuente | Actualización |
|-----------|--------|---------------|
| Total estudiantes activos | students | Diaria |
| Documentos pendientes | documents | Tiempo real |
| Visas por vencer (90 días) | visas | Diaria |
| Pagos pendientes | installments | Tiempo real |
| Próximos eventos (7 días) | events | Diaria |
| Total usuarios | users | Semanal |

---

## 6. API REST

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| GET | /dashboard/summary | Resumen general | ALL |
| GET | /dashboard/students | Estadísticas estudiantes | ALL |
| GET | /dashboard/documents | Documentos pendientes | ALL |
| GET | /dashboard/visas | Visas por vencer | ALL |
| GET | /dashboard/payments | Pagos pendientes | ALL |
| GET | /dashboard/events | Próximos eventos | ALL |

---

## 7. Respuesta

```json
{
  "students": {
    "total": 150,
    "active": 120,
    "newThisMonth": 15
  },
  "documents": {
    "total": 500,
    "pending": 25,
    "expired": 5
  },
  "visas": {
    "expiringIn90Days": 8,
    "expired": 2
  },
  "payments": {
    "pending": 15,
    "overdue": 3,
    "totalAmount": 25000
  },
  "events": {
    "next7Days": 3,
    "total": 50
  }
}
```

---

## 8. Casos de Prueba

| Código | Escenario | Resultado Esperado |
|---------|-----------|--------------------|
| TP-001 | Cargar dashboard | Indicadores correctos |
| TP-002 | Sin datos | Ceros en indicadores |
| TP-003 | Filtros de fecha | Datos filtrados |

---

## 9. Dependencias

- PostgreSQL
- Todos los módulos principales

---

## 10. Criterios de Aceptación

- Los indicadores muestran datos correctos
- La carga es rápida (< 2 segundos)
- Los datos se actualizan periódicamente

---

> *Última actualización: 2026-07-27*
