# User Journey — Sección Crédito (Mock UX/UI)

**App**: Risk Intelligence (RI)
**Date**: 2026-08-20
**Status**: Draft — awaiting PM gate (bead [GATE-PM] Fase 1)
**Scope**: Happy path only (edge cases y estados de error → Fase 2)

> **Notas globales del journey**
> - Todos los montos en **DOP** (abreviación MM/M — nunca K; separador de miles). Handoff §2/§10; Brain `Capa1_Diseno_Tokens.md` [inviolable].
> - El **badge de supuesto activo** (fuente de transición · método de correlación · ρ) se verifica en cada pantalla del flujo — tablero auditable (handoff §2 [no negociable]).
> - Paridad con Mercado: MenuSidebar título "Crédito", breadcrumb + badge as_of (`DataStatus`), tabs pill, molde tira 4 KPIs + rejilla 2×2 (Brain `Capa2_RI_PlataformaUX.md` [inviolable]: "crédito copia el contrato completo del módulo de mercado"; evidencia factual `context-mercado/screenshots/var-global.png`).
> - Selector **VaR · ES · Std** existe **solo** en Métricas de Riesgo (ex "VaR", corrección PM F1.9) y Marginal; ausente en Escenarios y Portafolio (handoff §5/§10; Brain `Capa2_RI_MetodologiaCredito.md`). Cambia datos, nunca layout.

## Perfil de usuario (roles Brain, `Capa2_RI_Producto.md`)

- **Primario**: **Analista de riesgo** — recorre el flujo completo (drill-down, marginal, escenarios).
- **Lector del primer vistazo**: **CRO** — pasos 1–2 (KPIs, top driver, supuestos) le bastan.
- **Secundario**: **Lector** — mismas vistas sin acciones de configuración.

## Initial State

El analista está autenticado en RI sobre el **corte oficial EOD** del tenant (dataset publicado; badge "Datos DD/MM/AAAA"). El nav superior muestra los módulos **Mercado · Liquidez · Crédito · Operacional** (hoy Crédito está deshabilitado — este mock lo activa). El analista conoce el módulo de Mercado, por lo que el molde de pantalla le es familiar. Aún no sabe cómo cambió el riesgo de crédito de su libro desde el corte anterior.

## Step Sequence

### Step 1: Entrar a Crédito
- **User action**: Clic en **Crédito** en el nav superior — aterriza en **Visión General** (default del módulo, F1.8) — y clic en **Métricas de Riesgo** en el sidebar (o en su NavCard).
- **Screen**: **Crédito › Métricas de Riesgo**, tab de aterrizaje **A la Fecha**. (Nota F1.8/F1.9: la entrada default del módulo es ahora **Visión General** — el analista llega aquí vía sidebar o NavCard; el nombre y los tabs reflejan la corrección PM F1.9.)
- **Information needed**: MenuSidebar "Crédito" con las secciones núcleo activas (Visión General, Portafolio, Métricas de Riesgo, Marginal, Escenarios) y las 3 recomendadas restantes (Factores de Riesgo, Sensibilidades, Backtesting) **en gris como "próximamente"** (Brain: "futuro visible pero inactivo").
- **Decision point**: ninguno — aterrizaje directo.

### Step 2: Primer vistazo — KPIs y supuestos
- **User action**: Verifica el badge as_of ("Datos DD/MM/AAAA") y el **badge de supuesto activo** (p.ej. "S&P · ρ=25% axiomático"); lee la tira de 4 KPIs.
- **Screen**: Crédito › Métricas de Riesgo › A la Fecha.
- **Information needed**: KPIs (handoff §7.2): **Medida Total vs corte EOD anterior** (Δ y %) · **Medida/VM** · **Top Driver** (emisor que más aporta — informativo, **no navegable**, en paridad con Mercado) · **Beneficio de diversificación** (F1.9: la Volatilidad anualizada es propiedad histórica y vive en el tab Histórico). Todos los montos DOP.
- **Decision point** (opcional): cambia el selector **VaR · ES · Std** según su propósito (σ → límites; VaR/ES → capital; handoff §4). El layout no cambia; solo los datos.

