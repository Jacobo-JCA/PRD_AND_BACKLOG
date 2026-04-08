# TEST CASES — Calculadora de Nómina

## HU-01 — Registro de empleado con contratos

### TC-001 — Registro exitoso con contrato tiempo completo

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-001 |
| Nombre del test | Registro exitoso con contrato tiempo completo |
| Prioridad | Crítico |
| Endpoint | POST /api/v1/employees |
| Escenario | Dado que no existe el empleado en el sistema<br>Cuando se registra un empleado con name, grossSalary y contractType válidos<br>Entonces el empleado queda guardado en el sistema |
| Precondiciones | Ambiente de QA disponible y estable<br>No existe previamente un empleado con el mismo nombre |
| Datos | name = "Juan Fernando Quintero"<br>grossSalary = 3000.00<br>contractType = "FULL_TIME" |
| Pasos de ejecución | 1. Enviar POST /api/v1/employees con los datos de entrada<br>2. Verificar código de respuesta HTTP<br>3. Verificar id, name, grossSalary y activeContract.contractType en la respuesta<br>4. Ejecutar GET /api/v1/employees/{id} con el id retornado<br>5. Verificar que los datos guardados coinciden con los enviados |
| Resultado esperado | POST /api/v1/employees retorna HTTP 201<br>El body contiene id, name, grossSalary y activeContract.contractType correctos<br>GET /api/v1/employees/{id} retorna HTTP 200 con los mismos datos |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-002 — Registro exitoso con contrato medio tiempo

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-002 |
| Nombre del test | Registro exitoso con contrato medio tiempo |
| Prioridad | Crítico |
| Endpoint | POST /api/v1/employees |
| Escenario | Dado que no existe el empleado en el sistema<br>Cuando se registra un empleado con datos válidos<br>Entonces el empleado queda guardado en el sistema |
| Precondiciones | Ambiente de QA disponible y estable<br>No existe previamente un empleado con el mismo nombre |
| Datos | name = "Gonzalo Martinez"<br>grossSalary = 1500.00<br>contractType = "PART_TIME" |
| Pasos de ejecución | 1. Enviar POST /api/v1/employees con los datos de entrada<br>2. Verificar HTTP 201<br>3. Verificar campos principales en la respuesta<br>4. Ejecutar GET /api/v1/employees/{id}<br>5. Verificar persistencia |
| Resultado esperado | El empleado se crea correctamente con activeContract.contractType = PART_TIME y grossSalary = 1500.00 |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-003 — Registro exitoso con contrato servicios profesionales

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-003 |
| Nombre del test | Registro exitoso con contrato servicios profesionales |
| Prioridad | Crítico |
| Endpoint | POST /api/v1/employees |
| Escenario | Dado que no existe el empleado en el sistema<br>Cuando se registra un empleado con datos válidos<br>Entonces el empleado queda guardado en el sistema |
| Precondiciones | Ambiente de QA disponible y estable<br>No existe previamente un empleado con el mismo nombre |
| Datos | name = "Lucas Pratto"<br>grossSalary = 5000.00<br>contractType = "PROFESSIONAL_SERVICES" |
| Pasos de ejecución | 1. Enviar POST /api/v1/employees<br>2. Verificar HTTP 201<br>3. Verificar id, name, grossSalary y activeContract.contractType<br>4. Ejecutar GET /api/v1/employees/{id}<br>5. Verificar persistencia |
| Resultado esperado | El empleado se crea correctamente con activeContract.contractType = PROFESSIONAL_SERVICES y grossSalary = 5000.00 |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-004 — Registro fallido por nombre vacío

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-004 |
| Nombre del test | Registro fallido por nombre vacío |
| Prioridad | Alto |
| Endpoint | POST /api/v1/employees |
| Escenario | Dado que no existe el empleado en el sistema<br>Cuando se intenta registrar un empleado sin name<br>Entonces el sistema no permite guardar el empleado |
| Precondiciones | Ambiente de QA disponible y estable |
| Datos | name = ""<br>grossSalary = 2000.00<br>contractType = "FULL_TIME" |
| Pasos de ejecución | 1. Enviar POST /api/v1/employees con name vacío<br>2. Verificar código HTTP<br>3. Verificar mensaje de error retornado |
| Resultado esperado | POST /api/v1/employees retorna HTTP 400<br>Mensaje indica que el campo name es obligatorio |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-005 — Registro fallido por tipo de contrato vacío

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-005 |
| Nombre del test | Registro fallido por tipo de contrato vacío |
| Prioridad | Alto |
| Endpoint | POST /api/v1/employees |
| Escenario | Dado que no existe el empleado en el sistema<br>Cuando se intenta registrar un empleado sin contractType<br>Entonces el sistema no permite guardar el empleado |
| Precondiciones | Ambiente de QA disponible y estable |
| Datos | name = "Luis Torres"<br>grossSalary = 2000.00<br>contractType = "" |
| Pasos de ejecución | 1. Enviar POST /api/v1/employees con contractType vacío o inválido<br>2. Verificar código HTTP<br>3. Verificar mensaje de error |
| Resultado esperado | POST /api/v1/employees retorna HTTP 400<br>Mensaje indica que el tipo de contrato es obligatorio o inválido |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-006 — Registro fallido por salario bruto vacío

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-006 |
| Nombre del test | Registro fallido por salario bruto vacío |
| Prioridad | Alto |
| Endpoint | POST /api/v1/employees |
| Escenario | Dado que no existe el empleado en el sistema<br>Cuando se intenta registrar un empleado sin grossSalary<br>Entonces el sistema no permite guardar el empleado |
| Precondiciones | Ambiente de QA disponible y estable |
| Datos | name = "Franco Armani"<br>grossSalary = vacío<br>contractType = "PART_TIME" |
| Pasos de ejecución | 1. Enviar POST /api/v1/employees sin grossSalary<br>2. Verificar código HTTP<br>3. Verificar mensaje de error |
| Resultado esperado | POST /api/v1/employees retorna HTTP 400<br>Mensaje indica que el campo grossSalary es obligatorio |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-007 — Registro fallido por salario bruto en cero

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-007 |
| Nombre del test | Registro fallido por salario bruto en cero |
| Prioridad | Alto |
| Endpoint | POST /api/v1/employees |
| Escenario | Dado que el empleado no existe en el sistema<br>Cuando se intenta registrar al empleado con grossSalary en cero<br>Entonces el sistema no permite guardar el empleado |
| Precondiciones | Ambiente de QA disponible y estable |
| Datos | name = "Gonzalo Montiel"<br>grossSalary = 0<br>contractType = "FULL_TIME" |
| Pasos de ejecución | 1. Enviar POST /api/v1/employees con grossSalary = 0<br>2. Verificar código HTTP<br>3. Verificar mensaje de error |
| Resultado esperado | POST /api/v1/employees retorna HTTP 400<br>Mensaje indica que el salario bruto debe ser positivo |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-008 — Registro fallido por salario bruto negativo

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-008 |
| Nombre del test | Registro fallido por salario bruto negativo |
| Prioridad | Alto |
| Endpoint | POST /api/v1/employees |
| Escenario | Dado que el empleado no existe en el sistema<br>Cuando se intenta registrar al empleado con grossSalary negativo<br>Entonces el sistema no permite guardar el empleado |
| Precondiciones | Ambiente de QA disponible y estable |
| Datos | name = "Jonatan Maidana"<br>grossSalary = -1500.00<br>contractType = "PART_TIME" |
| Pasos de ejecución | 1. Enviar POST /api/v1/employees con grossSalary negativo<br>2. Verificar código HTTP<br>3. Verificar mensaje de error |
| Resultado esperado | POST /api/v1/employees retorna HTTP 400<br>Mensaje indica que el salario bruto debe ser positivo |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-009 — Registro fallido por nombre con caracteres especiales

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-009 |
| Nombre del test | Registro fallido por nombre con caracteres especiales |
| Prioridad | Alto |
| Endpoint | POST /api/v1/employees |
| Escenario | Dado que el empleado no consta en el sistema<br>Cuando se intenta registrar al empleado con un nombre que contiene caracteres especiales<br>Entonces el sistema no permite guardarlo |
| Precondiciones | Ambiente de QA disponible y estable |
| Datos | name = "Matias@#!"<br>grossSalary = 2000.00<br>contractType = "FULL_TIME" |
| Pasos de ejecución | 1. Enviar POST /api/v1/employees con name inválido<br>2. Verificar código HTTP<br>3. Verificar mensaje de error |
| Resultado esperado | POST /api/v1/employees retorna HTTP 400<br>Mensaje indica que el nombre no debe contener caracteres especiales |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-010 — Registro fallido por nombre con caracteres numéricos

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-010 |
| Nombre del test | Registro fallido por nombre con caracteres numéricos |
| Prioridad | Medio |
| Endpoint | POST /api/v1/employees |
| Escenario | Dado que el empleado no consta en el sistema<br>Cuando se intenta registrar al empleado con un nombre que contiene caracteres numéricos<br>Entonces el sistema no permite guardarlo |
| Precondiciones | Ambiente de QA disponible y estable |
| Datos | name = "1234"<br>grossSalary = 4000.00<br>contractType = "PROFESSIONAL_SERVICES" |
| Pasos de ejecución | 1. Enviar POST /api/v1/employees con name numérico<br>2. Verificar código HTTP<br>3. Verificar mensaje de error |
| Resultado esperado | POST /api/v1/employees retorna HTTP 400<br>Mensaje indica que el nombre no debe contener números |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-011 — GET empleado existente retorna HTTP 200

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-011 |
| Nombre del test | GET empleado existente retorna HTTP 200 |
| Prioridad | Crítico |
| Endpoint | GET /api/v1/employees/{id} |
| Escenario | Dado que existe un empleado registrado en el sistema<br>Cuando se consulta el empleado por su identificador<br>Entonces el sistema retorna el detalle del empleado con su contrato activo |
| Precondiciones | Existe un empleado previamente registrado |
| Datos | id = ID de empleado existente |
| Pasos de ejecución | 1. Registrar un empleado y obtener su id<br>2. Ejecutar GET /api/v1/employees/{id}<br>3. Verificar código HTTP<br>4. Verificar que la respuesta incluye name, grossSalary y activeContract |
| Resultado esperado | GET /api/v1/employees/{id} retorna HTTP 200<br>La respuesta incluye name, grossSalary y activeContract.contractType |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-012 — GET empleado inexistente retorna HTTP 404

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-012 |
| Nombre del test | GET empleado inexistente retorna HTTP 404 |
| Prioridad | Alto |
| Endpoint | GET /api/v1/employees/{id} |
| Escenario | Dado que no existe un empleado con el identificador consultado<br>Cuando se consulta el empleado por ese identificador<br>Entonces el sistema informa que el empleado no fue encontrado |
| Precondiciones | El ID consultado no existe en base de datos |
| Datos | id = 99999 |
| Pasos de ejecución | 1. Ejecutar GET /api/v1/employees/99999<br>2. Verificar código HTTP |
| Resultado esperado | GET /api/v1/employees/99999 retorna HTTP 404 |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-013 — GET listado de empleados retorna HTTP 200

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-013 |
| Nombre del test | GET listado de empleados retorna HTTP 200 |
| Prioridad | Crítico |
| Endpoint | GET /api/v1/employees |
| Escenario | Dado que existen empleados registrados<br>Cuando se consulta el listado de empleados<br>Entonces el sistema retorna la colección de empleados |
| Precondiciones | Existe al menos un empleado registrado |
| Datos | N/A |
| Pasos de ejecución | 1. Registrar uno o más empleados<br>2. Ejecutar GET /api/v1/employees<br>3. Verificar código HTTP<br>4. Verificar que la respuesta es una lista con al menos un elemento |
| Resultado esperado | GET /api/v1/employees retorna HTTP 200<br>La respuesta contiene una lista de EmployeeResponse con id, name, grossSalary y activeContract |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-014 — Actualización de contrato exitosa para empleado existente

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-014 |
| Nombre del test | Actualización de contrato exitosa para empleado existente |
| Prioridad | Alto |
| Endpoint | PATCH /api/v1/employees/{id}/contracts/{contractId} |
| Escenario | Dado que existe un empleado registrado con contrato activo<br>Cuando se actualiza el contrato con datos válidos<br>Entonces el contrato queda actualizado |
| Precondiciones | Existe un empleado registrado con contractId conocido |
| Datos | id = ID de empleado existente<br>contractId = ID de contrato activo<br>contractType = "PART_TIME"<br>startDate = "2025-01-01" |
| Pasos de ejecución | 1. Registrar un empleado y obtener id y contractId<br>2. Ejecutar PATCH /api/v1/employees/{id}/contracts/{contractId}<br>3. Verificar código HTTP<br>4. Consultar el empleado y validar el contrato actualizado |
| Resultado esperado | PATCH /api/v1/employees/{id}/contracts/{contractId} retorna HTTP 200<br>El contrato refleja los nuevos datos enviados |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-015 — Cierre de contrato exitoso para empleado existente

