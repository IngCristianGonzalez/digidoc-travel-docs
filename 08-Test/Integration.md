# Tests de Integración

## Cobertura

| Componente | Tipo |
|------------|------|
| API + Database | Integración |
| API + Redis | Integración |
| API + Kafka | Integración |
| Módulos entre sí | Integración |

## Estructura

```
test/
├── auth.integration.spec.ts
├── users.integration.spec.ts
├── students.integration.spec.ts
└── jest-e2e.json
```

## Comandos

```bash
# Ejecutar tests de integración
npm run test:e2e

# Con base de datos de prueba
npm run test:integration
```

## Setup

```typescript
beforeAll(async () => {
  const module = await Test.createTestingModule({
    imports: [AppModule],
  }).compile();

  app = module.createNestApplication();
  await app.init();
});

afterAll(async () => {
  await app.close();
});
```

## Base de Datos de Prueba

| Base | Uso |
|------|-----|
| digidoc_test | Tests de integración |
| digidoc_e2e | Tests E2E |

---

> *Última actualización: 2026-07-27*
