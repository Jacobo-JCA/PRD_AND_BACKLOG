# REALITY_CHECK: Retrospectiva de Micro-Sprints (MVP)

## 1. Introducción y Contexto del Sprint

* **Sprint ID:** Micro-Sprints 1 & 2.
* **Objetivo del MVP:** Lograr el flujo funcional completo: desde la creación del empleado, el procesamiento automático de cálculos de nómina (con sus respectivas deducciones y bonificaciones), hasta la generación exitosa del archivo PDF listo para descarga.
* **Estado de Entrega:** **EXITOSO (100%)**. Se completaron los **21 Story Points** planificados. El equipo logró integrar la lógica de negocio, la comunicación entre microservicios y la generación de documentos, cumpliendo con el alcance definido en el PRD.

---

## 2. Análisis de Estimaciones vs. Realidad

### ¿Qué tareas subestimamos (o sobrestimamos) y por qué?

* **Sobreestimación de la HU-03 (Lógica de Cálculos):**

  * **Puntaje asignado:** Fue la historia con mayor puntaje del backlog (estimada como "Dificultad Alta").
  * **Realidad:** El esfuerzo real fue menor al esperado.
  * **Causa:** No se contempló inicialmente que el desarrollo se apoyaría en **Inteligencia Artificial** como acelerador. La IA permitió implementar las fórmulas de deducción (9.45% y 8.00%) y la lógica de bonificaciones de manera mucho más ágil, transformando una tarea "compleja" en una ejecución de dificultad media.

---

### 2.1 Configuración del entorno multi-servicio

**Tarea afectada:** Entorno de QA (criterio de entrada de todos los microsprints)

La arquitectura del sistema se compone de dos microservicios independientes (`employee-service` y `payroll-service`) orquestados mediante Docker Compose. Al momento del diseño inicial, se asumió un entorno homogéneo con una única URL base; sin embargo, en la práctica cada servicio expone su propio endpoint.

Desde el lado de desarrollo, esto implicó:

* Definir correctamente los puertos y nombres de servicio en Docker Compose.
* Asegurar la resolución interna de servicios mediante networking de Docker.
* Externalizar configuraciones mediante variables de entorno (`ENV`) para evitar hardcoding de URLs.

**Causa:** Falta de alineación temprana entre DEV y QA respecto a la arquitectura distribuida y su impacto en la configuración de entornos.

---

### 2.2 Consistencia eventual entre microservicios (retry logic)

**Tarea afectada:** HU-03 · T04 — `POST /api/v1/payroll/calculate/{employeeId}`

En el diseño inicial se asumió una consistencia inmediata entre servicios. Sin embargo, en la práctica, la comunicación entre `employee-service` y `payroll-service` introduce latencia, generando escenarios donde un empleado recién creado aún no está disponible para el cálculo de nómina.

Desde backend, esto evidenció que:

* La arquitectura sigue un modelo de **consistencia eventual**.
* No existe un mecanismo de sincronización fuerte entre servicios.
* Las operaciones distribuidas dependen del estado propagado entre servicios.

**Causa:** Falta de consideración explícita de patrones de sistemas distribuidos en la fase de diseño (eventual consistency, retry, tolerancia a fallos).

---

### 2.3 Divergencia entre el diseño de API del backlog y la API real implementada

**Tarea afectada:** HU-01 · HU-03

El backlog original definía un modelo más granular (empleados, contratos y salarios como recursos independientes). Sin embargo, durante la implementación se optó por un enfoque simplificado orientado al MVP:

* Se consolidó la creación del empleado en un único endpoint:
  `POST /api/v1/employees`
* El `contractType` y `grossSalary` se manejan como atributos directos del empleado.

**Impacto en desarrollo:**

* Reducción de complejidad en la API.
* Menor número de endpoints y menor acoplamiento entre recursos.
* Simplificación del flujo de creación.

**Causa:** Decisión de diseño orientada a velocidad de entrega del MVP, sin un acuerdo formal previo con QA sobre el contrato final.

---

### 2.4 Configuración del stack SerenityBDD + Screenplay

**Tarea afectada:** Integración E2E con frontend

Aunque este punto impacta directamente a QA, desde backend se identificó que:

* La estabilidad de endpoints y contratos es crítica para pruebas E2E.
* Cambios menores en la API generan alto impacto en capas superiores (UI testing).

**Causa:** Subestimación del impacto de cambios en backend sobre herramientas de automatización E2E.

---

### 2.5 Diseño del setup de datos para pruebas de rendimiento k6

**Tarea afectada:** HU-03 · HU-05

Las pruebas de rendimiento evidenciaron que el backend requiere estados previos válidos para operar correctamente (empleados creados, nóminas confirmadas).

