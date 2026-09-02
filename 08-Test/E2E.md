# Tests E2E (End-to-End)

## Flujos Probados

| # | Flujo | Pasos |
|---|-------|-------|
| 1 | Login completo | Login → Dashboard → Logout |
| 2 | CRUD Usuarios | Crear → Editar → Listar → Eliminar |
| 3 | Gestión Estudiantes | Registrar → Adjuntar docs → Seguir |
| 4 | Documentos | Cargar → Validar → Descargar |
| 5 | Visa | Crear solicitud → Actualizar estado |

## Herramientas

| Herramienta | Uso |
|-------------|-----|
| Supertest | HTTP requests |
| Jest | Test runner |
| Puppeteer | Browser automation (futuro) |

## Comandos

```bash
# Ejecutar E2E
npm run test:e2e

# Con reporte
npm run test:e2e -- --reporters=default --reporters=jest-junit
```

## Ejemplo

```typescript
describe('Auth E2E', () => {
  it('should login and get profile', async () => {
    const loginResponse = await request(app.getHttpServer())
      .post('/auth/login')
      .send({ email: 'test@email.com', password: 'password' })
      .expect(200);

    const { accessToken } = loginResponse.body;

    await request(app.getHttpServer())
      .get('/auth/profile')
      .set('Authorization', `Bearer ${accessToken}`)
      .expect(200);
  });
});
```

---

> *Última actualización: 2026-07-27*