| Campo | Valor |
|---|---|
| HU asociada | HU-01 |
| ID del caso | TC-015 |
| Nombre del test | Cierre de contrato exitoso para empleado existente |
| Prioridad | Alto |
| Endpoint | PATCH /api/v1/employees/{id}/contracts/{contractId}/end-date |
| Escenario | Dado que existe un empleado con contrato activo<br>Cuando se registra una fecha de cierre válida para el contrato<br>Entonces el contrato queda cerrado |
| Precondiciones | Existe un empleado registrado con contractId conocido |
| Datos | id = ID de empleado existente<br>contractId = ID de contrato activo<br>endDate = fecha actual o futura |
| Pasos de ejecución | 1. Registrar un empleado y obtener id y contractId<br>2. Ejecutar PATCH /api/v1/employees/{id}/contracts/{contractId}/end-date<br>3. Verificar código HTTP |
| Resultado esperado | PATCH /api/v1/employees/{id}/contracts/{contractId}/end-date retorna HTTP 204<br>El contrato queda con fecha de cierre registrada |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

## HU-03 — Cálculo de salario neto

### TC-016 — Cálculo correcto para contrato tiempo completo

| Campo | Valor |
|---|---|
| HU asociada | HU-03 |
| ID del caso | TC-016 |
| Nombre del test | Cálculo correcto para contrato tiempo completo |
| Prioridad | Crítico |
| Endpoint | POST /api/v1/payroll/calculate/{employeeId} |
| Escenario | Dado que existe un empleado registrado con contrato FULL_TIME y salario bruto definido<br>Cuando se procesa la nómina del empleado<br>Entonces el sistema calcula el salario neto aplicando deducción y bonificación correspondientes |
| Precondiciones | Existe un empleado registrado con contractType = FULL_TIME y grossSalary = 3000.00 |
| Datos | employeeId = ID de empleado existente<br>grossSalary = 3000.00<br>deductionAmount esperado = 283.50<br>bonusAmount esperado = 249.90<br>netSalary esperado = 2966.40 |
| Pasos de ejecución | 1. Registrar empleado con los datos indicados<br>2. Ejecutar POST /api/v1/payroll/calculate/{employeeId}<br>3. Verificar código HTTP<br>4. Verificar deductionAmount, bonusAmount y netSalary |
| Resultado esperado | POST /api/v1/payroll/calculate/{employeeId} retorna HTTP 201<br>deductionAmount = 283.50<br>bonusAmount = 249.90<br>netSalary = 2966.40 |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-017 — Cálculo correcto para contrato medio tiempo

