# Buenas prácticas en la captura y tratamiento de datos: de la capa operativa al repositorio analítico

nota: el borrador inicial de este documento ha sido elaborado usando IA; tomando ese borrador como inspiración y guia, se ha escrito este documento manualmente partiendo desde un documento en blanco.

## Conceptos básicos

Los datos transaccionales tienen distintas caracteristicas que los datos analíticos.

Los **sistemas transaccionales** están orientados a la gestión de lo que ocurre en la operatoria habitual de la empresa. Van registrando lo que va ocurriendo, de forma continua. Su riesgo más típico son los registros incompletos o tardios; (o en sistemas manuales paralelos no integrados).

Los **sistemas analíticos** están orientados al análisis de lo que ha ocurrido (y, en los sistemas más avanzados, también de lo que está ocurriendo). Para evaluar tendencias, determinar causas y tomar decisiones. Recogen datos de otros sistemas (principalmente desde los sistemas transaccionales) y los elaboran antes de poder ser utilizados para fines analíticos. Su riesgo más típico son las políticas de elaboración implícitas que nunca han sido adoptadas/documentadas formalmente.

### Decisiones claras y documentadas

Es imprescindible que los datos representen lo más fielmente posible la realidad. Además, su semántica ha de estar clara para toda la organización, sabiendo todos lo que cada dato representa y evitando así malinterpretaciones.

En ese sentido, las decisiones de política organizativa han de tomarse de forma consciente. Y han de quedar documentadas, ser versionadas y poderse auditar.

La parametrización de los sistemas no es una mera configuración técnica. Han de tenerse en cuenta sus aspectos relativos a política organizativa. Si no, se corre el riesgo de que las decisiones de política organizativa las tome aisladamente cada equipo técnico en los distintos sistemas; con la consiguiente fragmentación. Y, encima, acaben silenciosamente "enterradas" dentro de la configuración de cada sistema; con la consiguiente falta de transparencia.

La consensuación y homogeneización de datos maestros (tales como códigos de artículos,  códigos de clientes, códigos de proveedores, estructuras, categorias,...) es de vital importancia en el tratamiento y consolidación de datos para analítica. Aquí también las decisiones y modificaciones han de quedar documentadas, ser versionadas y poderse auditar

### Principio de captura única

Cada hecho se ha de capturar una sola vez, en el punto y momento en que se produce. Con la máxima granularidad económicamente razonable.

La captura ha de tener estar bien integrada con el propio proceso transaccional y ha de tener una fricción mínima, evitando interferir con el trabajo del operario.

Son preferibles capturas implícitas (códigos de barras, pesajes o contajes automáticos, señales capturadas en las máquinas,...) a capturas declarativas (rellenar formularios). Cuando sea necesaria una captura declarativa, que sea lo más concisa posible.

Son preferibles capturas unitarias en lugar de agregadas. Lo que se captura separado se puede agregar después, pero lo que captura agregado no se puede separar después.

Prestar especial atención a los sellos de tiempo. Asegurar que reflejan fielmente el momento del hecho y no el del registro. Se pueden recoger ambos, pero ha de quedar claro cual es cual.

Relacionado con los sellos de tiempo. Asegurar que todos los sistemas están adecuadamente sincronizados y que las capturas tienen en cuenta las distintas zonas horarias que pudiera haber.

Algunos peligros típicos a evitar/solventar:

- Duplicación de captura (por ejemplo, en hojas de papel y en el sistema). Es un síntoma de que el sistema transaccional carece de la granularidad y ergonomía necesarias. Se ha de mejorar el sistema para que registrar en él sea tan o más fácil que anotar en papel; evitando así transcripciones posteriores.

- Archivos ofimáticos (generalmente hojas de cálculo) paralelos. Son un síntoma de que el sistema transaccional no cubre ciertos aspectos; (o de que los usuarios prefieren tener control local sobre ciertos aspectos). Se ha de mejorar el sistema para resolver sus carencias; (o reforzar la confianza de los usuarios en el buen uso posterior de los datos).

