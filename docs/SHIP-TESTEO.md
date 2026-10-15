# Ship de testeo (LinkedIn / amigos)

Objetivo: mucha gente **prueba** la candidata `0.1.0-rc1`, no que crean que es producto cerrado.

## Mensaje corto (pegar en LinkedIn)

```
Abro a testeo público product-flow: un método para Cursor/Claude Code.

No es un plugin mágico. Es idea → preguntas → requisitos → código → prueba que CORRIÓ → entrega, con carpeta workflow/ y un validador que frena el “ya está” inventado.

Versión candidata 0.1.0-rc1. Quiero fallos reales, no likes.

Primero 15 min: https://github.com/franciscosdafas133/product-flow/blob/main/docs/PRIMEROS-PASOS.md
Repo: https://github.com/franciscosdafas133/product-flow

Si lo pruebas, dime: (1) dónde te trabaste (2) si llegaste a una TASK verificada (3) Cursor o Claude.
```

## Antes de publicar el post

1. `python3 scripts/run_regresion.py` → `7/7 → ok`
2. README y PRIMEROS-PASOS apuntan al repo público correcto
3. No afirmar lo prohibido en [LIMITES-CANDIDATA.md](LIMITES-CANDIDATA.md)

## Qué pedir a testers

- Seguir [PRIMEROS-PASOS.md](PRIMEROS-PASOS.md) o [TUTORIAL-E2E.md](TUTORIAL-E2E.md)
- Feedback en 3 bullets (traba / TASK verificada sí-no / host)
- Opcional: corrida larga [PROBAR-TODO.md](PROBAR-TODO.md) solo si ya entienden el método

## Qué no prometer en el post

- Marketplace oficial de Cursor
- “Ya lo validaron N equipos”
- Que la ventana HTML se abre sola
- Que sustituye diseño de producto humano
