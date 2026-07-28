# Prompt: Diagrama de Secuencia - Login Flow

## Instrucciones

Usa este prompt con una herramienta de generación de diagramas de secuencia.

## Prompt

```
Genera un diagrama de secuencia para el flujo de login de DigiDoc Travel con los siguientes participantes:

Participantes:
- User (Actor)
- Angular (Frontend)
- NestJS API (Backend)
- Auth Module
- Redis (Cache)
- PostgreSQL (Database)
- Kafka (Events)

Flujo:
1. User → Angular: Ingresa email y contraseña
2. Angular → NestJS API: POST /auth/login {email, password}
3. NestJS API → Auth Module: validateCredentials(email, password)
4. Auth Module → PostgreSQL: findOneByEmail(email)
5. PostgreSQL → Auth Module: user data
6. Auth Module → Auth Module: comparePassword(password, hash)
7. Auth Module → Auth Module: generateTokens(user)
8. Auth Module → Redis: storeRefreshToken(userId, token)
9. Auth Module → Kafka: publish('auth.login', {userId, email})
10. Auth Module → NestJS API: {accessToken, refreshToken, user}
11. NestJS API → Angular: 200 OK {tokens, user}
12. Angular → User: Login exitoso, redirigir a dashboard

Estilo: Diagrama de secuencia UML con notas
```

## Salida Esperada

Un diagrama que muestre:
- Flujo completo de login
- Intercambio de mensajes entre componentes
- Almacenamiento en Redis
- Publicación de evento en Kafka
- Respuesta al usuario

---

> *Última actualización: 2026-07-27*
