# Cómo instalar el método

Versión: ver [VERSION](VERSION).  
**Empezar a usarlo:** [docs/PRIMEROS-PASOS.md](docs/PRIMEROS-PASOS.md).  
Invocación en Cursor (slash, reinicio, carpeta vs plugin): [docs/CURSOR.md](docs/CURSOR.md).  
Uso CLI: [docs/GUIA-USUARIO.md](docs/GUIA-USUARIO.md).  
Límites: [docs/LIMITES-CANDIDATA.md](docs/LIMITES-CANDIDATA.md).

Lo que se descarga para usar es la skill en `skills/product-flow/` (y el plugin en `.cursor-plugin/`).

## Opción A — Skill (la más directa para testeo)

```bash
git clone https://github.com/franciscosdafas133/product-flow.git
cp -R product-flow/skills/product-flow ~/.cursor/skills/product-flow
# Claude Code:
# cp -R product-flow/skills/product-flow ~/.claude/skills/product-flow
```

Reinicia Cursor. En el chat: pide **product-flow** (no hace falta el menú `/`).

```bash
python3 ~/.cursor/skills/product-flow/scripts/product_flow.py iniciar --proyecto . --idea "Mi app…"
```

## Opción B — Plugin en Cursor

1. Clona o abre este repo.
2. En Cursor: Customize → importar plugin **From GitHub Repository**  
   `https://github.com/franciscosdafas133/product-flow`  
   (o “from folder” si tu Cursor lo permite sobre este clone).
3. Debe cargar la skill desde `skills/` (ver `.cursor-plugin/plugin.json`).

Aún no está en el Marketplace oficial. Si el plugin no lista el slash, usa la Opción A o pega texto: ver [docs/CURSOR.md](docs/CURSOR.md).

## Opción C — Instalador del repo

```bash
cd product-flow
python3 scripts/install_metodo.py install --alcance global --hosts cursor,claude
python3 scripts/install_metodo.py status --alcance global
```

Solo un proyecto:

```bash
python3 scripts/install_metodo.py install --alcance proyecto --proyecto /ruta/al/proyecto --hosts cursor
```

## Comprobar el paquete

```bash
cd product-flow
python3 scripts/run_regresion.py
```

Tiene que terminar en `7/7 → ok`.
