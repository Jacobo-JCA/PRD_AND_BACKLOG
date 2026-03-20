
# HU-01 — Registro de empleados con contratos

## Task Dev

> **Story Points:** 5

### Database

| ID  | Tarea | Esfuerzo |
|-----|-------|----------|
| T01 | Crear tabla `empleados` (id, nombre, fecha_creacion) | Media |
| T02 | Crear tabla `contratos` con FK → empleados.id (tipo_contrato, fechas) | Media |


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
| T04 | Que pasa si la nomina cambia a calculada mientras Recursos Humanos esta en el formulario de editar? Documentar lo encontrado | Medio |
