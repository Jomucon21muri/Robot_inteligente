# Metodología de desarrollo de prototipos robóticos

## Metodología aplicada

**Modelo espiral iterativo con desarrollo ágil adaptado para robótica**

El desarrollo del presente proyecto se fundamenta en un modelo espiral iterativo que integra elementos del desarrollo ágil (Scrum y Kanban), específicamente adaptado para el contexto de prototipos robóticos. Esta aproximación metodológica híbrida ha sido seleccionada por su capacidad de ofrecer:

- Gestión continua de riesgos técnicos (característica heredada del modelo espiral)
- Iteraciones rápidas con entregas incrementales (principio fundamental de las metodologías ágiles)
- Validación temprana con componentes físicos (requisito específico del desarrollo en robótica)
- Flexibilidad para realizar ajustes estratégicos basados en hallazgos experimentales

La metodología se estructura en cinco fases principales —conceptualización, diseño, implementación, integración y pruebas, y evaluación— que se ejecutan de forma iterativa en ciclos de desarrollo de una a dos semanas.

## Introducción

La naturaleza multidisciplinaria del desarrollo de sistemas robóticos inteligentes demanda una metodología que equilibre el rigor de la ingeniería con la flexibilidad necesaria para la investigación aplicada. Este documento establece el marco metodológico para el diseño, desarrollo y validación de prototipos robóticos con integración de inteligencia artificial.

El enfoque propuesto combina lo mejor de diversos paradigmas: la gestión de riesgos del modelo espiral, la adaptabilidad de las metodologías ágiles, y las prácticas específicas de validación incremental que caracterizan al desarrollo de sistemas ciber-físicos. Esta síntesis metodológica responde a las particularidades del dominio, donde la teoría debe validarse constantemente con el comportamiento real del hardware.

## Modelo de desarrollo

### Modelo espiral iterativo

El modelo espiral, propuesto originalmente por Boehm (1988), se caracteriza por ciclos de desarrollo que incorporan análisis de riesgos en cada iteración. Para el contexto de prototipos robóticos, este modelo ha sido adaptado para incluir:

- Ciclos iterativos de corta duración (sprints de una a dos semanas)
- Evaluación continua de riesgos técnicos y de integración
- Validación incremental con componentes de hardware
- Refinamiento progresivo tanto de software como de elementos mecánicos

```
        Planificación
              ↓
    ┌─────────────────────┐
    │                     │
Evaluar ←          → Diseñar
Riesgos              Solución
    │                     │
    └─────────────────────┘
              ↓
    Implementar y Probar
              ↓
        [Iteración] ──→ Siguiente ciclo
```

La estructura cíclica permite detectar problemas de manera temprana y ajustar el rumbo del proyecto sin comprometer significativamente los recursos invertidos. Cada iteración completa produce un incremento funcional del prototipo que puede ser demostrado y evaluado.

### Principios metodológicos fundamentales

La metodología se sustenta en cinco principios rectores que guían todas las decisiones de desarrollo:

**Iteración rápida.** Los ciclos de desarrollo se mantienen deliberadamente cortos (una a dos semanas) para facilitar la retroalimentación frecuente y permitir ajustes tempranos en la dirección del proyecto.

**Validación temprana.** Dada la complejidad de los sistemas ciber-físicos, es fundamental probar con hardware real lo antes posible. Las simulaciones son útiles pero insuficientes; el comportamiento emergente del sistema completo solo puede observarse en condiciones reales.

**Evolución modular.** El desarrollo se estructura por subsistemas independientes que pueden evolucionar en paralelo. Esta modularidad reduce el acoplamiento y permite que múltiples aspectos del prototipo se desarrollen simultáneamente.

**Gestión proactiva de riesgos.** Los riesgos técnicos se identifican, documentan y mitigan de manera continua. Cada iteración incluye una evaluación explícita de los riesgos emergentes y del estado de los riesgos previamente identificados.

**Documentación paralela.** La documentación se genera durante el proceso de desarrollo, no como una actividad posterior. Esto asegura mayor precisión y evita la pérdida de conocimiento tácito.

