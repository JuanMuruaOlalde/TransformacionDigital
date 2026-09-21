# Construir sobre datos sólidos

## Introducción

Los usos de datos pueden ser muy variados:
- *Gestión*: para manejar las acciones operativas habituales.
- *Informes y Listados*: para saber qué está ocurriendo o qué ha ocurrido.
- *Automatización*: para desencadenar ciertas acciones operativas ante determinadas situaciones específicas.
- *Analítica*: para identificar relaciones y entender porqués.
- *IA*: para asistirnos en nuestro trabajo, en diversos ámbitos y alcances.
- etc.

Atendiendo al calado/impacto de posibles errores u omisiones, se pueden diferenciar varias tipologías en el consumo de datos:
- *Operativo*: para la gestión del trabajo habitual.
- *Experimental*: para estudiar situaciones hipotéticas y explorar nuevas formas de hacer las cosas.
- *Exploratorio*: para estudiar situaciones reales y pensar cómo abordarlas.
- *Certificado*: para automatización, análisis y toma de decisiones.

En general, los datos han de ser: accesibles, representativos, actualizados, semánticamente claros, trazables, suficientemente estables y adecuados para el uso previsto.

Como regla general, siempre es necesario preguntarse: **¿este dato, con este origen y estas transformaciones, es apto para este uso y este nivel de riesgo?**.

Tener en cuenta que el riesgo crece a medida que el dato:
- se aleja del contexto original para el que ha sido recogido
- se usa para decisiones/operaciones de mayor calado/impacto

Por otro lado, también se pueden aplicar tipologias a la toma de decisiones:
- Decisiones *autónomas*: dentro de estandares definidos y con bajo o nulo impacto fuera de su ámbito de decisión.
- Decisiones *gobernadas*: cuando se ven afectados dominios compartidos, seguridad corporativa, datos críticos, múltiples consumidores recurrentes,...
- Decisiones *escaladas*: cuando tienen impacto estratégico, riesgo alto, costes elevados, conflictos entre áreas,...

Dos son los peligros a evitar en la toma de decisiones:
- Sobregobernanza: pedir aprobación gobernada o escalada para todo, ralentizando la ejecución y generando rechazo.
- Infragobernanza: tomar aisladamente, dentro de un proyecto o ámbito concreto, decisiones que deberian ser gobernadas o escaladas; sin tener en cuenta su impacto fuera de dicho ámbito.

## Una operatoria fiable

En general, el procesamiento de datos se ha de llevar a cabo en  sistemas automatizados donde:

- Los datos de entrada tienen calidad suficiente. Y han sido evaluados con criterios estadísticos para evitar sesgos indeseados o pérdida de detalles relevantes.

- Los cambios en la programación interna del sistema están auditados, documentados y versionados.

- La operación del sistema está monitorizada (detectar anomalias) y es trazable (llegar a la causa de las anomalias).

- Los resultados llegan a sus destinatarios a tiempo para actuar. Y esos destinatarios tienen conocimiento y potestad suficientes para hacerlo.

- Los resultados llegan acompañados por información de contexto tal como: grado de confianza (si han sido validados o son automáticos), grado de frescura (última fecha de actualización), grado de validez (si tienen alguna degradación parcial o no), etc.

- Los resultados se integran en el flujo normal de trabajo. Sin requerir consultarlos expresamente en otras herramientas aparte. 

- Los resultados tienen unos límites de uso conocidos por todos.

Un sistema robusto no asume funcionamiento perfecto. Sino que define degradación segura en caso de fallo.



### Criterios y acuerdos

Antes de utilizar una determinada fuente de datos en un sistema se deben de tener en cuenta algunos **criterios**: 

- Definir el uso previsto y evaluar el impacto de posibles errores.

- Identificar personas propietarias ("owners" o "stewards") responsables de cada fuente.

- Medir dimensiones críticas de calidad de cada fuente.
- Definir umbrales mínimos aceptables.

- Revisar captación y transformaciones a aplicar.
- Diseñar gestión de errores y excepciones.
- Diseñar trazabilidad.
- Diseñar la latencia adecuada.

