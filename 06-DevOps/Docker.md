# Docker

## Estructura

```
├── docker-compose.yml
├── docker-compose.prod.yml
├── Dockerfile
└── .dockerignore
```

## Servicios

| Servicio | Puerto | Descripción |
|----------|--------|-------------|
| app | 3000 | NestJS API |
| frontend | 4200 | Angular App |
| postgres | 5432 | PostgreSQL |
| redis | 6379 | Redis |
| kafka | 9092 | Kafka |

## Comandos

```bash
# Desarrollo
docker-compose up -d

# Producción
docker-compose -f docker-compose.prod.yml up -d

# Logs
docker-compose logs -f app

# Detener
docker-compose down
```

---

> *Última actualización: 2026-07-27*
