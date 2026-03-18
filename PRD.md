# Taller — Semana 6: Construcción de PRD y Backlog
Tema: Product Requirement Document (PRD), Refinamiento Ágil, Tasking, Estimación Técnica,
BDD (Gherkin)

## Visión:
Nuestra Calculadora de Nómina está pensada para los analistas de Recursos Humanos que hoy luchan con cálculos manuales lentos y propensos a errores en Excel. A diferencia de las herramientas genéricas, nuestra solución ofrece un cálculo exacto de salarios netos, deducciones de ley e incentivos de forma automatizada. Buscamos que el empleado tenga total claridad de su pago y que la empresa elimine el riesgo de multas legales, entregando en segundos lo que antes tomaba horas de revisión manual.

## Objetivos
* Automatizar el cálculo del salario neto de los empleados a partir de su salario bruto, eliminando la dependencia de procesos manuales en Excel.
* Permitir revisar y corregir la información del empleado antes de procesar el cálculo, para garantizar que los datos sean correctos desde el inicio.
* Facilitar el cálculo de nómina considerando distintos tipos de contrato laboral (tiempo completo, medio tiempo y freelance).
* Mostrar un desglose detallado del cálculo para validar los resultados antes de emitir el documento final.

## Alcance del MVP
### IN (MVP Scope)
- Registrar la información básica del empleado necesaria para el cálculo de nómina.
- Permitir al usuario corregir los datos ingresados antes de procesar el cálculo.
- Calcular el salario neto del empleado según su tipo de contrato.
- Mostrar el resultado del cálculo para que el usuario lo confirme antes de generar el documento.
- Generar un documento PDF descargable con el desglose completo del salario neto.


### OUT
- Integración con sistemas contables externos.
- Soporte para múltiples monedas o configuraciones por país.
- Notificaciones por correo electrónico al empleado.
- Historial completo de nóminas por empleado.
- Exportación a Excel o generación de reportes avanzados.
- Autenticación y gestión de roles de usuario.
- Cálculo de horas extra, ausencias o descuentos adicionales.

## Riesgos de Negocio:
- Si la ley cambia los porcentajes de impuestos o bonos y nadie actualiza el sistema, los recibos van a estar mal y la empresa puede tener problemas legales. Mitigación: Alguien de RRHH se encarga de estar al tanto de cambios y actualizar antes de correr la siguiente nómina.
- Al pasar de manual a automático, RRHH puede dejar de validar los resultados y no darse cuenta de un error a tiempo. Mitigación: Que el equipo haga revisiones periódicas comparando recibos contra cálculos manuales.
- Si al equipo de RRHH le parece complicado de usar, el sistema pasa a perder valor y el problema original no se resuelve. Mitigación: Incluir al equipo desde el inicio del desarrollo.
