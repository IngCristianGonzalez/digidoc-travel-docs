# CI/CD

## Pipeline

```text
┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐
│  Push   │───▶│  Build  │───▶│  Test   │───▶│ Deploy  │
└─────────┘    └─────────┘    └─────────┘    └─────────┘
```

## Etapas

| Etapa | Comandos | Requisitos |
|-------|----------|------------|
| Build | `npm run build` | Node 20+ |
| Test | `npm run test` | PostgreSQL, Redis |
| Lint | `npm run lint` | ESLint |
| Deploy | `eb deploy` | AWS CLI |

## Variables de Entorno

| Variable | Descripción |
|----------|-------------|
| NODE_ENV | production |
| DATABASE_URL | PostgreSQL connection |
| REDIS_URL | Redis connection |
| JWT_SECRET | Secret key |
| AWS_ACCESS_KEY | AWS credentials |

## Branches

| Branch | Acción |
|--------|--------|
| develop | Deploy a staging |
| main | Deploy a producción |
| feature/* | Solo build y test |

---

> *Última actualización: 2026-07-27*
