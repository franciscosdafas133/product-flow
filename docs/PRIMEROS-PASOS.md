# Primeros 15 minutos

Versión: ver [VERSION](../VERSION).  
Límites honestos: [LIMITES-CANDIDATA.md](LIMITES-CANDIDATA.md).  
Palabras raras: [GLOSARIO.md](GLOSARIO.md).  
Cursor en detalle: [CURSOR.md](CURSOR.md).

## Qué es esto (30 segundos)

**product-flow** no es un juego, ni un plugin mágico que “hace la app sola”.

Es un **método de construcción** para Cursor / Claude Code: tú traes una idea; el agente te hace preguntas, escribe documentos en `workflow/`, propone requisitos y tareas, **construye código** y solo marca “listo” si una prueba **corrió de verdad**. Un validador frena estados inventados.

| Sí | No |
|---|---|
| Guía idea → requisitos → código → prueba → entrega | Un marketplace oficial de Cursor (aún no) |
| Tú decides producto (“puertas”) | Que el chat diga “ya está” sin evidencia |
| Carpeta `workflow/` visible en tu proyecto | Editar JSON a mano |

## Antes de empezar

1. Cursor (o Claude Code) abierto.
2. Python 3 en la terminal.
3. 10–15 minutos.

## Instalar (elige una)

**A — Copiar la skill (más rápida para probar)**

```bash
git clone https://github.com/franciscosdafas133/product-flow.git
cp -R product-flow/skills/product-flow ~/.cursor/skills/product-flow
```

**B — Plugin desde GitHub** (Customize → import plugin → From GitHub Repository → `https://github.com/franciscosdafas133/product-flow`)

**C — Instalador del repo**

```bash
cd product-flow
python3 scripts/install_metodo.py install --alcance global --hosts cursor
```

Detalle y “¿y si no aparece `/`?” → [CURSOR.md](CURSOR.md).

## Minuto 0–2: abre un proyecto vacío

```bash
mkdir -p ~/mdvtp-prueba-15min && cd ~/mdvtp-prueba-15min
# Ábrelo en Cursor como carpeta de trabajo
```

## Minuto 2–5: pega esto en el chat

```
Usa product-flow.
Instala/usa la skill si hace falta.
Quiero empezar un producto mínimo:
idea = "Contador CLI: imprime visitas: N y guarda el número en un archivo"
Modo rápido. Hazme las preguntas ASK; yo respondo. No inventes requisitos.
Cuando respondas, dime qué acaba de aparecer en workflow/.
```

Si no tienes `/product-flow`, el texto de arriba basta: la skill se activa por nombre.

## Qué debería pasar (tú → agente → disco)

| Tú dices | El agente hace | Ves en el proyecto |
|---|---|---|
| “Empieza con esta idea” | Corre `iniciar --modo rapido` | Carpeta `workflow/` + docs + 3 ASK |
| Respuestas a las preguntas | `anotar --resuelto` por cada ASK | Apuntes enlazados; `continuar` ya no repite las mismas preguntas |
| “Acepto el enfoque” | `requisito` + `decidir --aceptar` | REQ y DEC en `workflow/` |
| “Construye la primera tarea” | Código + `tarea --comprobacion` + prueba | Archivos de app + evidencia al verificar |

### Cómo se ve `workflow/` (texto, no captura)

Tras `iniciar`:

```text
workflow/
  estado.json
  relaciones.json
  eventos.jsonl
  evidencias.json
  docs/
    producto.md
    descubrimiento.md
    …
  decisiones/     (vacío o plantillas según fase)
```

El chat te resume el **informe**; la verdad está en esos archivos. Si no aparece `workflow/`, la skill no corrió el script (revisa [CURSOR.md](CURSOR.md)).

## Minuto 5–12: cierra un ciclo mínimo

Pega (ajusta respuestas a tu gusto):

```
1) Anota mis respuestas y marca las ASK resueltas.
2) Crea un requisito claro para el contador CLI.
3) Yo acepto: decide con --aceptar --aprobado-por "yo".
4) Crea una TASK con --comprobacion que se pueda correr en bash.
5) Implementa el contador (escanear → planificar → evaluar → aplicar).
6) evidenciar --origen comando --cubre <programa>,<test> --ejecutar
7) presentar → verificar
8) Muéstrame estado y la salida del validador.
```

Éxito de estos 15 minutos: **una TASK verificada** con evidencia vigente (prueba en verde), no “un README bonito”.

## Minuto 12–15: comprueba el paquete (opcional pero útil para feedback)

```bash
cd ~/ruta/a/product-flow
python3 scripts/run_regresion.py
```

Debe terminar en `7/7 → ok`.

## Siguiente lectura

- Tutorial completo: [TUTORIAL-E2E.md](TUTORIAL-E2E.md)
- ¿En qué fase estoy?: [MAPA-FASES.md](MAPA-FASES.md)
- Cheatsheet CLI: [GUIA-USUARIO.md](GUIA-USUARIO.md)
- Preguntas típicas: [FAQ.md](FAQ.md)

## Feedback para el testeo público

Si lo estás probando por LinkedIn / un amigo: anota 3 cosas — (1) dónde te trabaste, (2) si entendiste “puerta”, (3) si llegaste a una TASK verificada. Eso vale más que un “está cool”.