## Fases del desarrollo

El proceso de desarrollo se articula en cinco fases claramente diferenciadas. Aunque se presentan de manera secuencial para facilitar su comprensión, en la práctica se ejecutan de forma iterativa, regresando a fases anteriores según sea necesario para refinar aspectos específicos del prototipo.

### Fase 1: Conceptualización y requisitos

La primera fase establece los cimientos conceptuales del proyecto. Su objetivo principal es definir con claridad qué se construirá y por qué. Esta fase responde a la pregunta fundamental de investigación y establece los límites del prototipo.

**Actividades principales:**

Durante esta fase se lleva a cabo la identificación de la necesidad o problema que el prototipo abordará. Se definen tanto los requisitos funcionales (qué debe hacer el sistema) como los no funcionales (restricciones de desempeño, seguridad, consumo energético, entre otros). Es crucial establecer criterios de éxito medibles que permitan evaluar objetivamente si el prototipo cumple su propósito. 

También se realiza una evaluación inicial de viabilidad técnica, considerando los recursos disponibles (materiales, tiempo, conocimiento) y las limitaciones conocidas. Finalmente, se define el alcance mínimo viable del prototipo (MVP, por sus siglas en inglés), identificando qué funcionalidades son esenciales para una primera versión funcional.

**Productos entregables:**

- Documento de requisitos del sistema
- Casos de uso principales con sus escenarios de operación
- Lista de restricciones técnicas y limitaciones conocidas
- Criterios de aceptación medibles

### Fase 2: Diseño del sistema

Esta fase traduce los requisitos abstractos en especificaciones técnicas concretas. El objetivo es diseñar la arquitectura completa del prototipo, tanto en sus aspectos físicos como computacionales.

**Actividades principales:**

Se diseña la arquitectura de hardware, seleccionando y especificando sensores, actuadores, controladores y estructuras mecánicas. En paralelo, se desarrolla la arquitectura de software, definiendo los módulos principales, sus interfaces, y los flujos de datos entre componentes.

La selección de componentes y tecnologías se basa en un análisis que equilibra capacidades técnicas, disponibilidad, costo y compatibilidad con el ecosistema de desarrollo. Para los algoritmos críticos del sistema (por ejemplo, localización, planificación de trayectorias, o reconocimiento de objetos), se diseñan las aproximaciones técnicas a emplear. import

Un elemento fundamental de esta fase es el análisis de riesgos técnicos, donde se identifican posibles problemas de implementación, integración o desempeño, estableciendo estrategias de mitigación para cada uno.

**Productos entregables:**

- Diagramas de arquitectura del sistema (vistas lógica, física y de despliegue)
- Especificaciones técnicas detalladas de componentes
- Diagramas de flujo de los algoritmos principales
- Lista de materiales (bill of materials, BOM)
- Matriz de riesgos con estrategias de mitigación

### Fase 3: Implementación incremental

La implementación se aborda de manera modular e incremental. En lugar de construir el sistema completo de una vez, se desarrollan subsistemas independientes que gradualmente se integran.

**Enfoque de desarrollo:**

El desarrollo se organiza por subsistemas que pueden evolucionar en paralelo. Los subsistemas típicos en un robot inteligente incluyen:

- **Percepción:** Adquisición y procesamiento de datos sensoriales
- **Cognición:** Algoritmos de toma de decisiones, planificación y aprendizaje
- **Actuación:** Control de motores, manipuladores y otros efectores
- **Integración:** Middleware de comunicación y coordinación entre subsistemas

**Estructura de los sprints de desarrollo:**

Cada sprint tiene una duración de una a dos semanas y busca producir un incremento funcional demostrable. La estructura semanal típica incluye:

- **Inicio de sprint:** Planificación detallada, asignación de tareas y definición de objetivos específicos
- **Desarrollo:** Implementación de funcionalidades y pruebas unitarias continuas
- **Integración:** Ensamblaje de componentes nuevos con el sistema existente
- **Validación:** Pruebas del subsistema completo
- **Cierre:** Retrospectiva del sprint y documentación de lecciones aprendidas

