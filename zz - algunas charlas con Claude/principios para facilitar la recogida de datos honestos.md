# Principios para facilitar la recogida de datos honestos


## 1 Los tres bloqueos

Un dato no se recoge honesto por tres razones distintas, y cada una exige una palanca propia. Confundirlas lleva a aplicar la palanca equivocada:

| Bloqueo | Qué es | Palanca |
|---|---|---|
| **Motivo** | Registrar es autoinculpatorio | Cultura justa, o ingeniería que la haga innecesaria (triangulación) |
| **Fricción** | Registrar cuesta tiempo y no le retorna nada al que registra | Diseño de baja fricción |
| **Epistémico** | No está claro si esto cuenta como el fenómeno | Criterios de clasificación claros |

La cultura justa (buscar causas/soluciones en lugar de quien/culpables) solo disuelve la primera de las razones. Confianza e instrumentación son **sustitutos**: la confianza rinde más donde no se pudo instrumentar.

## 2 Gateo: la calidad viene de la involuntariedad

- Un dato vale lo que vale su **eslabón más tecleado a mano**. La intervención que más sube la calidad no es preguntar mejor: es *gatear el evento débil*.
- El gate puede ser digital (escaneo en muelle, sello de sistema) o **físico** (etiqueta que viaja con el lote, plano marcado). Lo que importa no es el soporte, sino que borrar la señal exija un acto visible y no un simple no-teclear.
- Corolario: "tener sistemas digitales" es necesario pero no suficiente. La pregunta útil no es *si* hay sistema, sino **qué eventos gatea**.
- El registro volcado *a posteriori* pierde la involuntariedad: el sello deja de significar cuándo pasó y pasa a significar cuándo se contó. Para prevención es inservible; abre además una ventana de renarración.

## 3 Reparto de ejes: la máquina clasifica, el humano adjudica

- **Eje objetivo → máquina.** Todo lo derivable se computa (deltas, desviación respecto al default, disponibilidad real). Cada campo que pides pudiendo derivarlo es fricción autoinfligida.
- **Eje causal → humano.** Solo el *porqué*, aquello que no tiene rastro involuntario posible.
- El sistema **preensambla la hipótesis** y el humano solo confirma/niega y elige causa. Adjudicación, no redacción: redactar es caro y no agregable.

## 4 Baja fricción (cinco reglas)

1. No preguntes lo derivable.
2. Adjudicación, no redacción. Presupuesto: <5 segundos, ≤2 decisiones. Si es un formulario, has fracasado.
3. Captura en el gesto natural, colgada de un acto que ya se ejecuta — nunca en un paso aparte que compite con el trabajo real.
4. **Dispara solo cuando importa.** Preguntar solo cuando se detecta posibilidad real de problemas, baja el volumen dos órdenes de magnitud y *sube* la tasa de respuesta: la escasez de la pregunta es mecanismo de calidad, no de comodidad.
5. **Devuelve valor al que registra.** El único cálculo que cada cual hace es *coste de registrar < coste de no registrar, para mi*. Si el beneficiario es otro (o el yo-futuro de otro), el registro no se sostiene: hay que devolverle algo a la persona que registra o reasignar el registro a quien no lo siente como extra (porque es su trabajo registrar eso).

## 5 Momento de captura

- **En el instante de dudar, no en el de cerrar.** El rationale exigido en un gate de cierre produce racionalización *a posteriori*, no conocimiento — y ese fallo es de *timing y fricción*, no de miedo: sobrevive intacto a la cultura justa.
- Donde el dato se evapora en minutos (una negociación, una decisión de diseño), la ventana de captura es estrecha: hay que capturar *en la mesa*, no en la transcripción posterior.

## 6 Criterios de clasificación

