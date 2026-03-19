
# HU-01 — Registro de empleados con contratos

## Task Dev

> **Story Points:** 5

### Database

| ID  | Tarea | Esfuerzo |
|-----|-------|----------|
| T01 | Crear tabla `empleados` (id, nombre, fecha_creacion) | Media |
| T02 | Crear tabla `contratos` con FK → empleados.id (tipo_contrato, fechas) | Media |


**Justificación:** La complejidad se justifica por la cantidad de combinaciones que deben validarse en nombre y salario bruto.

### Task QA

| ID | Tarea | Esfuerzo |
|----|-------|----------|
| T01 | Diseñar matriz de datos de prueba: nombre (caracteres especiales, números, longitud), salario bruto (negativo, cero, límites numéricos, decimales) y campos vacíos | Medio |
| T02 | Diseñar casos de prueba para registro exitoso con combinaciones válidas de nombre, tipo de contrato y salario bruto verificando que retorna **HTTP 201** | Bajo |
| T03 | Diseñar casos de prueba para campos obligatorios vacíos verificando que el sistema informe cuál falta y retorna **HTTP 400** | Medio |
| T04 | Diseñar casos de prueba para salario bruto en cero o negativo verificando mensaje de error y que retorna **HTTP 400** | Bajo |
| T05 | Diseñar casos de prueba para nombre con caracteres especiales o numéricos verificando rechazo, mensaje de error y que retorna **HTTP 400** | Bajo |
