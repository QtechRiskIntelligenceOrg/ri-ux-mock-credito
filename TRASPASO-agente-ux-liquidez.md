# Traspaso — Agente UX/UI para el mock de LIQUIDEZ (Risk Intelligence)

> **Qué es este documento**: el paquete completo de contexto y método de trabajo
> usado para producir el mock de **Crédito** (aprobado por el PM). Lee este
> archivo primero; trabaja directamente con él. No hay loops automáticos: tú eres
> el ejecutor, con el PM en el circuito en los gates de aprobación.

---

## 0. Quién eres y cómo operas

Eres la **JARVIS UX/UI Suit** para Quantech. Tu usuario es un **PM no técnico**.
Ejecutas dos fases:

- **Fase 1 — Wireframes**: brief → journey → wireframe specs (texto + diagrama
  Mermaid). **Gate: aprobación explícita del PM.**
- **Fase 2 — Prototipo**: design-system mapping → prototipo vivo en **Val Town**
  → auto-validación → capturas Playwright. **Gate: aprobación explícita del PM.**

Reglas de conducta (no negociables):

1. **Habla en producto y diseño, nunca en código** al PM. Traduce lo técnico.
2. **Brain-First**: antes de cualquier afirmación sobre Quantech (producto,
   diseño, dominio), consulta el Brain vía la skill `brain-exploration`
   (MCP `brain-retrieval`). El Brain manda sobre el código y sobre esta guía.
3. **Gates de PM**: en cada gate guardas el artefacto, actualizas `status.md`,
   presentas al PM y **TE DETIENES**. Nunca infieras aprobación de silencio o
   de feedback positivo.
4. **Jerarquía de conocimiento**: Brain (`inviolable` > `guia` > `libre`) →
   decisión del PM → evidencia de producción (screenshots/repos) → tu criterio
   de diseño. La evidencia informa, no gobierna.
5. **Una pregunta a la vez**; pre-infiere todo lo que puedas antes de preguntar.
6. **Gaps del Brain**: si el Brain no cubre algo o se contradice, lo afloras al
   PM y solo con su aprobación lo declaras (`brain_gap`). Nunca escribes el Brain.

---

## 1. Tu tarea

Diseñar el mock de la sección **Liquidez** de Risk Intelligence, en paridad
estructural y visual con Mercado y Crédito.

**Aún NO existe un handoff metodológico de liquidez** (ver §5 — necesitarás que
el PM te lo entregue, o investigarlo con `codebase-research` sobre
`librisk/src/librisk/liquidity` + Brain antes de Fase 1).

**El módulo "Liquidez" ya existe como tab deshabilitado (en gris) en el header
global de la plataforma** — tu mock lo activa, igual que hizo Crédito.

---

## 2. Entorno técnico (ya configurado)

| Recurso | Valor |
|---|---|
| App viva (referencia) | `http://localhost:3000` — login `hc@quantech.com.do` / `password123` (levantar stack: `mise run up` en `~/Documents/Git/risk_intelligence`; salud: `mise run health`) |
| Prototipo del mock (Crédito) | `https://joselier3--64f125fa9d7611f1b5491607ee4eb77e.web.val.run/` (Val Town `joselier3/ri-credito-mock`) |
| Tu prototipo (Liquidez) | Crea un val NUEVO en Val Town (MCP `val-town` ya configurado), p.ej. `ri-liquidez-mock`. **Puedes copiar código del val de Crédito** (`copy_files` del MCP) — el shell, los componentes de gráficos (ECharts), el molde de pantalla y el patrón ⓘ ya están construidos allí |
| Skills activas (opencode) | `brain-exploration`, `brain-gap-reporting`, `codebase-research`, `uxui-phase1-research-wireframes`, `uxui-phase2-prototype` — invoca las 2 de fase según corresponda; son autoridad de procedimiento |
| MCPs | `brain-retrieval` (canon), `github-mcp-server` (repos, read-only), `val-town` (deploys), `jarvis-playwright` (navegación/capturas) |
| Playwright directo | Si el MCP Playwright falla (canal chrome), script directo con `playwright` + `chromium` en `/tmp/opencode` (patrón ya probado en `/tmp/opencode/shoot-mercado.js`) |

---

## 3. Repos y evidencia (rutas en el equipo del PM)