- Reducir los acoplamientos entre sistemas. Cuantas menos dependencias haya, menos puntos de posible rotura al realizar modificaciones.

- Evaluar confidencialidad y controles de acceso.

- Estimar costes de integración y de operación, según el volumen de uso previsto.
- Estimar costes de escalado si ese uso aumentara.


Antes de integrar una determinada fuente en un sistema, se ha de elaborar un **contrato de datos** para esa integración. Indicando con claridad:

- Persona responsable ("owner" o "steward"), encargada de velar por el cumplimento y adecuación del contrato.

- Persona custodia ("custodian"), encargada de velar por la correcta ejecución técnica del contrato.

- Esquemas técnicos, con nombres y tipos de cada dato.

- Definiciones y significados, clarificando el concepto real que representa cada dato.

- Usos previstos, clarificando en qué ámbitos se puede aplicar esta fuente de datos.

- Frecuencias de actualización.

- Tratamiento de errores, cómo proceder en caso de problemas.

- Tratamiento de modificaciones, cómo proceder cuando haya solicitudes de cambio.

- Compatibilidad de versiones, cómo proceder cuando se vaya a romper esa compatibilidad.

- etc.

En un modelo federado de datos, conviviendo sistemas centrales con soluciones locales. Suele ser necesario un **catálogo corporativo** mínimo de datos y categorias maestros, compartido por todos.


### Evitar riesgos

Integraciones sin contrato de datos ni validaciones son frágiles. El contrato de datos es imprescindible. Y los "pipelines" de procesamiento/consumo han de incorporar **mecanismos automáticos para validar esquemas y detectar problemas**.

Toda **modificación** en los procesos de tratamiento y consumo de datos ha de quedar **documentada y versionada**. Si no, puede llevar confundir esas modificaciones técnicas (distintos datos) con cambios de realidad (distintos comportamientos).

Todo informe o comunicación críticos han de incluir **información contextual acerca de la calidad** (completitud, frescura, excepciones,...) de los datos y procesos que los han producido. Sobre todo si el informe o comunicación es recurrente y habitualmente suele ir bien. La persona que los recibe ha de poder identificar cuando algo haya ido mal en su elaboración.

Sistemas con mucha arbitrariedad y poca trazabilidad,

- Pueden resultar útiles para gestión operativa manual (donde el conocimiento de las personas compensa las deficiencias del sistema) o, como mucho, para informes mensuales/anuales (donde se tiene tiempo para revisar y corregir lo que sea necesario durante la elaboración del informe).

- Pero, son inviables para avanzar hacia ámbitos analíticos más complejos o automatismos. Antes de plantearse ese otro tipo de usos, es imprescindible resolver previamente los problemas de calidad.

>Por ejemplo, las fuentes de datos "tipo papel" (hojas de cálculo y procesos manuales),
>
>- Solo son útiles en la operación local del día a día.
>
>- No pueden ser fuente para informes o analítica. Mucho menos para automatización o IA.
>
>Antes de plantearse cualquier uso fuera de la operatoria local, han de resolverse los problemas de calidad que pudieran tener y migrarse a repositorios gobernados (estructurados).


La analítica y los automatismos (al combinar fuentes, transformar variables, establecer relaciones,...) amplifican problemas de calidad preexistentes. Esto es especialmente problemático si, encima, son asistidos por IA.

### Algunas consideraciones prácticas

Las responsabilidades de cada cual no pueden delegarse en proveedores externos ni terceras personas; ni, mucho menos, en sistemas o herramientas. La persona responsable de algo puede apoyarse en otras para ejercer esa responsabilidad; pero no puede delegarla completamente.

Eso no quita para que los proveedores externos también deban explicar:
- dependencias tecnológicas
- fuentes de datos
- integraciones
- transformaciones
- gestión de privacidad
- monitorización y trazabilidad
- costes
- mantenibilidad
- escalabilidad
- reversibilidad
- límites de uso

Las soluciones que nos entreguen han de poder ser operadas, auditadas e integradas de forma sostenible en nuestros sistemas. Además, una gobernanza responsable de proveedores debe incluir también la transferencia de conocimiento.

