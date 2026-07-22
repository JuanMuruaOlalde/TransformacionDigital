# Charla: recopilación de datos operacionales y estratégicos

Datos que no se pueden derivar de la capa transaccional existente. Análisis detallado, proceso a proceso, área a área.

---

## Encuadre inicial

Algunos aspectos que se plantean no son ortodoxos desde el punto de vista empresarial actual; se trata precisamente de eso, de encontrar nuevas maneras de hacer las cosas.

Cada herramienta / técnica / procedimiento se analiza y debate desde:
- Su efectividad para resolver una problemática específica.
- El esfuerzo o coste de implementarla en una empresa o grupo de trabajo.
- Las posibles oposiciones de personas acostumbradas a otra forma de trabajar.
- Posibles maneras de sabotearla o manipularla para alcanzar los objetivos o métricas establecidas saltándose la filosofía de la herramienta de forma que se menoscabe su efectividad.

**Modo de trabajo acordado:** análisis técnico directo. Barrido rápido de todos los procesos primero; profundización proceso a proceso después.

*notas:* 
- Cuando en este documento se cita a la `Roseta`, se está refiriendo a https://www.susosise.es/documentos/roseta_de_prioridades.pdf y a una charla anterior que tuve con Claude sobre ella. 
- Sucede algo parecido cuando cita un `flow board`, que se refiere a https://www.susosise.es/documentos/Lista_de_tareas_priorizada_en_cabeza.pdf y a otra charla anterior con Claude sobre ella.
- Cuando en este documento cita un `objeto frontera`, se está refiriendo a https://en.wikipedia.org/wiki/Boundary_object (Star & Griesemer); algo que sacó a colación el propio Claude en charlas anteriores.

