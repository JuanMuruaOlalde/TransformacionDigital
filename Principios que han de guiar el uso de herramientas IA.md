# Principios que han de guiar el uso de herramientas IA

## Responsabilidad

> Se use la herramienta que se use, la persona humana que la usa es la responsable.

La persona humana es la responsable de **mantener los estándares de calidad y seguridad pertinentes.**

Para ello, la persona debe **revisar y comprender los resultados obtenidos**.

Puede no saber cómo funciona internamente la herramienta. Pero sí que ha de saber manejarla y saber interpretar/revisar/comprender los resultados que produce.

Si la herramienta genera tal volumen de resultados que hacen prácticamente muy difícil la verificación manual de todos ellos. La persona debe ingeniárselas para encontrar un procedimiento de trabajo que posibilite dicha verificación; (muy posiblemente incorporando otras herramientas que asistan en la verificación).

## Transparencia

> Cuando la IA contribuya sustancialmente (*) a algo. Se debe indicar cómo ha sido esa contribución, de forma clara e inequívoca.

(*) Contribuir sustancialmente es participar en la generación, estructuración o comprensión/diseño/concepción. Es decir, influenciar más allá de meras adaptaciones editoriales u operaciones mecánicas.

Para reportar la contribución, como mínimo se ha de incluir una firma del estilo de
- Autor/a/es: *nombre_y_apellidos_de_las_personas*
- Asistido/a/s por: *nombre_y_versión_de_los_modelos_o_herramientas_IA*

Pero es mejor si se incluye un párrafo resumiendo en qué partes y para qué tareas se han utilizado qué herramientas IA. Por ejemplo: [Rust LLM use disclosure guidelines](https://rustc-dev-guide.rust-lang.org/llm-guidance/writing.html#disclosure-guidelines)

## Trabajo propio, aportar valor

A la hora de enviar nuestra contribución a alguien. Se aplica lo que suelen comentar en algunos foros: "*si quisieramos la opinión de la IA tal cual, se la pediriamos nosotros mismos*".

## Agentes IA

> Un agente IA puede realizar **acciones** de parte de la persona que lo utiliza.

Cuando se usen agentes IA, **la persona que los utiliza debe asegurarse de** que:

- Los agentes están adecuadamente protegidos frente a instrucciones maliciosas de terceros que pudieran afectar a su funcionamiento.

- Los agentes tienen acceso solo a las herramientas que necesiten para el trabajo, y no a más.

- Los agentes tienen acceso solo a los datos/documentos que necesiten para el trabajo, y no a más.

- Hay suficientes puntos de parada, verificación y aprobación humana a lo largo del trabajo. Sobre todo antes de acciones irreversibles (*) o potencialmente peligrosas (**).

(*) Acciones irreversibles tales como, por ejemplo, enviar comunicaciones o entregar resultados.

(**) Acciones potencialmente peligrosas tales como, por ejemplo, alterar datos sensibles o modificar procesos.

# Resumen final

Lo dicho al principio: *Se use la herramienta que se use, la persona humana que la usa es la responsable.*

> Si una persona no puede revisar y comprender los resultados obtenidos con cierta herramienta en cierto trabajo. Si no puede responder a cuestiones (*) que se planteen acerca de los resultados obtenidos. => Esa persona no debería usar esa herramienta para ese trabajo.

(*) Cuestiones relativas al dominio de aplicación de los resultados. La persona puede no saber cómo funciona internamente la herramienta. Pero sí que ha de saber manejar la herramienta y saber interpretar/revisar/comprender los resultados que produce.