- Utilizar los datos recogidos para monitorización de rendimiento individual de personas o departamentos. Son un síntoma de cultura "de buscar culpables". Se han de cambiar hábitos en dirección para establecer un clima de confianza donde los datos se usen para "buscar soluciones".

### Diversas capas de procesamiento posterior

Como se ha comentado al principio, no es lo mismo un sistema transaccional que un sistema analítico. La forma y exigencias de los datos en unos u otros es distinta. Normalmente suelen seguir una progresión:

- Fuentes: los datos tal cual se capturan y se manejan en los sistemas transaccionales.

- Repositorio de datos en bruto: datos recopilados desde diversas fuentes,  con la adecuada limpieza, reconciliación y etiquetado (metadata) antes de ser almacenados.

- Repositorio de productos de datos: datos elaborados, con los adecuados controles de calidad; subconjuntos de esos datos suelen ser enriquecidos y preprocesados según ciertas dimensiones, para facilitar ciertos usos posteriores.

- Consumidores: aplicaciones analíticas donde se utilizan los productos de datos.


### Mapa de los principales sistemas fuente

| Sistema | Dominio | Datos clave | Patologías frecuentes |
|---|---|---|---|
| ERP | Económico-administrativo | Pedidos, órdenes, movimientos de stock, costes, facturación | Cierres que reescriben el pasado; campos de texto libre usados como dimensión |
| MES / MOM | Ejecución de producción | Declaraciones de producción, paradas, scrap, tiempos | Motivos de parada con catálogo inservible; umbral de registro que censura paradas cortas |
| PLM / PDM | Ingeniería | BOM, rutas, revisiones, ECO | Efectividad temporal de revisiones mal propagada al ERP; alternativas descartadas nunca registradas |
| CRM | Comercial | Oportunidades, ofertas, motivos de pérdida | Motivo de pérdida cumplimentado por el propio vendedor (sesgo de autoinforme) |
| WMS | Almacén | Ubicaciones, movimientos, inventarios | Regularizaciones que absorben errores de otros procesos |
| GMAO / CMMS | Mantenimiento | Órdenes, averías, preventivos, repuestos | Avería y síntoma confundidos; horas reales imputadas a posteriori en bloque |
| SCADA / Historian | Proceso | Señales de sensor, estados de máquina | Compresión con pérdida en origen; sellos de tiempo sin zona horaria ni sincronización |
| LIMS | Calidad | Ensayos, resultados, certificados | Resultados fuera de especificación gestionados fuera del sistema |
| EDI / portales cliente | Cadena de suministro | Previsiones, llamadas, ASN | Revisiones de previsión que sobrescriben el histórico |

Nota: Pueden ser útiles los estandares ISA-95 / IEC 62264 para la jerarquía empresa–centro–área–línea–celda–equipo y para el modelo de intercambio entre nivel 3 (operaciones de fabricación) y nivel 4 (operaciones de logística y empresariales).

## Algunos detalles prácticos

### Captura de datos

Tener en cuenta todo lo indicado en el apartado previo de `Principio de captura única`.

Otros aspectos a tener en cuenta también:

- Sistemas automáticos de medición o pesaje han de estar calibrados. Si no, posteriores análisis de sus datos mezclaran las variaciones de su precisión de medida con las variaciones en la realidad que miden.

- Las incertidumbres en las medidas también son una información a tener en cuenta. Han de ir asociadas al dato (en sus metadatos).

- Las ausencias de datos ("gaps") son inevitables. Se han de procurar los mecanismos adecuados para que no afecten a la validez de los datos que sí se han recogido. Es conveniente distinguir tres estados en el modelo de datos: valor presente, valor ausente (se sabe que se debió de capturar pero no se capturó), valor desconocido/nulo (no se sabe si se produjo o no).