Desde desarrollo, esto implica:

* Diseñar APIs idempotentes y predecibles.
* Considerar endpoints auxiliares o estrategias para inicialización de datos.
* Entender que el rendimiento depende también del flujo completo, no solo de endpoints aislados.

**Causa:** Falta de consideración del ciclo completo de datos en pruebas de carga.

---

### ¿Por qué ocurrió la desviación? (Complejidad Técnica)

* **Investigación en Seguridad y Buenas Prácticas:**

  La implementación de seguridad no fue planificada detalladamente en el refinamiento inicial. Al ser un **sistema distribuido**, surgió la necesidad de investigar e implementar mecanismos de autenticación y validación entre servicios (ej. firmas internas, headers seguros), lo que añadió una carga técnica no prevista.

---

  ### Orquestación y Resiliencia de Infraestructura
  La configuración de Docker y Docker Compose no fue una simple creación de contenedores, convirtiéndose en un reto de ingeniería de confiabilidad.

  - Networking: Se requirió un diseño preciso de redes internas para que los servicios se descubrieran mediante nombres de host virtuales ej. http://payroll-db:5432 en lugar de IPs estáticas.

  - Gestión de Dependencias y Healthchecks: La implementación de depends_on fue esencial para garantizar la disponibilidad de los services dependientes. Evitando fallos en cascada durante el despliegue del MVP.

  - Persistencia Volátil: La configuración de volúmenes para asegurar que los datos de los empleados y nóminas no se perdieran al reiniciar los contenedores requirió múltiples iteraciones de prueba y error.

---
  
### Diseño de Arquitectura Distribuida

Orquestación de Mensajería Asincrónica (RabbitMQ)
La integración entre employee-service y payroll-service fue el reto técnico más demandante del MVP.

- Evolución del Enfoque: Inicialmente, la comunicación se gestionó de forma manual y aislada en cada servicio. Sin embargo, para garantizar la integridad de los datos, se migró hacia un modelo basado en eventos utilizando RabbitMQ.

- Optimización vía Dependencias: Para agilizar el desarrollo, se refactorizó el código asignando dependencias compartidas y contratos de mensajes específicos, lo que simplificó la implementación final pero requirió un tiempo de "re-work" técnico que no estaba en el backlog original.

- Lógica de Consumo: La configuración de los Consumers en el payroll-service para procesar los cambios de estado de los empleados en tiempo real introdujo una capa de complejidad en el manejo de colas y confirmaciones de lectura (ACKs).

---

## 3. Evaluación del MVP: Valor de Negocio

### ¿El MVP construido es realmente valioso para el negocio?

* **Optimización del Tiempo en RRHH:**

  * **Impacto:** El sistema elimina la carga operativa de realizar cálculos manuales en hojas de cálculo.
  * Permite automatizar completamente el flujo de nómina desde el registro del empleado.

* **Disponibilidad de Información:**

  * Se centraliza la información en un sistema accesible vía API.
  * Permite consultas rápidas y consistentes de datos de empleados y nómina.

* **Cumplimiento de Funcionalidades Críticas:**

  * Implementación completa de los **tres tipos de contrato**:

    * Full Time
    * Part Time
    * Servicios Profesionales
  * Aplicación correcta de reglas de negocio:

    * Deducciones (9.45% / 8.00%)
    * Bonificaciones
  * Generación de PDF como salida final del proceso.

---

### Trade-offs y Funcionalidades Adicionales

* **Sin Sacrificios (Trade-offs):**

  * No se eliminaron funcionalidades del backlog original.
  * Se mantuvo el alcance completo sin comprometer calidad.

* **Funcionalidades de Valor Agregado (Plus):**

  * Implementación de **Finalización de Contrato**:

    * Mejora la gestión del ciclo de vida del empleado.
    * Añade valor administrativo desde la primera versión del sistema.

---

## 4. Aseguramiento de Calidad (QA) bajo Presión

### 4.1 Pirámide de pruebas con tres capas complementarias

El equipo de QA implementó cobertura en tres niveles independientes, cada uno apuntando a un tipo de defecto distinto:

| Capa | Herramienta | Qué detecta | Cobertura alcanzada |
|---|---|---|---|
| **API / Contrato** | Karate | Códigos HTTP incorrectos, estructura de respuesta rota, datos no persistidos, reglas de negocio erróneas | TC-001 a TC-044 — todos cubiertos por `.feature` files |
| **Rendimiento** | k6 | Degradación de tiempo de respuesta bajo carga concurrente (50 usuarios virtuales) | TC-028 (`calculate`) y TC-050 (`PDF`) con umbrales `p(95) < 3000ms` |
| **E2E de interfaz** | SerenityBDD + Cucumber + Screenplay | Flujos de usuario que involucran la UI: confirmación del resumen, habilitación del botón de PDF, notificación de descarga | TC-031, TC-045, TC-050, TC-051 |