### Step 3: Drill-down por rating (eje primario)
- **User action**: Lee el gráfico **Medida × calificación** — barras por rating, **en orden de escala AAA→D** (el máximo se identifica por altura, no por reordenamiento — specs §8.1) — e identifica el rating que concentra la medida.
- **Screen**: Crédito › Métricas de Riesgo › A la Fecha — el gráfico es una **celda de la rejilla 2×2** (nunca vista modal/full-screen; paridad con el molde de `var-global.png`).
- **Information needed**: medida por rating en DOP; el **rating es el eje primario de drill-down** (handoff §2 [no negociable]).
- **Decision point**: ¿qué rating merece profundizar?
- *Nota F1.9*: el tab **Histórico** (evolución de la medida y cambios de mezcla) queda **fuera del happy path** — el flujo del analista es as_of. No se asume cross-filter clic-en-barra (sin evidencia en Mercado).

### Step 4: Desglose de exposición por emisor dentro del rating
- **User action**: Lee la **dona por emisor** (top-7 + "Otros", regla de specs §8) y la **tabla jerárquica rating → emisor** en la celda inferior-derecha de la misma rejilla.
- **Screen**: Crédito › Métricas de Riesgo › A la Fecha (in-place; misma pantalla del paso 3).
- **Information needed**: contribución por emisor **etiquetada** de forma fija: *"Contribución prorrateada por exposición — el modelo opera a nivel rating"*. El emisor se diferencia **solo por exposición y realización aleatoria**; el drill-down analítico termina en rating y ninguna vista promete distribución propia por emisor (handoff §2 [no negociable]). Tabla detallada en la celda inferior-derecha, **exportable** — posición y exportabilidad espejan `var-global.png` de Mercado (paridad empírica) y el handoff §6 ("BR suele ser una tabla detallada y exportable").
- **Decision point**: ¿qué emisor concentra la exposición del rating identificado?

