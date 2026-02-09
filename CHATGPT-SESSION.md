## 1) Crítica de tu documentación + propuesta de mejor organización

### Lo que ya está muy bien (y yo mantendría)

* **“Single source of truth”** de reglas (un `base.md`) y **puntos de entrada por herramienta** (symlinks `CLAUDE.md`, `AGENTS.md`, etc.). Es una idea potente para evitar divergencias y drift. ([GitHub][1])
* El enfoque **XP/TDD + baby steps** como “guardrails” del agente (reduce alucinación y refactors temerarios). ([GitHub][1])
* La incorporación del **FIC (Research → Plan → Implement → Validate) + /clear entre fases** como disciplina operativa (no solo “mejores prompts”). ([nikeyes.github.io][2])

### Problemas típicos que veo en este tipo de repos (y que te están afectando)

1. **Demasiadas puertas de entrada “al mismo concepto”**: Playbook, Patterns, base rules, comandos… pero no está claro *qué leer primero*, *qué es referencia* vs *qué es operativo*.
2. **FIC está “mezclado” con configuración multi-herramienta**: son dos ejes distintos:

    * (A) *Cómo se organiza el repo para que lo lean herramientas* (Claude/Codex/Cursor/…)
    * (B) *Cómo trabajas tú en sesiones largas sin perder el control del contexto* (FIC)
3. **Ausencia de un “happy path” minimalista** (5–10 min) y luego “advanced path”.
4. **Nomenclatura y capas**: “rules / playbook / patterns / commands” suenan solapados si no defines jerarquía (qué manda sobre qué).

### Propuesta de reorganización (con un mapa claro)

Piensa el repo en 4 capas, ordenadas por “lo que necesitas hoy para trabajar”:

#### A. `README.md` como “portal” (2 rutas)

* **Ruta 1: Empezar en 10 minutos**

    1. Copiar/crear `CLAUDE.md` (o symlink) → 2) Primer comando → 3) Primera sesión con FIC “light”
* **Ruta 2: Montaje completo (multi-tool + compaction)**
  Estructura completa, `thoughts/`, comandos, feedback loop, etc.

*(Esto reduce muchísimo la fricción de adopción.)*

#### B. `docs/` (documentación estable y legible)

* `docs/00-concepts.md`

    * Context window, por qué “un CLAUDE.md no basta”, qué es compaction, qué significa “<60% contexto” (citando el artículo). ([nikeyes.github.io][2])
* `docs/10-fic-workflow.md`

    * Research/Plan/Implement/Validate + cuándo hacer `/clear` y qué persiste.
* `docs/20-tdd-with-agents.md`

    * Reglas operativas: *un test rojo*, *un cambio*, *verde*, *refactor*, *commit*.
* `docs/30-recipes.md`

    * “Recetas” (katas, refactors, debugging, code review) en formato checklist.

#### C. `rules/` (lo que “manda”)

* `rules/base.md` (tu single source of truth)
* `rules/profiles/` (opcional)

    * `kotlin-tdd.md`, `refactoring.md`, `cli-apps.md`…
      En vez de meterlo todo en `base.md`, activas perfil según tarea.

#### D. `tooling/` (adaptadores por herramienta)

* `tooling/claude/` → `CLAUDE.md` (o symlink) + comandos específicos si aplica
* `tooling/cursor/` → `.cursor/commands`, `.cursor/rules`
* `tooling/codex/` → `AGENTS.md` (o equivalente)

> Esto separa *contenido* (rules/docs) de *integración* (tooling). En repos multi-tool se nota muchísimo.

#### E. `thoughts/` (persistencia FIC, trackeado)

Tu enfoque encaja perfecto con la estructura que describe la implementación de FIC y “thoughts” (research/plans/PRs). ([GitHub][3])

* `thoughts/shared/research/`
* `thoughts/shared/plans/`
* `thoughts/shared/prs/`
* `thoughts/<username>/notes/` (privado o gitignored, según prefieras)

---

## 2) Tutorial práctico: empezar con Claude Code + aplicar tu marco (FIC) a 2 katas

### 2.1. Setup de Claude Code (lo mínimo)

1. **Instalar** (según tu SO). En la guía oficial tienes los comandos (macOS/Linux/WSL y Windows). ([Claude Code][4])
2. **Autenticación** siguiendo el setup oficial. ([Claude Code][5])
3. **Probar en un repo**: entra en una carpeta cualquiera y ejecuta Claude Code (quickstart). ([Claude Code][4])

> Referencia: Claude Code es un agente en terminal que entiende el repo y ayuda en tareas de código y git workflows. ([GitHub][6])

### 2.2. “Bootstrap” de tu estilo (tu base rules + FIC)

En cada kata, empieza así:

**Paso 0 — crear un repos limpio**

* `git init`
* añade un `CLAUDE.md` (symlink a tu `base.md`, como tu repo propone). ([GitHub][1])

**Paso 1 — activar FIC “light” (sin plugin)**

* Research → guarda en `thoughts/shared/research/…`
* `/clear`
* Plan → guarda en `thoughts/shared/plans/…`
* `/clear`
* Implement por micro-iteraciones
* Validate (tests + checklist)

La lógica es exactamente la del artículo: separar fases + compaction frecuente para mantener el control del contexto. ([nikeyes.github.io][2])

**Prompt patrón para cada fase (copy/paste)**

* **Research**

    * “Lee el enunciado y resume requisitos *solo del paso actual* + lista de decisiones pendientes. No implementes nada. Escribe el resultado en `thoughts/shared/research/<kata>-step-01.md`.”
