# Cambios formales e informales, en Ingenieria/Taller

Extracto de una charla con [Claude](https://claude.ai).

## Análisis previo realizado por Claude

Profundización — Ingeniería (flujo de una decisión de diseño)

Aquí lo que se fuga es *conocimiento* —el porqué de las decisiones—, y su pérdida es más cara porque no se recupera.

**1. Captura de requisitos.** Escapa la *negociación*: qué se descartó, qué se dio por supuesto, qué requisito es firme y cuál es "así lo hicimos siempre".

**2. Concepción / arquitectura — el núcleo.** Escapan *las alternativas evaluadas y el criterio de descarte*. El PLM ve la decisión, no el espacio de decisión. Se repite el análisis de alternativas ya descartadas cada vez que alguien "tiene una idea nueva" que ya se rechazó.

**3. Cálculo / dimensionamiento.** Escapan las *hipótesis*: carga supuesta, coeficiente, norma, margen. Sin ellas el resultado es un número mágico intocable; congela sobredimensionamientos.

**4. Diseño de detalle / modelado.** El más instrumentado (CAD/PLM: geometría, versiones, quién y cuándo). Aun así escapa el *rationale de la geometría*: por qué este radio, por qué esta tolerancia (¿funcional o defensiva?).

**5. Revisión / validación.** Guarda el veredicto. Escapa el *contenido*: qué se cuestionó, qué objeción se resolvió, qué se aprobó con reservas. Reduce un evento de conocimiento denso a un sello.

**6. Cambios de ingeniería (ECO/ECR).** Bien registrado. Escapa la *causa raíz honesta* del cambio y el patrón agregado (si el 60% de los ECO nacen del mismo subproceso, es un diagnóstico).

**7. Cambios informales de taller — eslabón perdido.** El plano dice X; en taller se ajusta y *el plano nunca se corrige*. La siguiente serie repite el problema. Se pierde la *verdad sobre el producto*.

**Juicio.** Trío: **2 (alternativas descartadas), 3 (hipótesis de cálculo), 7 (divergencia taller-plano)**. Asimetría con Producción: aquí el detalle (4) y los cambios formales (6) están *bien* cubiertos; la fuga se concentra en el *porqué* aguas arriba y la *realidad* aguas abajo. El PLM registra el *qué* y es ciego al *porqué* y al *en realidad*.

**Manipulación: teatro de documentación.** Un campo "justificación" obligatorio para cerrar produce justificaciones *a posteriori* ("según buenas prácticas"), es peor que el vacío porque simula que el conocimiento está capturado. El rationale sincero se escribe al dudar, no al cerrar.

**Encaje.** El subproceso 2 es una *decisión con posicionamiento explícito* → Roseta. El subproceso 7 es un *objeto frontera roto*: cuando el taller reinterpreta el plano sin que este lo absorba, deja de ser objeto frontera y pasa a ficción compartida.


Interfaces entre áreas

La capa transaccional está organizada por área, así que su ceguera máxima está en las **costuras entre áreas**, que no pertenecen a nadie. Se mapean solo las costuras **portantes**: costuras por las que cruza una entidad real y en las cuales el traspaso tiene dato propio que ningún área reclama.

| # | Interfaz | Qué cruza | Qué se pierde |
|---|----------|-----------|---------------|
| ... | | | |
| **I2** | Ingeniería → Producción/Taller | El plano/modelo | Divergencia taller→plano *y* restricción de fabricación que Ingeniería no conoció ([DFM](https://en.wikipedia.org/wiki/Design_for_manufacturability) que no ocurrió). Bidireccional. |
| ... | | | |
| **I4** | Compras → Almacén → Producción | El material | La misma causa recorre tres áreas cambiando de nombre: incidencia tolerada → rotura enmascarada → espera "falta de material". |
| ... | | | |
| **I6** | Producción/Campo → Postventa → Ingeniería | El producto y su comportamiento real | El bucle largo: modo de fallo de campo que debería cerrar hacia diseño y calidad. Sale y vuelve a entrar en la empresa. |
| ... | | | |


**notas:** 

[ECR (Engineering Change Request)](https://en.wikipedia.org/wiki/Change_request)

[ECO (Engineering Change Order)](https://en.wikipedia.org/wiki/Engineering_change_order)

[DFM (Design For Manufacturability)](https://en.wikipedia.org/wiki/Design_for_manufacturability)

[MBD (Model Based Definition)](https://en.wikipedia.org/wiki/Model-based_definition)

## Extracto de la charla

> Me gustaria abordar otro aspecto concreto en profundidad. Igual que en  el que estábamos, en este otro también haciendo especial hincapié en procedimientos y mecanismos concretos mediante los cuales se pueden recoger los datos necesarios. Estudiando su facilidad de recogida y su capacidad de garantizar la calidad de lo recogido.
>
> Concretamente el aspecto relacionado con los puntos 6 (Cambios de ingenieria) y 7 (Cambios informales en taller) de Ingeniería.

El reencuadre que ordena estos dos, y que es más fuerte que en los casos anteriores: **6 y 7 son el mismo fenómeno —el diseño cambió— por dos canales distintos**. El 6 es el cambio que pasa por la puerta; el 7 es el que pasa por la ventana. Y de ahí sale la consecuencia de diseño que los separa de todo lo que hemos visto hasta ahora:

**El 7 no es un fallo de documentación: es una respuesta racional al coste del canal formal.** Nadie modifica el plano en taller por desidia; lo hace porque abrir un ECO cuesta días y la pieza sale hoy. Así que la palanca principal *no es añadir captura al 7* —eso es perseguir el síntoma—, sino **bajar el coste del canal 6 hasta que el 7 deje de ser atractivo**. Es la primera vez en toda la conversación que el mecanismo correcto no es capturar mejor, sino *rediseñar la alternativa*. En I4 y en 1/4 el dato no existía; aquí existe y **está eligiendo la puerta equivocada**.

Corolario que conviene fijar ya: la métrica que de verdad importa no es cuántos ECO hay ni cuántos cambios informales, sino **la proporción entre ambos**. Es el indicador directo de si tu proceso formal está calibrado. Y tiene un modo de fallo perverso que verás repetido: si castigas el cambio informal, no obtienes menos cambios informales — obtienes menos *reportados*. Idéntico a "días sin accidentes" suprimiendo el near-miss.

### Subproceso 6 — Cambios de ingeniería (ECO/ECR)

Sustrato: el mejor de toda la empresa junto con el 4. El flujo formal ya registra qué cambió, quién lo pidió, quién aprobó, con sellos de tiempo. El *qué* está al 100%. Y aquí hay algo que ninguno de los casos anteriores tenía: **una cantidad enorme de dato derivable gratis que casi nadie explota**.

Derivable sin preguntar nada: volumen de ECO por proyecto/producto; **momento del ciclo de vida en que aparecen** (un cambio en preserie es barato, uno en producción es carísimo — la distribución temporal *es* el diagnóstico); lead time del propio ECO (cuánto tarda en aprobarse, que es lo que empuja al 7); qué subsistema los concentra; reincidencia sobre la misma pieza. Todo eso sale del rastro involuntario, como los deltas de fecha en I4.

Lo que escapa es solo una cosa, y es la de siempre: **la causa raíz honesta**. El campo "motivo" existe en casi todos los PLM y casi siempre está inservible, por dos razones distintas —una de diseño y otra de incentivo—.

**Mecanismo.** Mismo reparto de ejes que ya hemos usado: la máquina posee el objetivo (qué cambió, cuándo, coste, reincidencia); el humano aporta solo el causal, por lista cerrada. Y el disparo tiene que ser en el **ECR (la petición)**, no en el ECO cerrado: cuando alguien pide el cambio, la razón está viva; cuando se cierra semanas después, es racionalización. Mismo principio del instante-de-dudar.

**Lista de causa raíz** —MECE, auditable, definida por origen observable, nunca por intención—:

- **Cambio de cliente / requisito externo.** Auditable: ¿hay comunicación del cliente? Y conecta con 1(b) — si el requisito que cambia era una *cesión negociada*, ya lo sabes.
- **Error u omisión de diseño.** La honesta-costosa.
- **Imposibilidad o sobrecoste de fabricación (DFM).** El eslabón con el 7 y con I2.
- **Problema de suministro** (componente obsoleto, no disponible). Auditable contra compras.
- **Fallo detectado en validación o en campo.** Auditable contra el aviso de postventa — cierra I6.
- **Mejora deliberada** (coste, rendimiento), sin fallo previo.

**Manipulación, y es la que ya conoces con otra cara:** "cambio de cliente" es la categoría **externa y socialmente segura** — el "precio" de Comercial 5, la "falta de material" de Producción 4. Se sobreelige. La defensa es la misma que aplicamos en I4: **falsabilidad por puntero** — si marcas cambio de cliente, enlaza la comunicación; si marcas suministro, la notificación del proveedor. Las categorías externas exigen prueba barata; la interna ("error de diseño") **no exige nada**, un clic. Invertimos la fricción a propósito, igual que hicimos con "defensivo" en el subproceso 4: que la admisión honesta sea siempre la más barata de marcar.

Y un segundo vector, más sutil y muy real: **la reclasificación a "cambio menor"** para esquivar la ruta de aprobación pesada. No falsea el motivo, falsea la *magnitud* — y su efecto es doble: distorsiona el dato y empuja el cambio hacia el canal informal. Es literalmente el puente hacia el 7. Se contiene con [criterio de línea brillante](https://en.wikipedia.org/wiki/Bright-line_rule) (qué es menor se define ex ante por impacto en intercambiabilidad/función/coste, no por juicio del solicitante), que es tu criterio de clasificación clara aplicado aquí.

**Facilidad:** muy alta —el sustrato existe, el 80% del valor es derivable de lo que ya se registra y solo requiere explotarlo—. **Calidad:** alta en el eje objetivo; en el causal, buena con disparo en el ECR + punteros de falsabilidad; sin eso, el campo "motivo" es teatro puro.

### Subproceso 7 — Cambios informales de taller

Aquí el sustrato desaparece y el problema vuelve a ser el de 1(b): **el dato no tiene existencia obligada**. La pieza sale bien, el cliente la recibe, nadie necesita el registro para que el trabajo avance. Nada lo fuerza.

Pero hay una diferencia con 1(b) que es la buena noticia del caso, y merece subrayarse porque cambia la estrategia: **aquí el que registra *es* el beneficiario**. El descarte de requisito lo escribía alguien para un yo-futuro ajeno, dentro de dos años — altruismo puro, y por eso fallaba tu propio test de "coste de registrar < coste de no registrar *para el registrador*". En el 7, el operario que ajusta la pieza **se va a encontrar la misma pieza en la siguiente serie**, y si no lo devuelve, la volverá a sufrir él. El retorno es directo, personal y relativamente próximo. Es de los pocos datos de toda la conversación que **pasa el test de valor devuelto por su propia naturaleza**, sin tener que fabricarle un incentivo artificial.

Eso define la estrategia: no hay que motivar el reporte, hay que **quitarle los obstáculos** y hacer visible el retorno. Tres mecanismos concretos:

**1. El plano anotado (red-line) como objeto físico de reporte.** El operario no redacta nada: **marca sobre el propio plano** —el artefacto que ya tiene en la mano— y ese plano anotado va a una bandeja o se fotografía al cierre de turno. Es el equivalente exacto de la etiqueta física del caso 2 de I4: gateo en átomos, no en bits. Ventajas: coste de registro casi nulo (un boli sobre un papel que ya está allí), no exige verbalizar ni clasificar, y produce evidencia inequívoca del delta plano↔realidad. Con MBD/tablet en planta, la versión digital es la misma idea: anotar sobre el modelo, no rellenar un formulario paralelo.

**2. Discriminación —qué se reporta y qué no.** Igual que no perseguíamos toda "falta de material": aquí no se persigue todo ajuste. El criterio es el mismo que en el subproceso 4 (*captura lo que querrás poder tocar en un futuro*): se reporta el ajuste que (a) se repetirá en la siguiente serie, o (b) afecta a función/intercambiabilidad. La rebaba que se limó una vez no interesa. Sin este filtro, el canal se satura y muere — y el operario, con razón, deja de usarlo.

**3. Cierre visible del bucle.** El asesino silencioso de este canal no es la fricción, es la **ausencia de respuesta**: si reportas tres planos anotados y ninguno se traduce en un plano corregido, dejas de reportar. Racionalmente. Así que el mecanismo exige un compromiso de retorno —el red-line entra en la cola de ECO con prioridad y el operario ve el plano actualizado—. Aquí el 7 se conecta con el 6: **el canal informal deja de ser sumidero y pasa a ser la entrada natural de ECO originados en planta**. Y esa es la reparación de I2 en el sentido taller→ingeniería, que quedaba abierta.

**Manipulación y modo de fallo dominante.** El más grave no es del operario: es de la organización. Si el cambio informal se trata como incumplimiento —"ha modificado el plano sin autorización"—, el reporte se hunde y te quedas ciego *creyendo que vas bien*, con la divergencia plano/realidad intacta y ahora además invisible. Es el patrón de "días sin accidentes" clavado. La cultura justa no es aquí un lujo idealista: es **condición de existencia del dato**, más que en cualquier otro punto que hayamos tratado — porque el dato consiste, literalmente, en admitir que se saltó el procedimiento. El segundo vector es el opuesto: si reportar el plano con anotaciones se vuelve trámite (formulario, justificación, firma del encargado), el coste supera al beneficio personal y vuelve el silencio. **Cada gramo de formalidad que añadas al canal de retorno lo mata un poco.**

**Facilidad:** media-alta en el gesto (anotar en un plano es barato), baja-media en el sistema (exige el bucle de retorno funcionando, que es trabajo de ingeniería, no de taller). **Calidad:** el plano anotado es evidencia física de alta fidelidad —no es un relato, es el delta dibujado—; su debilidad no es la veracidad sino la **completitud**, que depende enteramente de que el bucle responda. Dato honesto pero parcial, y la parcialidad es autoinfligida por el diseño del retorno.

### Lo que une los dos, y sus conexiones

**El diagnóstico agregado es más valioso que cualquier cambio individual.** Un ECO aislado dice poco; que el 60% de ECOs nazcan del mismo subsistema, o que los cambios se concentren en producción en vez de en preserie, o que el ratio informal/formal sea alto en una sección concreta, son diagnósticos de proceso. Y el ratio 7/(6+7) mide algo que ningún KPI convencional captura: **cuánto está la organización esquivando su propio proceso formal**, que es un dato sobre el *diseño del proceso*, no sobre la disciplina de la gente.

Tres conexiones:

- **I2 reparada en sus dos sentidos.** El plano es el objeto frontera; el 7 lo rompe cuando el taller reinterpreta sin que el artefacto lo absorba (ficción compartida: el plano dice una cosa y la pieza es otra, y todos lo saben). El plano anotado con bucle de retorno es exactamente el mecanismo que hace que **la reinterpretación local vuelva al artefacto compartido** — plasticidad local con identidad mantenida, que es la definición de Star & Griesemer funcionando en vez de fallando.
- **Vaughan, otra vez.** El ajuste de taller que se repite serie tras serie sin volver nunca al plano *es* normalización de la desviación: se vuelve norma no escrita, y el plano queda como ficción oficial. Mismo fenómeno que la categoría 4 de I4 y que la "herencia no examinada" del subproceso 1.
- **Tu vector de parametrización**, en el sitio más cargado de los dos: **quién define el umbral de "cambio menor"** decide qué cambios son visibles para la organización y cuáles se procesan por una vía que no deja diagnóstico. Fijar ese umbral es política de gobierno disfrazada de configuración técnica —tu variabilidad tipo 6, la de tolerancia, que no es sostenible por mecanismo técnico—. No lo fija TI, sino que se revisa periódicamente.