**Productos entregables por sprint:**

- Código fuente funcional y documentado
- Suite de pruebas unitarias y de integración
- Demostración del incremento funcional
- Documento de lecciones aprendidas

### Fase 4: Integración y pruebas

Esta fase se centra en la validación del sistema completo. Mientras que las pruebas unitarias se realizan continuamente durante la implementación, aquí se ejecutan pruebas de sistema que evalúan el comportamiento integrado del prototipo.

**Niveles de prueba:**

Las pruebas se organizan en una jerarquía que va desde componentes individuales hasta el sistema completo operando en su entorno objetivo:

1. **Pruebas unitarias:** Verificación de componentes individuales aislados
2. **Pruebas de integración:** Validación de interfaces entre subsistemas
3. **Pruebas de sistema:** Evaluación del robot completo en entorno controlado
4. **Pruebas de campo:** Operación en escenarios reales o simulados realistas
5. **Pruebas de aceptación:** Validación formal contra requisitos establecidos

**Progresión segura con hardware:**

Dada la naturaleza física de los sistemas robóticos, es fundamental seguir una progresión gradual en las pruebas con hardware:

1. Pruebas en banco de trabajo con componentes fijos y movimiento restringido
2. Movimientos individuales de cada actuador con límites de seguridad activos
3. Secuencias coordinadas de movimiento bajo supervisión continua
4. Operación autónoma en entorno controlado y delimitado
5. Validación en el entorno objetivo con supervisión reducida

**Productos entregables:**

- Plan de pruebas detallado con casos de prueba específicos
- Registro de ejecución de casos de prueba con resultados
- Reporte de defectos identificados y su resolución
- Métricas de desempeño del sistema

### Fase 5: Evaluación y refinamiento

La última fase de cada ciclo iterativo se dedica al análisis crítico de los resultados obtenidos y a la planificación de mejoras para la siguiente iteración.

**Actividades principales:**

Se realiza un análisis exhaustivo de las métricas de desempeño recolectadas durante las pruebas, comparándolas con los criterios de éxito establecidos en la fase de conceptualización. Se identifican tanto los aspectos que cumplieron las expectativas como aquellos que requieren mejora.

Basándose en este análisis, se toma una decisión go/no-go para continuar con una siguiente iteración. Si se decide continuar, se elabora una lista priorizada de mejoras y, si es necesario, se actualizan los requisitos del sistema para reflejar lo aprendido durante el ciclo.

**Productos entregables:**

- Reporte de evaluación con análisis de resultados
- Lista priorizada de mejoras para la siguiente iteración
- Plan de trabajo para el siguiente ciclo
- Documentación técnica actualizada

## Gestión de tareas y priorización

La gestión eficiente de tareas es fundamental para mantener el progreso del proyecto y asegurar que los recursos limitados se inviertan en las funcionalidades más importantes.

### Sistema de priorización MoSCoW

Para la priorización de requisitos y tareas se emplea el método MoSCoW, ampliamente utilizado en gestión de proyectos ágiles. Este método clasifica los elementos en cuatro categorías:

- **Must have (debe tener):** Requisitos críticos sin los cuales el prototipo no cumple su propósito fundamental. Estos elementos definen la funcionalidad mínima viable.

- **Should have (debería tener):** Elementos importantes que agregan valor significativo pero cuya ausencia no impide la operación básica del prototipo.

- **Could have (podría tener):** Mejoras deseables que se implementarán si el tiempo y los recursos lo permiten.

- **Won't have (no tendrá):** Elementos explícitamente fuera del alcance de la iteración actual, pero que podrían considerarse en el futuro.

### Gestión del backlog de desarrollo

El backlog es una lista priorizada y dinámica de todas las tareas, funcionalidades y mejoras pendientes. Su gestión adecuada es crucial para el flujo de trabajo. Los criterios para priorizar elementos en el backlog incluyen:

- **Impacto en funcionalidad crítica:** Tareas que afectan la capacidad del prototipo de cumplir sus requisitos fundamentales reciben mayor prioridad.

