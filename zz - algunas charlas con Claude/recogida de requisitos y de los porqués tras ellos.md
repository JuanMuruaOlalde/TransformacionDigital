# Recogida de requisitos y de los porqués tras ellos

Extracto de una charla con [Claude](https://claude.ai).

## Análisis previo realizado por Claude

Profundización — Ingeniería (flujo de una decisión de diseño)

Aquí lo que se fuga es *conocimiento* —el porqué de las decisiones—, y su pérdida es más cara porque no se recupera.

**1. Captura de requisitos.** Escapa la *negociación*: qué se descartó, qué se dio por supuesto, qué requisito es firme y cuál es "así lo hicimos siempre".

**2. Concepción / arquitectura — el núcleo.** Escapan *las alternativas evaluadas y el criterio de descarte*. El PLM ve la decisión, no el espacio de decisión. Se repite el análisis de alternativas ya descartadas cada vez que alguien "tiene una idea nueva" que ya se rechazó.

**3. Cálculo / dimensionamiento.** Escapan las *hipótesis*: carga supuesta, coeficiente, norma, margen. Sin ellas el resultado es un número mágico intocable; congela sobredimensionamientos.

**4. Diseño de detalle / modelado.** El más instrumentado (CAD/PLM: geometría, versiones, quién y cuándo). Aun así escapa el *rationale de la geometría*: por qué este radio, por qué esta tolerancia (¿funcional o defensiva?).

**5. Revisión / validación.** Guarda el veredicto. Escapa el *contenido*: qué se cuestionó, qué objeción se resolvió, qué se aprobó con reservas. Reduce un evento de conocimiento denso a un sello.

**6. Cambios de ingeniería ([ECO/ECR](https://en.wikipedia.org/wiki/Engineering_change_order)).** Bien registrado. Escapa la *causa raíz honesta* del cambio y el patrón agregado (si el 60% de los ECO nacen del mismo subproceso, es un diagnóstico).

**7. Cambios informales de taller — eslabón perdido.** El plano dice X; en taller se ajusta y *el plano nunca se corrige*. La siguiente serie repite el problema. Se pierde la *verdad sobre el producto*.

**Juicio.** Trío: **2 (alternativas descartadas), 3 (hipótesis de cálculo), 7 (divergencia taller-plano)**. Asimetría con Producción: aquí el detalle (4) y los cambios formales (6) están *bien* cubiertos; la fuga se concentra en el *porqué* aguas arriba y la *realidad* aguas abajo. El PLM registra el *qué* y es ciego al *porqué* y al *en realidad*.

**Manipulación: teatro de documentación.** Un campo "justificación" obligatorio para cerrar produce justificaciones *a posteriori* ("según buenas prácticas"), es peor que el vacío porque simula que el conocimiento está capturado. El rationale sincero se escribe al dudar, no al cerrar.

**Encaje.** El subproceso 2 es una *decisión con posicionamiento explícito* → Roseta. El subproceso 7 es un *objeto frontera roto*: cuando el taller reinterpreta el plano sin que este lo absorba, deja de ser objeto frontera y pasa a ficción compartida.

## Extracto de la charla

> Abordar otro aspecto concreto en profundidad. Igual que en el que estábamos, en este otro también haciendo especial hincapié en procedimientos y mecanismos concretos mediante los cuales se pueden recoger los datos necesarios. Estudiando su facilidad de recogida y su capacidad de garantizar la calidad de lo recogido.
>
>Concretamente querria abordar el aspecto relacionado con los puntos 1 (Captura de requisitos) y 4 (Diseño de detalle/modelado) de Ingeniería.

Antes de los mecanismos, un reencuadre que cambia el espacio de diseño por completo respecto a I4 —y que además explica por qué agrupaste bien estos dos—: **1 y 4 son el mismo dato en dos puntos del flujo**. No son "requisitos" y "geometría"; son *la razón detrás de un valor* —el intent de diseño— aguas arriba (por qué este requisito) y aguas abajo (por qué esta cota/tolerancia). Y ese dato tiene una propiedad que lo separa tajantemente de todo lo que vimos en I4:

**El rationale no tiene rastro involuntario, porque no es un evento en el mundo: es un estado mental en el instante de decidir.** En I4, el *qué* era un evento (una tolerancia, una rotura, un paro) que dejaba huella o se podía gatear, y por eso el motor podía preensamblar la hipótesis y dejarle al humano solo *adjudicar*. Aquí no hay nada que triangular: no existe sensor del que derivar "por qué el radio es 5 y no 8". La triangulación —el mecanismo que salvó el caso 1 de I4— **no está disponible**. El dato solo puede venir del autor, y solo cerca del momento de decidir. Estamos, desde el minuto uno, en el régimen más difícil: autorreporte obligado, sin red.

De ahí que el enemigo único de ambos subprocesos sea el que ya bautizamos para Ingeniería: **el teatro de documentación**. Y conviene descomponerlo, porque tiene dos motores y solo uno lo apaga la cultura justa:

- *Motor de incentivo*: registrar el porqué ayuda al yo-futuro y a otros, no al yo-presente. Lo apaga la cultura justa (más bien, lo apaga que no cueste nada; el miedo aquí pesa menos que en I4 porque el rationale rara vez es autoinculpatorio).
- *Motor de tiempo y fricción*: si el porqué se exige en un gate de cierre —semanas después de decidir—, la razón viva ya se evaporó y lo que se escribe es racionalización *a posteriori* ("según buenas prácticas"). **Este motor sobrevive intacto a la cultura justa.** No es mala fe: es memoria y coste. Por eso el principio rector no es cultural sino de diseño: *capturar en el instante de dudar, embebido en el gesto de autoría, nunca en un trámite posterior.*

Trato primero el 4, porque el sustrato rico lo hace más limpio y ahí el mecanismo se ve mejor; luego el 1, donde el sustrato pobre y el contrafactual complican.

### Subproceso 4 — Diseño de detalle

El sustrato es el más rico de toda la empresa: cada cota y tolerancia es un dato estructurado, versionado, atribuido, en el CAD/PLM. El *qué* está capturado al 100%. Falta *solo* el porqué. Y el problema de diseño dominante no es el de I4 (enlazar eventos) sino el de **volumen**: una pieza tiene cientos de cotas. Pedir rationale de todas es absurdo y es teatro garantizado. La pregunta central es de **discriminación**: ¿cuáles de los cientos de valores merecen un porqué?

Y aquí está la clave, porque el discriminador es objetivo y derivable, igual que el filtro de exposición aguas abajo lo era en I4: **la desviación respecto al valor por defecto**. El sistema conoce la tolerancia estándar (tabla general, norma de la casa). Una cota con tolerancia general no necesita rationale: es el default barato. Una tolerancia *apretada por debajo del estándar* sí, porque apretar es el acto costoso —el que dispara coste de fabricación— exactamente como "tolerar" era el acto costoso en compras. La máquina posee el eje objetivo (¿desvía del default? sí/no, cero juicio humano); el humano posee solo el causal. Mismo reparto que en I4.

**Mecanismo concreto.** En el instante en que el diseñador fija una tolerancia más apretada que el default, el sistema dispara una captura ligera *sobre esa cota* —no un formulario aparte, un atributo de la propia entidad geométrica—. Esto exige que el sustrato lo permita: definición basada en modelo (MBD) o un PLM que deje colgar atributos estructurados de una tolerancia individual en el momento de autoría. Y aquí reaparece, calcado, el corolario de I4 caso 1: **"tener CAD/PLM" es necesario pero no suficiente**. Si las tolerancias viven en un PDF 2D tonto, no hay dónde pegar el porqué salvo un documento separado → teatro asegurado. La pregunta de sustrato no es *si hay PLM*, es *si la definición deja que el rationale viva sobre el valor restringido*.

**La lista del porqué** (una selección, jamás texto libre en el eje analizable), y fíjate en un detalle que la hace bonita:

- **Interfaz funcional** — casa con la feature X. Verificable: nombrar la feature que acopla.
- **Cálculo** — sale de un análisis concreto. Verificable: enlace al cálculo. *Apunta al subproceso 3* (hipótesis de cálculo).
- **Requisito / norma** — impuesto desde arriba. Verificable: enlace al requisito. *Apunta al subproceso 1.*
- **Herencia probada** — copiado de un diseño que funciona. Verificable: enlace al origen. Riesgo: propaga sobrerrestricción si el origen ya era defensivo.
- **Defensivo / incertidumbre** — "por si acaso", no sé cuánto hace falta de verdad. *No* verificable, y está bien que no lo sea: es la admisión honesta, y es **el dato de oro** —marca el candidato exacto a análisis de tolerancias / DFM, la tolerancia apretada que dispara coste sin función—.

El detalle bonito: tres de las cinco categorías (cálculo, requisito, herencia) son **punteros a decisiones aguas arriba**. Capturar el porqué de la geometría *construye la cadena de trazabilidad* requisito→cálculo→geometría. Ese encadenamiento es el entregable real: es lo que hace el diseño **revisable**. Y esto reencuadra todo el subproceso —lo desarrollo al cerrar—.

**Vector de manipulación y su defensa**, que aquí es fina e invierte la trampa habitual de fricción. El riesgo es el *lavado de la tolerancia defensiva*: quien apretó "por si acaso" pero no quiere admitir incertidumbre marca "interfaz funcional" o "cálculo" en su lugar, y la sobrerrestricción se esconde. La defensa correcta es contraintuitiva: **haz que la categoría honesta (defensivo) sea la más barata —un clic, sin justificación— y que las sustantivas exijan su puntero verificable barato** (nombrar la feature, enlazar el cálculo). Normalmente la respuesta honesta-costosa es la que pide el ensayo; aquí lo invertimos a propósito. Así "defensivo" nunca se evita por fricción, y una "cálculo" falsa se cae sola porque le falta el enlace. La falsabilidad por puntero es el análogo exacto de "cada categoría auditable contra el rastro" de I4.

**Facilidad**: alta en la discriminación (gratis, la computa el sistema); media en la captura, condicionada por completo al sustrato MBD. **Calidad**: alta en qué-discriminar (objetivo); en el porqué, buena si se respeta el instante-de-autoría y la selección-no-ensayo, y con la defensa anti-lavado, la categoría "defensivo" se vuelve autoauditable en agregado (si un diseñador marca todo "interfaz funcional", auditas si esas interfaces existen).

### Subproceso 1 — Captura de requisitos

Aquí cambia todo a peor en dos frentes. **El sustrato es pobre**: los requisitos nacen de una negociación —con cliente, con comercial (otra vez I1/I2), interna— que vive en correos, actas, conversaciones. Y a diferencia del 4, **ni siquiera el *qué* está capturado del todo**: el requisito final se registra, pero los descartados y los supuestos no.

Hay que separar dos datos de valor muy distinto:

**(a) La procedencia y firmeza de cada requisito.** ¿"Cota = 40" es restricción dura del cliente, imposición normativa, requisito derivado de otro, o herencia no examinada ("siempre lo hicimos así")? Este es el dato que evita el *número mágico intocable*: sin él, dos años después nadie sabe si 40 es sagrado o accidental, así que nadie se atreve a tocarlo → sobrerrestricción congelada. Idéntico al fallo del subproceso 3 y, de hecho, al de la tolerancia del 4.

Es capturable con calidad decente, y el mecanismo es un **registro de requisitos con la firmeza como atributo estructurado obligatorio por requisito**, no como campo opcional. Lista de procedencia, otra vez auditable donde puede serlo: "cliente duro" contrastable contra el documento del cliente; "normativa" contra la cláusula; solo "derivado" y "herencia no examinada" son juicios internos. Y **"herencia no examinada" es la categoría autoinculpatoria** —el análogo exacto de la categoría 4 de I4 (práctica no examinada, Vaughan)—: mismo diseño, no puede ser la salida fácil, y su aparición recurrente en agregado *es* el diagnóstico. El vector aquí es la *inflación de firmeza*: marcar todo "cliente duro" para blindar el requisito contra futuros cuestionamientos. Se contiene con la auditabilidad contra el documento fuente.

**(b) El requisito descartado —el camino no tomado.** El cliente pidió X, le convencimos de Y, se registra Y y se evapora X y el porqué de X→Y. Esto es un **contrafactual puro** —misma categoría que la razón de pérdida de Comercial 5— y, como todo contrafactual, no tiene rastro alguno. Y aquí te debo honestidad en lugar de venderte un mecanismo: **este dato es caro y su completitud siempre será baja.** Solo se captura en el instante de la negociación, por alguien que se moleste en registrar algo que "ya se resolvió", sin retorno inmediato. Es el mismo problema irreducible del win/loss. Lo máximo razonable es un registro ligerísimo *en el momento del acuerdo de requisitos* —una línea: "el cliente pedía X; acordamos Y porque Z"— y aceptar que capturarás los descartes *conscientes y relevantes*, no todos. Prometer captura completa aquí sería el error.

**Facilidad**: media-baja para (a) —exige disciplina de registro estructurado en un momento relacional poco instrumentado—; baja para (b) —contrafactual sin rastro—. **Calidad**: (a) buena si el atributo es obligatorio y auditable; (b) intrínsecamente incompleta, y ninguna sofisticación lo arregla, igual que el volcado del caso 2 de I4 era basura para su propósito.

### El reencuadre que unifica los dos, y sus conexiones

Lo que de verdad importa, y que reordena para qué sirve todo esto: **el rationale no se captura para documentar; se captura para preservar grados de libertad.** Una cota o un requisito cuyo porqué nadie conoce es intocable —modificarlo exige rehacer un razonamiento no escrito—, así que se congela y arrastra su sobrecoste para siempre. Capturar el porqué es lo que mantiene el diseño *plástico*: registras por qué para poder *cambiar* con seguridad después. El entregable no es un archivo, es la revisabilidad. Esto cambia el criterio de qué merece captura: no "lo importante", sino **lo que querrás poder tocar sin miedo** —que es justamente lo apretado, lo restringido, lo que desvía del default—. El discriminador del subproceso 4 (desviación) y la firmeza del 1 no son dos mecanismos: son el mismo criterio —marca lo que restringe grados de libertad— en los dos extremos del flujo.

Tres conexiones con lo tuyo:

La **cultura justa pesa aquí más que en I4 y a la vez menos**. Más, porque no hay red de triangulación: *todo* es autorreporte, así que sin confianza no hay dato. Menos, porque el enemigo principal —el teatro— es un fallo de *timing y fricción*, no de miedo: lo apagas capturando en el instante de autoría, tengas la cultura que tengas. Buena separación para no atribuirle a la cultura lo que le toca al diseño del momento de captura.

El **objeto frontera**, en el subproceso 1: el requisito que cruza de cliente/comercial a ingeniería debería viajar con su firmeza pegada, como el material del caso 2 de I4 viajaba con su etiqueta de anomalía. Cuando cruza *sin* procedencia, ingeniería no distingue restricción dura de accidente, y "cota = 40" se vuelve ficción compartida —sagrada sin que nadie sepa por qué—. Reparar el subproceso 1 es darle al requisito ese objeto frontera.

Y tu **vector de parametrización**, en las dos listas: quién define las categorías de firmeza (1) y las del porqué de la tolerancia (4) decide *qué causas son pensables*. Si "defensivo / incertidumbre" no está en la lista del 4, la sobrerrestricción no desaparece: se pliega sobre "interfaz funcional" y se vuelve invisible —una empresa que ha decidido, sin decidirlo, no poder verse las tolerancias infladas—. Las dos listas son objeto de la capa decisional, no las congela TI.

Dos caminos desde aquí: aterrizar el **mecanismo del subproceso 4 en un PLM concreto** —cómo dispara la desviación, cómo se pega el atributo a la tolerancia, cómo se cierra el bucle con el análisis DFM que consume el "defensivo"—; o atacar el punto duro del **subproceso 1(b)**, el requisito descartado, viendo si hay algún gateo del momento de negociación que lo rescate parcialmente sin caer en teatro, aceptando de antemano que la completitud será baja. ¿Cuál?

### Estrategias y procedimientos que tienden a facilitar la recogida consistente de esta información

> El subproceso 1(b), el requisito descartado. ¿Qué tipo de estrategias y procedimientos tienden a facilitar la recogida consistente de esta información?. O, viéndolo desde el otro lado de la balanza, ¿Por qué es más difícil recoger requisito descartado que requisito aceptado.? (Una vez puestos a escribir, en ese momento, es simplemente un poco más trabajo escribirlo todo; o por lo menos citarlo sin detalle.) ¿no?

Tu objeción es exactamente la correcta y merece que la tome en serio antes de matizarla, porque contiene una verdad y esconde un error, y separar los dos es toda la respuesta.

**La verdad:** tienes razón en un caso concreto y nada trivial —el descarte que ocurre *en el mismo acto de escribir el requisito aceptado*—. Si estoy redactando "cota = 40" y en mi cabeza acabo de rechazar 50, añadir "(el cliente pedía 50; acordamos 40 por peso)" es, literalmente, un poco más de teclear. Ahí el coste marginal es casi cero y tu intuición es correcta. Si *todo* el requisito descartado fuera de este tipo, no habría problema y yo estaría inventándome una dificultad.

**El error** está en "una vez puestos a escribir". Esa cláusula da por hecho lo que precisamente no se cumple. El requisito descartado no es más difícil de *escribir*; es más difícil de **llevar hasta el momento y el estado mental en que se escribe**. 

#### Asimetrías

Y ahí hay al menos cinco asimetrías que no son de esfuerzo de redacción. Te las pongo porque cada una sugiere una contramedida distinta:

**1. Asimetría de existencia (la decisiva).** El requisito aceptado *tiene que* escribirse: sin él no hay plano, no hay pieza, el trabajo no avanza. Es coproducto obligado del flujo. El descartado no bloquea nada por no registrarse —el diseño sale igual—, así que su escritura es siempre *opcional*, y lo opcional bajo carga se omite. No es que cueste más escribirlo; es que **nada te obliga a hacerlo y todo sigue si no lo haces**. Esta es la raíz. Las otras cuatro son agravantes.

**2. Asimetría de estado terminal.** El aceptado es un objeto único, presente, con un valor final que copias de la realidad del diseño. El descartado es un objeto *plural y ausente*: no hay "un" descarte, hay las tres alternativas que se consideraron y las cinco que ni se nombraron. ¿Cuál registras? La frontera de "qué cuenta como descarte digno de registro" no está dada —hay que *decidirla*—, y esa decisión es un coste cognitivo que el aceptado no te impone. Escribir el aceptado es transcribir; escribir el descarte es primero *seleccionar de un conjunto difuso* y luego transcribir.

**3. Asimetría de momento (la que rompe tu "una vez puestos a escribir").** El aceptado se escribe *después*, tranquilo, transcribiendo un resultado estable. El descarte solo es recuperable *durante* —en la negociación, cuando 50 todavía está vivo en la conversación—. Media hora después, cerrado el acuerdo, 50 ya no está en tu cabeza con sus razones: está la conclusión, no el camino. De modo que "una vez puestos a escribir" es precisamente el instante en que el descarte **ya se evaporó**, si el escribir ocurre en el gate de cierre y no en la mesa. La ventana de captura barata del aceptado está abierta siempre; la del descarte se cierra en minutos. No compiten en esfuerzo: compiten en *disponibilidad temporal del dato*.

**4. Asimetría de completitud del rationale.** Del aceptado, el porqué está fresco y es único ("es 40"). Del descarte, el porqué es comparativo —por qué 40 *mejor que* 50— y además intervino gente que no está cuando por fin te sientas a documentar (el cliente, el comercial). Reconstruir "por qué le convencimos" exige recuperar la posición del otro, que tú quizá ni conociste del todo. Más superficie de razón, y parte en cabeza ajena.

**5. Asimetría de valor percibido por el que escribe.** Y esta conecta con tu propio principio de "devolver valor al registrador". El aceptado le sirve *a él, ahora*: es su instrucción de trabajo. El descarte no le sirve a él nunca —sirve al yo-futuro de otro, dentro de dos años, cuando alguien pregunte si 40 se puede tocar—. Registrar el descarte es puro altruismo temporal e interpersonal, sin retorno para el autor. Bajo tu propio criterio (coste de registrar < coste de *no* registrar, *para el registrador*), el descarte **casi nunca pasa el test**, porque su coste de no-registrar lo paga otro.

#### Cómo combatir esas asimetrias y recoger la información

Fíjate en lo que sale de juntarlas: tu intuición ("es solo un poco más escribir") es verdadera *solo* cuando las cinco se anulan a la vez —el descarte es único y consciente (anula 2), estás escribiendo en el momento de la negociación (anula 3), tú viviste el rationale completo (anula 4)—. Ese caso existe y es justo el objetivo alcanzable. El problema es que el diseño *por defecto* —documentar en un gate de cierre, con campo de descarte opcional— viola las cinco a la vez. Casi todo el fallo de captura es **diseño equivocado del momento y la obligatoriedad**, no dificultad intrínseca. Tu optimismo es correcto sobre el techo; el pesimismo es correcto sobre lo que se consigue por defecto.

De ahí las estrategias, cada una atacando una asimetría concreta, no "animar a documentar mejor":

**Contra la existencia opcional (1) — hacer el descarte coproducto, no apéndice.** El único arreglo estructural. Si el artefacto donde se fija el requisito tiene el par *pedido / acordado* como **campo único**, no como "valor" + "notas opcionales", entonces cuando pedido ≠ acordado el hueco del descarte existe físicamente y su vacío es visible. No lo haces obligatorio por decreto (eso genera relleno basura); lo haces **estructuralmente presente**: un requisito donde alguien tuvo que ceder y el campo "posición inicial del cliente" está vacío se *ve* incompleto. Conviertes la omisión de invisible en visible —que es justo lo que un contrafactual nunca es por su cuenta—.

**Contra el estado plural (2) — no pidas "los descartes", pide el delta.** No registres el conjunto de alternativas; registra solo *dónde acordado ≠ lo primero pedido*. Un único delta por requisito negociado, binario de disparo (¿hubo cesión? sí/no), y si sí, una línea. Acotas el conjunto difuso a un objeto único y recuperas la simetría con el aceptado. Los descartes que "ni se nombraron" los sueltas a propósito: perseguirlos es lo que hace la tarea infinita.

**Contra el momento (3) — captura en la mesa, no en el gate. La más importante y la que refuta directamente tu "una vez puestos a escribir".** El registro del descarte tiene que colgar del *acto de negociar*, no del acto de documentar el diseño. En la práctica: el artefacto donde se cierra el acuerdo de requisitos con el cliente/comercial —el acta de esa reunión, no el PLM de la semana siguiente— es donde el campo pedido/acordado tiene que vivir. Movido ahí, tu intuición *se vuelve cierta*: en ese momento sí es solo un poco más de teclear, porque el 50 está vivo. El problema nunca fue el esfuerzo; fue que preguntábamos en el sitio equivocado del tiempo. Esto es exactamente "capturar en el instante de dudar" aplicado al 1(b).

**Contra la completitud (4) — plantilla mínima que no exija reconstruir al otro.** Tres ranuras: qué se pidió, qué se acordó, palabra clave del porqué (lista corta: coste / plazo / fabricabilidad / normativa / el cliente cedió sin más). No pidas narrar la posición ajena; pide el eje del trade-off. Convierte reconstrucción en selección.

**Contra el valor percibido (5) — devolver algo al que escribe, o aceptar que no lo hará.** Es la más dura y la más honesta. Si registrar el descarte no le da nada al que lo registra, ninguna plantilla lo sostiene en el tiempo. Dos salidas reales: o el registro *le sirve ya* —p. ej. es su cobertura ante el cliente cuando dentro de seis meses reclame el 50 que él mismo cedió: "está en acta que lo acordamos"—, y entonces lo escribe por interés propio; o no le sirve, y entonces el único mecanismo fiable es que lo capture **alguien cuyo trabajo *es* la reunión**, no el diseño —el que levanta el acta—, para quien registrar lo acordado no es altruismo sino su función. Reasignar la captura a quien no paga el coste como extra es, muchas veces, más realista que motivar al que sí lo paga.

Respuesta corta a tu pregunta, entonces: **no es más difícil de escribir. Es más difícil de *provocar*** —porque nada lo exige, se evapora en minutos, y lo paga quien no lo cobra—. Cuando alineas los tres (lo haces estructural, lo capturas en la mesa, lo registra quien ya está tomando el acta), tu "es solo un poco más" pasa de ser falso por defecto a ser verdadero por diseño. Tu idealismo, otra vez, no es ingenuo sobre el techo; subestima cuánto diseño hace falta para tocarlo.

Y una nota que no te ahorro, porque cierra la balanza que tú mismo planteaste: aun con las cinco contramedidas perfectas, la completitud del 1(b) será **estructuralmente menor** que la del requisito aceptado, porque el aceptado tiene la existencia-obligatoria de su lado y el descarte nunca la tendrá del todo. La meta correcta no es capturar todos los descartes —eso es la trampa—; es capturar con fiabilidad los descartes *conscientes y con impacto* (los que dejaron una cota apretada o un requisito que alguien querrá tocar), y soltar el resto sin culpa. Igual que en I4 no perseguíamos toda "falta de material": perseguíamos la que trazaba a una tolerancia. Mismo principio de discriminación, otra vez: no lo captures todo, captura lo que querrás poder tocar.

¿Quieres que aterricemos el artefacto concreto de captura en la mesa de negociación —la estructura del acta pedido/acordado/eje, quién la posee, cómo fluye al PLM sin recaptura— o prefieres mover el foco a cómo ese dato de descarte, una vez recogido, se conecta con el subproceso 4 aguas abajo (el descarte de requisito que explica la tolerancia apretada tres pasos después)?

#### Cómo hacer fluir la información al PLM sin recaptura

> cómo fluye al PLM sin recaptura?

Lo primero, porque reencuadra la pregunta: **"sin recaptura" no es una optimización de eficiencia aquí, es condición de supervivencia del dato**. Y por una razón específica del 1(b): quien transcribe el acta al PLM necesita el *valor acordado* para hacer su trabajo, y no necesita el descarte para nada. Así que en el paso de traducción la asimetría de existencia (la nº 1) **se reinstala intacta**: el aceptado sobrevive porque es imprescindible, el descarte se cae porque es prescindible —sin mala fe, por pura economía del transcriptor—. La recaptura no es un coste añadido: es un **filtro que selecciona sistemáticamente contra el contrafactual**. Puedes tener una captura perfecta en la mesa y perderla entera en la transcripción del lunes.

De ahí que la regla de diseño sea dura: **no muevas el dato; apúntalo**. Copiar es transcribir aunque lo haga una máquina, y cada copia es una oportunidad de que el campo incómodo no viaje.

**Mecanismo base — un objeto, dos vistas.** La mesa de negociación no produce un acta que luego alimenta un registro; produce **el registro**, y el acta es una *vista renderizada* de él (imprimible, firmable por el cliente). Las filas requisito con sus campos —pedido / acordado / eje del trade-off— son el objeto. El PLM no ingiere prosa: consume las mismas filas. Elimina la traducción no automatizándola, sino haciéndola innecesaria: nunca hubo dos formatos.

**La pieza técnica que lo hace posible: identidad estable desde el minuto cero.** Cada requisito recibe un ID **en la mesa**, antes de existir en ingeniería. Sin ID en origen, cualquier flujo posterior es reconciliación manual por texto ("¿este 'cota de altura' es el mismo que aquel?"), y reconciliar *es* recapturar. Es el detalle sin glamour del que depende todo lo demás; si te lo saltas, ningún grado de integración te salva.

**Dirección del flujo: push desde la mesa, nunca pull desde ingeniería.** Si el ingeniero tiene que ir a leer el acta y volcar, has puesto la captura del descarte en manos de quien no estuvo en la negociación (asimetría 4: no puede reconstruir el porqué) y no cobra nada por ello (asimetría 5). El registro llega solo, ya estructurado, y el ingeniero lo *consume*.

**El degradado realista, por si no hay integración** —que es el caso habitual en pyme y sigue siendo válido—: el PLM guarda **un puntero al requisito, no una copia**. Enlace en vez de duplicado. Fuente única de verdad, cero recaptura, coste de implantación casi nulo. Es peor en ergonomía (hay que abrir el enlace) y mucho mejor en integridad que copiar. Regla práctica: donde no puedas integrar, enlaza; donde no puedas enlazar, asume que el descarte no llegará.

Tres detalles que en la práctica deciden si esto funciona:

**Visibilidad de dos capas.** El eje del trade-off no siempre es compartible con el cliente ("cedimos porque no sabíamos fabricarlo a ese coste"). Si el acta es el objeto y el objeto se firma, o mientes o te callas. Solución: la fila lleva un atributo de visibilidad —lo que se renderiza en el acta del cliente vs. lo que queda interno—. Sin esto, el campo del porqué se autocensura y capturas el *qué* del descarte sin su razón, que es la mitad inútil.

**Congelación en la firma.** El acta firmada fija la versión pública con su sello; el atributo interno, si sigue editable después, es renarrable —el mismo problema del volcado a posteriori del caso 2 de I4—. Versionado con timestamp en el momento del acuerdo, no fecha de última edición.

**Bidireccionalidad.** El enlace tiene que seguir vivo aguas abajo: cuando en el subproceso 4 alguien aprieta una tolerancia y marca "requisito", el puntero va a esa fila —y esa fila lleva pegado si el requisito era firme o una cesión negociada—. Ahí se cierra la cadena que te interesaba: una tolerancia cara colgando de un requisito que resulta que **no era duro, era una posición inicial del cliente que aceptamos sin más**. Ese es el hallazgo que justifica todo el aparato, y solo aparece si el enlace sobrevive los tres saltos sin recaptura.

Un vector que conviene tener fichado: **quien renderiza el acta controla qué queda**. Si la generación de la vista permite omitir filas o campos, la asimetría vuelve por la puerta de atrás, ahora con apariencia de sistema. La vista debe ser una proyección determinista del registro, no una selección editorial.

Síntesis en tus dos ejes: *facilidad* alta en la variante enlace (nada que integrar, solo disciplina de ID y de fuente única) y media en la variante integrada (el coste está en el PLM, no en la captura); *calidad* — el paso sin recaptura no mejora el dato, **impide que se degrade**, que en 1(b) es lo que estaba matándolo. Es defensa de la integridad, no ganancia de contenido.

¿Seguimos con el eslabón que acaba de asomar —el requisito-cesión que explica la tolerancia cara tres pasos después, es decir la cadena 1→4 completa— o cerramos Ingeniería y actualizamos los documentos con lo trabajado en I4 y en 1/4?