Ninguna capa reemplaza a las demás: Karate puede detectar que `POST /api/v1/payroll/calculate` retorna el salario neto correcto, pero no puede verificar que el botón de descarga de PDF se habilita en la interfaz tras confirmar. SerenityBDD cubre ese gap.

---

### 4.2 Estrategia de etiquetas (@smoke / @regression / @negative)

Todos los escenarios de Karate fueron etiquetados con al menos un tag. Esto permite:

- **@smoke**: ejecutar únicamente los escenarios críticos (TC-001, TC-011, TC-016, TC-029) en cada build del entorno de QA para verificar que el sistema responde antes de lanzar la suite completa.
- **@regression**: ejecutar la cobertura total al final de cada microsprint.
- **@negative**: aislar los casos de error para análisis específico de validaciones de entrada.

---

### 4.3 Aislamiento de datos de prueba

Cada escenario de Karate que requiere crear un empleado utiliza la función `uniqueName()` definida en `karate-config.js` para generar un nombre único con timestamp. Esto garantiza que:

- Ningún escenario depende de datos creados por otro escenario.
- La suite puede ejecutarse en paralelo sin colisiones de datos.
- Los datos de prueba son trazables: cada empleado creado por la suite tiene un nombre con prefijo que lo identifica como dato de test.

---

### 4.4 Validación de esquemas (Schema Matching)

Para los endpoints críticos de respuesta, Karate valida la estructura del JSON contra esquemas definidos en `schemas/nomina/empleado-response.json` y `nomina-response.json`. Esto detecta regresiones en la forma del contrato de API (campos renombrados, tipos de dato cambiados, campos removidos) sin necesidad de escribir assertions individuales para cada campo.

---

### 4.5 Cobertura de los criterios de aceptación BDD

Cada criterio de aceptación de las USER_STORIES tiene al menos un caso de prueba implementado en Karate y/o SerenityBDD. La trazabilidad es directa:

| Historia | Criterio de aceptación | Caso(s) que lo cubre |
|---|---|---|
| HU-01 | Registro exitoso | TC-001, TC-002, TC-003 |
| HU-01 | Registro fallido por falta de datos | TC-004, TC-005, TC-006 |
| HU-01 | Salario inválido | TC-007, TC-008 |
| HU-01 | Nombre con caracteres inválidos | TC-009, TC-010 |
| HU-02 | Corrección exitosa antes del cálculo | TC-035, TC-036 |
| HU-02 | Corrección inválida | TC-037, TC-038, TC-044 |
| HU-02 | Bloqueo por nómina calculada | TC-039 |
| HU-03 | Fórmula FULL_TIME correcta | TC-016, TC-019 |
| HU-03 | Fórmula PART_TIME correcta | TC-017, TC-027 |
| HU-03 | Fórmula PROFESSIONAL_SERVICES correcta | TC-018, TC-020 |
| HU-03 | Bloqueo sin empleado registrado | TC-021 |
| HU-04 | Resumen con desglose completo | TC-029, TC-033 |
| HU-04 | Datos del resumen coinciden con los persistidos | TC-030 |
| HU-04 | Confirmación habilita PDF | TC-031 (E2E) |
| HU-04 | Bloqueo de PDF sin confirmar | TC-032 |
| HU-05 | Generación exitosa del PDF | `pdfGenerate.feature` |
| HU-05 | Bloqueo sin confirmación | TC-032 |
| HU-05 | Notificación de descarga | TC-051 (E2E) |
| HU-05 | Rendimiento ≤ 3 segundos | TC-050 (k6) |

---

## 5. Lecciones aprendidas

| # | Lección                                                                                                    | Aplicación futura                                                              |
| - | ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| 1 | En arquitecturas de microservicios, la consistencia eventual entre servicios debe anticiparse en el diseño | Incluir sección de "comportamiento asincrónico esperado" en el contrato de API |
| 2 | El contrato de API debe quedar definido antes del desarrollo                                               | Incorporar Definition of Ready con validación conjunta DEV + QA                |
| 3 | Simplificar el modelo de dominio acelera el MVP, pero puede generar deuda técnica                          | Definir roadmap para refactorización futura hacia un modelo más desacoplado    |
| 4 | Docker es parte crítica del desarrollo, no solo del despliegue                                             | Estandarizar entornos desde el inicio del proyecto                             |
| 5 | Las pruebas de rendimiento requieren diseño previo del flujo de datos                                      | Incluir estrategias de setup automatizado en el diseño técnico                 |
