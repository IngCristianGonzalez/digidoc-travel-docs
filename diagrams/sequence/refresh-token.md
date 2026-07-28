# Prompt: Diagrama de Secuencia - Refresh Token

## Instrucciones

Usa este prompt con una herramienta de generación de diagramas de secuencia.

## Prompt

```
Genera un diagrama de secuencia para el flujo de refresh token de DigiDoc Travel con los siguientes participantes:

Participantes:
- User (Actor)
- Angular (Frontend)
- NestJS API (Backend)
- Auth Module
- Redis (Cache)

Flujo:
1. User → Angular: Acción que requiere token
2. Angular → NestJS API: POST /auth/refresh {refreshToken}
3. NestJS API → Auth Module: validateRefreshToken(token)
4. Auth Module → Redis: getRefreshToken(userId)
5. Redis → Auth Module: stored token
6. Auth Module → Auth Module: verify JWT signature
7. Auth Module → Auth Module: generateNewAccessToken(user)
8. Auth Module → NestJS API: {newAccessToken}
9. NestJS API → Angular: 200 OK {accessToken}
10. Angular → Angular: Update stored token
11. Angular → User: Operación exitosa

Flujo alternativo (token inválido):
4a. Redis → Auth Module: token not found
5a. Auth Module → NestJS API: 401 Unauthorized
6a. NestJS API → Angular: Error
7a. Angular → User: Redirigir a login

Estilo: Diagrama de secuencia UML con notas
```

## Salida Esperada

Un diagrama que muestre:
- Flujo normal de refresh
- Flujo alternativo cuando token es inválido
- Validación en Redis
- Generación de nuevo token

---

> *Última actualización: 2026-07-27*