1. **Reglas predefinidas claras** ([bight-line rule](https://en.wikipedia.org/wiki/Bright-line_rule)), no juicio en el momento: la persona nunca decide si algo cuenta como anomalía; lo decide una regla pactada de antemano.
2. Categorías **MECE, lista cerrada corta**, definidas por estado observable o por decisión — **nunca por intención inferida**. Elegir, no interpretar.
3. Sin texto libre en el eje analizable (un campo libre opcional para el matiz, podria tener sentido).
4. **Cada categoría, falsable**: auditable contra un rastro o exigiendo un puntero barato a una justificación (enlazar la comunicación, nombrar la feature, citar la norma). Una categoría no contrastable es coartada cómoda incluso sin mala fe.
5. **Ninguna categoría puede ser la salida fácil universal.** Equilibrar el *coste de selección*, no solo la cobertura semántica.
6. **Invertir la fricción a propósito:** la categoría honesta-costosa (cota defensiva, error propio, práctica no regulada) debe ser la **más barata** de marcar; las categorias externas y socialmente seguras son las que exigen justificación expresa. Sin esto, la causa externa se sobreelige siempre — "precio", "falta de material", "cambio solicitado por el cliente" son el mismo patrón de categoria socialmente segura.

## 7 Discriminación: no lo captures todo

- Captura **lo que querrás poder revisar o tocar en un futuro**: lo que restringe grados de libertad (la tolerancia estrecha estricta, el requisito firme) o lo que tiene exposición aguas abajo; aquello que puede resultar difícil de revisar sin información de por qué se fijó al valor que tiene. Perseguir la completitud (capturar todo) satura el canal y lo mata.
- El **rationale no se captura para documentar, sino para preservar grados de libertad**: un valor cuyo porqué nadie conoce es intocable, se congela y arrastra su sobrecoste. El beneficio no es el archivo en sí: es la revisabilidad que facilita.

## 8 Fluir sin recapturar

- Cada transcripción entre soportes es un **filtro que selecciona contra el dato incómodo**: el transcriptor necesita el valor aceptado para trabajar y no necesita el descarte para nada. Se cae sin mala fe.
- No muevas el dato: **enlázalo**. Un objeto, varias vistas. Identidad estable (ID en origen) desde el primer instante; *push* desde donde se genera, nunca *pull* desde quien no estuvo. Donde no puedas integrar, **enlaza**; donde no puedas enlazar, asume que el dato incómodo no llegará al nuevo registro.

## 9 Métricas que destruyen su propio dato

Patrón recurrente en todas las áreas: la métrica que premia la ausencia del fenómeno suprime su **reporte**, no el fenómeno — y la organización se vuelve ciega justo cuando cree que va bien. Casos: días sin accidentes, exactitud de inventario (cuadrar el número en vez de entender el descuadre), disponibilidad y tiempo de resolución (parchear en vez de diagnosticar), cumplimiento del plan (planes laxos o replanificados a diario), cambio informal tratado como incumplimiento,...

Corolario para procesos con canal formal e informal: la métrica útil no es el volumen de ninguno de los dos, sino **su proporción** — mide si el proceso formal está bien calibrado, no si la gente es disciplinada. Y cuando el canal informal es una respuesta racional al coste del formal, la palanca no es capturar mejor el informal: es **abaratar el formal** hasta que el informal deje de ser atractivo.

---

# Síntesis operativa

- El dato de alto valor es siempre **decisional, tácito o contrafactual** — nunca transaccional.
- Donde lo genera un agente con implicación personal (repercusiones para sí), está **sesgado en origen**: la captura acoplada a ese agente hereda su sesgo. Triangular o desacoplar.
- La captura acoplada al **cierre de tarea** produce coartadas (teatro), no conocimiento. El registro sincero se hace en el momento de dudar, no en el de cerrar.
- Las fugas más ricas viven en las **interfaces**, no dentro de las áreas — y son territorio de nadie.
- No sobre-instrumentar: embeber la captura en el artefacto de gestión que ya existe, en lugar de añadir un parte extra encima.
