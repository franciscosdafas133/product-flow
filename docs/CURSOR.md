# Cómo invocarlo en Cursor

## Skill ≠ menú / siempre

| Cosa | Qué es |
|---|---|
| **Skill `product-flow`** | Instrucciones + scripts que el agente carga cuando le pides el método |
| **Slash `/product-flow`** | Atajo opcional del chat; **no** siempre aparece |
| **Plugin GitHub** | Empaqueta la skill para importarla desde el repo |
| **Copiar carpeta** | `~/.cursor/skills/product-flow` — instalación clásica |

Si no ves el slash, **no está roto**: pega texto en el chat pidiendo la skill por nombre.

## Qué pegar en el chat (funciona sin `/`)

```
Usa la skill product-flow.
Quiero [empezar | continuar | ver estado] el producto en este proyecto.
Idea: "…"
```

O más corto:

```
/product-flow
empezar con idea "Contador CLI que guarda visitas en un archivo", modo rápido
```

## Si no aparece en slash

1. Confirma que existe la carpeta:
   ```bash
   ls ~/.cursor/skills/product-flow/SKILL.md
   ```
2. **Reinicia Cursor** (cerrar ventana / reload window) tras copiar o instalar.
3. Abre un **proyecto** (carpeta), no solo un chat suelto sin workspace.
4. Sigue pegando el texto “Usa product-flow…”: muchas builds activan la skill por `description` aunque no listen el slash.
5. Si instalaste solo el plugin: Customize → revisa que el plugin esté cargado; si falla, usa la Opción A de [INSTALL.md](../INSTALL.md) (copiar carpeta).

## Install carpeta vs plugin GitHub

| | Carpeta (`cp -R … ~/.cursor/skills/`) | Plugin (From GitHub) |
|---|---|---|
| Velocidad para probar | Alta | Depende del UI de Cursor |
| Actualizar | Vuelves a copiar o `install_metodo.py` | Reimportar / actualizar plugin |
| Marketplace oficial | No hace falta | Tampoco está (aún) en marketplace |
| Qué carga | `SKILL.md` + `scripts/` + `procedures/` | Lo declarado en `.cursor-plugin/plugin.json` → `skills/` |

Para el **testeo público** recomendamos carpeta o `install_metodo.py`: menos misterio.

## Claude Code

Misma skill, otra ruta:

```bash
cp -R product-flow/skills/product-flow ~/.claude/skills/product-flow
```

En el chat: “usa product-flow”.

## Comprobar que los scripts responden

```bash
python3 ~/.cursor/skills/product-flow/scripts/product_flow.py --help
```

Si eso falla, la skill no está donde crees: reinstala con [INSTALL.md](../INSTALL.md).

## Siguiente

[PRIMEROS-PASOS.md](PRIMEROS-PASOS.md) · [FAQ.md](FAQ.md)