- "Nadie está obligado a declarar en su contra". Prestar especial atención al diseñar sistemas de recogida y uso de datos que puedan "incriminar" a alguien; y más si ese alguien es la propia persona o departamento que registra esos datos.


### Ingesta de datos

Al capturar datos procedentes de sistemas transaccionales son preferibles métodos CDC (Change Data Capture) frente a métodos por extracción incremental o por volcados batch masivos de los datos originales.

Los métodos CDC pueden ser basados en los logs de transacciones de las bases de datos involucradas o basados en eventos publicados por las propias aplicaciones.

Algunos aspectos importantes a tener en cuenta:

- Los controles de esquemas y formatos no son opcionales. Cualquier modificación en las fuentes o cualquier error de transmisión ha de detectarse durante la ingesta.

- Cambios en esquemas, en formatos o en semántica han de estar aprobados, documentados y serializados. No deberian de ser detectados por sorpresa en los controles de la ingesta o, peor aún, en el consumo final de los datos.

- Prestar especial atención a la idempotencia. Es decir, reingestar el mismo lote de datos no debe alterar el resultado final en el repositorio.

- Los datos almacenados han de llevar asociados los correspondientes metadatos indicando desde dónde y cuándo fueron ingestados.

- Se ha de conservar un histórico de las transmisiones originales. Para así disponer de trazabilidad y reproducibilidad de las ingestas realizadas.


### Procesamiento de datos

Se han de separar con claridad:
- datos procesados para análisis exploratorios
- datos certificados para indicadores de soporte decisional

En ambos casos, la semántica de cada dato (lo que se supone que representa y el método seguido para obtenerlo/calcularlo) ha de estar clara. Pero en el caso de los datos certificados ha de estar ademas documentada, versionada y publicada de forma oficial.

Un dato solo es comparable si su procedimiento de obtención está bien definido y es comprendido por todas las personas que van a utilizarlo.

Algunos aspectos importantes a tener en cuenta:

- La monitorización y trazabilidad no son opcionales. La monitorización ha de detectar y alertar sobre cualquier problema que se pueda producir en el procesamiento. La trazabilidad ha de permitir rastrear las causas de esos problemas.

- Cambios en los procesos han de quedar documentados y versionados. Sobre todo en procesos que guarden datos históricos, donde pueden quedar mezcladas diversas formas de procesar/calcular un mismo dato a lo largo de la historia.

- Es importante hacer estudios periódicos acerca de la significación estadística de los datos y de su calidad. Para no atribuirles más mérito del que realmente tienen. Y para ver si es necesaria alguna modificación en la captura o en las fuentes para garantizar su validez según los usos previstos.


### Consumo de datos

Algunos aspectos importantes a tener en cuenta a la hora de analizar datos:

- Correlación no implica causalidad.

- La estacionalidad o efectos del calendario han de tenerse en cuenta antes de declarar tendencias.

- Efectos debidos a la variación en volumen requieren ponderación y normalización antes de que los datos involucrados puedan ser comparados.


## Aspectos de gobernanza


 Hay tres arquetipos en cuanto a gobernanza de datos:
 
 - Gestión centralizada: Con un único equipo de datos. Viable solo en organizaciones pequeñas. Ya que en organizaciones grandes el equipo central no puede llegar a conocer/atender toda la casuística local.
 
- Gestión federada: Con varios equipos de datos, coordinados todos ellos gracias a una disciplina de estándares comunes respetados por todos.
> La gestión federada es la más común en organizaciones medianas o grandes.
> - A nivel de toda la organización, se mantienen una plataforma, unos estándares, unos maestros mínimos, un catálogo y unos criterios de seguridad centralizados.
> - Mientras que la propiedad semántica y la responsabilidad de calidad de los datos residen en el equipo que genera/procesa/transmite cada dato localmente.