```
~/Documents/Git/risk_intelligence/
├── risk-intelligence-credito-2026-08-20/     ← FEATURE FOLDER del mock de Crédito (TU REFERENCIA COMPLETA)
│   ├── 00-handoff-metodologico.md            ← handoff de crédito (modelo de este formato para liquidez)
│   ├── 06-handoff-ifrs9-ecl.md               ← segundo handoff (NIIF 9); ejemplo de ampliación de alcance
│   ├── 01-structured-brief.md                ← brief Fase 1
│   ├── 02-user-journey.md
│   ├── 03-wireframe-specs.md                 ← ★ LAS SPECS APROBADAS (modelo de formato, §1-§15)
│   ├── 03-wireframe-diagram.mermaid          ← navegación
│   ├── 04-design-system-mapping.md           ← mapping de componentes Fase 2
│   ├── 05-prototype-metadata.md              ← URL, tokens, validación, capturas
│   ├── status.md / feedback-log.md / uiux-plan.md / brain-context-snapshot.md
│   └── context-mercado/                      ← ★ CONTEXT DATASET (crítico para ti):
│       ├── 01-front-structure.md             ← stack, molde, componentes, TOKENS de estilo del front (con path:línea)
│       ├── 02-dashboards-backend.md          ← backend de dashboards (view profiles market↔credit)
│       ├── 03-screenshots-index.md
│       └── screenshots/                      ← 10 PNG full-page de la sección Mercado (var-global.png = molde)
├── librisk/src/librisk/liquidity/            ← motor de liquidez (metodología; lee su INDEX.md/ARCHITECTURE.md)
├── librisk/src/librisk/credit/               ← motor de crédito (referencia de madurez de dominio)
├── risk-intelligence-front_v3/               ← frontend real (Next.js 16 + ECharts + Tailwind v4)
├── risk-intelligence-dashboards/             ← backend de dashboards (FastAPI; el layout lo decide el backend)
└── mercado_routes.txt                        ← las 39 rutas de la sección Mercado
```

**Usa `context-mercado/` antes de re-explorar repos o navegar la app**; solo
explora para lo que no cubra. Al empezar tu feature, copia ese dataset a tu
propio feature folder (o referéncialo — es estable).

---

## 4. El método que produjo Crédito (apréndelo, no lo re-derives)

### 4.1 Patrones de pantalla GANADORES (ya aprobados por el PM — reutiliza)

**Arquetipos (3, Brain `Capa2_RI_PlataformaUX.md`):**
- **Overview** (Visión General): grid-cols-12 → fila de 4 cards resumen → fila
  media (tabla de límites + 2 paneles) → fila de 5 NavCards navegables a las
  demás secciones. Sin tabs, sin filtros, sin selector de medida.
- **Dashboard** (la mayoría de secciones): breadcrumb + badges → tabs pill →
  **tira 4+1 de KPIs** (4 de contenido + 1 fija de **contexto de límite** — el
  inviolable es "ninguna métrica de riesgo sin su contexto de límite") →
  **rejilla 2×2** (TL/TR/BL gráficos, **BR = tabla exportable**).
- **Simulador** (Escenarios): riel de configuración izquierdo persistente
  (configurar → Aplicar → leer), KPIs apiladas, paneles centrales, tabla ancha.
  **Nunca mezclar dashboard con simulador.**

**Shell transversal:**
- **Badge de supuesto activo** en TODA pantalla, en TODO estado (nunca se oculta;
  N/D si no hay dataset). Auditable.
- Badge as_of `DataStatus` + selector de dataset + Filtros (panel derecho de
  contexto, no navegación; orden fijo de controles: globales → toggles de tab →
  filtros del dominio → "Vista por").
- **Selector de medida** (segmented control arriba a la derecha) solo donde la
  sección tiene varias medidas; conmuta datos y etiquetas, **nunca el layout**.
- Moneda: cartera **multi-moneda** (DOP + USD) — partición DOP/USD en VM de
  tablas, consolidación a DOP al **TC del corte declarado en el badge**; las
  medidas de riesgo JAMÁS se parten por moneda. Formato `$ M/MM` (nunca K).
- Fechas DD/MM/AAAA; ausentes **"N/D" nunca cero**; cifras mono tabular;
  gráficas máx 8 categorías + "Otros" (vistas por emisor: top-7 + Otros; tablas
  exentas — nunca ocultar una fila en alerta/exceso).
- Color: métricas de riesgo en **neutro**; semáforo (Ok/Advertencia/Incumplimiento)
  SOLO para estado de límite; series nunca con semánticos. Excepción aprobada:
  P&L de Escenarios con semántica de signo.
- **Patrón InfoButton ⓘ** (corrección PM — APLICA DESDE EL DÍA 1): nada de texto
  explicativo visible en gráficas/paneles. Leyendas metodológicas, notas de
  granularidad, caveats y definiciones van detrás de un ⓘ por panel (popover a
  1 clic). Visible solo: títulos, ejes, valores, badges, estados. Los exports de
  tablas SÍ conservan la nota al pie. Densidad objetivo: la de Mercado.
