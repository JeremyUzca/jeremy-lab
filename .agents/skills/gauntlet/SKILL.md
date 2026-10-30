---
name: gauntlet
description: "Construir, comprobar, auditar y corregir con evidencia. Usar en jeremy-lab para cambios funcionales no triviales, lógica de datos, modificaciones sensibles o cuando Jeremy solicite Gauntlet. Aplicar revisión proporcional al alcance y al riesgo."
---

# Gauntlet

## Principios

Respeta los `AGENTS.md` aplicables, la solicitud y los permisos del entorno.
Conserva la autonomía técnica ampliada: resuelve decisiones ordinarias, implementa
y corrige sin pedir aprobaciones intermedias innecesarias. Reconoce las
autorizaciones ya concedidas para la operación.

Usa pruebas y resultados observables como criterio de aceptación. El acuerdo
entre agentes no demuestra corrección. No reduzcas requisitos, ocultes fallos
ni debilites controles para conseguir un dictamen favorable.

## Responsabilidades

- **Agente principal:** define criterios, construye, prueba, coordina la revisión,
  corrige y comunica el resultado.
- **Auditor separado:** examina los requisitos originales, los archivos y los
  cambios reales; busca contraejemplos, regresiones y requisitos incumplidos.
  No se limita al resumen ni a las pruebas del constructor.

Para cambios relevantes o Gauntlet completo, utiliza un auditor separado cuando
exista delegación disponible. Solicita revisión sin edición de los archivos
compartidos; permite comprobaciones aisladas y autorizadas. Evita escritores
concurrentes sobre los mismos archivos y espera el resultado antes de cerrar.

Si no puedes delegar, realiza autorrevisión estructurada y declara
«sin auditor independiente». No inventes agentes, pruebas ni aprobaciones.
Para cambios de alto riesgo —permisos, datos confidenciales, migraciones
destructivas o transacciones reales— exige revisión independiente antes de
declarar verificado el cambio.

## Procedimiento

1. **Definir.** Inspecciona el estado existente. Identifica objetivo, alcance,
   restricciones, supuestos, riesgos y criterios observables de aceptación.
   Asocia cada criterio esencial con una comprobación. No presupongas
   herramientas ni comandos que el proyecto no tenga.

2. **Construir.** Implementa la solución dentro del alcance. Conserva el trabajo
   ajeno y justifica las dependencias o reorganizaciones necesarias. Si el
   encargo consiste solo en revisar, omite la implementación.

3. **Comprobar.** Ejecuta las verificaciones pertinentes sobre la versión
   candidata: comportamiento solicitado, casos límite, errores y regresiones.
   Registra procedimiento o comando, resultado observado y limitaciones.
   Distingue ejecución real, simulación y mocks.

4. **Auditar.** Entrega al auditor los requisitos originales, los criterios,
   los cambios y su evidencia. Solicita que examine los archivos e intente
   refutar el cumplimiento mediante casos relevantes. Una revisión sustantiva
   basta si no quedan hallazgos bloqueantes; no impongas una cuota de rondas.

5. **Corregir y revalidar.** Investiga los hallazgos y corrige los defectos.
   Cierra los falsos positivos con evidencia. Repite las comprobaciones
   afectadas y las regresiones pertinentes sobre la versión final.
   Solicita al auditor verificar el cierre de sus hallazgos cuando esté
   disponible. Los cambios posteriores invalidan la evidencia afectada.

## Evidencia y proporcionalidad

Para cada hallazgo registra: ubicación, gravedad, evidencia o reproducción,
impacto y condición de cierre. Distingue defectos demostrados de sospechas;
investiga estas últimas antes de presentarlas como hechos.

- **Crítico:** compromete seguridad o integridad.
- **Mayor:** incumple un requisito obligatorio o causa una regresión relevante.
- **Menor:** mejora no bloqueante.

Verifica según el tipo de trabajo:

- **Código:** comportamiento, errores y regresiones; tipos, lint o compilación
  cuando existan y sean pertinentes.
- **Interfaces:** resultado renderizado, recorridos esenciales, estados vacíos
  y de error, adaptación y accesibilidad básica.
- **Datos y modelos:** fuentes, fechas, unidades, faltantes, duplicados y cálculos;
  separación temporal y ausencia de información futura cuando corresponda.
- **Integraciones:** contratos y fallos previsibles; identifica expresamente
  lo simulado y lo comprobado contra un servicio real.

No declares inspección visual sin haber visto el resultado. No confundas una
compilación correcta o pruebas con mocks con cumplimiento funcional completo.
Para cambios mínimos sin efecto funcional basta una comprobación focalizada,
salvo solicitud expresa de Gauntlet completo.

## Límites del ciclo

Realiza como máximo cinco ciclos de corrección, respetando primero el presupuesto
o límite de la sesión. Cada ciclo debe cerrar un hallazgo o aportar evidencia
nueva. Tras dos ciclos sin progreso, cambia el enfoque una vez dentro del límite;
si persiste el bloqueo, conserva el avance y explica qué falta.

No repitas verificaciones que ya pasaron salvo que cambios, fallos o incertidumbres
pendientes lo justifiquen. Alcanzar el límite detiene el proceso: no autoriza
a aprobarlo.

## Dictamen y entrega

Emite uno de estos dictámenes:

- **VERIFICADO PARA EL ALCANCE SOLICITADO:** criterios y comprobaciones esenciales
  satisfechos, revisión exigida por el riesgo realizada y ningún hallazgo
  crítico o mayor abierto.
- **PARCIALMENTE VERIFICADO:** existe un resultado útil, pero faltan comprobaciones
  esenciales o la revisión independiente requerida. Identifica lo pendiente.
- **BLOQUEADO:** persisten defectos críticos o mayores, faltan permisos
  indispensables o una dependencia impide completar el objetivo.

Indica qué cambió, la evidencia de la versión final, el tipo de revisión
realizado, los hallazgos corregidos y pendientes, y las limitaciones.
Reserva «Gauntlet completo» para un resultado verificado que incluya
auditoría independiente real.

La verificación técnica no concede permisos de publicación, integración,
despliegue ni operaciones sensibles. Ejecuta efectos externos únicamente
cuando la autorización vigente los cubra; no la solicites de nuevo.
Si falta evidencia suficiente para una operación sensible, conserva el
entregable preparado y comunica el bloqueo.