| Campo | Valor |
|---|---|
| HU asociada | HU-03 |
| ID del caso | TC-017 |
| Nombre del test | Cálculo correcto para contrato medio tiempo |
| Prioridad | Crítico |
| Endpoint | POST /api/v1/payroll/calculate/{employeeId} |
| Escenario | Dado que existe un empleado registrado con contrato PART_TIME y salario bruto definido<br>Cuando se procesa la nómina del empleado<br>Entonces el sistema calcula el salario neto correcto |
| Precondiciones | Existe un empleado registrado con contractType = PART_TIME y grossSalary = 1500.00 |
| Datos | employeeId = ID de empleado existente<br>deductionAmount esperado = 141.75<br>bonusAmount esperado = 124.95<br>netSalary esperado = 1483.20 |
| Pasos de ejecución | 1. Registrar empleado con los datos indicados<br>2. Ejecutar POST /api/v1/payroll/calculate/{employeeId}<br>3. Verificar código HTTP<br>4. Verificar valores calculados |
| Resultado esperado | POST /api/v1/payroll/calculate/{employeeId} retorna HTTP 201<br>deductionAmount = 141.75<br>bonusAmount = 124.95<br>netSalary = 1483.20 |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-018 — Cálculo correcto para contrato servicios profesionales

| Campo | Valor |
|---|---|
| HU asociada | HU-03 |
| ID del caso | TC-018 |
| Nombre del test | Cálculo correcto para contrato servicios profesionales |
| Prioridad | Crítico |
| Endpoint | POST /api/v1/payroll/calculate/{employeeId} |
| Escenario | Dado que existe un empleado registrado con contrato PROFESSIONAL_SERVICES y salario bruto definido<br>Cuando se procesa la nómina del empleado<br>Entonces el sistema calcula el salario neto correcto |
| Precondiciones | Existe un empleado registrado con contractType = PROFESSIONAL_SERVICES y grossSalary = 5000.00 |
| Datos | employeeId = ID de empleado existente<br>deductionAmount esperado = 400.00<br>bonusAmount esperado = 0.00<br>netSalary esperado = 4600.00 |
| Pasos de ejecución | 1. Registrar empleado con los datos indicados<br>2. Ejecutar POST /api/v1/payroll/calculate/{employeeId}<br>3. Verificar código HTTP<br>4. Verificar que bonusAmount = 0.00 y netSalary es correcto |
| Resultado esperado | POST /api/v1/payroll/calculate/{employeeId} retorna HTTP 201<br>deductionAmount = 400.00<br>bonusAmount = 0.00<br>netSalary = 4600.00 |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-019 — Formato de 2 decimales en tiempo completo

| Campo | Valor |
|---|---|
| HU asociada | HU-03 |
| ID del caso | TC-019 |
| Nombre del test | Formato de 2 decimales en tiempo completo |
| Prioridad | Alto |
| Endpoint | POST /api/v1/payroll/calculate/{employeeId} |
| Escenario | Dado que existe un empleado registrado con salario bruto definido<br>Cuando se procesa la nómina<br>Entonces todos los valores numéricos del resultado están redondeados a 2 decimales |
| Precondiciones | Existe un empleado registrado con grossSalary que genera decimales en el cálculo |
| Datos | contractType = FULL_TIME<br>grossSalary = 1000.00 |
| Pasos de ejecución | 1. Ejecutar POST /api/v1/payroll/calculate/{employeeId}<br>2. Verificar que deductionAmount, bonusAmount y netSalary tienen 2 decimales |
| Resultado esperado | Todos los valores numéricos retornados tienen exactamente 2 decimales |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-020 — Redondeo a 2 decimales en servicios profesionales

| Campo | Valor |
|---|---|
| HU asociada | HU-03 |
| ID del caso | TC-020 |
| Nombre del test | Redondeo a 2 decimales en servicios profesionales |
| Prioridad | Alto |
| Endpoint | POST /api/v1/payroll/calculate/{employeeId} |
| Escenario | Dado que existe un empleado registrado con salario bruto definido<br>Cuando se procesa la nómina<br>Entonces todos los valores numéricos del resultado están redondeados a 2 decimales |
| Precondiciones | Existe un empleado registrado con grossSalary = 333.33 |
| Datos | contractType = PROFESSIONAL_SERVICES<br>grossSalary = 333.33 |
| Pasos de ejecución | 1. Ejecutar POST /api/v1/payroll/calculate/{employeeId}<br>2. Verificar el formato de todos los valores numéricos |
| Resultado esperado | Todos los valores retornados tienen exactamente 2 decimales |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-021 — Cálculo bloqueado si el empleado no existe