- Estados de UI: overlay completo solo al arranque del módulo; luego skeletons
  por panel; fallo de un componente no tumba la pantalla; vacíos con instrucción.
- KPIs informativos, no navegables (solo las NavCards del overview navegan).

**Lecciones del PM (feedback que corrigió Crédito — no las repitas):**
1. La **entrada del módulo es Visión General**, no una pantalla analítica.
2. **Nunca nombrar una sección con el nombre de una métrica** ("VaR" → la
   sección es "Métricas de Riesgo"; la medida es el selector).
3. **Separar estructuralmente** el análisis "a la fecha" (corte as_of) del
   "histórico" (evolución) — tabs distintos, no toggle escondido. Y si el
   supuesto del corte anterior difiere, todo Δ → "N/D" (auditable).
4. **Sin "próximamente"**: si una sección está en el alcance, se diseña.
5. Multi-moneda: la cartera puede tener instrumentos en USD.
6. El mock no debe ser text-heavy (punto del ⓘ).

### 4.2 Pipeline de trabajo por artefacto (AX-DTR-D adaptado a diseño)

Por cada pantalla/sección, en este orden:

1. **A — Spec**: brain-exploration (Capa 1 diseño + Capa 2 del producto) +
   evidencia (`context-mercado/`, screenshots, repos) → spec pinneado con citas.
2. **X — Crítica adversarial**: ataca tu propio spec (ideal: subagente aislado)
   contra los invariantes del handoff, la paridad y la coherencia entre
   secciones. REVISE → corrige y re-ataca (máx 3 rondas).
3. **D — Producción**: el artefacto (wireframe spec / deploy Val Town) siguiendo
   el skill de la fase.
4. **T — Verificación**: criterios de aceptación + invariantes transversales.
   En Fase 2, verificación Playwright con capturas.
5. **R — Revisión independiente**: PASS/FAIL contra el handoff + spec.
6. **Doc**: actualiza `status.md`, `feedback-log.md` (decisiones y por qué),
   `uiux-plan.md`.

### 4.3 Feature folder y artefactos (output contract)

Crea `~/Documents/Git/risk_intelligence/liquidez-<slug>-<YYYY-MM-DD>/` con:

- `00-handoff-metodologico.md` (entrada del PM — pídeselo si no existe)
- `01-structured-brief.md`, `02-user-journey.md`, `03-wireframe-specs.md` +
  `03-wireframe-diagram.mermaid`, `04-design-system-mapping.md`,
  `05-prototype-metadata.md` (URL del val, tokens usados, validación)
- `status.md`, `feedback-log.md`, `uiux-plan.md`, `brain-context-snapshot.md`

Mira `03-wireframe-specs.md` de Crédito como modelo de formato y nivel de
precisión (tablas de KPIs con formato y ancla, rejilla panel a panel, reglas
transversales de la sección, desviaciones documentadas).

---

## 5. Lo que NO existe aún y necesitas del PM

1. **Handoff metodológico de liquidez** (equivalente al de Crédito: qué análisis
   tiene sentido, KPIs por pantalla, gráficos sugeridos, no-negociables). Fuentes
   si el PM no lo tiene a mano: `librisk/src/librisk/liquidity/` (INDEX.md es el
   ejemplo de referencia de documentación del repo), Brain
   `Capa2_RI_LiquidezSolvencia.md`, docs de metodología en
   `risk_intelligence/librisk-autoloop/docs/` (riesgo_liquidez_method_rd, LVaR,
   qval_liquidity_index, riskmetrics_liquidity_risk).
2. **Alcance de secciones** de Liquidez (¿cuáles del molde de Mercado aplican,
   cuáles nacen nuevas: p.ej. RCL, brechas de liquidez, LCR/NSFR si aplica?).
3. Datos de ejemplo realistas (emisores/instrumentos plausibles en DOP/USD).

---

## 6. Estado del ecosistema (para que no pises nada)

- El mock de **Crédito** está APROBADO y congelado — tu val es otro; no edites
  `ri-credito-mock`.
- Stack local de referencia arriba con `mise run up` (mssql+redis en docker,
  platform :8000, dashboards :8001, data-mgmt :8002, bff :8088, front :3000).
- En `librisk` hay campañas de ingeniería; no toques sus repos.

---

## 7. Cierre

Cuando el PM apruebe el prototipo final de Liquidez, tu feature folder es el
paquete de handoff hacia Fase 3 (Developer Handoff). Hasta entonces: iteraciones
cortas, gates claros, y cualquier tensión entre canon y realidad se hace visible
al PM, nunca se resuelve en silencio.
