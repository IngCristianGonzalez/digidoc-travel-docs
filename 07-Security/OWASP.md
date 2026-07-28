# OWASP Top 10

## Cobertura

| # | Vulnerabilidad | Mitigación |
|---|----------------|------------|
| A01 | Broken Access Control | RBAC, Guards |
| A02 | Cryptographic Failures | bcrypt, TLS 1.3 |
| A03 | Injection | TypeORM, Validación |
| A04 | Insecure Design | Threat Modeling |
| A05 | Security Misconfiguration | Helmet, CORS |
| A06 | Vulnerable Components | npm audit |
| A07 | Auth Failures | Rate Limiting, JWT |
| A08 | Data Integrity | HMAC, Signatures |
| A09 | Logging Failures | Audit Logs |
| A10 | SSRF | Input Validation |

## Implementación

### A01: Broken Access Control
- RBAC estricto
- Guards en cada endpoint
- Validación de permisos

### A02: Cryptographic Failures
- bcrypt para contraseñas
- TLS 1.3 para tránsito
- AES-256 para reposo

### A05: Security Misconfiguration
- Helmet habilitado
- CORS configurado
- Rate limiting activo

## Auditorías

| Frecuencia | Tipo |
|------------|------|
| Mensual | npm audit |
| Trimestral | Penetration testing |
| Anual | Auditoría completa |

---

> *Última actualización: 2026-07-27*