| Campo | Valor |
|---|---|
| HU asociada | HU-03 |
| ID del caso | TC-021 |
| Nombre del test | Cálculo bloqueado si el empleado no existe |
| Prioridad | Alto |
| Endpoint | POST /api/v1/payroll/calculate/{employeeId} |
| Escenario | Dado que no existe ningún empleado registrado en el sistema<br>Cuando el administrador intenta procesar una nómina<br>Entonces el sistema no permite realizar el cálculo |
| Precondiciones | El employeeId utilizado no existe en base de datos |
| Datos | employeeId = 99999 |
| Pasos de ejecución | 1. Ejecutar POST /api/v1/payroll/calculate/99999<br>2. Verificar código HTTP<br>3. Verificar mensaje de error |
| Resultado esperado | POST /api/v1/payroll/calculate/99999 retorna HTTP 404<br>Mensaje indica que el empleado no existe o no ha sido sincronizado |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-022 — GET nómina existente por id retorna HTTP 200

| Campo | Valor |
|---|---|
| HU asociada | HU-03 |
| ID del caso | TC-022 |
| Nombre del test | GET nómina existente por id retorna HTTP 200 |
| Prioridad | Crítico |
| Endpoint | GET /api/v1/payroll/{payrollId} |
| Escenario | Dado que existe una nómina calculada<br>Cuando se consulta por su identificador<br>Entonces el sistema retorna el detalle de la nómina |
| Precondiciones | Existe una nómina previamente calculada |
| Datos | payrollId = ID de nómina existente |
| Pasos de ejecución | 1. Calcular una nómina y obtener payrollId<br>2. Ejecutar GET /api/v1/payroll/{payrollId}<br>3. Verificar código HTTP<br>4. Verificar campos del detalle |
| Resultado esperado | GET /api/v1/payroll/{payrollId} retorna HTTP 200<br>La respuesta contiene employeeId, employeeName, contractType, grossSalary, deductionAmount, bonusAmount y netSalary |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-023 — GET última nómina por empleado retorna HTTP 200

| Campo | Valor |
|---|---|
| HU asociada | HU-03 |
| ID del caso | TC-023 |
| Nombre del test | GET última nómina por empleado retorna HTTP 200 |
| Prioridad | Alto |
| Endpoint | GET /api/v1/payroll/employee/{employeeId} |
| Escenario | Dado que existe al menos una nómina para el empleado<br>Cuando se consulta la última nómina por employeeId<br>Entonces el sistema retorna el último cálculo disponible |
| Precondiciones | Existe al menos una nómina calculada para el empleado |
| Datos | employeeId = ID de empleado existente |
| Pasos de ejecución | 1. Calcular una o más nóminas para el empleado<br>2. Ejecutar GET /api/v1/payroll/employee/{employeeId}<br>3. Verificar código HTTP<br>4. Verificar que retorna la última nómina |
| Resultado esperado | GET /api/v1/payroll/employee/{employeeId} retorna HTTP 200 con la nómina más reciente del empleado |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-024 — GET última nómina por empleado inexistente retorna HTTP 404

| Campo | Valor |
|---|---|
| HU asociada | HU-03 |
| ID del caso | TC-024 |
| Nombre del test | GET última nómina por empleado inexistente retorna HTTP 404 |
| Prioridad | Alto |
| Endpoint | GET /api/v1/payroll/employee/{employeeId} |
| Escenario | Dado que no existe una nómina asociada al employeeId consultado<br>Cuando se consulta la última nómina por empleado<br>Entonces el sistema retorna no encontrado |
| Precondiciones | El empleado no tiene nóminas registradas |
| Datos | employeeId = 99999 |
| Pasos de ejecución | 1. Ejecutar GET /api/v1/payroll/employee/99999<br>2. Verificar código HTTP |
| Resultado esperado | GET /api/v1/payroll/employee/99999 retorna HTTP 404 |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-025 — Resultado de nómina persistido correctamente

| Campo | Valor |
|---|---|
| HU asociada | HU-03 |
| ID del caso | TC-025 |
| Nombre del test | Resultado de nómina persistido correctamente |
| Prioridad | Crítico |
| Endpoint | GET /api/v1/payroll/{payrollId} |
| Escenario | Dado que existe un empleado con tipo de contrato y salario bruto definidos<br>Cuando se procesa la nómina del empleado<br>Entonces el resultado queda persistido con todos los campos correctos |
| Precondiciones | Existe un empleado registrado con salario y tipo de contrato definidos |
| Datos | grossSalary esperado = 3000.00<br>deductionAmount esperado = 283.50<br>bonusAmount esperado = 249.90<br>netSalary esperado = 2966.40 |
| Pasos de ejecución | 1. Ejecutar POST /api/v1/payroll/calculate/{employeeId}<br>2. Obtener payrollId retornado<br>3. Ejecutar GET /api/v1/payroll/{payrollId}<br>4. Verificar campos persistidos |
| Resultado esperado | grossSalary = 3000.00<br>deductionAmount = 283.50<br>bonusAmount = 249.90<br>netSalary = 2966.40<br>createdAt y updatedAt presentes con valores válidos |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-026 — Timestamps de nómina se guardan correctamente

| Campo | Valor |
|---|---|
| HU asociada | HU-03 |
| ID del caso | TC-026 |
| Nombre del test | Timestamps de nómina se guardan correctamente |
| Prioridad | Medio |
| Endpoint | GET /api/v1/payroll/{payrollId} |
| Escenario | Dado que existe una nómina calculada<br>Cuando se consulta la nómina<br>Entonces los campos createdAt y updatedAt están presentes y son válidos |
| Precondiciones | Existe una nómina calculada |
| Datos | payrollId = ID de nómina existente |
| Pasos de ejecución | 1. Calcular nómina y obtener payrollId<br>2. Ejecutar GET /api/v1/payroll/{payrollId}<br>3. Verificar createdAt y updatedAt |
| Resultado esperado | La nómina persistida contiene createdAt y updatedAt con formato y valores válidos |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-027 — Redondeo a 2 decimales en medio tiempo

