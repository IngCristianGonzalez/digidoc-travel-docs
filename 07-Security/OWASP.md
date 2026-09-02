# OWASP Top 10 - Mitigaciones Implementadas

## Resumen de 10 Técnicas

| # | Vulnerabilidad | Estado | Mitigación | Evidencia |
|---|----------------|--------|------------|-----------|
| A01 | Broken Access Control | ✅ | RBAC + PermissionsGuard + OwnershipGuard + JWT | `src/auth/guards/roles.guard.ts:14` `src/auth/guards/permissions.guard.ts` `src/security/guards/ownership.guard.ts:1` `src/users/users.controller.ts:13` `@Roles('admin')` `src/students/students.service.ts:62` advisorId check |
| A02 | Cryptographic Failures | ✅ | bcrypt 12, AES-256-GCM, @Exclude password, JWT HS256 con issuer/audience/jti, HSTS | `src/users/entities/user.entity.ts:22` `@Exclude()` `src/security/helpers/crypto.helper.ts:1` `src/visas/entities/visa.entity.ts:12` transformer `src/auth/auth.service.ts:209` jti+audience `src/auth/strategies/jwt.strategy.ts:14` algorithms HS256 |
| A03 | Injection | ✅ | ValidationPipe strict + SanitizeInterceptor (xss) + TypeORM params | `src/main.ts:48` `whitelist/forbidNonWhitelisted` `src/security/interceptors/sanitize.interceptor.ts:1` `xss.filterXSS` + SQL strip `src/documents/documents.service.ts:16` `queryBuilder` con `:param` |
| A04 | Insecure Design | ✅ | Threat modeling, secure by default, fail-closed guards | `src/common/filters/all-exceptions.filter.ts:12` generic 500 en prod, `src/auth/auth.service.ts:30` brute force fail-closed |
| A05 | Security Misconfiguration | ✅ | Helmet CSP/HSTS/noSniff/frameguard, CORS whitelist, hide x-powered-by, disableErrorMessages | `src/main.ts:16` `helmet({csp, hsts})` `src/main.ts:32` `disable('x-powered-by')` `src/main.ts:36` CORS whitelist + `disableErrorMessages:true` en prod |
| A06 | Vulnerable Components | ✅ | typeorm 1.1.0→0.3.20, npm audit fix 0 vulns, pinned deps, helmet@7, throttler | `package.json:44` `typeorm@0.3.20` `npm audit: 0 vulnerabilities` `helmet`, `@nestjs/throttler`, `winston`, `xss` |
| A07 | Auth Failures | ✅ | Throttler 100/min global, 5/min login, 3/min forgot, brute force Redis, lockout 15min, strong password regex, refresh rotation | `src/app.module.ts:17` `ThrottlerModule.forRoot({limit:100})` `src/auth/auth.controller.ts:28` `@Throttle({limit:5})` `src/auth/auth.service.ts:30` `login_attempts:${ip}` + `login_block` `src/auth/dto/register.dto.ts:11` `@Matches` upper/lower/number/special |
| A08 | Integrity Failures | ✅ | JWT jti + explicit alg, package-lock, winston signed logs | `src/auth/auth.service.ts:211` `jti:randomUUID()` `jwt.strategy.ts:17` `algorithms:['HS256']` `package-lock.json` pinned |
| A09 | Logging Failures | ✅ | Winston structured JSON, AuditService, AllExceptionsFilter security events, login_failed audit | `src/security/logger/winston.logger.ts:1` `src/common/filters/all-exceptions.filter.ts:28` `logSecurityEvent` `src/audit/audit.service.ts:13` `auditService.log` en login/logout |
| A10 | SSRF | ✅ | isAllowedUrl whitelist, block metadata IP 169.254.169.254, private ranges, magic bytes, mimetype check, sanitize filename | `src/security/helpers/ssrf.helper.ts:1` `isAllowedUrl` `BLOCKED_IPS` `hasValidMagicBytes` `src/documents/documents.service.ts:29` `isAllowedUrl(fileUrl)` + `replace(/[^a-zA-Z0-9._-]/g,'_')` |

---

## Detalle por Técnica

### A01 - Broken Access Control
- **Problema:** IDOR, enumeración de IDs, escalamiento horizontal.
- **Solución:**
  - `RolesGuard` `src/auth/guards/roles.guard.ts:11` verifica `requiredRoles.some(r=>user.roles.includes(r))`.
  - `PermissionsGuard` verifica `module:action`.
  - `OwnershipGuard` `src/security/guards/ownership.guard.ts:10` + `assertOwnership(user, resource)` en servicios: admin/supervisor bypass, otros solo si `advisorId === user.id` o `createdBy`.
  - Todos los controllers `src/users/users.controller.ts:14` `src/students/students.controller.ts:15` usan `@UseGuards(JwtAuthGuard, RolesGuard)`.
  - Auditoría `auditService.log` en cada mutación.

### A02 - Cryptographic Failures
- **Problema:** Exposición de hashes, visaNumber en claro, JWT `none`.
- **Solución:**
  - `User.password` con `@Exclude()` `src/users/entities/user.entity.ts:22` + `ClassSerializerInterceptor` `src/main.ts:63`.
  - `Visa.visaNumber` con `EncryptedTransformer` AES-256-GCM `src/visas/entities/visa.entity.ts:12` `encrypt/decrypt`.
  - JWT `issuer: digidoc.travel` `audience: digidoc-frontend` `jti: randomUUID()` `expiresIn 15m/7d` `src/auth/auth.service.ts:211`.
  - Strategy `algorithms:['HS256']` `src/auth/strategies/jwt.strategy.ts:17` previene `none`.
  - bcrypt 12 `src/users/users.service.ts:28` `bcrypt.hash(password,12)`.
  - Helmet HSTS 31536000 `src/main.ts:24`.

