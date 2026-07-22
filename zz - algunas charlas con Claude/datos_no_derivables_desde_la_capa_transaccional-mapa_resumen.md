# Mapa de datos no derivables de la capa transaccional

**Qué es este documento.** Mapa consolidado de los datos operacionales y estratégicos que una empresa genera pero que su capa transaccional (ERP/CRM/PLM/GMAO) es estructuralmente incapaz de registrar. No son campos que falten: son datos que no tienen tabla donde vivir porque pertenecen a la capa decisional, al  ámbito tácito o al contrafactual.

**nota:** Este documento es una especie de resumen de una charla sobre el tema detallada en este otro [documento](datos_no_derivables_desde_la_capa_transaccional-transcripcion_de_la_charla.md)

**Disclaimer:** Este documento es fruto de unas cuantas charlas con [Claude](https://claude.ai). La mayor parte de su contenido lo ha pensado y redactado esa IA.

---

## 1. Por qué se escapan: las cuatro categorías

La capa transaccional registra **cambios de estado de entidades modeladas** (un pedido pasa a servido, un lote a terminado, una factura a cobrada). Lo que se le escapa cae casi siempre en cuatro categorías:

1. **El contrafactual** — lo que no llegó a ocurrir (venta perdida, proveedor descartado, avería evitada, cuasi-accidente).
2. **El criterio** — el porqué de la decisión (capa decisional pura), no su resultado.
3. **La textura temporal entre eventos** — esperas, colas, bloqueos y *su causa*. El sistema da inicio y fin; nunca el motivo del hueco.
4. **Lo no modelado** — retrabajos informales, apaños, coordinación verbal, percepciones. Ocurre *fuera* del sistema porque el sistema no lo contempla.

**Corolario de diseño.** Capturar esto **no** es añadir campos al ERP (eso casi siempre fracasa: produce teatro de cumplimentación). Es otra capa de registro, con otra lógica.

**Distinción de cadencia.** Lo **operacional** (por qué esperó este lote) exige registro ligero, en el punto de trabajo, casi en tiempo real. Lo **estratégico** (por qué perdemos en el segmento X) tolera captura periódica y reflexiva. Mezclar ambos mecanismos rompe los dos.

---

## 2. Áreas

Para cada área: el trío de datos de alto valor + el modo de fallo dominante de su captura.

### Comercial
- **Razón real de pérdida** de una oportunidad (precio/plazo/alcance/producto/relación). Gameable hacia la coartada externa ("precio"), igual que el operario declara "falta de material".
- **Criterio real de decisión del cliente** (qué valora el mercado), visible solo en la negociación y colapsado por el sistema en "condiciones pactadas".
- **Promesas hechas para ganar el pedido** (plazo apretado, flexibilidad) que condicionan producción y no viajan con el pedido.
- *Modo de fallo:* el dato lo genera un agente con **incentivos estructurales para distorsionarlo** (posee la relación como capital personal; la razón de pérdida le exculpa; el forecast se gestiona, no se reporta). Único origen limpio del dato de pérdida: el lado del cliente (win/loss por un tercero).

### Ingeniería
- **Alternativas de arquitectura evaluadas y criterio de descarte** — el PLM ve la decisión, no el espacio de decisión.
- **Hipótesis de cálculo** (carga supuesta, coeficiente, norma, margen deliberado) — sin ellas el resultado es un número mágico intocable.
- **Divergencia taller↔plano** — el taller ajusta y el plano no se corrige; se pierde la verdad sobre el producto.
- *Modo de fallo:* **teatro de documentación**. El rationale exigido como paso de cierre produce justificaciones *a posteriori* ("según buenas prácticas"), peor que el vacío porque simula que el conocimiento está capturado.

### Producción
- **Causa de la espera entre operaciones** (material/cola/utillaje/decisión/operario) — el tiempo de cola es el 80-95% del lead time; se puede medir el cuánto, es imposible derivar el porqué.
- **Causa de la variación de setup** — sin ella no hay SMED posible.
- **Microparadas y velocidad real vs. nominal** dentro del bloque de operación (las pérdidas de disponibilidad y rendimiento del OEE).
- *Modo de fallo:* si se pide al operario **clasificar** la causa, elige la socialmente segura ("falta de material") y nunca "esperé instrucción". Contramedida: categorías no incriminatorias + triangulación contra un sistema que sepa la verdad.

### Compras
- **Criterio de selección** en compra puntual (por qué este proveedor).
- **Incidencia tolerada sin devolución** (llegó tarde, calidad al límite): el coste de "tragar" no se registra.
- **Coste real de gestionar un proveedor problemático** (no se imputa a ese proveedor).
- *Modo de fallo:* el rating lo alimenta el comprador, que tiene relación personal con el proveedor. Mismo patrón que Comercial.

### Mantenimiento
- **Síntoma previo a la avería** que el operario percibe ("iba raro", vibración) antes de que haya orden de reparación.
- **Reparación informal sin orden** que compromete el historial real de fiabilidad del activo.
- **Causa raíz honesta** vs. la que cierra la orden ("se cambió la pieza" no es por qué falló).
- *Modo de fallo:* fuga **sensorial** (conocimiento tácito del operario sobre su máquina), no capturable por evento.

### Calidad
- **No conformidad menor resuelta en línea sin declarar** (la misma fuga que Producción, vista desde el dueño del dato).
- **Concesión/desviación aceptada y su criterio.**
- **Coste real de la no calidad** agregado por causa (se diluye y nunca se agrega).
- *Modo de fallo:* declarar una NC "cuesta" (papeleo, señalamiento) → subdeclaración. Cuanto más burocrático el sistema de calidad, más falso el dato. Dato *compartido* con Producción: ninguno lo posee limpio.

### Logística / Almacén
- **Discrepancia stock teórico vs. real** resuelta ad hoc.
- **Tiempo y causa de espera en carga/descarga** (muelle ocupado).
- **Rotura enmascarada** (faltaba, se cogió de otro lado): borra la señal de que el aprovisionamiento falló — contrafactual que además destruye la evidencia de su propia causa.

### Postventa / SAT / Servicio
- **Causa raíz real del fallo y su retorno agregado** — el patrón de fallos de campo que debería volver a Ingeniería, Calidad y Comercial (bucle I6) y casi nunca vuelve. Cada avería de campo es el único dato de fiabilidad *real* que existe.
- **Incidencias no reportadas** — la resuelta por teléfono sin aviso y, sobre todo, el cliente que se harta y no recompra (contrafactual).
- **Señal de relación desde campo** — el técnico percibe la salud del cliente antes que Comercial.
- *Modo de fallo:* las métricas de SAT (tiempo de resolución, avisos cerrados) empujan a *parchear y cerrar* en vez de diagnosticar: la eficiencia destruye el dato de fiabilidad. El dato limpio no puede depender de quien tiene interés en que el producto parezca fiable.
- *Nota:* capa transaccional de las más pobres; el valor está en el patrón agregado (decisional), no en el aviso individual. Infravalorada por diseño —se ve como coste, no como fuente del dato más caro de obtener de otro modo—.

### RRHH
- **Mapa de conocimiento real** (quién sabe hacer qué de verdad, no la ficha de puesto): sostiene el [bus factor](https://en.wikipedia.org/wiki/Bus_factor).
- **Motivos reales de rotación** (entrevista de salida sincera vs. de trámite).
- **Sobrecarga y conocimiento tácito no visible en fichajes** (el cuello de botella humano al que todos preguntan).
- *Nota:* casi todo su transaccional es administrativo; el valor está entero fuera de él. Es donde se ve el bus factor que los demás departamentos generan.

### Administración / Finanzas
- Casi todo es transaccional. Lo que escapa es el **criterio**: el por qué de una aprobación excepcional, cómo se prioriza qué se paga, coste real de gestionar un moroso,...

### Dirección
- La **estrategia** rara vez tiene capa transaccional: decisiones, supuestos de mercado y su seguimiento. Materia de la Roseta.

**Patrón que cierra las áreas:** en todas las áreas el dato de alto valor es **decisional o tácito**, nunca transaccional. Y donde lo genera un agente con relación personal (Compras→proveedor, Comercial→cliente, Mantenimiento→su máquina) está **sesgado en origen**, no solo ausente.

---

## 3. Interfaces entre áreas

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

**Portantes de verdad (candidatas a captura):** I2, I4, I6 — donde cruza una entidad física y la fuga de información se propaga aguas abajo multiplicándose. I1 ya fichada. I3/I5/I7 son señales tempranas de segundo orden. I8/I9 no se capturan, se *diseñan*.

### Tres lecturas transversales
1. **La causa migra y se renombra** (I4 es el caso canónico). El dato de interfaz no es un evento nuevo: es *el mismo* evento que cada área ve mutilado. Capturarlo es **reconciliar** vistas parciales, algo que ninguna área puede hacer sola.
2. **Casi toda interfaz portante es un [objeto frontera](https://en.wikipedia.org/wiki/Boundary_object)** (Star & Griesemer): un artefacto que debería mantener identidad compartida y admitir reinterpretación local. La fuga ocurre cuando un lado reinterpreta *sin que el artefacto lo absorba* → deja de ser objeto frontera y pasa a ser ficción compartida. Una forma de mitigarla = hacer que el artefacto viaje con su rationale/promesa/desviación pegada.
3. **Las interfaces no son territorio de nadie, y por eso han de ser de la Dirección.** Ahí viven los *undiscussables* de Argyris ("eso lo prometió Comercial", "eso lo mal-diseñó Ingeniería"). Alguien por encima de las dos áreas tiene que poseer la costura: es materia de capa decisional / Roseta, no de captura operacional distribuida.

---

## 4. Procesos transversales

- **Postventa / SAT / Servicio** — analizada como área (sección 2). Se incluye aquí por su rol transversal: es el *sensor de campo* que cierra la interfaz I6 desde fuera, devolviendo a Ingeniería (fallo de campo), Calidad y Comercial (cliente que se enfría) el único dato de fiabilidad *real* que existe.
- **Planificación / S&OP como proceso propio** — replanificar es acto decisional denso: por qué cambió el plan, qué se sacrificó, qué plan alternativo se descartó. Equivalente en operaciones al espacio de decisión evaporado de Ingeniería.
- **Seguridad / near-miss** — el cuasi-accidente: contrafactual puro, mismo modo de fallo que la razón de pérdida (quien lo reporta puede quedar señalado).
- **Parametrización de sistemas / TI** — no genera dato: decide *qué se puede registrar*. Quien parametriza fija política sin hacerla explícita (ver I9).

Otros *procesos transversales condicionados al tipo de empresa (no universales)*: por ejemplo, I+D/Proyectos (en ETO absorbe a Ingeniería y Planificación) y Medioambiente (sube de rango en proceso continuo).

---

## 5. Síntesis operativa

- El dato de alto valor es siempre **decisional, tácito o contrafactual** — nunca transaccional.
- Donde el dato lo genera un agente con vinculación personal en él, está **sesgado en origen**: cualquier captura acoplada a ese agente hereda su sesgo. Es mejor triangular o desacoplar.
- La captura acoplada al **cierre de tarea** produce coartadas (teatro), no conocimiento. El registro sincero se hace en el momento de dudar, no en el de cerrar.
- Las fugas más ricas viven en las **interfaces**, no dentro de las áreas — y son territorio de nadie.
- No sobre-instrumentar: embeber la captura en un artefacto de gestión ya existente (p. ej. un [flow board](https://www.susosise.es/documentos/Lista_de_tareas_priorizada_en_cabeza.pdf) captura la causa de espera sin acto de registro adicional) en lugar de añadir un parte extra encima.
