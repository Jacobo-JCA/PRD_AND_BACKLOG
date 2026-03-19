# Historias de Usuario - Calculadora de Nómina y Beneficios

---

## HU-01 — Registro de empleado 
**Como** administrador de recursos humanos <br>
**Quiero** registrar los datos básicos del empleado <br>
**Para** contar con la información necesaria antes de iniciar el cálculo de nómina.

### Criterios de aceptacion
- El tipo de contrato debe ser tiempo completo, medio tiempo o servicios profesionales.
- El sueldo bruto tiene que ser positivo
- El nombre tiene que contener solo letras y espacios

```gherkin
Feature: Registro de empleado para cálculo de nómina

  Background:
    Given el administrador de recursos humanos

  Scenario Outline: Registro exitoso del empleado
    When registra un empleado con nombre "Matias", tipo de contrato "<tipo_contrato>" y salario bruto de <salario_bruto>
    Then el empleado queda habilitado para procesar su nómina

    Examples:
      | tipo_contrato           | salario_bruto |
      | tiempo completo         | 10000         |
      | medio tiempo            | 10000         |
      | servicios profesionales | 10000         |

  Scenario Outline: Registro fallido por salario bruto inválido
    When registra un empleado con nombre "Matias", tipo de contrato "<tipo_contrato>" y salario bruto de <salario_bruto>
    Then el sistema informa que el salario bruto no es valido
    And el empleado no queda registrado

    Examples:
      | tipo_contrato           | salario_bruto |
      | tiempo completo         | -200          |
      | medio tiempo            | 0             |
      | servicios profesionales | -100          |

  Scenario Outline: Registro fallido por nombre vacío
    When registra un empleado con nombre "", tipo de contrato "<tipo_contrato>" y salario bruto de <salario_bruto>
    Then el sistema informa que el nombre del empleado es obligatorio
    And el empleado no queda registrado

    Examples:
      | tipo_contrato           | salario_bruto |
      | tiempo completo         | 2000          |
      | medio tiempo            | 2000          |
      | servicios profesionales | 2000          |

  Scenario Outline: Registro fallido por nombre con caracteres inválidos
    When registra un empleado con nombre "<nombre>", tipo de contrato "tiempo completo" y salario bruto de 5000
    Then el sistema informa que el nombre no es valido
    And el empleado no queda registrado

    Examples:
      | nombre  |
      | Matias1 |
      | Matias@ |
      | 123     |

  Scenario: Registro fallido por tipo de contrato no permitido
    When registra un empleado con nombre "Matias", tipo de contrato "Contractor" y salario bruto de 1000
    Then el sistema informa que el tipo de contrato no es válido
    And el empleado no queda registrado

```
