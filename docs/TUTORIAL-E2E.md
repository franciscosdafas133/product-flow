# Tutorial E2E — producto mínimo (idea → TASK verificada)

Objetivo: en un proyecto limpio, salir con **una tarea verificada** y el validador en verde.

Producto: *Contador CLI que imprime `visitas: N` y guarda el número en un archivo.*

Más corto: [PRIMEROS-PASOS.md](PRIMEROS-PASOS.md). Playbook para agentes: [tests/scenarios/producto-simple/PLAYBOOK.md](../tests/scenarios/producto-simple/PLAYBOOK.md).

## 0. Preparar

```bash
git clone https://github.com/franciscosdafas133/product-flow.git
cp -R product-flow/skills/product-flow ~/.cursor/skills/product-flow

mkdir -p ~/mdvtp-e2e-contador && cd ~/mdvtp-e2e-contador
# Ábrelo en Cursor
```

Script (ajusta la ruta si instalaste global):

```bash
PF=~/.cursor/skills/product-flow/scripts/product_flow.py
VAL=~/.cursor/skills/product-flow/scripts/validate_workflow.py
```

## 1. Iniciar (descubrir)

```bash
python3 "$PF" iniciar --proyecto . --idea "Contador CLI: imprime visitas: N y guarda el número" --modo rapido
```

**Esperado:** existe `workflow/`, hay ASK activas, docs de producto/descubrimiento.

En el chat (o a mano), responde algo como:

- Usuarios: yo en la terminal  
- Recorrido: un comando → imprime y persiste  
- Datos: un archivo local de conteo  

```bash
python3 "$PF" anotar --proyecto . --enlaza ASK-01 --texto "Usuario: yo en CLI" --resuelto
# repite ASK-02, ASK-03 con tus textos
```

```bash
python3 "$PF" continuar --proyecto .
```

**Esperado:** pide pasar a requisito; no vuelve a las mismas ASK.

## 2. Requisito + decisión (puerta humana)

```bash
python3 "$PF" requisito --proyecto . \
  --titulo "Contador persistente en CLI" \
  --texto "Al ejecutar, muestra visitas: N y guarda N en un archivo local."
```

Tú aceptas el enfoque (puerta humana):

```bash
python3 "$PF" decidir --proyecto . \
  --titulo "Enfoque CLI local" \
  --elegida "Contador en terminal con archivo local" \
  --motivo "Producto mínimo para probar el método" \
  --aprobado-por "tester" \
  --aceptar
```

## 3. Sistema (opcional pero recomendable)

Rellena `workflow/docs/sistema.md` con el ejemplo de [EJEMPLO-SISTEMA.md](EJEMPLO-SISTEMA.md) (sección CLI).

## 4. Tarea con comprobación

```bash
python3 "$PF" tarea --proyecto . \
  --titulo "CLI contador + script de prueba" \
  --comprobacion "bash comprobar.sh"
```

Anota el id que imprima (p. ej. `TASK-02`). Abajo usamos `TASK-ID`.

## 5. Implementar (aquí ya es código)

Ciclo obligatorio: **escanear → planificar → evaluar → aplicar**.

Ejemplo mínimo de producto (el agente puede escribirlo; esto es la meta):

`contador.py` — lee/escribe un archivo, imprime `visitas: N`.  
`comprobar.sh` — corre el programa dos veces y comprueba que el número sube.

Corre la prueba **tú o el agente** hasta que salga 0:

```bash
bash comprobar.sh
```

## 6. Evidenciar → presentar → verificar

Sustituye `TASK-ID` por el id real:

```bash
python3 "$PF" evidenciar --proyecto . \
  --tarea TASK-ID \
  --origen comando \
  --cubre contador.py,comprobar.sh \
  --ejecutar
```

Sin `--cubre` → debe rechazar. En rojo → no vigente. En verde:

```bash
python3 "$PF" presentar --proyecto . --tarea TASK-ID
python3 "$PF" verificar --proyecto . --tarea TASK-ID
```

## 7. Cierre

```bash
python3 "$VAL" workflow
python3 "$PF" estado --proyecto .
python3 "$PF" operar --proyecto . \
  --resumen "Contador CLI local con prueba automatizada" \
  --uso "python3 contador.py" \
  --pendientes "Sin empaquetado; sin usuarios reales"
```

## Criterio de éxito

| Check | OK si… |
|---|---|
| `workflow/` | Existe y el validador pasa |
| TASK | Estado verificada con evidencia vigente |
| Honestidad | Pendientes reales en `operar` (nada de “ya en producción”) |

## Si algo falla

- Slash / skill: [CURSOR.md](CURSOR.md)  
- Palabras raras: [GLOSARIO.md](GLOSARIO.md)  
- “¿Solo documenta?”: [FAQ.md](FAQ.md) · [MAPA-FASES.md](MAPA-FASES.md)  
- Límites de lo que puedes afirmar: [LIMITES-CANDIDATA.md](LIMITES-CANDIDATA.md)
