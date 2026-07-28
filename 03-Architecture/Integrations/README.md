# Integraciones

## Servicios Externos

| Servicio | Propósito | Protocolo |
|----------|-----------|-----------|
| Supabase | PostgreSQL + Auth | HTTPS |
| AWS S3 | Almacenamiento | HTTPS |
| AWS SES | Email | HTTPS |
| Kafka | Mensajería | TCP |

## Webhooks

| Evento | Destino | Método |
|--------|---------|--------|
| auth.login | Notification Service | POST |
| payment.completed | Notification Service | POST |
| document.validated | Notification Service | POST |

---

> *Última actualización: 2026-07-27*
