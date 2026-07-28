# Tests Unitarios

## Cobertura Objetivo

| Módulo | Cobertura Mínima |
|--------|------------------|
| Auth | 90% |
| Users | 85% |
| Students | 85% |
| Documents | 85% |
| Visa | 80% |
| Payments | 80% |

## Estructura

```
src/
├── modules/
│   └── auth/
│       ├── auth.service.spec.ts
│       ├── auth.controller.spec.ts
│       └── auth.module.spec.ts
```

## Comandos

```bash
# Ejecutar todos los tests
npm run test

# Tests con cobertura
npm run test:cov

# Tests en watch mode
npm run test:watch

# Tests específicos
npm run test -- --testPathPattern=auth
```

## Ejemplo

```typescript
describe('AuthService', () => {
  let service: AuthService;

  beforeEach(async () => {
    const module = await Test.createTestingModule({
      providers: [AuthService],
    }).compile();

    service = module.get<AuthService>(AuthService);
  });

  it('should validate credentials', async () => {
    const result = await service.validateUser('test@email.com', 'password');
    expect(result).toBeDefined();
  });
});
```

---

> *Última actualización: 2026-07-27*