## Calidad

La calidad del dato se define como el grado en que un conjunto de datos resulta adecuado para un uso concreto; bajo unas condiciones técnicas, operativas y de riesgo determinadas.

Es importante que cada conjunto de datos responda a criterios establecidos de:

- **Completitud**: Las ausencias de datos (siempre hay ausencias) no comprometen la decisión o el proceso que se quiere soportar.

- **Exactitud y Representatividad**: Los datos representan correctamente la realidad que pretenden describir. (Y esta realidad está clara para todas las personas que los van a usar.)

- **Consistencia**: No hay contradicciones entre fuentes o a lo largo del tiempo.

- **Unicidad**: Cada entidad relevante está representada una sola vez y sus identificadores permiten identificarla sin ambigüedad en todos los contextos donde se presente.

- **Actualidad**: El dato llega cuando todavia sirve, a tiempo para el uso previsto.

- **Validez**: Se cumplen los formatos, rangos, dominios,... esperados.

- **Trazabilidad**: Se puede conocer el origen, las transformaciones y las transmisiones realizadas para una determinada información que ha sido utilizada en un momento dado.


Para poder responder a esos criterios, es necesario disponer de mecanismos tales como:

- *Indicadores certificados*. La certificación garantiza que el indicador se calcula y se utiliza de igual/equivalente manera en todas partes.

  > Para estar certificado, un indicador debe contar con:
  >  - definición acordada
  >  - fuente identificada
  >  - forma de cálculo documentada
  >  - persona responsable
  >  - frecuencia de actualización definida
  >  - monitorización de calidad
  >  - restricciones de interpretación (usos válidos definidos)
  >
  > Deben evitarse nombres iguales para indicadores con formas de cálculo diferentes según contexto donde se aplican o se usan. A efectos prácticos son indicadores diferentes y deben de poder identificarse claramente como tales.
  >
  > Deben de evitarse que distintos usos publiquen un mismo indicador con valores divergentes sin explicación.

- *Diccionarios/Catálogos de datos*. En datos con múltiples consumidores recurrentes, todos ellos han de tener claro qué representa cada dato, cómo se calcula y para qué usos está pensado.

- *Documentación y versionado* de las reglas de recopilación y transformación. Para saber qué datos históricos se han obtenido cómo según cuándo han sido recopilados.

- *Controles* para asegurar exactitud (representatividad) y consistencia (ausencia de contradiciones) en los datos que se manejan.

- *Gobierno de datos maestros* para asegurar unicidad, tanto de información básica (claves) como de clasificación (categorias).


Es muy importante tener designada una **persona propietaria** de cada conjunto/producto de datos. Esta persona proprietaria ("owner" or "steward") es la responsable de asegurar que esos datos:
- Tienen un significado definido.
  > nota: Las decisiones semánticas deben de tomarse teniendo en cuenta todas las implicaciones, a nivel de toda la organización, allá donde pudiera tener relevancia. Y no pensando solo en el proyecto o contexto en el que nace el uso que se está evaluando.
- Tienen unas reglas de uso claras.
- Tienen un nivel de calidad adecuado a los usos acordados.

La persona propietaria es también la encargada de priorizar correcciones cuando aparecen problemas, de impulsar cambios en el proceso y de aceptar formalmente limitaciones de uso. Estas decisiones han de quedar documentadas.

Asimismo, es importante tener designada una **persona custodia** de cada conjunto/producto de datos. Esta persona custodia ("custodian") es la responsable de asegurar cómo esos datos:
- Se captan.
- Se transforman.
- Se almacenan.
- Se integran.
- Se protegen.
- Son útiles allá donde se consumen.

La persona custodia es también la encargada de alertar y proteger a la organización frente a "atajos no sostenibles" en el uso de datos.



## Seguridad

Como regla general, para cualquier manejo de datos sensibles, el criterio técnico básico es: "usar el mínimo dato suficiente, con el menor acceso necesario y durante el menor tiempo razonable".

Además, este manejo ha de estar regulado y contar con los adecuados controles.