- Data Mesh: Cada equipo de datos gestiona, produce y sirve su propio catálogo de datos. Disponibles para toda la organización, allá donde se necesiten.

>Un Data Mesh está solo al alcance de organizaciones muy maduras en gobernanza de datos.

Nota: Pueden ser útiles el estándar ISO/IEC 38505-1 y las recomendaciones del DAMA-DMBOK.


### Roles

Para cada conjunto de datos ha de haber:

- Una persona propietaria del dato ("owner"): perfil directivo que decide definiciones semánticas, criterios de acceso/uso y prioridades de calidad.

- Una persona administradora del dato ("steward"): perfil con un conocimiento operativo profundo que le permite mantener definiciones, resolver incidencias de calidad y validar reglas.

- Una persona custodia del dato ("custodian"): perfil técnico que implementa, opera y monitoriza los sistemas; asegurando su correcto funcionamiento según los parámetros establecidos.

Además se ha de establecer un foro de colaboración y resolución de conflictos semánticos. Para garantizar que no haya inconsistencias o incompatibilidades entre conjuntos de datos.


### Diccionarios y catálogos

Es importante que todas las personas involucradas tengan un mismo entendimiento de los datos que manejan. Conociendo:
- Qué aspecto de la realidad representan (definición semántica).
- Cómo lo representan (origen y transformaciones que los producen).
- Cuales son los usos establecidos (en qué aspectos son útiles y en cuales no)

Al existir numerosas necesidades y sensibilidades locales, suele ser importante buscar un consenso. No persiguiendo una imposición canónica única, sino construyendo objetos frontera: una definición estándar documentada, con variantes locales equivalentes declaradas y mapeadas.

Pero sin perder de vista que pueden haber dos tipos de variabilidad:

- Variabilidad "sintáctica": en representación, formato, granularidad, cadencia,... que puede ser compensada técnicamente y no afecta estructuralmente.

- Variabilidad "semática": en criterios de medida, umbrales de validación, reglas de cálculo,... que es imposible de compensar y puede afectar gravemente a la interoperabilidad/comparabilidad.

Nota: Pueden ser útil el estándar OpenLineage.


### Contratos de datos

Un contrato de datos es el acuerdo explícito entre productor y consumidor sobre:
- esquema (qué campos y de qué tipo),
- semántica (qué representa cada campo),
- calidad (requisitos mínimos para ser útil),
- frecuencia (cada cuánto se ha de refrescar)
- propiedad (quién decide cambios),
- versionado (hacer explícitos los cambios y la compatibilidad tras ellos)

### Datos maestros

Siempre hay ciertos datos que es imprescindible estandarizar para garantizar la interoperabilidad fluida entre distintos sistemas.

Si se pretende componer datos procedentes de dos o más sistemas. Estos han de compartir unas claves y categorias comunes que permitan dicha composición. Intentar mapear "adhoc" equivalencias entre unos sistemas y otros, puede funcionar si las divergencias son pocas; pero no como solución general.

Cada dato maestro ha de tener un sistema autoritativo que lo mantenga. Y el flujo propagación ha de ser siempre unidireccional: desde el sistema autoritativo hacia los sistemas consumidores.

### Principales riesgos a evitar

La causa dominante de problemas en el uso analítico de datos suele ser su mala calidad. Usualmente fruto de una pobre gobernanza y de unas definiciones semánticas y estándares inconsistentes o muy fragmentados.

Por otro lado, en el origen, en la propia captura de datos, pueden estar actuando múltiples factores:

- Si el coste de capturar unos determinados datos recae sobre personas o departamentos que no perciben su beneficio. Estos no tienen ningún interés en captarlos correctamente. -> Es importante devolver valor al punto de captura, en el mismo interfaz y a tiempo para ser útil.

