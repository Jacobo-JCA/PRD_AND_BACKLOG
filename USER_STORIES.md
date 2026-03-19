# Historias de Usuario - Calculadora de Nómina y Beneficios

---

## HU-01 — Registro de empleado 
**Como** administrador de recursos humanos <br>
**Quiero** registrar los datos básicos del empleado <br>
**Para** contar con la información necesaria antes de iniciar el cálculo de nómina.

### Criterios de aceptacion

**Registro exitoso del empleado**
```gherkin
    Given no existe el empleado en el sistema
    When se registra un empleado con sus datos necesarios (nombre, tipo de contrato y salario bruto)
    Then el empleado queda guardado en el sistema
    And queda habilitado para confirmar su nómina
```
**Registro fallido por falta de datos necesarios**
```gherkin
    Given no existe el empleado en el sistema
    When se intenta registrar un empleado sin ingresar datos necesarios
    Then el sistema no permite guardar el empleado
    And notifica cuales son los datos necesarios
```
**Registro fallido por salario bruto inválido**
```gherkin
    Given el empleado no existe en el sistema
    When se intenta registrar al empleado con un salario bruto negativo o en cero
    Then el sistema no permite guardar el empleado
    And notifica que el salario bruto debe ser positivo
```
**Registro fallido por caracteres en nombre**
```gherkin
    Given el empleado no consta en el sistema
    When se intenta registrar al empleado con un nombre que contiene caracteres especiales
    Then el sistema no permite guardarlo
    And notifica que el nombre no debe contener caracteres especiales
```
---

## HU-02 — Corrección de datos 
**Como** administrador de recursos humanos <br>
**Quiero** corregir los datos de un empleado antes de confirmar el cálculo <br>
**Para** asegurarme de que la información es correcta antes de obtener el resultado

### Criterios de aceptacion

**Correccion exitosa del nombre del empleado**
```gherkin
    Given el empleado esta registrado con los datos necesarios (nombre, tipo de contrato y sueldo bruto)
    And la nómina no fue confirmada
    When se cambia el nombre del empleado
    Then los datos del empleado quedan actualizados
```
**Correccion exitosa del salario bruto del empleado**
```gherkin
    Given el empleado esta registrado
    And la nómina del empleado no fue confirmada
    When se actualiza el salario bruto con un valor positivo valido
    Then los datos quedan actualizados con el nuevo valor
```
**Correccion erronea por nombre invalido**
```gherkin
    Given el empleado esta registrado
    And la nómina del empleado no fue confirmada
    When se intenta cambiar el nombre del empleado por uno que contiene caracteres especiales
    Then los datos del empleado no quedan actualizados
    And el sistema informa que el nombre no puede tener caracteres especiales
```
**Correccion fallida por salario bruto invalido**
```gherkin
    Given existe un empleado registrado con sus datos
    And la nómina del empleado no fue confirmada
    When se intenta actualizar el salario bruto con un valor negativo
    Then los datos del empleado permanecen sin cambios
    And el sistema informa que el salario bruto tiene que ser positivo
```
___

## HU-03 — Cálculo de salario neto 
**Como** administrador de recursos humanos 
**Quiero** calcular automáticamente el salario neto del empleado según su tipo de contrato 
**Para** procesar la nómina sin intervención manual y sin riesgo de errores.
