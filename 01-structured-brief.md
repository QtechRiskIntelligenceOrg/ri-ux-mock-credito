# Structured Brief — Sección Crédito (Mock UX/UI)

**App**: Risk Intelligence (RI)
**Date**: 2026-08-20
**Status**: Draft — awaiting PM gate (bead [GATE-PM] Fase 1)

## Research Basis

- **Brain evidence** (ver `brain-context-snapshot.md`, corpus `36d2a031b434c89e`):
  - `capas/Capa2_RI_MetodologiaCredito.md` — canon metodológico del módulo de crédito; respalda el handoff §1–§9 punto por punto (4 secciones núcleo, selector VaR·ES·Std, iso-risk, adaptación RD).
  - `capas/Capa2_RI_PlataformaUX.md` — baseline visual vigente de RI (excepción de rebranding), arquetipos de pantalla, contrato de navegación, y la regla [inviolable]: "crédito, liquidez y operacional copian el contrato completo del módulo de mercado".
  - `capas/Capa2_RI_Producto.md` — roles RBAC (Administrador, CRO, Analista, Lector), corte oficial EOD, localización DOP/DD-MM-AAAA, límites con contexto obligatorio.
  - `capas/Capa1_Diseno_Principios.md` + `capas/Capa1_Diseno_Tokens.md` — reglas de uso transversales (riesgo en neutro, MM/M, N/D, mono tabular); tokens visuales corporativos NO gobiernan RI durante la excepción.
- **Contrato metodológico vinculante**: `00-handoff-metodologico.md` — las implicaciones de diseño del §2 son no negociables.
- **Canonical constraints**: ver "Known Constraints" abajo.
- **Assumptions**: los datos del mock son ilustrativos (cartera dominicana en DOP: bonos, SBB, SBB con garantía, CDs — handoff §2); as_of estilo Mercado ("Datos DD/MM/AAAA").
- **Gaps**: ninguno declarado. Nota menor registrada en `feedback-log.md` sobre el patrón "próximamente" en el MenuSidebar.
- **Design judgment**: donde el canon calla (composición exacta de cada panel 2×2, copys de tooltips), se sigue el catálogo de gráficos del handoff §7/§9 y el precedente visual de Mercado.
- **Additional evidence**: `context-mercado/` (estructura front, backend de dashboards, 10 screenshots reales) — precedente factual de paridad, no canon.

## User Profile

**Primarios**: **Analista de riesgo** y **CRO** del tenant (roles RBAC canónicos de RI — `Capa2_RI_Producto.md`). El Analista profundiza (drill-down rating → emisor → sector → tipo, marginal, escenarios); el CRO lee el primer vistazo (tira de KPIs, top driver, estado vs. supuestos).
**Secundario**: **Lector** (consumo de las mismas vistas sin acciones de configuración).
**Contexto institucional**: entidades del mercado dominicano (puestos, EIF, SAFIs, AFPs) con libro de inversiones/tesorería en DOP.

## Job-to-be-Done

El usuario debe poder **evaluar el riesgo de crédito de su cartera** — entender de qué está hecho el libro (composición y concentración), cuánto puede perder y dónde se concentra (medida VaR/ES/Std por dimensión y en el tiempo), qué posición añade más riesgo en el margen (marginal / iso-risk), y qué pasa bajo estrés del libro y de los supuestos (escenarios) — siempre sabiendo **bajo qué supuestos** se calculó (fuente de transición, método de correlación, ρ).

## Usage Context

- **Device**: Web (desktop; breakpoints del front actual, referencia 1600px)
- **Frequency**: Alta — monitoreo diario sobre el corte oficial EOD
- **Urgency**: Rutinaria (monitoreo) con picos críticos (excesos de límite, estrés)

## Known Constraints

**Del handoff §2 (no negociables, respaldados por Brain `Capa2_RI_MetodologiaCredito.md` [inviolable]):**
1. **Rating = eje primario de drill-down**; el emisor se diferencia por exposición y realización aleatoria — no prometer visualmente granularidad emisor-específica que el modelo no tiene.
2. **Badge de supuesto activo visible en toda pantalla**: fuente de transición · método de correlación · ρ usado. Tablero auditable.
3. **Sensibilidad a supuestos como entregable de primera clase**: espacio de UI para barrer ρ ∈ {15%, 25%, 35%} (Escenarios §7.4).
4. **Moneda base DOP** (abreviación MM/M — nunca K; separador de miles).