**Disclaimer:** Este documento es fruto de unas cuantas charlas con [Claude](https://claude.ai). La mayor parte de su contenido lo ha pensado y redactado esa IA.

---

## El hilo conductor

La capa transaccional registra **cambios de estado de entidades modeladas** (un pedido pasa a servido, un lote a terminado, una factura a cobrada). Lo que se le escapa no es accidental, es estructural: no tiene tabla donde vivir. Cae casi siempre en cuatro categorías:

- **El contrafactual**: lo que no llegó a ocurrir (venta perdida, proveedor descartado, avería evitada).
- **El criterio**: el porqué de la decisión —capa decisional pura—, no su resultado.
- **La textura temporal entre eventos**: esperas, colas, bloqueos y *su causa*. El ERP, con suerte, da inicio y fin; nunca el motivo del hueco temporal.
- **Lo no modelado**: retrabajos informales, apaños, (des)coordinación verbal, percepciones. Ocurre precisamente *fuera* del sistema porque el sistema no lo contempla.

**Corolario:** capturar esto **no** es añadir campos al ERP (eso casi siempre fracasa). Es otra capa de registro, con otra lógica.

---

## Barrido inicial (área a área)

**Comercial** — Motivo real de pérdida de una oportunidad (precio/plazo/alcance/relación); el ERP guarda el pedido ganado, no el perdido ni el porqué. Concesiones informales al cliente (promesas de plazo/flexibilidad) que condicionan producción y no viven en ningún campo.

**Compras** — Por qué este proveedor y no otro en una compra puntual. Incidencias toleradas sin devolución formal (llegó tarde pero se aceptó, calidad al límite): el coste de "tolerar" no se registra.

**Producción** — La *causa* de cada espera entre operaciones (falta de material, de utillaje, de decisión, cola). Microparadas y reajustes que no llegan a parte, y el criterio de secuenciación del encargado.

**Mantenimiento** — Síntomas previos a la avería que el operario percibe ("iba raro", vibración) y que no se capturan hasta que hay una orden correctiva. Reparaciones informales sin orden de trabajo.

**Calidad** — No conformidades menores resueltas en línea sin registro. Concesiones/desviaciones aceptadas y su justificación; reclamaciones verbales que no escalan a formal. Coste de no calidad agregado por causa. Modo de fallo: declarar una NC cuesta → subdeclaración; cuanto más burocrático, más falso. Dato compartido con Producción: ninguno lo posee limpio.

**Logística/Almacén** — Discrepancias de stock resueltas ad hoc. Tiempos y causas de espera en carga/descarga; roturas "salvadas" tirando de otra existencia.

**Ingeniería/Diseño** — Rationale de las decisiones de diseño y alternativas descartadas. Cambios de taller respecto al plano.

**Administración/Finanzas** — Casi todo es transaccional; lo que escapa es el criterio: el por qué de una aprobación excepcional, cómo se prioriza qué se paga, el coste real de gestionar un moroso.

**Dirección** — La estrategia rara vez tiene "capa transaccional": decisiones, supuestos de mercado y su seguimiento. Aquí encaja la Roseta.

**RRHH.** Casi todo su transaccional es administrativo; el valor está entero fuera.  Mapa de competencias real(quién sabe hacer qué de verdad); causa real de rotación; sobrecarga no visible en los fichajes. Es donde se ve el bus factor que los demás áreas generan.

---

## Profundización — Producción (flujo físico de una orden)

**1. Lanzamiento / secuenciación real.** El ERP tiene la orden y su fecha. Escapa el *criterio de secuencia real* del encargado, que diverge del plan. El sistema registra que se hizo C; no que se saltó el plan de hacer A y B, ni el por qué de ese cambio.

**2. Preparación / cambio.** Escapa la *causa de la variación*: cambio estándar 20 min, real 55 min porque faltaba una brida. Sin el porqué no hay [SMED](https://en.wikipedia.org/wiki/Single-minute_exchange_of_die): optimizas un tiempo cuya varianza no entiendes.

**3. Operación / transformación.** Registra inicio/fin y buenas/rechazadas. Escapan las *microparadas dentro del bloque* y la velocidad real vs. nominal (disponibilidad y rendimiento del [OEE](https://en.wikipedia.org/wiki/Overall_equipment_effectiveness). El ERP ve el bloque, nunca su interior.

**4. Espera entre operaciones — el núcleo.** El tiempo de cola *sí* es derivable (fin de N, inicio de N+1). La causa no lo es de ningún modo, y las causas exigen acciones opuestas: material, cola de máquina, utillaje, decisión, operario. El ERP colapsa las cinco acciones en "tiempo entre operaciones". Como la cola es el 80-95% del lead time, es *el* dato de producción: se mide el cuánto, es imposible saber el porqué, y sin el porqué el cuánto es inaccionable.

**5. Autocontrol en proceso.** Escapan la [NC](https://en.wikipedia.org/wiki/Nonconformity_(quality)) menor corregida en línea sin declarar y la deriva que el operario detecta *antes* de sacar pieza mala.

**6. Movimiento interno.** Normalmente no registra nada. Muda pura e invisible.

**7. Cierre / declaración.** Escapa la ficción del propio acto: imputación "cuadrada" a fin de turno. El cierre no describe lo que pasó realmente, describe lo que cuadra.

**Juicio.** Trío de alto valor: **4 (causa de espera), 2 (causa de variación de setup), 3 (microparadas)**. El 6 no se mide, se elimina por diseño de layout. El 1 es materia de la Roseta.

**Manipulación (subproceso 4).** Pedir al operario *clasificar* la causa es manipulable: siempre elegirá la socialmente segura ("falta de material") y nunca algo como "esperé instrucción". Contramedida: categorías no incriminatorias, o triangular con otro sistema (el sistema de materiales sabe si el material faltaba de verdad).

**Encaje con el [flow board](https://www.susosise.es/documentos/Lista_de_tareas_priorizada_en_cabeza.pdf).** El parte separado muere por fricción. El tablero *ya es* el mecanismo: una tarea parada en una zona con etiqueta de motivo captura el dato 4 sin acto de registro adicional. En single-piece flow la cola debería tender a cero; medir su causa es el diagnóstico de por qué el flujo no fluye.

---

## Profundización — Ingeniería (flujo de una decisión de diseño)

Cambio de naturaleza: aquí lo que se fuga es *conocimiento* —el porqué de las decisiones—, y su pérdida es más cara porque no se recupera.

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

---

## Profundización — Comercial (flujo de una oportunidad por el [embudo](https://en.wikipedia.org/wiki/Purchase_funnel))

Cambio decisivo: aquí se fuga **el contrafactual** y aparece por primera vez con fuerza un factor —**el dato lo genera un agente con incentivos estructurales para distorsionarlo**—. El CRM está envenenado en origen.

**1. Captación / prospección.** Escapa el universo de prospectos *no* contactados y por qué. El comercial trabaja las cuentas cómodas; el segmento que nadie toca es invisible.

**2. Cualificación (go/no-go).** Escapa el *criterio* de perseguir o soltar. ¿Se soltó por mal encaje real o porque era difícil? Indistinguible desde el sistema.

**3. Oferta / presupuesto.** Bien instrumentado. Escapan las *concesiones e hipótesis del precio* y el plazo/flexibilidad prometidos *verbalmente*.

**4. Negociación — núcleo.** Escapa lo denso: en qué apretó el cliente, qué concedimos y por qué, qué ofrecía el competidor, el *criterio real de decisión del cliente*. El evento donde aprendes qué valora el mercado, colapsado en "pedido: estas condiciones".

**5. Cierre ganado/perdido — dato central.** El ganado se registra entero; el perdido casi nunca con su razón real. Paralelo literal con Producción: el comercial declara **"precio"** (causa externa, no es culpa mía) igual que el operario declara "falta de material". Es el dato más valioso y el más falseado.

**6. Traspaso a producción — las promesas.** Escapan las *promesas hechas para ganarlo* (plazo apretado, flexibilidad). Producción hereda un compromiso que nunca vio negociar: es el origen del pedido que "se cuela" en la planificación (Producción 1).

**7. Seguimiento de cuenta.** Escapan la salud de la relación y la *señal temprana de fuga* ("el cliente está tibio"). Análogo al síntoma previo a la avería, aquí previo a la pérdida del cliente.

**Juicio.** Trío: **5, 4, 6**. Asimetría: aquí las fugas están *activamente distorsionadas* por un agente con incentivos propios, y la contramedida del material en Producción (triangular contra un sistema que sabe la verdad) *no existe*: solo el cliente sabe por qué dijo no, y esa información no está en tu ERP.

**Manipulación (centro del área).** Tres incentivos estructurales: (1) posee la relación como *capital personal* → cuanto más opaco el CRM, más insustituible él; (2) la razón de pérdida le exculpa; (3) el forecast se *gestiona* (sandbagging, hockey stick). Un CRM exigido como trámite produce **teatro comercial**, con incentivo económico detrás. Único origen no contaminado del dato 5: entrevista win/loss al cliente, por alguien distinto del comercial que perdió.

**Encaje.** (a) Comercial es el área más *decisional*: meter campos en la capa transaccional es un error de categoría. (b) El criterio de cualificación (2) es posicionamiento estratégico → Roseta; la razón de pérdida agregada por segmento (5) la alimenta. (c) El pedido cruzando a Producción (6) es un objeto frontera roto (cruza sin las promesas). (d) Comercial es dominio de captura **estratégica** (periódica, reflexiva), no de captura operacional en tiempo real.

---


## Profundización — Postventa / SAT / Servicio (flujo de una incidencia de campo)

Único punto donde la empresa toca la realidad de uso del producto. Doble fuga: dato de producto (fiabilidad real) y dato de relación. Capa transaccional de las más pobres (a menudo un teléfono y un cuaderno). Es un *sensor de campo*: cierra la interfaz I6 desde fuera.

**1. Recepción / apertura de aviso.** Escapa el síntoma *en palabras del cliente* vs. la categoría que impone el sistema, y la incidencia resuelta por teléfono sin abrir aviso. Contrafactual de fondo: las incidencias *no reportadas* (el cliente que se harta y no recompra).

**2. Diagnóstico.** Escapa la *causa raíz real* vs. la acción que cierra el aviso. Análogo a Mantenimiento, sobre el producto vendido.

**3. Intervención.** Registra repuestos, horas, desplazamiento. Escapa el *apaño en campo* no previsto (Ingeniería 7, en casa del cliente).

**4. Cierre.** Escapa si quedó *resuelto* o solo parcheado, y la satisfacción real vs. el aviso cerrado (eco de Producción 7).

**5. Retorno del conocimiento — eslabón crítico (I6).** El *patrón agregado* de fallos de campo que debería volver a Ingeniería (rediseño), Calidad (control) y Comercial (qué prometer). Casi nunca vuelve. Cada avería de campo es el único dato de fiabilidad *real* que existe y se disipa aviso a aviso.

**6. Señal de relación.** El técnico percibe la salud del cliente antes que Comercial (conecta con Comercial 7 / I7).

**Trío:** 2+5 (causa raíz real y su retorno agregado), 1 (incidencias no reportadas), 6 (señal de relación desde campo).

**Manipulación.** Las métricas de SAT (tiempo de resolución, avisos cerrados/día) empujan a *parchear y cerrar* en vez de diagnosticar: la eficiencia destruye el dato de fiabilidad. Si el SAT depende de quien vendió, hay incentivo a no escalar el fallo sistémico. El dato de fallo de campo limpio no puede depender de quien tiene interés en que el producto parezca fiable.

**Encaje.** Nodo de I6 (bucle largo). El aviso es transaccional; el valor —decisional— está en el patrón agregado. Cadencia mixta. Postventa está infravalorada por diseño: se ve como coste (reparar), no como fuente del dato más caro de obtener por otra vía (fiabilidad real).

---

## Profundización — Compras (flujo de una necesidad de aprovisionamiento)

Espejo de Comercial: allí la empresa persuade hacia fuera; aquí es persuadida desde fuera. Mismo patrón de dato sesgado en origen, invertido, con un agravante.

**1. Detección de necesidad.** Escapa quién decide qué se necesita y con qué antelación. Sobre todo la **compra urgente**, que destruye poder de negociación y cuya causa (fallo de previsión aguas arriba) no se imputa a nadie.

**2. Selección / homologación — núcleo decisional.** Escapa el *criterio real* (precio/calidad/inercia/comodidad) y las alternativas no consultadas. Análogo al go/no-go de Comercial 2 y a Ingeniería 2.

**3. Negociación.** Espejo de Comercial 4 desde el otro lado: qué palanca se usó, qué se concedió, qué condición verbal quedó fuera del pedido.

**4. Recepción / incidencia tolerada.** Aceptada sin devolución formal (llegó tarde, calidad al límite). El coste de "tragar" no se imputa al proveedor.

**5. Evaluación de proveedor.** Escapa el rating real vs. el formal y el coste oculto de gestionar al problemático. Lo alimenta el comprador, que tiene la relación.

**Trío:** 2 (criterio de selección + alternativas no consultadas), 4 (incidencia tolerada), 1 (urgencia que enmascara fallo de planificación).

**Manipulación —agravante—.** Comercial tiene *sesgo cognitivo*; Compras puede tener **conflicto de interés material** (comisiones, favores, captura). El "por qué este proveedor" es justo el dato que un comprador capturado quiere opaco: la opacidad puede ser *diseño*, no descuido. Asimetría cruel con Comercial: allí el dato limpio venía del cliente; aquí la contraparte —el proveedor— es *cómplice* del dato opaco, no víctima. No hay fuente externa limpia para el criterio; solo es triangulable lo objetivo (¿cumplía especificación? ¿histórico real de incidencias?). Mayor exposición a manipulación por interés propio de todas las áreas.

**Encaje.** El criterio de homologación (coste/plazo/calidad/riesgo) → Roseta. La incidencia tolerada (4) es el **origen de la cadena I4**: Compras tolera → Almacén enmascara → Producción sufre como "falta de material".

---

## Profundización — Logística / Almacén (flujo físico y su reconciliación con el registro)

Caso atípico: el **más rico** en capa transaccional (WMS). Su fuga no es que falte registro, es que el registro **diverge de la realidad física en silencio**. El área donde el ERP *cree* saber la verdad y no la sabe.

**1. Recepción.** Escapa la discrepancia albarán/pedido/real resuelta ad hoc, y si la comprobación de calidad se hizo o se dio por buena.

**2. Ubicación.** Escapa la ubicación real vs. teórica (se puso donde había hueco). El WMS cree saber dónde está cada cosa; se descubre la divergencia solo al buscar.

**3. Conservación / obsolescencia.** Escapa el stock "muerto" que figura como disponible: capital inmovilizado que envejece sin evento. Contrafactual.

**4. Picking / rotura enmascarada — el dato que destruye su propia evidencia.** Faltaba, se cogió de otro lado, se salvó la entrega. Al resolver el problema se elimina la prueba de que aprovisionamiento falló. Eslabón central de I4.

**5. Expedición / muelle.** Espera de carga/descarga y su causa. Textura temporal, análogo a Producción 4 en el borde externo.

**6. Inventario / recuento — el momento de la verdad.** Escapa el *patrón* de las discrepancias (dónde y por qué se descuadra). El recuento corrige el número y borra la causa.

**Trío:** 4 (rotura enmascarada), 2 (fiabilidad del registro de ubicación), 5 (espera de muelle).

**Manipulación.** El "ajuste de inventario" es el sumidero donde se entierran sin diagnóstico los errores de todo el proceso. El KPI de exactitud empuja a *cuadrar el número, no a entender el descuadre*: premia tapar la evidencia.

**Encaje.** Directo con el modelo de flujo financiero dinámico vs. balance estático: el almacén es donde el "inventario" del balance oculta el flujo real (lo que se mueve vs. lo muerto, 3). En Goldratt, el stock muerto es inventario que no fluye, capital inmovilizado invisible que el balance cuenta como activo. El material con su etiqueta es un objeto frontera: cuando la ubicación real diverge sin que el registro lo absorba, el WMS pasa a ficción compartida.

---

## Profundización — Mantenimiento (sensor tácito-predictivo del activo)

El mejor instrumentado (GMAO, [CMMS](https://en.wikipedia.org/wiki/Computerized_maintenance_management_system)), pero su valor está donde el GMAO no llega. Gemelo interno de Postventa: allí se diagnostica el producto en campo, aquí el activo en casa. Contrafactual dominante (como Seguridad): la avería *evitada* no deja rastro.

**1. Conocimiento del activo.** Escapa el mapa tácito de "qué máquina es delicada, cuál aguanta", que vive en el veterano. Bus factor sobre activos.

**2. Síntoma débil / deriva — núcleo predictivo.** Percepción sensorial temprana ("suena raro, vibra, huele"). Contrafactual predictivo, análogo al near-miss y al enfriamiento del cliente. No hay evento hasta que es tarde.

**3. Fallo incipiente detectado.** Escapa la decisión "¿aguanta hasta la parada programada o paro ahora?" y su criterio (producción vs. riesgo). Decisional.

**4. Reparación.** Escapa la reparación informal sin orden de reparación (arreglado en 5 min, sin parte) que borra el historial de fiabilidad, y el apaño provisional que se vuelve permanente.

**5. Causa raíz.** Escapa el diagnóstico honesto vs. "se cambió la pieza". Análogo a Postventa 2 y Seguridad 6.

**6. Preventivo / predictivo.** Escapa si el plan se ejecuta o se firma sin hacer (*pencil whipping*), y si la frecuencia responde a datos reales o a inercia.

**Trío:** 2 (síntoma sensorial previo), 5 (causa raíz real), 4 (reparación informal que borra el historial).

**Manipulación.** Tres a la vez: preventivo firmado sin ejecutar (teatro de documentación sobre checklist); KPI de disponibilidad que empuja a parchear en vez de diagnosticar (como Postventa); reparación informal no declarada porque declararla admite trabajo fuera de proceso (subdeclaración, como la NC menor).

**Encaje.** El GMAO trata todas las averías igual, pero en Goldratt no lo son: una avería en la **restricción** cuesta throughput de toda la planta; en un no-cuello es casi gratis. El dato ausente no es un atributo de la máquina, es su **criticidad de flujo** (posición en el flujo), que ninguna orden de trabajo contiene. Como Seguridad, el contrafactual domina: quien mantiene bien produce *no-eventos* (averías evitadas, invisibles). La fuga sensorial (2) es tácita por definición (Polanyi): no capturable por evento, solo por presencia.

---

**Nota de cierre (I4 completa).** Con Compras, Logística y Mantenimiento quedan analizados los **tres tramos de I4**: Compras (origen: tolera) → Almacén (enmascara) → Producción (sufre). La costura más traicionera del mapa tiene ya sus tres piezas por separado; queda reconciliarlas, que es lo que ninguna de las tres áreas puede hacer sola.


---
## Revisión del alcance — ¿faltaban procesos por analizar?

**Punto ciego estructural:** los barridos por área no ven las **interfaces**. La capa transaccional está organizada por área, así que su ceguera máxima está en las costuras que no pertenecen a nadie. Síntoma: dos de los tres análisis terminaron en una interfaz (Comercial→Producción, Ingeniería→taller). Ahí viven los *undiscussables* de Argyris.

**Procesos omitidos que importan:**
- **Planificación / S&OP como proceso propio** — replanificar es acto decisional denso (qué se sacrificó, qué plan se descartó). Equivalente al espacio de decisión evaporado de Ingeniería.
- **Seguridad / near-miss** — cuasi-accidente: contrafactual puro, mismo modo de fallo (quien reporta queda señalado).
- **Parametrización / TI** — no genera dato, decide *qué se puede registrar*. Es un vector de política implícita.

Otros *procesos transversales condicionados al tipo de empresa (no universales)*: por ejemplo, I+D/Proyectos (ETO) y Medioambiente (proceso continuo).


---

## Interfaces (entre áreas)

La capa transaccional está organizada por área, así que su ceguera máxima está en las **costuras entre áreas**, que no pertenecen a nadie. Se mapean solo las costuras **portantes**: costuras por las que cruza una entidad real y en las cuales el traspaso tiene dato propio que ningún área reclama.

| # | Interfaz | Qué cruza | Qué se pierde |
|---|----------|-----------|---------------|
| **I1** | Comercial → Planificación/Producción | El pedido | Las promesas (plazo, flexibilidad). Origina la perturbación del pedido "que se cuela" en la planificación. |
| **I2** | Ingeniería → Producción/Taller | El plano/modelo | Divergencia taller→plano *y* restricción de fabricación que Ingeniería no conoció ([DFM](https://en.wikipedia.org/wiki/Design_for_manufacturability) que no ocurrió). Bidireccional. |
| **I3** | Producción → Calidad | La pieza y su conformidad | NC menor resuelta en línea: dato compartido y por eso huérfano. |
| **I4** | Compras → Almacén → Producción | El material | La misma causa recorre tres áreas cambiando de nombre: incidencia tolerada → rotura enmascarada → espera "falta de material". |
| **I5** | Producción ↔ Mantenimiento | La máquina y su estado | El síntoma previo que ve quien *usa* el activo no llega a quien lo *cuida* antes de la avería. |
| **I6** | Producción/Campo → Postventa → Ingeniería | El producto y su comportamiento real | El bucle largo: modo de fallo de campo que debería cerrar hacia diseño y calidad. Sale y vuelve a entrar en la empresa. |
| **I7** | Comercial ↔ Postventa | La cuenta | El enfriamiento del cliente que Postventa detecta antes que Comercial. |
| **I8** | Planificación ↔ todas | (hub, no costura) | La interfaz hecha proceso: planes descartados y trade-off al meter la urgencia. Nodo donde convergen I1, I4, I5. |
| **I9** | Parametrización/TI → todas | (meta-interfaz) | No cruza una entidad: cruza la *forma* de todas. Al fijar qué campos existen, decide qué fugas son incapturables. Vector de política implícita. |

**Lecturas transversales:**
1. **La causa migra y se renombra** (I4). Capturarla es *reconciliar* vistas parciales, algo que ninguna área puede hacer sola.
2. **Casi toda interfaz portante es un objeto frontera** (Star & Griesemer). La fuga ocurre cuando un lado reinterpreta sin que el artefacto lo absorba → ficción compartida. Reparar = el artefacto viaja con su rationale/promesa/desviación pegada.
3. **Las interfaces son territorio de nadie, y por eso han de ser de la Dirección.** Undiscussables de Argyris. Alguien por encima de las dos áreas tiene que poseer la costura → capa decisional / Roseta.

**No sobre-instrumentar:** portantes de verdad son **I2, I4, I6**. I1 ya fichada. I3/I5/I7 son señales de segundo orden. I8/I9 no se capturan, se diseñan.

---

## Ideas generales / próximos pasos

**Patrón:** en las áreas el dato de alto valor estratégico es **decisional o tácito**; y allá donde lo genera/captura un agente con implicación personal en él, suele estar **sesgado en origen**.

**Distinción de cadencia:** lo **operacional**(transaccional) exige registro ligero, en el punto de trabajo, casi en tiempo real. Lo **estratégico** tolera captura periódica y reflexiva. Mezclar ambos mecanismos suele romper los dos.


- Candidatos a profundización: **Comercial 5** (win/loss desacoplado), **Ingeniería 2** (alternativas vía Roseta), **Interfaz I4** (la causa que se renombra por tres áreas).
