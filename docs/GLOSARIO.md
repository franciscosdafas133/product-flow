# Glosario (español llano)

Nada de esto es un botón mágico del IDE. Son **palabras del método**: las verás en el chat, en comandos y en `workflow/`.

## Puerta

Una **pregunta de producto** que solo tú puedes responder: ¿quién es el usuario?, ¿cobramos?, ¿qué queda fuera?

No es un menú de Cursor ni un slash command. El agente **propone**; tú **aceptas o corriges**. Sin tu respuesta, no debería inventar requisitos “confirmados”.

## ASK

Una pregunta formal registrada en el workflow (p. ej. `ASK-01`). En modo rápido suelen ser 3.

Responder = el agente corre `anotar` (y `--resuelto` cuando ya contestaste). No es lo mismo que una decisión (`DEC`).

## REQ (requisito)

Algo que el producto **debe cumplir**, escrito y enlazado (p. ej. `REQ-01`). Se crea/edita con el comando `requisito`, no editando JSON a mano.

## DEC (decisión)

Una elección de producto **aceptada** (quién aprobó, qué se aceptó). Comando típico: `decidir --aceptar --aprobado-por "…"`.

Si más tarde cambia: `reabrir` o `impactar`, no “hacer como si nada”.

## TASK (tarea)

Un trozo de trabajo concreto, idealmente con `--comprobacion` (comando que prueba que quedó bien). Estados legales (preparada → en curso → … → verificada) los vigila el **validador**.

## Evidencia

Prueba de que algo se ejecutó de verdad. Con `evidenciar --ejecutar` el script **corre** el comando; `--cubre` nombra el programa (y la prueba). Sin eso, no hay evidencia de comando válida.

## Vigente

La evidencia sigue siendo válida: los archivos de `--cubre` no cambiaron desde entonces y la prueba salió bien. Si tocas el programa cubierto, la evidencia **deja de estar vigente** y la tarea no puede seguir “verificada” a ciegas.

## Impacto / impactar

Cuando cambias un REQ, DEC o TASK que ya tenía dependientes: `impactar` invalida lo que ya no se sostiene (p. ej. tareas que estaban verificadas). Evita el autoengaño de “seguimos igual”.

## workflow/

Carpeta **dentro de tu proyecto** (no dentro del repo del método, salvo demos). Ahí viven estado, docs, decisiones, evidencias. Si no la ves, el método no arrancó en ese proyecto.

## product-flow

La **única entrada** del método: una skill. Tú no eliges media docena de skills auxiliares; el agente enruta (iniciar, continuar, evidenciar, etc.).

## Validador

Script (`validate_workflow.py`) que comprueba que el estado es legal. Si dice que no, no ignores el error para “seguir el vibe”.

## MANUAL_VERIFY_REQUIRED

Marca de **integración real** (login, pago, API de terceros) que no se puede fingir con un test local. Esa pieza **no** se evidencia ni se verifica como si estuviera hecha. Queda pendiente a propósito.

## Modo rápido / completo

Al `iniciar`: `rapido` = pocas ASK (aprox. 3); `completo` = más preguntas. Para los primeros 15 minutos, usa rápido.

## Checkpoint

“Guardar partida”: snapshot / commit del punto en el que estás, para poder recuperar después.

## Presentar / verificar

Tras evidenciar en verde: `presentar` (mostrar al humano) y `verificar` (cerrar la tarea solo si la evidencia está vigente). El agente no debe decir “verificado” solo con palabras.