**Del handoff §4 (forma de la distribución):**
5. **La distribución de valor del portafolio nunca se dibuja como campana de Gauss**: es asimétrica, multimodal (jorobas = 0,1,2,3… defaults) y de cola pesada. Alcance: aplica a la silueta de la distribución simulada de valor/pérdida (histogramas de Escenarios y cualquier referencia visual a "la distribución"). No prohíbe la densidad normal estándar del gráfico de **Umbrales de Merton** (§8, sección Factores — fuera del alcance del mock), que es un gráfico canónico distinto.

**De paridad con Mercado (Brain `Capa2_RI_PlataformaUX.md` [inviolable] + handoff §5–§6):**
6. Crédito **copia el contrato completo del módulo de mercado**: jerarquía Módulo→Sección→Tab→Visual, contrato de navegación analítica, molde de pantalla (breadcrumb + badge as_of + tabs + tira de 4 KPIs + rejilla 2×2 con tabla BR exportable).
7. **Resolución Sección vs. Tab** (jerarquía inviolable): las 4 secciones núcleo (Portafolio, VaR/Riesgo, Marginal, Escenarios) son **ítems del MenuSidebar** (título "Crédito"), igual que en Mercado (sidebar = sección; tabs = sub-vistas de la sección, patrón `tabs.ts`). La fila "Tabs" del molde §6 se lee como **sub-vistas dentro de cada sección** (p.ej. VaR: Global · Por Calificación…), a definir en los wireframes; cada sección tiene al menos una tab para preservar la jerarquía. **Pantalla por defecto: VaR.** Las 4 secciones recomendadas (Factores, Sensibilidades, Backtesting, Visión General) visibles en el sidebar como "próximamente" (futuro visible pero inactivo, en gris).
8. **Selector VaR · ES · Std** solo en VaR y Marginal; cambia datos, **nunca** el layout.
9. Baseline visual vigente de RI (excepción de rebranding): tokens del front actual, Inter, semáforo Ok/Advertencia/Incumplimiento solo en estado de límite.
10. Métricas de riesgo **en neutro** (nunca rojo/verde); rojo/verde solo juicio económico (P&L); umbral excedido = warning. N/D explícito, nunca cero. Fechas DD/MM/AAAA.
11. Métrica con límite existente nunca se expone sin su contexto de límite.
12. **No-objetivo**: no es pricing de crédito ni ECL contable (handoff §10; Brain).

**De alcance del mock:**
13. Solo las **4 secciones núcleo** (Portafolio, VaR/Riesgo, Marginal, Escenarios) se diseñan; el resto solo navegación "próximamente".
14. Es un mock/prototipo: datos ilustrativos plausibles bajo el patrón backend-driven del producto (chart_types del catálogo existente).

## Success Criteria

1. El PM navega el mock por las 4 secciones núcleo desde el MenuSidebar "Crédito" sin ayuda externa. Paridad verificable con `var-global.png` por checklist de elementos: breadcrumb arriba-izquierda, badge "Datos DD/MM/AAAA" arriba-derecha, tabs pill bajo la cabecera, columna/tira de 4 tarjetas KPI (valor + anterior + Δ/Δ% + tendencia), rejilla 2×2 con tabla en BR.
2. En cada pantalla, el badge de supuesto activo (fuente de transición · método correlación · ρ) es visible sin scroll.
3. Desde la pantalla por defecto (VaR), un analista identifica el **top driver** de riesgo y llega a la vista Marginal de esa dimensión en **≤3 clics**.
4. En Escenarios, el usuario configura un barrido de ρ (15/25/35%) y compara base vs. shockeado en la misma pantalla.
5. Cero violaciones verificables de las restricciones 1–5: sin campana de Gauss como silueta de la distribución de valor del portafolio, sin granularidad emisor-específica prometida (ningún control ni gráfico ofrece distribución propia por emisor), DOP en todos los montos, badge de supuesto presente en las 4 secciones.

---
**Source**: Handoff metodológico `00-handoff-metodologico.md` (contrato vinculante) + sketch de 4 secciones, 2026-08-20
**Brain context loaded**: ver `brain-context-snapshot.md`
