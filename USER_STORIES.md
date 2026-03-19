# Historias de Usuario - Calculadora de Nómina y Beneficios

---

## HU-01 — Registro de empleado 
**Como** administrador de recursos humanos <br>
**Quiero** registrar los datos básicos del empleado <br>
**Para** contar con la información necesaria antes de iniciar el cálculo de nómina.

### Criterios de aceptacion

**Registro exitoso del empleado**
```gherkin
    Given el administrador de recursos humanos
    When registra un empleado con sus datos necesarios (nombre, tipo de contrato y salario bruto)
    Then el empleado queda habilitado para procesar su nómina
```
**Registro fallido por falta de datos necesarios**
```gherkin
    Given el administrador de recursos humanos
    When intenta registrar un empleado sin ingresar datos necesarios
    Then el sistema no permite guarda el empleado
    And informa cuales son los datos necesarios
```
**Registro fallido por salario bruto inválido**
```gherkin
    Given el administrador de recursos humanos
    When intenta registrar un empleado con un salario bruto negativo o en cero
    Then el sistema no permite guardar el empleado
    And informa que el salario bruto debe ser positivo
```
**Registro fallido por caracteres en nombre**
```gherkin
    Given el administrador de recursos humanos
    When intenta registrar un empleado con un nombre que contiene caracteres
    Then el sistema no permite guardar el empleado
    And informa que el nombre no debe contener caracteres
```
---

## HU-02 — Corrección de datos 
**Como** administrador de recursos humanos <br>
**Quiero** corregir los datos de un empleado antes de confirmar el cálculo <br>
**Para** asegurarme de que la información es correcta antes de obtener el resultado

### Criterios de aceptacion

**Correccion exitosa del nombre del empleado**
```gherkin
    Given existe un empleado registrado con los datos necesarios (nombre, tipo de contrato y sueldo bruto)
    And la nómina del empleado no fue confirmada
    When el administrador cambia el nombre del empleado
    Then los datos del empleado quedan actualizados
```
**Correccion exitosa del salario bruto del empleado**
```gherkin
    Given existe un empleado registrado con los datos necesarios (nombre, tipo de contrato y sueldo bruto)
    And la nómina del empleado no fue confirmar
    When el administrador cambia el salario bruto positivo
    Then los datos del empleado quedan actualizados
```
**Correccion erronea por nombre invalido**
```gherkin
    Given existe un empleado registrado con los datos necesarios (nombre, tipo de contrato y sueldo bruto)
    And la nómina del empleado no fue confirmar
    When el administrador intenta cambiar el nombre del empleado por uno que contiene caracteres especiales
    Then los datos del empleado no quedan actualizados
    And el sistema informa que el nombre no puede tener caracteres
```
**Correccion fallida por salario bruto invalido**
```gherkin
    Given existe un empleado registrado con los datos necesarios (nombre, tipo de contrato y sueldo bruto)
    And la nómina del empleado no fue confirmar
    When el administrador cambia el salario bruto a menor a cero o cero
    Then los datos del empleado no quedan actualizados
    And el sistema informa que el salario bruto tiene que ser positivo
```