| Campo | Valor |
|---|---|
| HU asociada | HU-03 |
| ID del caso | TC-027 |
| Nombre del test | Redondeo a 2 decimales en medio tiempo |
| Prioridad | Alto |
| Endpoint | POST /api/v1/payroll/calculate/{employeeId} |
| Escenario | Dado que existe un empleado registrado con salario bruto definido<br>Cuando se procesa la nómina<br>Entonces todos los valores numéricos del resultado están redondeados a 2 decimales |
| Precondiciones | Existe un empleado registrado con grossSalary que genera decimales en el cálculo |
| Datos | contractType = PART_TIME<br>grossSalary = 777.77 |
| Pasos de ejecución | 1. Ejecutar POST /api/v1/payroll/calculate/{employeeId}<br>2. Verificar que todos los campos numéricos tienen exactamente 2 decimales |
| Resultado esperado | Todos los valores numéricos retornados tienen exactamente 2 decimales |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-028 — Tiempo de respuesta del cálculo de nómina ≤ 3 segundos

| Campo | Valor |
|---|---|
| HU asociada | HU-03 |
| ID del caso | TC-028 |
| Nombre del test | Tiempo de respuesta del cálculo de nómina ≤ 3 segundos |
| Prioridad | Alto |
| Endpoint | POST /api/v1/payroll/calculate/{employeeId} |
| Escenario | Dado que existe un empleado registrado con tipo de contrato y salario bruto definidos<br>Cuando se solicita el cálculo de la nómina<br>Entonces el sistema responde en 3 segundos o menos |
| Precondiciones | Existe un empleado registrado con salario y tipo de contrato definidos<br>Ambiente de QA disponible y estable |
| Datos | employeeId = ID de empleado existente<br>Umbral = 3000 ms |
| Pasos de ejecución | 1. Ejecutar POST /api/v1/payroll/calculate/{employeeId}<br>2. Medir el tiempo de respuesta completo<br>3. Comparar contra el umbral |
| Resultado esperado | El tiempo de respuesta es ≤ 3000 ms<br>La respuesta retorna HTTP 201 dentro del umbral definido |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

## HU-04 — Confirmación del resultado

### TC-029 — Resumen muestra todos los campos del cálculo

| Campo | Valor |
|---|---|
| HU asociada | HU-04 |
| ID del caso | TC-029 |
| Nombre del test | Resumen muestra todos los campos del cálculo |
| Prioridad | Crítico |
| Endpoint | GET /api/v1/payroll/{payrollId} |
| Escenario | Dado que la nómina del empleado fue calculada<br>Cuando el administrador accede al resumen del cálculo<br>Entonces el sistema muestra todos los campos requeridos |
| Precondiciones | Existe un empleado con nómina ya calculada |
| Datos | payrollId = ID de nómina calculada |
| Pasos de ejecución | 1. Registrar empleado y calcular su nómina<br>2. Ejecutar GET /api/v1/payroll/{payrollId}<br>3. Verificar código HTTP<br>4. Verificar los campos principales del resumen |
| Resultado esperado | GET /api/v1/payroll/{payrollId} retorna HTTP 200<br>La respuesta incluye employeeName, contractType, grossSalary, deductionAmount, bonusAmount y netSalary |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-030 — Datos del resumen coinciden con datos persistidos

| Campo | Valor |
|---|---|
| HU asociada | HU-04 |
| ID del caso | TC-030 |
| Nombre del test | Datos del resumen coinciden con datos persistidos |
| Prioridad | Crítico |
| Endpoint | GET /api/v1/payroll/{payrollId} |
| Escenario | Dado que la nómina del empleado fue calculada<br>Cuando el administrador accede al resumen del cálculo<br>Entonces los valores mostrados son idénticos a los persistidos |
| Precondiciones | Existe un empleado con nómina calculada y persistida |
| Datos | payrollId = ID de nómina calculada |
| Pasos de ejecución | 1. Calcular nómina y registrar los valores retornados<br>2. Ejecutar GET /api/v1/payroll/{payrollId}<br>3. Comparar cada campo del resumen con lo calculado previamente |
| Resultado esperado | grossSalary, deductionAmount, bonusAmount y netSalary del resumen son idénticos a los del cálculo |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-031 — Confirmación del resumen habilita descarga de PDF

| Campo | Valor |
|---|---|
| HU asociada | HU-04 |
| ID del caso | TC-031 |
| Nombre del test | Confirmación del resumen habilita descarga de PDF |
| Prioridad | Crítico |
| Endpoint | PATCH /api/v1/payroll/{payrollId}/confirm |
| Escenario | Dado que la nómina del empleado fue calculada y el administrador revisa el resumen en la interfaz<br>Cuando confirma que los datos son correctos<br>Entonces el sistema habilita la descarga del PDF |
| Precondiciones | Existe un empleado con nómina calculada<br>El administrador accedió a la vista de resumen |
| Datos | payrollId = ID de nómina calculada |
| Pasos de ejecución | 1. Acceder al resumen de la nómina en la interfaz<br>2. Verificar que el botón de descarga PDF está deshabilitado<br>3. Confirmar los datos desde la interfaz<br>4. Verificar que el botón de descarga queda habilitado |
| Resultado esperado | Antes de confirmar: botón de descarga deshabilitado o no visible<br>Después de confirmar: botón de descarga habilitado<br>La nómina queda confirmada |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-032 — Bloqueo de generación de PDF sin confirmar resumen

| Campo | Valor |
|---|---|
| HU asociada | HU-04 |
| ID del caso | TC-032 |
| Nombre del test | Bloqueo de generación de PDF sin confirmar resumen |
| Prioridad | Crítico |
| Endpoint | GET /api/v1/payroll/{payrollId}/pdf |
| Escenario | Dado que la nómina del empleado fue calculada y el administrador no confirma los datos<br>Cuando intenta generar el PDF<br>Entonces el sistema debe informar que debe confirmar antes de seguir |
| Precondiciones | Existe una nómina calculada pero no confirmada |
| Datos | payrollId = ID de nómina calculada sin confirmar |
| Pasos de ejecución | 1. Calcular la nómina sin confirmar el resumen<br>2. Ejecutar GET /api/v1/payroll/{payrollId}/pdf<br>3. Verificar código HTTP<br>4. Verificar mensaje de error retornado |
| Resultado esperado | GET /api/v1/payroll/{payrollId}/pdf retorna HTTP 400 o 403<br>Mensaje indica que debe confirmar los datos antes de generar el PDF |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-033 — Confirmación de nómina exitosa por API