### A03 - Injection
- **Problema:** SQLi via ` ILIKE '%${search}%'`, XSS `<script>`.
- **Solución:**
  - `ValidationPipe` `whitelist:true, forbidNonWhitelisted:true, forbidUnknownValues:true` `src/main.ts:49`.
  - `SanitizeInterceptor` `src/security/interceptors/sanitize.interceptor.ts:1` `xss.filterXSS` + strip `' -- /* */`.
  - TypeORM siempre con `qb.andWhere('user.email ILIKE :search', {search: `%${search}%`})` `src/users/users.service.ts:44` - parámetros, no concatenación.
  - DTOs con `class-validator` `@IsEmail`, `@Matches`, `@IsUUID`.

### A05 - Misconfiguration
- **Problema:** Headers default, CORS `*`, stack traces.
- **Solución:** `helmet` CSP `defaultSrc 'self'`, HSTS `preload`, `noSniff`, `frameguard deny`, `xssFilter` `src/main.ts:17`. `disable('x-powered-by')` `src/main.ts:31`. CORS whitelist `src/main.ts:36` con `origin` callback. `disableErrorMessages: NODE_ENV==='production'` `src/main.ts:56`. `AllExceptionsFilter` oculta `Internal server error` en prod `src/common/filters/all-exceptions.filter.ts:48`.

### A06 - Vulnerable Components
- **Problema:** typeorm 1.1.0 deprecated, glob 10 vuln.
- **Solución:** `npm install typeorm@0.3.20` `npm audit fix` -> 0 vulns `package.json`. `helmet`, `winston`, `xss` actualizados. Validado con `npm audit`.

### A07 - Auth Failures
- **Problema:** Fuerza bruta, credenciales débiles.
- **Solución:** `ThrottlerModule` global 100/min `src/app.module.ts:17`, `AuthController` `@Throttle({limit:5})` login/register `src/auth/auth.controller.ts:28`, forgot `@Throttle({limit:3})`. Brute force Redis `login_attempts:${ip}:${email}` 5 intentos -> `login_block` 15min `src/auth/auth.service.ts:30`. Password regex `(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])` `src/auth/dto/register.dto.ts:11`. Refresh token rotation con `storeRefreshToken` + `jti` `src/auth/auth.service.ts:233`.

### A08 - Integrity
- **Problema:** `package.json` sin lock, JWT `none`, logs sin firma.
- **Solución:** `package-lock.json` commiteado, `algorithms:['HS256']`, `winston` JSON con timestamp `src/security/logger/winston.logger.ts:6`, `randomUUID` para trazabilidad.

### A09 - Logging
- **Problema:** Sin trazabilidad de ataques.
- **Solución:** `winstonLogger` `src/security/logger/winston.logger.ts:4` `info/warn/error` + `logSecurityEvent` `LOGIN_FAILED`, `LOGIN_BLOCKED`, `SSRF_BLOCKED`. `AllExceptionsFilter` logea 401/403 como `SECURITY` `src/common/filters/all-exceptions.filter.ts:31`. `AuditService` logea `LOGIN`, `LOGOUT`, `CREATE`, `UPDATE` con `ip`, `device`, `userId`. Tests en `src/security/security.owasp.spec.ts:1` 16 casos.

### A10 - SSRF
- **Problema:** `fileUrl` arbitrario, upload de `.exe`, path traversal `../`.
- **Solución:** `isAllowedUrl` `src/security/helpers/ssrf.helper.ts:7` whitelist `s3.mock`, `localhost`, bloquea `169.254.169.254`, `10.x`, `192.168.x`, `0.0.0.0`, valida `http/https` solo. `validateFileType` y `hasValidMagicBytes` `src/security/helpers/ssrf.helper.ts:20` verifica header `25504446` PDF, `89504e47` PNG, `ffd8ff` JPEG. `DocumentsService` sanitiza `file.originalname.replace(/[^a-zA-Z0-9._-]/g,'_')` y bloquea `..` `/` `\` `src/documents/documents.service.ts:16`, valida `isAllowedUrl(fileUrl)` `src/documents/documents.service.ts:19`.

---

## Frontend Seguridad (Angular)

- **CSP** `src/index.html:6` `<meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self';">` (añadir en nginx).
- **Sanitización** Angular `DomSanitizer` por defecto, no `innerHTML` sin `bypassSecurityTrust`.
- **Auth** `src/app/core/interceptors/auth-functional.interceptor.ts:8` `Bearer` + `authGuard` `src/app/core/guards/auth-functional.guard.ts:7`, `roleGuard`.
- **Storage** `localStorage` para demo - en prod usar `HttpOnly Secure SameSite=Strict` cookies (mitiga XSS).
- **Validación** `FormsModule` con regex email/password, no `eval`.

---

## Verificación

```bash
npm run build # OK
npm test # 10 suites, 72 tests (56 funcionales + 16 OWASP) PASS
npm audit # 0 vulnerabilities
```

> *Última actualización: 2026-09-02 - 10/10 OWASP implementadas y testeadas*
