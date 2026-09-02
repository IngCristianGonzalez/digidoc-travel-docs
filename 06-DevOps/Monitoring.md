# Monitoreo

## Métricas

| Métrica | Umbral | Alerta |
|---------|--------|--------|
| CPU Usage | > 80% | Email |
| Memory Usage | > 85% | Email |
| Response Time | > 2s | Slack |
| Error Rate | > 1% | Email |
| Uptime | < 99.9% | Email |

## Logs

| Tipo | Destino | Retención |
|------|---------|-----------|
| Application | CloudWatch | 30 días |
| Access | CloudWatch | 30 días |
| Error | CloudWatch | 90 días |
| Audit | CloudWatch | 1 año |

## Dashboards

- **CloudWatch Dashboard:** Métricas de AWS
- **Grafana:** Métricas personalizadas
- **Sentry:** Errores de aplicación

## Alertas

| Alerta | Canal | Severidad |
|--------|-------|-----------|
| Error crítico | PagerDuty | P1 |
| Alto uso CPU | Email | P2 |
| Error rate alto | Slack | P2 |
| Disk full | Email | P1 |

---

> *Última actualización: 2026-07-27*