| Campo | Valor |
|---|---|
| HU asociada | HU-04 |
| ID del caso | TC-033 |
| Nombre del test | Confirmación de nómina exitosa por API |
| Prioridad | Alto |
| Endpoint | PATCH /api/v1/payroll/{payrollId}/confirm |
| Escenario | Dado que existe una nómina calculada<br>Cuando se confirma la nómina por API<br>Entonces el sistema actualiza el estado de confirmación |
| Precondiciones | Existe una nómina calculada con confirmed = false |
| Datos | payrollId = ID de nómina existente |
| Pasos de ejecución | 1. Calcular la nómina y obtener payrollId<br>2. Ejecutar PATCH /api/v1/payroll/{payrollId}/confirm<br>3. Verificar código HTTP<br>4. Verificar que confirmed = true en la respuesta |
| Resultado esperado | PATCH /api/v1/payroll/{payrollId}/confirm retorna HTTP 200<br>La respuesta refleja confirmed = true |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-034 — GET nómina inexistente retorna HTTP 404

| Campo | Valor |
|---|---|
| HU asociada | HU-04 |
| ID del caso | TC-034 |
| Nombre del test | GET nómina inexistente retorna HTTP 404 |
| Prioridad | Alto |
| Endpoint | GET /api/v1/payroll/{payrollId} |
| Escenario | Dado que no existe una nómina con el identificador consultado<br>Cuando se consulta esa nómina<br>Entonces el sistema informa que la nómina no fue encontrada |
| Precondiciones | El payrollId utilizado no existe en base de datos |
| Datos | payrollId = 99999 |
| Pasos de ejecución | 1. Ejecutar GET /api/v1/payroll/99999<br>2. Verificar código HTTP |
| Resultado esperado | GET /api/v1/payroll/99999 retorna HTTP 404 |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

## HU-02 — Corrección de datos del empleado

### TC-035 — Corrección exitosa del nombre del empleado

| Campo | Valor |
|---|---|
| HU asociada | HU-02 |
| ID del caso | TC-035 |
| Nombre del test | Corrección exitosa del nombre del empleado |
| Prioridad | Crítico |
| Endpoint | PATCH /api/v1/employees/{id} |
| Escenario | Dado que el empleado está registrado con los datos necesarios<br>Cuando se cambia el nombre del empleado por uno válido<br>Entonces los datos del empleado quedan actualizados |
| Precondiciones | Existe un empleado registrado con id conocido |
| Datos | id = ID de empleado existente<br>name = "Gonzalo Fernando Martinez" |
| Pasos de ejecución | 1. Registrar un empleado y obtener su id<br>2. Ejecutar PATCH /api/v1/employees/{id} con el nuevo name<br>3. Verificar código HTTP<br>4. Ejecutar GET /api/v1/employees/{id} y validar el cambio |
| Resultado esperado | PATCH /api/v1/employees/{id} retorna HTTP 200<br>GET /api/v1/employees/{id} retorna el nombre actualizado correctamente |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-036 — Corrección exitosa del salario bruto

| Campo | Valor |
|---|---|
| HU asociada | HU-02 |
| ID del caso | TC-036 |
| Nombre del test | Corrección exitosa del salario bruto |
| Prioridad | Crítico |
| Endpoint | PATCH /api/v1/employees/{id} |
| Escenario | Dado que el empleado está registrado<br>Cuando se actualiza el salario bruto con un valor positivo válido<br>Entonces los datos quedan actualizados con el nuevo valor |
| Precondiciones | Existe un empleado registrado con id conocido |
| Datos | id = ID de empleado existente<br>grossSalary = 3500.00 |
| Pasos de ejecución | 1. Registrar un empleado con grossSalary = 3000.00<br>2. Ejecutar PATCH /api/v1/employees/{id} con grossSalary = 3500.00<br>3. Verificar código HTTP<br>4. Consultar el empleado y validar el cambio |
| Resultado esperado | PATCH /api/v1/employees/{id} retorna HTTP 200<br>GET /api/v1/employees/{id} retorna grossSalary = 3500.00 |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-037 — Corrección fallida por nombre con caracteres especiales

| Campo | Valor |
|---|---|
| HU asociada | HU-02 |
| ID del caso | TC-037 |
| Nombre del test | Corrección fallida por nombre con caracteres especiales |
| Prioridad | Alto |
| Endpoint | PATCH /api/v1/employees/{id} |
| Escenario | Dado que el empleado está registrado<br>Cuando se intenta cambiar el nombre por uno que contiene caracteres especiales<br>Entonces los datos del empleado no quedan actualizados |
| Precondiciones | Existe un empleado registrado con id conocido |
| Datos | id = ID de empleado existente<br>name = "Carlos@#2025" |
| Pasos de ejecución | 1. Ejecutar PATCH /api/v1/employees/{id} con name inválido<br>2. Verificar código HTTP<br>3. Verificar mensaje de error<br>4. Consultar el empleado y validar que no cambió |
| Resultado esperado | PATCH /api/v1/employees/{id} retorna HTTP 400<br>El nombre del empleado permanece sin cambios |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-038 — Corrección fallida por salario bruto negativo

| Campo | Valor |
|---|---|
| HU asociada | HU-02 |
| ID del caso | TC-038 |
| Nombre del test | Corrección fallida por salario bruto negativo |
| Prioridad | Alto |
| Endpoint | PATCH /api/v1/employees/{id} |
| Escenario | Dado que existe un empleado registrado con sus datos<br>Cuando se intenta actualizar el salario bruto con un valor negativo<br>Entonces los datos del empleado permanecen sin cambios |
| Precondiciones | Existe un empleado registrado con id conocido |
| Datos | id = ID de empleado existente<br>grossSalary = -500.00 |
| Pasos de ejecución | 1. Ejecutar PATCH /api/v1/employees/{id} con grossSalary negativo<br>2. Verificar código HTTP<br>3. Verificar mensaje de error<br>4. Consultar el empleado y validar que no cambió |
| Resultado esperado | PATCH /api/v1/employees/{id} retorna HTTP 400<br>El salario del empleado permanece sin cambios |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-039 — Bloqueo de corrección por nómina ya calculada

| Campo | Valor |
|---|---|
| HU asociada | HU-02 |
| ID del caso | TC-039 |
| Nombre del test | Bloqueo de corrección por nómina ya calculada |
| Prioridad | Crítico |
| Endpoint | PATCH /api/v1/employees/{id} |
| Escenario | Dado que el empleado está registrado y la nómina ya fue calculada<br>Cuando el administrador intenta modificar datos del empleado<br>Entonces el sistema no lo permite |
| Precondiciones | Existe un empleado registrado con nómina ya calculada |
| Datos | id = ID de empleado existente<br>name = "Carlos Sanchez" |
| Pasos de ejecución | 1. Registrar empleado y calcular su nómina<br>2. Ejecutar PATCH /api/v1/employees/{id} con nuevos datos válidos<br>3. Verificar código HTTP y mensaje retornado |
| Resultado esperado | PATCH /api/v1/employees/{id} retorna HTTP 403<br>Mensaje indica que los datos no pueden modificarse porque la nómina ya fue calculada |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-040 — Race condition: nómina calculada durante sesión de edición