La regulación y control de datos sensibles puede incluir operaciones tales como: minimización, anonimización, seudonimización, autentificación y autorización de acceso, registros de acceso, monitorización de anomalias en el acceso, etc.

Las decisiones de seguridad se han de incorporar desde el inicio de la solución, desde su concepción/diseño, No después de que se haya comenzado a construir. Y, mucho menos, después de que esté construida.

Desde el principio, se deben de establecer umbrales claros acerca de:

- Qué tipos de datos requieren control.

- Qué finalidad justifica su uso.

- Quién va a poder acceder.

- Qué controles son obligatorios.

- Qué usos están prohibidos.

- Qué registros ("logs") han de conservarse.

- Cómo van a destruirse (tanto los datos como los registros) cuando ya no sean necesarios.

- Quién puede autorizar excepciones. Cómo se van a documentar y registrar esas excepciones.


Además, las personas consumidoras o usuarias de datos sensibles tienen también responsabilidades en su uso. Han de comprometerse a:

- Preocuparse por, y pedir ser informadas de, el alcance y las restricciones de uso. 

- Respetar las restricciones.

- Interpretar correctamente el alcance.

- No reutilizar datos ni resultados fuera del contexto autorizado.

### Algunas consideraciones prácticas

Un control de accesos debe incluir:
- revisión periódica
- segregación por roles
- registro y trazabilidad de accesos
- gestión de bajas en autorizaciones
- separación entre procesos de lectura y procesos de escritura
- control de copias y exportaciones

Los controles se han de aplicar en cualquier proceso de acceso, búsqueda, transformación almacenamiento o transmisión. Nunca se deben copiar o mover datos sensibles a o a través de sistemas que tengan menos controles que el sistema origen del que proceden.

Los controles se han de mantener también para cualquier tipo de copia de seguridad o de almacenamiento histórico que se haga. 

Y también se han de mantener para cualquier tipo de copia de pruebas o de desarrollo que se haga. (De todas formas, para desarrollo o pruebas en sistemas sensibles, mejor utilizar datos sintéticos ficticios en lugar de los datos reales.)

El cifrado reduce riesgos en tránsito o en reposo. Pero no elimina totalmente el riesgo ni la consiguiente necesidad de controles en el manejo de esos datos cifrados.

La anonimización o seudonimización o agregación reducen riesgos en el uso. Pero no eliminan totalmente el riesgo. Se debe prestar especial atención a que no sea razonablemente posible reidentificar los datos originales con técnicas tales como la correlación con otras fuentes adicionales.

Obviamente, todo tipo de secretos (credenciales, tokens API, claves,...) no deben de aparecer nunca en códigos fuente, en programas ejecutables, en scripts, en notebooks,... Utilizar siempre las técnicas adecuadas de inyección de dichos secretos en tiempo de ejecución.

Ni que decir tiene que los secretos no deben de aparecer nunca en documentación publica ni en logs, ni en mensajes de error o avisos similares.


## Arquitectura

La primera cosa a tener clara es que los **repositorios de datos operativos** (para gestión) tienen distintas caracteristicas y requisitos que los **repositorios de datos analíticos** (para análisis/decisión).

Los datos analíticos se suelen elaborar desde los datos operativos, más otras fuentes complementarias. No suele ser posible usar directamente datos operativos para usos analíticos.

Una arquitectura típica de un sistema de datos consta de varias capas:

- `Sistemas de origen`: los entornos donde se capta y se consume la información primaria (usualmente datos operativos).

- `Ingesta e integración`: los diferentes procesos para mover y mapear datos de un sitio a otro, con los consiguientes controles de estructura, trazabilidad, validación y alineación con los usos previstos.

- `Preparación y normalización`: los diferentes procesos para transformar datos y hacerlos compatibles con los usos previstos.

- `Almacén de datos analíticos brutos controlados`: lo que se suele conocer como "Data Warehouse".

- `Almacén de productos de datos analíticos`: la parte del "Data Warehouse" que se suele pre-procesar para facilitar ciertos usos.

- `Sistemas de consumo analítico`, tales como: cuadros de mando ("dashboards"), informes ("reports"), consultas ("queries"), aplicaciones, APIs de datos, automatismos, modelos IA, etc.

