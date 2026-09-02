# Autenticación

## JWT

| Campo | Valor |
|-------|-------|
| Algoritmo | RS256 |
| Access Token TTL | 15 minutos |
| Refresh Token TTL | 7 días |
| Issuer | digidoc.travel |

## bcrypt

| Campo | Valor |
|-------|-------|
| Salt Rounds | 12 |
| Algoritmo | blowfish |

## Rate Limiting

| Endpoint | Límite | Ventana |
|----------|--------|---------|
| /auth/login | 5 intentos | 15 min |
| /auth/forgot-password | 3 intentos | 1 hora |
| General | 100 requests | 1 min |

## HTTPS

- TLS 1.3 obligatorio
- HSTS habilitado
- Certificado SSL wildcard

---

> *Última actualización: 2026-07-27*