| Campo | Valor |
|---|---|
| HU asociada | HU-02 |
| ID del caso | TC-040 |
| Nombre del test | Race condition: nómina calculada durante sesión de edición |
| Prioridad | Medio |
| Endpoint | PATCH /api/v1/employees/{id} y POST /api/v1/payroll/calculate/{employeeId} |
| Escenario | Dado que el administrador tiene abierto el formulario de edición del empleado<br>Y la nómina pasa a estado calculada durante la sesión<br>Cuando intenta guardar los cambios<br>Entonces se documenta el comportamiento observado del sistema |
| Precondiciones | Existe un empleado registrado<br>El formulario de edición está abierto en la interfaz |
| Datos | Escenario de concurrencia: edición activa + cálculo concurrente |
| Pasos de ejecución | 1. Abrir el formulario de edición del empleado en la interfaz<br>2. Desde otra sesión ejecutar POST /api/v1/payroll/calculate/{employeeId}<br>3. Intentar guardar cambios con PATCH /api/v1/employees/{id}<br>4. Registrar código HTTP y mensaje retornado |
| Resultado esperado | Documentar el comportamiento observado: HTTP 403, HTTP 409 u otro código; claridad del mensaje; consistencia final de los datos |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-041 — Corrección exitosa de contrato

| Campo | Valor |
|---|---|
| HU asociada | HU-02 |
| ID del caso | TC-041 |
| Nombre del test | Corrección exitosa de contrato |
| Prioridad | Alto |
| Endpoint | PATCH /api/v1/employees/{id}/contracts/{contractId} |
| Escenario | Dado que el empleado está registrado con un contrato asociado<br>Cuando se edita el contrato con datos válidos<br>Entonces el contrato queda actualizado |
| Precondiciones | Existe un empleado registrado con contractId conocido |
| Datos | id = ID de empleado existente<br>contractId = ID de contrato existente<br>contractType = "PART_TIME" |
| Pasos de ejecución | 1. Registrar un empleado con contrato y obtener contractId<br>2. Ejecutar PATCH /api/v1/employees/{id}/contracts/{contractId}<br>3. Verificar código HTTP<br>4. Consultar el empleado y verificar el contrato actualizado |
| Resultado esperado | PATCH /api/v1/employees/{id}/contracts/{contractId} retorna HTTP 200<br>El contrato aparece actualizado en la consulta |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-042 — Corrección fallida de contrato por tipo vacío

| Campo | Valor |
|---|---|
| HU asociada | HU-02 |
| ID del caso | TC-042 |
| Nombre del test | Corrección fallida de contrato por tipo vacío |
| Prioridad | Alto |
| Endpoint | PATCH /api/v1/employees/{id}/contracts/{contractId} |
| Escenario | Dado que el empleado está registrado con un contrato asociado<br>Cuando se intenta editar el contrato con contractType vacío o inválido<br>Entonces el sistema no permite la actualización |
| Precondiciones | Existe un empleado registrado con contractId conocido |
| Datos | id = ID de empleado existente<br>contractId = ID de contrato existente<br>contractType = "" |
| Pasos de ejecución | 1. Ejecutar PATCH /api/v1/employees/{id}/contracts/{contractId} con contractType inválido<br>2. Verificar código HTTP |
| Resultado esperado | PATCH /api/v1/employees/{id}/contracts/{contractId} retorna HTTP 400<br>El contrato no es actualizado |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-043 — Cierre de contrato exitoso

| Campo | Valor |
|---|---|
| HU asociada | HU-02 |
| ID del caso | TC-043 |
| Nombre del test | Cierre de contrato exitoso |
| Prioridad | Alto |
| Endpoint | PATCH /api/v1/employees/{id}/contracts/{contractId}/end-date |
| Escenario | Dado que el empleado está registrado con un contrato activo<br>Cuando se registra una fecha de cierre válida<br>Entonces el contrato queda actualizado con su fecha de finalización |
| Precondiciones | Existe un empleado registrado con contractId conocido |
| Datos | id = ID de empleado existente<br>contractId = ID de contrato existente<br>endDate = fecha actual o futura |
| Pasos de ejecución | 1. Ejecutar PATCH /api/v1/employees/{id}/contracts/{contractId}/end-date<br>2. Verificar código HTTP |
| Resultado esperado | PATCH /api/v1/employees/{id}/contracts/{contractId}/end-date retorna HTTP 204 |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-044 — Cierre de contrato fallido por fecha en el pasado

| Campo | Valor |
|---|---|
| HU asociada | HU-02 |
| ID del caso | TC-044 |
| Nombre del test | Cierre de contrato fallido por fecha en el pasado |
| Prioridad | Alto |
| Endpoint | PATCH /api/v1/employees/{id}/contracts/{contractId}/end-date |
| Escenario | Dado que el empleado está registrado con un contrato activo<br>Cuando se intenta cerrar el contrato con una fecha en el pasado<br>Entonces el sistema no permite la actualización |
| Precondiciones | Existe un empleado registrado con contractId conocido |
| Datos | id = ID de empleado existente<br>contractId = ID de contrato existente<br>endDate = fecha pasada |
| Pasos de ejecución | 1. Ejecutar PATCH /api/v1/employees/{id}/contracts/{contractId}/end-date con fecha inválida<br>2. Verificar código HTTP<br>3. Verificar mensaje de error |
| Resultado esperado | PATCH /api/v1/employees/{id}/contracts/{contractId}/end-date retorna HTTP 400<br>Mensaje indica que la fecha de cierre no puede ser en el pasado |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-045 — Mensaje de confirmación tras edición exitosa

| Campo | Valor |
|---|---|
| HU asociada | HU-02 |
| ID del caso | TC-045 |
| Nombre del test | Mensaje de confirmación tras edición exitosa |
| Prioridad | Medio |
| Endpoint | PATCH /api/v1/employees/{id} |
| Escenario | Dado que el empleado está registrado<br>Cuando el administrador guarda una edición válida en la interfaz<br>Entonces el sistema muestra un mensaje de confirmación de cambios |
| Precondiciones | Existe un empleado registrado<br>El administrador tiene el formulario de edición abierto |
| Datos | name = "Pedro Gomez" |
| Pasos de ejecución | 1. Acceder al formulario de edición del empleado<br>2. Modificar el nombre con un valor válido<br>3. Guardar los cambios<br>4. Verificar mensaje de confirmación |
| Resultado esperado | El sistema muestra el mensaje de confirmación de cambios exitosos tras guardar |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

## HU-05 — Generación de PDF

