# Plan de Yachay

## Problema que resolvemos
La demanda se concentra cerca de los exámenes: la capacidad queda libre durante buena parte del ciclo y se agota en los picos. La coordinación manual impide aprovechar esa capacidad y deja a los tutores con trabajo impredecible. [1-evidencia/2-horas-de-tutores-por-semana.csv](../1-evidencia/2-horas-de-tutores-por-semana.csv) [1-evidencia/4-tutores-que-se-fueron.csv](../1-evidencia/4-tutores-que-se-fueron.csv)

No incluimos en esta versión evaluación de calidad, reubicación de sesiones ni gestión de cancelaciones: si una sesión se cancela, se cancela.

## Propuesta
Yachay deja de vender solo tutorías aisladas y ofrece un plan de estudio. El alumno elige curso, modalidad, fechas y horarios para sus sesiones antes del examen. Puede reservar una sesión individual o sumarse a un grupo.

El objetivo es que una parte de la demanda se reserve antes y que las horas disponibles de los tutores se asignen sin intervención de los socios.

## Planes que se mostrarán en la demo

La demo ofrece dos recorridos de estudio, no una sesión genérica:

- **Plan Enfoque:** dos sesiones antes del examen.
- **Plan Preparación:** tres sesiones antes del examen.

La cantidad de sesiones se mantiene dentro del rango observado en la muestra de alumnos, donde se registran entre una y tres sesiones. [1-evidencia/3-alumnos.csv](../1-evidencia/3-alumnos.csv)

Cada plan puede ser individual o grupal. Al cambiar curso, plan o modalidad, la interfaz recalcula fechas disponibles, horarios, tutores disponibles, precio regular, descuento y total. El alumno debe elegir horarios distintos hasta completar las sesiones de su plan.

Las fechas de examen de la demo se toman de la muestra de pedidos de octubre. La disponibilidad por hora y los nombres de tutores son datos ilustrativos de la demo porque la evidencia no contiene disponibilidad horaria individual. [1-evidencia/1-pedidos.csv](../1-evidencia/1-pedidos.csv)

## Alumno

1. Elige curso, modalidad individual o grupal, fecha y rango horario.
2. Ve cuántos tutores comprometidos están disponibles en cada horario; no ve sus nombres ni datos personales.
3. Completa todos los horarios requeridos por el plan; no puede elegir dos veces la misma sesión.
4. Ve un resumen con sesiones, precios, descuentos aplicables y total antes del pago.
5. En modalidad individual, confirma el plan y paga antes de que la reserva quede confirmada, como ocurre hoy. [CLAUDE.md](../CLAUDE.md)
6. En modalidad grupal, ve un panel filtrado por curso con grupos en formación, sesiones del plan y cupos. Puede unirse a uno o proponer otro turno si ningún grupo le sirve.
7. Un grupo se confirma al completar al menos dos alumnos y admite hasta cuatro, que es el formato actual. [CLAUDE.md](../CLAUDE.md)

## Tutor

1. Marca todas sus horas libres en un mapa semanal de calor.
2. Cada hora marcada es un compromiso de disponibilidad: solo puede recibir asignaciones dentro de esas horas.
3. El mapa muestra su disponibilidad y, cuando exista historial suficiente, la demanda observada por horario. No se inventará demanda por hora: la evidencia actual solo contiene demanda semanal y por fecha de pedido. [1-evidencia/1-pedidos.csv](../1-evidencia/1-pedidos.csv) [1-evidencia/2-horas-de-tutores-por-semana.csv](../1-evidencia/2-horas-de-tutores-por-semana.csv)
4. Recibe una notificación cuando el sistema le asigna una sesión; no hay competencia por aceptar primero.

## Asignación automática

El sistema considera únicamente tutores que cumplan curso y disponibilidad comprometida. Entre ellos asigna al que tenga menor carga de sesiones ya asignadas en el periodo activo; si hay empate, alterna de forma equitativa. Así se reemplaza la carrera por responder y se reparte la demanda existente.

La asignación equitativa no garantiza ingresos si no hay pedidos. Para crear demanda fuera de los picos, el plan destaca horarios con baja ocupación y ofrece el beneficio **Plan Adelántate**.

### Decisiones comerciales para el pitch

Estas son decisiones de producto para la demostración; no son cifras demostradas por la evidencia disponible.

- El beneficio se activa cuando el alumno reserva con al menos siete días antes de su examen y elige un horario de baja ocupación.
- La sesión individual con el beneficio cuesta S/ 35; el precio actual sin beneficio es S/ 40. [CLAUDE.md](../CLAUDE.md)
- La sesión grupal con el beneficio cuesta S/ 25 por alumno; el precio actual sin beneficio es S/ 28 por alumno. [CLAUDE.md](../CLAUDE.md)
- El descuento se aplica por sesión elegible, no al plan completo: un plan puede combinar sesiones con precio regular y sesiones con beneficio.
- El beneficio se muestra antes del pago y no se acumula con otros descuentos.
- Para el pitch, un horario de baja ocupación es el que tiene disponibilidad comprometida y no tiene reservas suficientes para considerarse lleno. En producción, esta condición debe calcularse con reservas reales por horario.

## Pago

Se conserva el pago por billetera digital antes de la sesión. [CLAUDE.md](../CLAUDE.md)

La interfaz muestra el pago como el último paso de confirmación. La elección e integración del proveedor de billetera digital se decidirán antes de operar reservas reales.

## Alcance de la primera versión

- Alumno: elegir curso, plan y modalidad; completar varias sesiones con horarios distintos y confirmar el total.
- Alumno: explorar grupos filtrados por curso, unirse a ellos o proponer otro turno.
- Tutor: marcar y editar todas sus horas comprometidas en el mapa semanal.
- Sistema: mostrar disponibilidad agregada y asignar un tutor de manera equitativa.
- Socios: ver reservas, grupos, tutor asignado y horas aún sin asignar.

## Criterios de aceptación

- Un alumno no puede confirmar un horario sin tutor disponible.
- Un alumno no puede pagar hasta completar todas las sesiones de su plan.
- Cambiar de curso, plan o modalidad cambia los horarios y recalcula el total.
- Un tutor no recibe una sesión fuera de una hora que marcó como disponible.
- Un tutor no puede obtener una sesión por responder antes que otro.
- Un grupo en formación puede ser visible, recibir alumnos y confirmar su tutor al tener entre dos y cuatro integrantes.
- Las cifras y descuentos no se muestran como decididos mientras no tengan evidencia o una decisión comercial explícita.
- El beneficio Plan Adelántate se muestra únicamente en horarios de baja ocupación elegibles.
