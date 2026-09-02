# Encriptación

## Datos en Tránsito

| Protocolo | Versión | Uso |
|-----------|---------|-----|
| TLS | 1.3 | HTTPS |
| WSS | 1.3 | WebSocket seguro |

## Datos en Reposo

| Campo | Algoritmo | Ejemplo |
|-------|-----------|---------|
| password | bcrypt | $2b$12$... |
| tokens | JWT RS256 | eyJhbGci... |
| documents | AES-256 | En S3 |

## Key Management

| Key | Ubicación | Rotación |
|-----|-----------|----------|
| JWT Private Key | AWS Secrets Manager | 90 días |
| JWT Public Key | AWS Secrets Manager | 90 días |
| Database Password | AWS Secrets Manager | 90 días |
| S3 Access Key | IAM | Manual |

## Cifrado de Datos Sensibles

```typescript
// Ejemplo de cifrado
const encrypted = crypto.createHash('sha256')
  .update(data)
  .digest('hex');
```

---

> *Última actualización: 2026-07-27*
