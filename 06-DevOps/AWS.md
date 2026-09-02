# AWS Services

## Servicios Utilizados

| Servicio | Uso | Configuración |
|----------|-----|---------------|
| EC2 | Compute | t3.medium |
| RDS | PostgreSQL | db.t3.micro |
| ElastiCache | Redis | cache.t3.micro |
| S3 | Storage | Standard |
| SES | Email | Configurado |
| CloudFront | CDN | Distribución |
| Route53 | DNS | Dominio |
| ACM | SSL | Certificado |
| CloudWatch | Monitoring | Logs y métricas |
| IAM | Security | Roles y políticas |

## Estructura de Carpetas S3

```
digidoc-bucket/
├── documents/
│   ├── students/
│   └── temporary/
├── uploads/
└── backups/
```

## Costos Estimados

| Servicio | Costo Mensual |
|----------|---------------|
| EC2 | ~$50 |
| RDS | ~$30 |
| ElastiCache | ~$25 |
| S3 | ~$10 |
| SES | ~$5 |
| **Total** | **~$120** |

---

> *Última actualización: 2026-07-27*
