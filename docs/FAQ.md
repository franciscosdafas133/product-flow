# FAQ

## ¿Solo documenta?

No. Documentar es la primera mitad. Con TASK + `--comprobacion` el agente **escribe código**, corre pruebas y solo verifica con evidencia. Si te quedaste en ASK/REQ, aún no llegaste a construir: ver [MAPA-FASES.md](MAPA-FASES.md).

## ¿Quién escribe el código?

El **agente** (Cursor / Claude), guiado por el método. Tú decides producto (puertas), revisas el plan y aceptas. El validador no programa: impide marcar “hecho” sin prueba.

## ¿Y si no hay slash `/product-flow`?

Normal. Pega en el chat: “Usa la skill product-flow…”. Revisa instalación y reinicio en [CURSOR.md](CURSOR.md).

## ¿En qué se diferencia de “pedirle a la IA que haga la app”?

Aquí queda rastro en `workflow/`: preguntas, requisitos, decisiones, evidencia vigente. Si cambias un requisito, `impactar` reabre lo afectado. El chat suelto se olvida; el workflow no (tanto).

## ¿Sirve para cualquier producto?

Para productos de software donde puedas tener pruebas locales. Integraciones reales (pago, OAuth) se marcan pendientes (`MANUAL_VERIFY_REQUIRED`), no se fingen.

## ¿Para quién / no para quién?

**Sí:** indies, estudiantes, equipos chicos que ya usan Cursor/Claude y quieren menos autoengaño (“ya está en prod”).

**No:** quien busque un generador one-click sin leer preguntas; quien necesite marketplace oficial ya; quien no pueda correr Python/bash local.

## ¿Es estable / producción?

Es **candidata** (`0.1.0-rc1`). Mira [LIMITES-CANDIDATA.md](LIMITES-CANDIDATA.md): no digas que “mucha gente lo validó” si aún estás en el testeo.

## ¿Rompe mi repo?

Escribe sobre todo en `workflow/` del proyecto. El código de la app lo escribe el agente donde acordéis. Usa un folder de prueba la primera vez ([PRIMEROS-PASOS.md](PRIMEROS-PASOS.md)).

## ¿Cómo reporto un fallo en el testeo?

Ideas útiles: sistema, pasos, comando, salida, y si el validador pasó. Un “no me gustó” sin eso no se puede arreglar.