- Si se penaliza el registro de desviaciones o problemas, estos no aflorarán nunca. Lo que es necesario penalizar es el ocultamiento de esa información. Pero eso ha de ir acompañado de una cultura empresarial "segura", orientada a "buscar soluciones". -> Es importante demostrar con claridad que la información ayuda a resolver o mitigar desviaciones y problemas. (Y que no se usa para "culpabilizar" ni evaluar a nadie.)

- Si no se separa explícitamente la captura de datos para operatoria de la captura de datos para evaluación de personas/equipos, los datos recogidos se verán degradados por la tendencia natural a registrar solo lo que favorece y a ocultar lo que perjudica.

- Si los datos se usan para métricas con repercusión personal (incentivos, penalizaciones,...), los datos recogidos se verán degradados por la tendencia natural a manipularlos ("gaming") para aumentar beneficio o reducir perjuicio. Por tanto, mucho cuidado con las métricas; en no pocas ocasiones acaban mediatizando el proceso que pretenden medir.



## Aspectos de calidad

### Dimensiones a asegurar

Marco de referencia: ISO/IEC 25012 y DAMA-DMBOK2.

| Dimensión | Pregunta | Ejemplo industrial de regla |
|---|---|---|
| Exactitud | ¿Refleja la realidad? | Stock de sistema vs recuento cíclico, desviación < x % |
| Completitud | ¿Está todo lo que debería? | Toda orden cerrada tiene al menos una declaración de producción |
| Consistencia | ¿Concuerda entre sistemas? | Cantidad declarada en MES = cantidad notificada en ERP |
| Validez | ¿Cumple el formato/dominio? | Motivo de parada ∈ catálogo vigente |
| Unicidad | ¿Hay duplicados? | Un solo registro por (orden, operación, turno) |
| Oportunidad | ¿Llega a tiempo? | Declaración registrada < 2 h tras el hecho |
| Integridad referencial | ¿Las referencias resuelven? | Todo movimiento apunta a un artículo existente en el maestro |
| Trazabilidad | ¿Se sabe de dónde viene? | Linaje completo hasta sistema y lote de origen |

### Validaciones a comprobar

En orden de eficacia decreciente y coste creciente:

- En origen: validación en el interfaz de captura, usando herramientas tales como escaneos, selección de entre opciones predefinidas, captura por instrumento automático,...

- En ingesta: validación de esquemas y formatos, con alertas/registro en caso de detectar discrepancias.

- En transformación: validación de unicidad, de rangos, de integridad referencial, de cumplimiento de reglas de negocio,...

- En consumo: validación contra fuente autoritativa, recuentos y sumas de control,...

- En operatoria: plataforma de observabilidad para detección de anomalias frente al funcionamiento habitual esperado.

- En revisión estadística: para detectar derivas tales como cambios en la distribución de una variable, variaciones en la tasa de nulos, volumen de datos procesados,...

## Algunos antipatrones a evitar

| Antipatrón | Por qué falla |
|---|---|
| Empezar por la herramienta | El stack no determina el resultado; la captura y la gobernanza sí |
| Migrar los informes existentes tal cual | Se importa la deuda semántica completa y no se obtiene beneficio percibido |
| Data lake como vertedero | Sin modelado ni contrato, el coste de descubrimiento supera al de reconstruir |
| Limpiar en el pipeline lo que está mal en origen | Impuesto permanente; el defecto sigue vivo y se propaga a todo lo no capturado |
| "El dashboard obligará a rellenar los campos" | El campo se rellena con ruido; empeora el dato en lugar de mejorarlo |
| Métrica única de rendimiento por persona | Se optimiza la métrica, no el proceso (Goodhart) |
| Definición canónica impuesta sin arbitraje | El área mantiene su versión en paralelo; se duplica el esfuerzo |
| Confundir disponibilidad del dato con capacidad de decisión | El cuello de botella suele ser el proceso de decisión, no la información |
| Cifrar el proyecto en la nube sin tocar la captura | Se obtiene el mismo dato deficiente, más rápido y más caro |
