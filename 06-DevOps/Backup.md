# Backup

## Estrategia

| Componente | Método | Frecuencia | Retención |
|------------|--------|------------|-----------|
| PostgreSQL | pg_dump | Diario | 30 días |
| Redis | RDB + AOF | Continuo | 7 días |
| S3 | Versionado | Continuo | 90 días |
| Configuración | Git | Continuo | Indefinido |

## Comandos

```bash
# Backup PostgreSQL
pg_dump -h localhost -U user digidoc > backup_$(date +%Y%m%d).sql

# Backup Redis
redis-cli BGSAVE

# Restaurar PostgreSQL
psql -h localhost -U user digidoc < backup_20260727.sql
```

## Almacenamiento

| Ubicación | Tipo | Encriptado |
|-----------|------|------------|
| S3 Standard | Backup diario | Sí |
| S3 Glacier | Backup mensual | Sí |
| Local | Backup semanal | No |

## Recovery

| Objetivo | Tiempo |
|----------|--------|
| RPO (Recovery Point Objective) | < 1 hora |
| RTO (Recovery Time Objective) | < 4 horas |

---

> *Última actualización: 2026-07-27*
