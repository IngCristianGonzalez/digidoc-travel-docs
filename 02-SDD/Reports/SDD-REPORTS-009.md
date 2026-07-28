# SDD-009 - Módulo de Reportes

## 1. Información General

| Campo | Valor |
|--------|-------|
| **Código** | SDD-REPORTS-009 |
| **Módulo** | Reports |
| **Versión** | 1.0.0 |
| **Estado** | Draft |
| **Prioridad** | Media |

### Objetivo

Diseñar e implementar el módulo de generación y exportación de reportes.

---

## 2. Alcance

### Incluye

- Reportes de estudiantes
- Reportes de documentos
- Reportes de visas próximas a vencer
- Reportes de pagos pendientes
- Exportación en PDF y Excel

---

## 3. Requerimientos Asociados

| ID | Descripción |
|----|-------------|
| RF-046 | Generar reportes de estudiantes |
| RF-047 | Generar reportes de documentos |
| RF-048 | Generar reportes de visas próximas a vencer |
| RF-049 | Generar reportes de pagos pendientes |
| RF-050 | Exportar reportes en PDF y Excel |

---

## 4. Casos de Uso

### CU-001 Generar Reporte

**Actor:** Supervisor, Administrador  
**Flujo:**

1. Selecciona tipo de reporte
2. Aplica filtros
3. Genera reporte en pantalla
4. Puede exportar a PDF o Excel

---

### CU-002 Exportar Reporte

**Actor:** Supervisor, Administrador  
**Flujo:**

1. Genera reporte
2. Selecciona formato (PDF/Excel)
3. Sistema genera archivo
4. Descarga archivo

---

## 5. Tipos de Reporte

| Tipo | Datos |
|------|-------|
| Estudiantes | Total, activos, por país, por universidad |
| Documentos | Total, por tipo, pendientes, vencidos |
| Visas | Próximas a vencer, vencidas, por país |
| Pagos | Pendientes, atrasados, totales recaudados |

---

## 6. API REST

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| GET | /reports/students | Reporte estudiantes | SUP, ADMIN |
| GET | /reports/documents | Reporte documentos | SUP, ADMIN |
| GET | /reports/visas | Reporte visas | SUP, ADMIN |
| GET | /reports/payments | Reporte pagos | SUP, ADMIN |
| GET | /reports/export/:type | Exportar reporte | SUP, ADMIN |

---

## 7. Servicios

| Servicio | Uso |
|----------|-----|
| PDF Generator | Generar PDF (pdfkit/puppeteer) |
| Excel Generator | Generar Excel (exceljs) |

---

## 8. Casos de Prueba

| Código | Escenario | Resultado Esperado |
|---------|-----------|--------------------|
| TP-001 | Generar reporte estudiantes | Reporte completo |
| TP-002 | Exportar a PDF | Archivo PDF válido |
| TP-003 | Exportar a Excel | Archivo XLSX válido |
| TP-004 | Reporte visas vencidas | Lista correcta |

---

## 9. Dependencias

- PostgreSQL
- SDD-003 (Students)
- SDD-004 (Documents)
- SDD-005 (Visa)
- SDD-006 (Payments)

---

## 10. Criterios de Aceptación

- Los reportes muestran datos correctos
- La exportación genera archivos válidos
- Los filtros funcionan correctamente

---

> *Última actualización: 2026-07-27*
