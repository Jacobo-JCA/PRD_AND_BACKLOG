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
**Registro fallido por datos vacios**
```gherkin
    Given el administrador de recursos humanos
    When intenta registrar un empleado con datos vacios
    Then el sistema no permite guarda el empleado
    And informa cuales son los datos vacios
```
