# Ejemplo: cómo rellenar `sistema.md`

Plantilla vacía: `skills/product-flow/templates/sistema.md` (en tu proyecto: `workflow/docs/sistema.md`).

No hace falta UML perfecto. Hace falta que **otra persona** entienda piezas, datos y qué toca el exterior.

---

## Ejemplo A — Contador CLI (miniproducto del tutorial)

### Componentes

- `contador.py` — lee el archivo de estado, suma 1, imprime `visitas: N`, guarda.
- `visitas.txt` (o similar) — persistencia local.
- `comprobar.sh` — prueba automatizada (no es runtime de usuario).

### Flujos de conexión entre sistemas

- No hay APIs externas ni login.
- Todo corre en la máquina local vía terminal.

### Flujos de datos

1. Arranque: si no existe el archivo → N = 0 (o 1 según regla acordada en REQ).
2. Lectura → incremento → escritura atómica simple.
3. Salida estándar: texto `visitas: N` para el humano / la prueba.

### Diagrama

```text
[usuario/terminal]
       │  ejecuta
       ▼
  contador.py ──lee/escribe──► visitas.txt
       │
       ▼
   stdout: "visitas: N"

comprobar.sh ──invoca──► contador.py (x2) ──assert──► N crece
```

---

## Ejemplo B — Minijuego local (puntuación en archivo)

### Componentes

- `juego.py` — bucle de turnos / input.
- `puntuacion.json` — mejor marca.
- `test_juego.sh` — smoke: arranca, juega un turno simulado, sale 0.

### Flujos de conexión

- Sin red. Input = teclado (o flags de test).

### Flujos de datos

- Partida en memoria → al terminar, si score > best, escribe `puntuacion.json`.
- Test no debe depender de scores viejos: usa directorio temporal o borra fixture.

### Diagrama

```text
teclado ──► juego.py ──► (estado en RAM)
                │
                └──► puntuacion.json (best)
test_juego.sh ──► juego.py --smoke
```

---

## Ejemplo C — SaaS chico (notas con cuenta)

### Componentes

- App web (frontend + API).
- Base de datos (notas, usuarios).
- Proveedor de auth (p. ej. magic link) → marcar `MANUAL_VERIFY_REQUIRED` hasta probarlo de verdad.
- Email / pagos: igual, pendientes honestos.

### Flujos de conexión entre sistemas

- Browser → HTTPS → API → DB.
- API → proveedor auth (token).
- API → email (si hay notificaciones).

### Flujos de datos

- Nota: nace en el cliente → POST → fila en DB → GET al listar.
- Sesión: cookie/token; no guardar secretos en el repo.

### Diagrama

```text
[browser] ──HTTPS──► [API] ──SQL──► [DB]
                       │
                       ├──► [Auth provider]   ← MANUAL_VERIFY_REQUIRED
                       └──► [Email]           ← pendiente real
```

### Qué NO poner como “verificado”

Login real, cobro, o webhook de terceros **sin** prueba manual registrada. El método prefiere dejarlos bloqueados a mentir.

---

## Cómo usarlo en el flujo

1. Tras REQ/DEC, el agente (o tú) edita `workflow/docs/sistema.md`.
2. Las TASK deben mapear a componentes de este diagrama.
3. Si cambia el diagrama de forma que rompa tareas verificadas → `impactar`.
