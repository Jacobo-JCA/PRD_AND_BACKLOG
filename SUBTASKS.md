
# HU-01 — Registro de empleados con contratos

> **Story Points:** 5

## Task Dev

### Database

| ID  | Tarea | Esfuerzo |
|-----|-------|----------|
| T01 | Crear tabla `empleados` (id, nombre, fecha_creacion) | Media |
| T02 | Crear tabla `contratos` con FK → empleados.id (tipo_contrato, fechas) | Media |

### Backend

| ID  | Tarea | Esfuerzo |
|-----|-------|----------|
| T03 | Exponer endpoint POST /empleados → alta de empleado | Media |
| T04 | Exponer endpoint GET /empleados/{id} → detalle de empleado con contratos | Media |
| T05 | Exponer endpoint POST /empleados/{id}/contratos → alta de contrato | Media |
| T06 | Configurar DTOs para Empleado y Contrato | Baja |

### Frontend

| ID  | Tarea | Esfuerzo |
|-----|-------|----------|
| T07 | Crear formulario para alta de empleado | Media |
| T08 | Crear formulario para agregar contrato | Media |
| T09 | Mostrar detalle del empleado con sus contratos | Baja |

---

## HU-02 — Corrección de datos

> *Story Points:* 3

### Database

| ID  | Tarea | Esfuerzo |
|-----|-------|----------|
| T01 | Verificar que tablas empleados, contratos y salarios soporten actualización (constraints y permisos) | Baja |

### Backend

| ID  | Tarea | Esfuerzo |
|-----|-------|----------|
| T02 | Exponer endpoint PUT /empleados/{id} → corrección de datos del empleado | Baja |
| T03 | Exponer endpoint PUT /empleados/{id}/contratos/{idContrato} → corrección de contrato | Baja |
| T04 | Exponer endpoint PUT /empleados/{id}/salarios/{idSalario} → corrección de salario | Baja |
| T05 | Configurar DTOs para actualización de Empleado, Contrato y Salario | Baja |

## Task QA

| ID | Tarea | Esfuerzo |
|----|-------|----------|
| T01 | Diseñar matriz de datos de prueba: nombre (caracteres especiales, números), salario bruto (negativo, cero, decimales) y campos vacíos | Medio |
| T02 | Diseñar casos de prueba para registro exitoso con combinaciones válidas de nombre, tipo de contrato y salario bruto verificando que retorna **HTTP 201** | Bajo |
| T03 | Diseñar casos de prueba para campos obligatorios vacíos verificando que el sistema informe cuál falta y retorna **HTTP 400** | Medio |
| T04 | Diseñar casos de prueba para salario bruto en cero o negativo verificando mensaje de error y que retorna **HTTP 400** | Bajo |
| T05 | Diseñar casos de prueba para nombre con caracteres especiales o numéricos verificando rechazo, mensaje de error y que retorna **HTTP 400** | Bajo |

---
# HU-02 — Corrección de datos


## Task QA 

| ID | Tarea | Esfuerzo |
|----|-------|----------|
| T01 | Diseñar casos de prueba para edición exitosa de nombre y salario bruto con nómina no calculada verificando que retorna **HTTP 200** | Bajo |
| T02 | Diseñar casos de prueba para edición inválida (nombre con caracteres especiales, salario en cero o negativo) verificando que no se actualiza y retorna **HTTP 400** | Bajo |
| T03 | Diseñar caso de prueba verificando que no se puede editar ningún dato si la nómina ya fue calculada y retorna **HTTP 403** | Medio |
| T04 | Verificar que pasa si la nomina cambia a calculada mientras Recursos Humanos esta en el formulario de editar. Documentar lo encontrado | Medio |

---
# HU-03 — Cálculo de salario neto


## Task QA

| ID | Tarea | Esfuerzo |
|----|-------|----------|
| T01 | Diseñar matriz de datos de prueba con distintos salarios brutos para los 3 tipos de contrato calculando el resultado esperado manualmente | Alto |
| T02 | Diseñar casos de prueba verificando fórmula para tiempo completo y medio tiempo: `neto = bruto − (bruto * 9.45%) + (bruto * 8.33%)` verificando que retorna **HTTP 200** | Medio |
| T03 | Diseñar casos de prueba verificando fórmula para servicios profesionales: `neto = bruto − (bruto * 8.00%)` sin bonificación verificando que retorna **HTTP 200** | Medio |
| T04 | Diseñar casos de prueba verificando redondeo a 2 decimales en todos los tipos de contrato | Medio |
| T05 | Diseñar caso de prueba verificando que el sistema bloquea el cálculo si no existe un empleado registrado previamente y retorna **HTTP 404** | Bajo |

---
# HU-04 — Confirmación del resultado



## Task QA

| ID | Tarea | Esfuerzo |
|----|-------|----------|
| T01 | Diseñar caso de prueba verificando que el resumen muestra todos los campos correctos: nombre, tipo de contrato, salario bruto, deducción, bonificación y salario neto | Bajo |
| T02 | Diseñar caso de prueba verificando que la confirmación del resumen habilita la descarga del PDF | Bajo |
| T03 | Diseñar caso de prueba verificando que sin confirmar el resumen el sistema bloquea la generación del PDF, informa al usuario y retorna **HTTP 400** | Bajo |
| T04 | Diseñar caso de prueba verificando que los datos persistidos son los mismos que los que muestra el resumen | Bajo |

---
# HU-05 — Generación de PDF


## Task QA

| ID | Tarea | Esfuerzo |
|----|-------|----------|
| T01 | Diseñar caso de prueba verificando que el PDF se genera con los campos correctos (nombre, tipo de contrato, salario bruto, deducción, bonificación y salario neto) y descarga correctamente tras confirmar el resumen, retornando **HTTP 200** con `Content-Type: application/pdf` | Bajo |
| T02 | Verificar que la generación del PDF es menor o igual a 3 segundos | Medio |
| T03 | Verificar que el PDF se ve igual en distintos navegadores. Documentar lo encontrado | Bajo |
