# Mapa de fases — ¿dónde estoy ahora?

El método **sí construye** (código + pruebas). Documentar sin implementar es quedarse a medias.

## Ciclo completo (diagrama)

```text
  idea
    │
    ▼
┌───────────┐   ASK + anotar     ┌────────────┐
│ Descubrir │ ─────────────────► │ Requisitos │
└───────────┘                    └─────┬──────┘
                                       │ decidir (puertas)
                                       ▼
                                 ┌───────────┐
                                 │  Sistema  │  flujos + diagrama
                                 └─────┬─────┘
                                       │
                                       ▼
                                 ┌───────────┐
                                 │   Plan /  │  TASK con --comprobacion
                                 │   tareas  │
                                 └─────┬─────┘
                                       │
                    escanear → planificar → evaluar → aplicar
                                       │
                                       ▼
                          evidenciar → presentar → verificar
                                       │
                                       ▼
                                 ┌───────────┐
                                 │  Operar / │  pendientes honestos
                                 │  entregar │
                                 └───────────┘
```

Tras un cambio de REQ/DEC ya enlazado: **impactar** y no fingir que lo verificado sigue igual.

## Checklist “dónde estoy”

Marca la **primera** casilla que aún no cumpliste:

- [ ] **Sin `workflow/`** → `iniciar --idea "…" --modo rapido`
- [ ] **ASK abiertas** → responde y `anotar --resuelto`
- [ ] **Sin REQ** → `continuar` debería pedir requisito; crea con `requisito`
- [ ] **Sin DEC de producto** → `decidir --aceptar --aprobado-por …`
- [ ] **Sistema vacío** → rellena `workflow/docs/sistema.md` (ver [EJEMPLO-SISTEMA.md](EJEMPLO-SISTEMA.md))
- [ ] **Sin TASK con comprobación** → `tarea --comprobacion "…"`
- [ ] **Código no corre / test rojo** → ciclo implementar; no evidencies en verde
- [ ] **Evidencia sin `--cubre` o no ejecutada** → `evidenciar … --ejecutar --cubre prog,test`
- [ ] **Evidencia verde no presentada** → `presentar` → `verificar`
- [ ] **Integración real pendiente** → `MANUAL_VERIFY_REQUIRED` (no la “verifiques” a mentiras)
- [ ] **Listo para hablar de entrega** → `operar --uso "…" --pendientes "…"`

Atajo en terminal:

```bash
python3 ~/.cursor/skills/product-flow/scripts/product_flow.py estado --proyecto .
python3 ~/.cursor/skills/product-flow/scripts/product_flow.py continuar --proyecto .
```

`continuar` contrasta validador + apuntes + git y te dice el siguiente paso razonable.

## Hueco idea → código (explícito)

| Fase | ¿Solo docs? | ¿Código? |
|---|---|---|
| Descubrir / ASK | Sí (preguntas) | No aún |
| REQ + DEC | Contratos de producto | Aún no obligatorio |
| Sistema / diagrama | Diseño | Preparación |
| TASK + implementar | Plan | **Aquí se escribe código** |
| Evidenciar / verificar | No | **Aquí se demuestra** |

Si alguien te dice “el método solo documenta”, está parado antes de TASK.

## Relacionado

[TUTORIAL-E2E.md](TUTORIAL-E2E.md) · [GLOSARIO.md](GLOSARIO.md) · [GUIA-USUARIO.md](GUIA-USUARIO.md)