La capa de consumo debe retroalimentar la arquitectura general del sistema. Y la arquitectura debe evolucionar según las necesidades de la capa de consumo.

### Algunas consideraciones prácticas

Los **campos libres** son útiles para capturar matices, pero son problemáticos para explotación estructurada.

Las **categorias ambiguas** (por ejemplo, `otros`) parecen estructuradas y son fáciles de utilizar, pero no representan bien la realidad. De usarlas, es necesario "dificultar" un poco su elección por parte de los usuarios (por ejemplo, pedir teclear una clasificación adicional obligatoria).

Atención a las **opciones "seguras"** (por ejemplo, `falta material` o `petición del cliente`). Esas categorias que "no comprometen a nadie" o que solo comprometen a terceros "fuera de nuestro círculo" tienden a ser las escogidas más a menudo, aunque no sean la opción más correcta. De usarlas, es necesario "dificultar" un poco su elección por parte de los usuarios (por ejemplo, pedir fecha del último pedido o pedir referencia a la comunicación del cliente).

La **retroalimentación** por parte de las personas usuarias es muy importante en cualquier sistema. Por ejemplo, si detectan una categorización incorrecta, o corrigen sistemáticamente resultados, o rechazan sistemáticamente alertas, etc. Han de tener (y utilizar) unos canales claros y sencillos para comunicarlo; a efectos de corregir/mejorar el sistema.

Esta retroalimentación ha de estar incorporada desde el principio, en la concepción y el diseño del sistema. Sin una retroalimentación gobernada, a medida que las necesidades evolucionan, los sistemas van perdiendo adecuación al uso esperado.

En sistemas capaces de desencadenar **acciones automáticas** en respuesta a ciertas condiciones. Es muy importante contar mecanismos que permitan:
- Monitorizar (detectar anomalias) y trazar (buscar causas) su funcionamiento habitual.
- Abortar o forzar sus acciones manualmente, si una persona autorizada lo considera necesario en ciertas situaciones excepcionales. (Eso sí, en cada intervención se ha documentar y registrar el por qué.)



# Uso responsable de Inteligencia Artificial


## Premisas básicas al utilizar IA

*Se use la herramienta que se use, la persona humana que la usa es la responsable.*

> Si una persona no es capaz de revisar y comprender los resultados obtenidos con cierta herramienta en cierto trabajo. Si no puede responder a cuestiones (*) que se planteen acerca de los resultados obtenidos. => Esa persona no debería usar esa herramienta para ese trabajo.

(*) Cuestiones relativas al dominio de aplicación de los resultados.

Un usuario puede no saber cómo funciona internamente la herramienta que usa. Pero sí que ha de saber manejar adecuadamente la herramienta y saber interpretar/revisar/comprender los resultados que esta produce.

Esto es especialmente importante al utilizar herramientas IA, ya que:

- No son deterministas (mismas entradas no producen mismos resultados).

- Pueden producir resultados incorrectos o incompletos con apariencia convincente de solvencia y completitud.

- Su comportamiento puede degradarse sin fallo técnico visible aparente (por ejemplo, a medida que se satura su ventana de contexto).


## Al construir sistemas que integran IA

Es muy importante tener designada una persona **responsable del modelo IA** que se ha integrado en el sistema. Esa persona es la encargada de asegurar que se tengan en cuenta aspectos tales como:

- Establecimiento de límites de uso adecuado.

- Entrenamiento y configuración adecuados del modelo IA.

- Adecuación y calidad de los datos de entrada, tanto para entrenamiento como para inferencia.

- Protección frente a entradas maliciosas.

- Validabilidad y explicabilidad de resultados inferidos.

- Control de derivas y sesgos.

- Monitorización del funcionamiento y de los resultados.

- Realimentación por parte de los usuarios.

- Métricas de uso.

- Identificar necesidad de reentrenamiento o reconfiguración.

- Documentación y versionado de modificaciones.

- Comunicación de modificaciones a los usuarios.

- Identificar necesidad de retirada o sustitución.

