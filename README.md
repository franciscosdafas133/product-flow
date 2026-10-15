# product-flow (el método)

Skill / plugin para **Cursor** y **Claude Code**: idea → preguntas → requisitos → código → pruebas honestas → entrega.

Versión candidata: [VERSION](VERSION) (`0.1.0-rc1`).  
**Testeo abierto:** [docs/SHIP-TESTEO.md](docs/SHIP-TESTEO.md) · empieza en **[docs/PRIMEROS-PASOS.md](docs/PRIMEROS-PASOS.md)**.

## Qué es (y qué no)

No es un juego ni un generador mágico. Es un **método de construcción**: tú decides producto; el agente propone, escribe en `workflow/`, implementa y solo marca listo si la prueba **corrió**. Un validador frena estados ilegales.

| Antes (chat suelto) | Después (con el método) |
|---|---|
| “Ya está” sin prueba | Evidencia con comando ejecutado + `--cubre` |
| Requisitos en el aire | ASK → REQ → DEC en `workflow/` |
| Integración real fingida | `MANUAL_VERIFY_REQUIRED` queda pendiente |
| No sabes en qué fase vas | `estado` / `continuar` + [mapa de fases](docs/MAPA-FASES.md) |

### Cómo se ve el rastro (`workflow/`)

```text
tu-proyecto/
  workflow/
    estado.json
    docs/          ← producto, sistema, plan…
    decisiones/
    evidencias.json
  contador.py      ← el código del producto (ejemplo)
  comprobar.sh
```

## Para quién / no para quién

**Sí:** indies, estudiantes, equipos chicos que ya usan Cursor o Claude Code y quieren menos autoengaño.

**No:** quien quiera un one-click sin responder preguntas; quien necesite marketplace oficial ya; quien no pueda correr Python/bash en local.

Límites honestos de esta RC: [docs/LIMITES-CANDIDATA.md](docs/LIMITES-CANDIDATA.md).

## Empezar en 15 minutos

1. [docs/PRIMEROS-PASOS.md](docs/PRIMEROS-PASOS.md) — copy-paste al chat  
2. [docs/CURSOR.md](docs/CURSOR.md) — skill vs `/` vs plugin  
3. [docs/GLOSARIO.md](docs/GLOSARIO.md) — puerta, ASK, evidencia, vigente…

```bash
git clone https://github.com/franciscosdafas133/product-flow.git
cp -R product-flow/skills/product-flow ~/.cursor/skills/product-flow
```

Más opciones: [INSTALL.md](INSTALL.md).

## Documentación

| Doc | Para qué |
|---|---|
| [PRIMEROS-PASOS](docs/PRIMEROS-PASOS.md) | Onboarding humano |
| [TUTORIAL-E2E](docs/TUTORIAL-E2E.md) | Idea → TASK verificada |
| [MAPA-FASES](docs/MAPA-FASES.md) | Dónde estoy / qué falta |
| [EJEMPLO-SISTEMA](docs/EJEMPLO-SISTEMA.md) | Rellenar flujos + diagrama |
| [FAQ](docs/FAQ.md) | Dudas típicas del testeo |
| [GUIA-USUARIO](docs/GUIA-USUARIO.md) | Cheatsheet CLI |
| [PROBAR-TODO](docs/PROBAR-TODO.md) | Recorrido exhaustivo (ya conoces el método) |

## Qué descargas

| Ruta | Para qué |
|---|---|
| `skills/product-flow/` | La skill (copiar a `~/.cursor/skills/` o `~/.claude/skills/`) |
| `.cursor-plugin/plugin.json` | Declaración del plugin (apunta a `skills/`) |

## Comprobar el paquete

```bash
cd product-flow && python3 scripts/run_regresion.py
```

Tiene que terminar en `7/7 → ok`.

## Licencias

[THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