* **Plan**

    * “Propón diseño mínimo para pasar el paso actual con TDD (interfaces, modelos, tests). Escribe plan en `thoughts/shared/plans/<kata>-step-01.md`.”
* **Implement**

    * “Sigue el plan. Un test rojo cada vez. No avances al siguiente requisito. Commits pequeños.”
* **Validate**

    * “Ejecuta tests, revisa duplicación, nombra claramente, y verifica que el comportamiento cumple el paso actual.”

---

## 2.3. Kata 1: Social Network (kata-log) con FIC + TDD

La kata está pensada como **incremental**: no mires el siguiente requisito hasta terminar el actual. ([kata-log.rocks][7])
Y los comandos típicos del enunciado (posting/reading/following/wall) se suelen modelar como consola. ([GitHub][8])

### Sesión propuesta (práctica y disciplinada)

**Research (solo “Posting”)**

* Resultado esperado: qué comandos existen, pero enfócate en *posting* únicamente (por la regla del kata). ([kata-log.rocks][7])
* Decide: salida exacta, formato de tiempo (“(5 minutes ago)”), y estrategia de reloj (inyección de clock para test).

`/clear`

**Plan**

* Diseño mínimo:

    * `CommandParser`
    * `SocialNetworkApp` (orquestador)
    * `PostRepository` en memoria (por ahora)
    * `Clock` inyectable
* 1er test: “Alice -> I love the weather today” crea un post asociado a Alice

`/clear`

**Implement (micro-pasos TDD)**

* Test rojo → implementación mínima → verde → refactor → commit
* No meter “reading” hasta terminar posting.

**Validate**

* Checklist: ¿cero IO real en tests? ¿clock controlado? ¿nombres claros?

> Repite el ciclo por requisito: Reading, Following, Wall.

---

## 2.4. Kata 2: Gilded Rose (Kotlin) con enfoque de refactoring seguro

La intención del ejercicio **no es reescribir desde cero**, sino refactorizar con pasos pequeños y tests frecuentes. ([GitHub][9])

### Sesión propuesta (la forma “clásica” que mejor encaja con tus reglas)

**Research**

* Lee el código Kotlin inicial y el README de reglas de items (Aged Brie, Sulfuras, Backstage passes, Conjured…).
* Identifica *puntos de dolor* (condicionales, magic strings, lógica duplicada).
* Escribe en `thoughts/shared/research/gilded-rose-baseline.md`:

    * invariantes
    * casos especiales
    * dónde tocar mínimo

`/clear`

**Plan**

* Primero: **golden master** o tests caracterización (si no vienen ya suficientes).
* Después: refactor en seguridad:

    1. extraer funciones pequeñas
    2. encapsular reglas por tipo (strategy/polimorfismo o when + tablas)
    3. eliminar duplicación
* Plan escrito en `thoughts/shared/plans/gilded-rose-plan.md`

`/clear`

**Implement**

* Paso 1: tests de caracterización que claven comportamiento actual.
* Paso 2: refactor mecánico (extract function, rename, etc.) con tests pasando.
* Paso 3: añadir requisito “Conjured” (si tu variante lo incluye) con TDD.

**Validate**

* “¿He mantenido comportamiento?” (tests)
* “¿He reducido complejidad accidental?” (lectura)
* “¿He dejado el código listo para cambios futuros?” (estructura)

---

## Referencias clave (las que yo usaría como “fuente de verdad”)

* Claude Code docs (setup + quickstart). ([Claude Code][5])
* Tu base: Augmented code configuration (single ruleset + entry points). ([GitHub][1])
* Artículo “Tu CLAUDE.md…” + descripción FIC y `/clear` entre fases. ([nikeyes.github.io][2])
* Implementación/explicación de FIC con comandos y `thoughts/`. ([GitHub][3])
* Kata Social Network (incremental). ([kata-log.rocks][7])
* Gilded Rose kata (refactor incremental, no rewrite). ([GitHub][9])

Si quieres llevarlo al siguiente nivel, tu “tercera tarea natural” sería: **convertir lo anterior en un “workshop script” de 90 minutos** (timing por fases, prompts exactos por paso, y checklist de validación por kata).

[1]: https://github.com/adelatorrefoss/augmentedcode-configuration/ "GitHub - adelatorrefoss/augmentedcode-configuration: Augmented code config from eferro"
[2]: https://nikeyes.github.io/tu-claude-md-no-funciona-sin-context-engineering-es/ "Tu CLAUDE.md no funciona (sin Context Engineering) – No hay preguntas tontas – Uno aprovecha la vida, si comparte lo que ha aprendido, si no la ha desperdiciado."
[3]: https://github.com/saski/augmentedcode-configuration "GitHub - saski/augmentedcode-configuration"
[4]: https://code.claude.com/docs/en/quickstart?utm_source=chatgpt.com "Quickstart - Claude Code Docs"
[5]: https://code.claude.com/docs/en/setup?utm_source=chatgpt.com "Set up Claude Code - Claude Code Docs"
[6]: https://github.com/anthropics/claude-code?utm_source=chatgpt.com "anthropics/claude-code"
[7]: https://kata-log.rocks/social-network-kata?utm_source=chatgpt.com "Social Network Kata"
[8]: https://github.com/sandromancuso/social_networking_kata?utm_source=chatgpt.com "sandromancuso/social_networking_kata: Exercise used for ..."
[9]: https://github.com/emilybache/GildedRose-Refactoring-Kata?utm_source=chatgpt.com "emilybache/GildedRose-Refactoring-Kata"
