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
**Quiero** corregir los datos de un empleado antes de procesar el cálculo <br>
**Para** asegurarme de que la información es correcta antes de obtener el resultado