- **Dependencias técnicas:** Se priorizan tareas que desbloquean otras actividades.

- **Nivel de riesgo e incertidumbre:** Elementos con alto riesgo técnico se abordan temprano para validar su viabilidad.

- **Valor para validación del concepto:** Se favorecen tareas que permiten demostrar y validar aspectos críticos de la hipótesis de investigación.

## Gestión de riesgos

La gestión proactiva de riesgos es uno de los pilares de la metodología espiral. En el contexto de robótica, donde múltiples dominios técnicos interactúan, la identificación temprana y mitigación de riesgos puede significar la diferencia entre el éxito y el fracaso del proyecto.

### Identificación de riesgos

Los riesgos en proyectos de robótica pueden categorizarse en cinco dimensiones principales:

**Riesgos técnicos:** Incluyen la viabilidad de algoritmos, limitaciones de procesamiento computacional, restricciones de los sensores, y capacidades de los actuadores. Estos riesgos a menudo se descubren durante la implementación cuando la teoría se confronta con la realidad física.

**Riesgos de integración:** La integración de componentes de diferentes fabricantes o paradigmas de programación puede presentar incompatibilidades imprevistas. Los problemas de sincronización, formatos de datos inconsistentes, y latencias inesperadas son ejemplos comunes.

**Riesgos de seguridad:** Los sistemas robóticos pueden causar daño físico si fallan. Esto incluye desde movimientos inesperados hasta fallas en mecanismos de parada de emergencia.

**Riesgos de recursos:** La disponibilidad limitada de componentes, restricciones presupuestarias, o falta de tiempo pueden comprometer el alcance del proyecto.

**Riesgos de conocimiento:** Tecnologías nuevas o poco familiares pueden requerir más tiempo de aprendizaje del estimado inicialmente.

### Análisis y mitigación de riesgos

Cada riesgo identificado se evalúa según dos dimensiones: probabilidad de ocurrencia e impacto potencial. Esta evaluación permite clasificar los riesgos y asignar estrategias de respuesta apropiadas:

| Probabilidad / Impacto | Bajo | Medio | Alto |
|------------------------|------|-------|------|
| Alta | Monitorear | Mitigar | Mitigar con urgencia |
| Media | Aceptar | Monitorear | Mitigar |
| Baja | Aceptar | Aceptar | Monitorear |

Las estrategias de respuesta a riesgos incluyen:

**Evitar:** Modificar el diseño del sistema para eliminar completamente el riesgo. Por ejemplo, cambiar un sensor problemático por uno de tecnología diferente.

**Transferir:** Utilizar soluciones probadas y maduras, como bibliotecas de software bien establecidas o componentes comerciales certificados.

**Mitigar:** Reducir la probabilidad o el impacto del riesgo mediante prototipos rápidos, pruebas tempranas, o implementación de redundancias.

**Aceptar:** Para riesgos de bajo impacto o muy baja probabilidad, se documenta su existencia pero no se toman acciones preventivas.

## Métricas y evaluación

La medición objetiva del progreso y la calidad es fundamental para el proceso iterativo. Las métricas proporcionan retroalimentación cuantitativa que informa la toma de decisiones.

### Métricas de proceso

Las métricas de proceso evalúan la eficiencia y efectividad del desarrollo mismo:

**Velocidad de desarrollo:** Se mide a través del número de tareas completadas por sprint, la tasa de reducción del backlog (burndown), y el tiempo de ciclo por funcionalidad. Estas métricas ayudan a estimar cuánto trabajo puede completarse en iteraciones futuras.

**Calidad del código:** Incluye la cobertura de pruebas automatizadas (objetivo mínimo de 70%), la densidad de defectos encontrados por cada mil líneas de código, y la acumulación de deuda técnica (código que funciona pero requiere refactorización).

### Métricas de producto

Las métricas de producto evalúan las características del prototipo resultante:

**Métricas funcionales:** Porcentaje de requisitos implementados exitosamente, tasa de éxito en la ejecución de casos de uso, y tiempo de respuesta del sistema a diferentes estímulos.