### TC-046 — Generación exitosa del PDF con campos correctos

| Campo | Valor |
|---|---|
| HU asociada | HU-05 |
| ID del caso | TC-046 |
| Nombre del test | Generación exitosa del PDF con campos correctos |
| Prioridad | Crítico |
| Endpoint | GET /api/v1/payroll/{payrollId}/pdf |
| Escenario | Dado que la nómina del empleado fue calculada y el administrador confirmó los datos del resumen<br>Cuando genera el PDF<br>Entonces el sistema devuelve un PDF descargable con los campos correctos |
| Precondiciones | Existe un empleado con nómina calculada y resumen confirmado |
| Datos | payrollId = ID de nómina confirmada |
| Pasos de ejecución | 1. Registrar empleado, calcular nómina y confirmar resumen<br>2. Ejecutar GET /api/v1/payroll/{payrollId}/pdf<br>3. Verificar código HTTP<br>4. Verificar Content-Type = application/pdf |
| Resultado esperado | GET /api/v1/payroll/{payrollId}/pdf retorna HTTP 200<br>Header Content-Type: application/pdf presente<br>El PDF contiene nombre, tipo de contrato, salario bruto, deducción, bonificación y salario neto |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-047 — Bloqueo de generación de PDF sin confirmar resumen

| Campo | Valor |
|---|---|
| HU asociada | HU-05 |
| ID del caso | TC-047 |
| Nombre del test | Bloqueo de generación de PDF sin confirmar resumen |
| Prioridad | Crítico |
| Endpoint | GET /api/v1/payroll/{payrollId}/pdf |
| Escenario | Dado que la nómina del empleado fue calculada y el administrador no confirmó los datos del resumen<br>Cuando intenta generar el PDF<br>Entonces el sistema bloquea la operación e informa que debe confirmar primero |
| Precondiciones | Existe un empleado con nómina calculada<br>El resumen no ha sido confirmado |
| Datos | payrollId = ID de nómina calculada sin confirmar |
| Pasos de ejecución | 1. Calcular la nómina sin confirmar el resumen<br>2. Ejecutar GET /api/v1/payroll/{payrollId}/pdf<br>3. Verificar código HTTP<br>4. Verificar mensaje de error |
| Resultado esperado | GET /api/v1/payroll/{payrollId}/pdf retorna HTTP 400 o 403<br>Mensaje indica que debe confirmar los datos del resumen antes de generar el PDF |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-048 — Previsualización del PDF muestra todos los campos correctos

| Campo | Valor |
|---|---|
| HU asociada | HU-05 |
| ID del caso | TC-048 |
| Nombre del test | Previsualización del PDF muestra todos los campos correctos |
| Prioridad | Alto |
| Endpoint | GET /api/v1/payroll/{payrollId}/pdf |
| Escenario | Dado que la nómina fue calculada y el resumen fue confirmado<br>Cuando el administrador accede a la previsualización del PDF en la interfaz<br>Entonces la previsualización muestra todos los campos correctos antes de descargar |
| Precondiciones | Existe un empleado con nómina calculada y resumen confirmado |
| Datos | payrollId = ID de nómina confirmada |
| Pasos de ejecución | 1. Navegar a la vista de previsualización del PDF<br>2. Verificar que se muestran los campos principales<br>3. Comparar los valores con el resumen confirmado |
| Resultado esperado | La previsualización muestra los campos correctos con los mismos valores que el resumen confirmado |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-049 — Notificación de descarga exitosa

| Campo | Valor |
|---|---|
| HU asociada | HU-05 |
| ID del caso | TC-049 |
| Nombre del test | Notificación de descarga exitosa |
| Prioridad | Alto |
| Endpoint | GET /api/v1/payroll/{payrollId}/pdf |
| Escenario | Dado que la nómina fue calculada y el resumen fue confirmado<br>Cuando el administrador descarga el PDF desde la interfaz<br>Entonces el sistema muestra una notificación de descarga exitosa |
| Precondiciones | Existe un empleado con nómina calculada y resumen confirmado |
| Datos | payrollId = ID de nómina confirmada |
| Pasos de ejecución | 1. Hacer clic en el botón de descarga del PDF<br>2. Esperar a que la descarga complete<br>3. Verificar la notificación al usuario |
| Resultado esperado | El sistema muestra la notificación de descarga exitosa y el archivo PDF queda disponible |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-050 — Tiempo de generación del PDF ≤ 3 segundos

| Campo | Valor |
|---|---|
| HU asociada | HU-05 |
| ID del caso | TC-050 |
| Nombre del test | Tiempo de generación del PDF ≤ 3 segundos |
| Prioridad | Alto |
| Endpoint | GET /api/v1/payroll/{payrollId}/pdf |
| Escenario | Dado que la nómina fue calculada y el resumen fue confirmado<br>Cuando se solicita la generación del PDF<br>Entonces el sistema responde en 3 segundos o menos |
| Precondiciones | Existe un empleado con nómina calculada y resumen confirmado |
| Datos | payrollId = ID de nómina confirmada<br>Umbral = 3000 ms |
| Pasos de ejecución | 1. Ejecutar GET /api/v1/payroll/{payrollId}/pdf<br>2. Medir el tiempo de respuesta completo<br>3. Comparar contra el umbral |
| Resultado esperado | El tiempo de respuesta es ≤ 3000 ms<br>La respuesta retorna HTTP 200 dentro del umbral definido |
| Estado | Sin ejecutar |
| Resultado ejecución | — |

### TC-051 — Consistencia visual del PDF en distintos navegadores

| Campo | Valor |
|---|---|
| HU asociada | HU-05 |
| ID del caso | TC-051 |
| Nombre del test | Consistencia visual del PDF en distintos navegadores |
| Prioridad | Bajo |
| Endpoint | GET /api/v1/payroll/{payrollId}/pdf |
| Escenario | Dado que la nómina fue calculada y el resumen fue confirmado<br>Cuando se genera y visualiza el PDF en distintos navegadores<br>Entonces se documenta si el PDF se ve igual en todos los navegadores evaluados |
| Precondiciones | Existe un empleado con nómina calculada y resumen confirmado<br>Navegadores disponibles: Chrome, Firefox, Edge |
| Datos | payrollId = ID de nómina confirmada |
| Pasos de ejecución | 1. Generar el PDF desde Chrome y tomar captura<br>2. Generar el PDF desde Firefox y tomar captura<br>3. Generar el PDF desde Edge y tomar captura<br>4. Comparar visualmente las capturas |
| Resultado esperado | Se documentan diferencias encontradas entre navegadores y se registra si el PDF es visualmente consistente |
| Estado | Sin ejecutar |
| Resultado ejecución | — |