### Step 5: Marginal — ¿quién añade riesgo en el margen?
- **User action**: Clic en **Marginal** en el sidebar (clic 1, contado desde Métricas de Riesgo › A la Fecha); en el **scatter iso-risk** (X = Valor de Mercado de la posición en DOP; Y = riesgo marginal %) identifica **la posición del cuadrante C (superior derecha) con mayor riesgo marginal** y hace clic en su punto/fila para ver el detalle (clic 2). Verifica el badge de supuesto de la pantalla. **Cumple el presupuesto ≤3 clics** (success criteria #3 de `01-structured-brief.md`).
- **Screen**: **Crédito › Marginal**.
- **Information needed**: scatter con **cuadrantes A/B/C** y **overlays de límite** (línea horizontal de %-riesgo, vertical de tamaño, hipérbola iso-risk — handoff §7.3); tabla por posición: VM, marginal, individual (*standalone*), % del total — la brecha marginal vs. individual = beneficio de diversificación. El concepto ***fallen angel*** aparece solo como **anotación conceptual del cuadrante C** (tooltip educativo), no como hallazgo del flujo ni requisito de datos. Selector VaR·ES·Std presente.
- **Decision point**: ¿la posición dominante excede algún límite (overlay)? ¿conviene reducirla?

### Step 6: Escenarios — estrés de los supuestos (barrido de ρ)
- **User action**: Clic en **Escenarios** en el sidebar. En el **riel de configuración persistente** (arquetipo simulador, Brain `Capa2_RI_PlataformaUX.md`; paridad con `escenarios-impacto-riesgo.png`) elige el shock de supuesto **barrido de ρ ∈ {15%, 25%, 35%}**, corre el recálculo y compara resultados alternando el **selector de ρ activo** del riel.
- **Screen**: **Crédito › Escenarios**. El área de resultados sigue el patrón del simulador de Mercado — **no hereda tal cual** la tira KPIs + 2×2 del dashboard ("nunca convertir dashboard en simulador ni viceversa"); F1.3 especifica el layout citando la captura.
- **Information needed**:
  - **Badge de supuesto con dos estados**: pre-run "S&P · ρ=25% (base)"; post-run "Base: S&P · ρ=25% → Barrido activo: ρ=15/25/35%". El journey verifica ambos.
  - **Histograma superpuesto** base vs. ρ-activo con líneas de VaR — **ambas siluetas asimétricas y multimodales** (jorobas = 0,1,2,3… defaults); **prohibida cualquier curva de densidad simétrica de referencia** (handoff §4 [no negociable]).
  - **Barras divergentes de Ganancia/Pérdida (G/P) por rating** (shock − base), **waterfall** por instrumento, y **tabla del barrido con las 3 columnas de ρ** (VM pre / post / G/P por cada ρ) — la sensibilidad a supuestos como entregable de primera clase (handoff §2/§7.4).
- **Decision point**: ¿cuán sensible es el VaR del libro a ρ? ¿el orden de magnitud del riesgo se sostiene bajo ρ=35%?

### Step 7: Cierre — exportar evidencia
- **User action**: Exporta la **tabla del barrido de Escenarios** (VM pre/post/G-P por ρ) para su comité. (Las tablas detalladas de Métricas de Riesgo y Marginal son igualmente exportables desde su celda inferior-derecha.)
- **Screen**: Crédito › Escenarios.

## Final State

El analista sabe: **cuánto puede perder** (medida total y por rating), **dónde se concentra** (exposición por emisor, correctamente encuadrada como prorrateo), **qué posición añade más riesgo en el margen** (iso-risk, cuadrante C) y **cuán sensible es todo a ρ** (barrido 15/25/35%). Todo bajo supuestos visibles y auditables, con evidencia exportada. El CRO obtiene lo suyo en los pasos 1–2 sin profundizar.

## Screens Identified

| # | Screen Name | Purpose | Entry From | Exit To |
|---|---|---|---|---|
| 0 | Crédito › Visión General | Overview ejecutivo — entrada default del módulo (F1.8); NavCards hacia las secciones | Nav superior "Crédito" (default) | NavCards / sidebar → cualquier sección |
| 1 | Crédito › Métricas de Riesgo (A la Fecha · Histórico) | Medida de riesgo al corte (descomposición, drill-down) y su historia (evolución, cambios de mezcla) | Sidebar o NavCard desde Visión General | Sidebar → Marginal / Portafolio / Escenarios; tabs de la sección |
| 2 | Crédito › Marginal | Contribución marginal por posición (scatter iso-risk, cuadrantes, overlays de límite) | Sidebar | Sidebar → cualquier sección |
| 3 | Crédito › Escenarios | Estrés del libro y de los supuestos (riel simulador; barrido de ρ) | Sidebar | Sidebar → cualquier sección |
| 4 | Crédito › Portafolio | Composición y concentración (sin medida de riesgo) — **entrada navegable activa del sidebar, fuera del happy path**; se especifica en F1.3 | Sidebar | Sidebar → cualquier sección |
| — | Sidebar: Factores de Riesgo · Sensibilidades · Backtesting | "Próximamente" — visibles, en gris, inactivas | — | — |

---
**Approved by PM**: pendiente — gate [GATE-PM] de Fase 1
**Fuentes**: `00-handoff-metodologico.md` §2, §4, §5, §6, §7; Brain `Capa2_RI_MetodologiaCredito.md`, `Capa2_RI_PlataformaUX.md`, `Capa2_RI_Producto.md`, `Capa1_Diseno_Tokens.md` (corpus `36d2a031b434c89e`); evidencia factual `context-mercado/` (screenshots + estructura front).
