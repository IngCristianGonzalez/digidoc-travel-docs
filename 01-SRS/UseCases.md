# Casos de Uso

## CU-001: Iniciar Sesión

**Actor:** Usuario  
**Precondiciones:** Usuario registrado y activo  
**Postcondiciones:** Sesión iniciada, token generado

### Flujo Principal
1. El usuario ingresa correo electrónico
2. Ingresa contraseña
3. El sistema valida las credenciales
4. Se genera un Access Token
5. Se genera un Refresh Token
6. Se retorna el perfil del usuario

### Flujo Alternativo
- 3a. Credenciales incorrectas → Error 401
- 3a. Cuenta bloqueada → Error 403

---

## CU-002: Cerrar Sesión

**Actor:** Usuario  
**Precondiciones:** Sesión activa  
**Postcondiciones:** Sesión invalidada

### Flujo Principal
1. El usuario solicita cerrar sesión
2. El sistema invalida el Refresh Token
3. Se elimina la sesión de Redis
4. Se registra la auditoría
5. Se retorna respuesta exitosa

---

## CU-003: Recuperar Contraseña

**Actor:** Usuario  
**Precondiciones:** Usuario registrado  
**Postcondiciones:** Contraseña restablecida

### Flujo Principal
1. El usuario ingresa correo electrónico
2. El sistema genera un Token temporal
3. Se publica evento en Kafka
4. Notification Service envía correo
5. El usuario restablece contraseña

### Flujo Alternativo
- 1a. Correo no registrado → Error 404

---

## CU-004: Cambiar Contraseña

**Actor:** Usuario autenticado  
**Precondiciones:** Sesión activa  
**Postcondiciones:** Contraseña actualizada

### Flujo Principal
1. El usuario ingresa contraseña actual
2. Ingresa nueva contraseña
3. El sistema valida la nueva contraseña
4. Se actualiza el hash
5. Se invalidan sesiones activas
6. Se registra la auditoría

---

## CU-005: Gestionar Usuarios

**Actor:** Administrador  
**Precondiciones:** Rol ADMIN  
**Postcondiciones:** Usuario creado/editado/eliminado

### Flujo Principal
1. El administrador accede a gestión de usuarios
2. Puede crear, editar o eliminar usuarios
3. Asigna roles
4. Se registra la auditoría

---

## CU-006: Gestionar Estudiantes

**Actor:** Consultor, Supervisor  
**Precondiciones:** Rol CONS o SUP  
**Postcondiciones:** Estudiante registrado

### Flujo Principal
1. El consultor registra un estudiante
2. Ingresa datos personales
3. Adjunta documentos iniciales
4. Se crea el registro

---

## CU-007: Cargar Documento

**Actor:** Consultor, Estudiante  
**Precondiciones:** Estudiante registrado  
**Postcondiciones:** Documento almacenado

### Flujo Principal
1. Selecciona tipo de documento
2. Selecciona archivo
3. El sistema valida formato y tamaño
4. Se almacena en S3
5. Se crea registro en BD

---

## CU-008: Seguimiento de Visa

**Actor:** Consultor, Asesor  
**Precondiciones:** Solicitud creada  
**Postcondiciones:** Estado actualizado

### Flujo Principal
1. Se crea solicitud de visa
2. Se adjuntan documentos requeridos
3. Se actualiza estado
4. Se notifican cambios

---

> *Última actualización: 2026-07-27*
