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
    - Regla de deducción por impuestos
        - tiempo completo = Se aplica 9.45% sobre el salario bruto
        - medio tiempo = Se aplica 9.45% sobre el salario bruto
        - servicios profesionales = Se aplica 8.00% sobre el salario bruto
    - Regla de bonificación
        - tiempo completo = Se aplica 8.33% sobre el salario bruto
        - medio tiempo = Se aplica 8.33% sobre el salario bruto
        - servicios profesionales = Se aplica 0% sobre el salario bruto
    - Regla de cálculo de salario neto = Fórmula Salario neto = Salario bruto − Deducción + Bonificación
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

## Riesgos Técnico
- La respuesta del sistema debe ser inmediata, caso contrario no habría ventaja sobre los cálculos manuales. Mitigación: garantizar que los cálculos y descarga de pdf tomen menos de 3 segundos.
- Al depender de herramientas externas el sistema podría romperse. Mitigación: probar que los documentos se construyan con la información completa. 
- El manejo inadecuado de decimales podría generar pagos irreales. Mitigación: definir el formato de los decimales.
- Los datos incorrectos harán que nuestros cálculos fallen. MItigación: verificación de los datos de entrada.
- La información de salida debe ser la misma para la pantalla como para el PDF, no pueden ser distintos. Mitigación: se debe calcular el salario una sola vez sin que haya cambios inesperados.