**Métricas no funcionales:** Fiabilidad medida como tiempo medio entre fallos (MTBF), disponibilidad del sistema (uptime), eficiencia en términos de consumo energético y uso de recursos computacionales, e incidentes de seguridad.

### Evaluación de iteraciones

Al final de cada sprint se realiza una evaluación estructurada que responde las siguientes preguntas:

- ¿Se cumplieron los objetivos planificados para el sprint?
- ¿Las demostraciones del incremento funcional son exitosas?
- ¿Se mantienen o mejoran las métricas de calidad?
- ¿Qué lecciones se aprendieron durante la iteración?
- ¿Qué ajustes metodológicos o técnicos son necesarios?

Las respuestas a estas preguntas informan la planificación del siguiente ciclo y contribuyen al proceso de mejora continua.

## Estrategia de documentación

La documentación es un componente esencial del proceso de investigación y desarrollo. Una documentación adecuada facilita la reproducibilidad, permite la transferencia de conocimiento, y constituye parte fundamental de los entregables del proyecto.

### Niveles de documentación

La estrategia de documentación se estructura en cuatro niveles complementarios:

**Documentación de código:** Incluye comentarios en línea y documentación estructurada (docstrings) que explican la lógica de implementación, parámetros de funciones, y valores de retorno. Esta documentación debe ser suficiente para que otro desarrollador pueda entender y modificar el código.

**Documentación técnica:** Comprende la arquitectura del sistema, especificaciones de interfaces entre componentes, documentación de APIs, y descripciones de algoritmos implementados. Este nivel de documentación es esencial para el mantenimiento y evolución del sistema.

**Documentación de usuario:** Incluye guías de operación, tutoriales de uso, y documentación de troubleshooting. Aunque el prototipo sea para investigación, esta documentación facilita las demostraciones y ayuda a usuarios futuros.

**Documentación de proyecto:** Engloba documentos de requisitos, decisiones de diseño con su justificación (Architecture Decision Records), reportes de pruebas, y lecciones aprendidas. Esta documentación captura el proceso y la evolución del proyecto.

### Principios de documentación efectiva

**Actualización continua:** La documentación se genera y actualiza durante el desarrollo, no como actividad posterior. Esto asegura mayor precisión y evita la pérdida de información contextual.

**Claridad y concisión:** Los documentos deben ser claros y directos, escritos pensando en quienes continuarán el proyecto o lo evaluarán.

**Trazabilidad:** Las decisiones de diseño deben vincularse con los requisitos que las motivaron, y los cambios deben documentarse con su justificación.

**Versionado:** La documentación debe sincronizarse con las versiones del código, permitiendo recuperar la documentación correspondiente a cualquier versión anterior del prototipo.

## Mejora continua

El concepto de mejora continua, inspirado en la filosofía Kaizen de la manufactura, se aplica tanto al prototipo como al proceso de desarrollo mismo.

### Retrospectivas

Al finalizar cada sprint se realiza una retrospectiva estructurada donde el equipo (o el investigador individual) reflexiona sobre el proceso. Un formato efectivo es el método Start-Stop-Continue:

**Start (comenzar a hacer):** Nuevas prácticas que se identifica podrían mejorar el proceso.

**Stop (dejar de hacer):** Prácticas actuales que están demostrando ser contraproducentes o ineficientes.

**Continue (continuar haciendo):** Prácticas que están funcionando bien y deben mantenerse.

Las conclusiones de cada retrospectiva se documentan y se traducen en acciones concretas para la siguiente iteración.

### Aprendizaje incremental

El desarrollo de un prototipo robótico implica necesariamente aprender sobre tecnologías, herramientas y dominios específicos. Se recomienda seguir la regla 80/20: dedicar aproximadamente el 80% del tiempo a implementación y el 20% a aprendizaje e investigación.

Cuando se encuentra un problema técnico, se sugiere la siguiente jerarquía de fuentes de información:

1. Documentación oficial de las herramientas y bibliotecas utilizadas
2. Comunidades especializadas y foros técnicos
3. Literatura académica para problemas de investigación
4. Tutoriales y recursos educativos
5. Consulta directa con expertos en la comunidad

Es recomendable mantener un registro de aprendizajes (TIL - Today I Learned) donde se documentan problemas encontrados, soluciones aplicadas, y conocimiento adquirido. Este registro se convierte en una base de conocimiento personal que facilita resolver problemas similares en el futuro.

### Optimización del proceso

La automatización de tareas repetitivas libera tiempo para actividades de mayor valor agregado. Se recomienda identificar tareas que se realizan frecuentemente y crear scripts o configuraciones que las simplifiquen. Ejemplos incluyen configuración del entorno de desarrollo, ejecución de baterías de pruebas, o generación de reportes.

## Cadencia de actividades

La estructura temporal del proyecto proporciona ritmo y puntos de sincronización. La cadencia propuesta opera en cuatro escalas temporales:

### Actividades diarias

- Registro de cambios en el sistema de control de versiones (commits)
- Documentación breve del progreso y obstáculos encontrados
- Revisión de objetivos del día siguiente

### Actividades semanales

- Retrospectiva del sprint anterior
- Planificación detallada del siguiente sprint
- Actualización de documentación técnica
- Revisión del estado de riesgos

### Actividades mensuales

- Revisión de cumplimiento de objetivos de la fase actual
- Ajuste del cronograma general si es necesario
- Evaluación cuantitativa de métricas acumuladas
- Comunicación de progreso a supervisores o stakeholders

### Actividades por fase

- Revisión exhaustiva de la fase completada
- Documentación completa de entregables de la fase
- Demostración formal de funcionalidades implementadas
- Decisión go/no-go para avanzar a la siguiente fase

## Definición de "terminado"

Para mantener estándares de calidad consistentes, es fundamental establecer criterios claros de cuándo una tarea está verdaderamente completa. Una tarea se considera terminada cuando cumple todos los siguientes criterios:

- El código está escrito, implementado y funciona según lo especificado
- Existen pruebas automatizadas que verifican su funcionamiento y estas pruebas están pasando
- El código y las funcionalidades están documentados apropiadamente
- Si aplica, el código ha sido revisado (code review)
- El nuevo componente está integrado con el sistema principal
- Si la funcionalidad involucra hardware, ha sido probada en condiciones reales
- Las pruebas anteriores del sistema siguen pasando (no se introdujeron regresiones)

Este criterio compartido evita acumular trabajo "casi terminado" y asegura que cada incremento es realmente utilizable.

## Consideraciones éticas y de seguridad

El desarrollo de sistemas robóticos autónomos plantea consideraciones éticas y de seguridad que deben abordarse desde el diseño metodológico.

### Seguridad física

Los prototipos robóticos pueden causar lesiones si no se manejan adecuadamente. Es imperativo implementar múltiples niveles de seguridad:

- Mecanismos de parada de emergencia siempre accesibles
- Límites de software y hardware para movimientos y fuerzas máximas
- Zona de operación claramente definida y señalizada
- Supervisión humana durante todas las pruebas con hardware
- Protocolos de seguridad documentados y ensayados

### Seguridad de datos

Si el prototipo recopila datos, especialmente en espacios públicos o que involucren personas, deben considerarse aspectos de privacidad y protección de datos. Los datos sensibles deben anonimizarse, y debe existir claridad sobre qué información se recopila y cómo se utiliza.

### Consideraciones éticas

El diseño del prototipo debe considerar las implicaciones éticas de su operación. Esto incluye reflexionar sobre el propósito del sistema, sus posibles usos indebidos, y el impacto que podría tener en individuos o grupos. Estas reflexiones deben documentarse como parte del proyecto.

---

**Nota final:** Esta metodología constituye un marco flexible que debe adaptarse según las necesidades específicas del proyecto y las lecciones aprendidas durante su ejecución. La rigidez metodológica puede ser tan perjudicial como la falta de método; el balance apropiado se encuentra mediante la reflexión continua sobre qué aspectos de la metodología están aportando valor y cuáles requieren ajustes.

**Última actualización:** Abril de 2026
