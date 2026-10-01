# Brain Context Snapshot — Crédito (Risk Intelligence)

**Feature**: Sección Crédito (mock UX/UI, 4 secciones núcleo)
**Corpus version**: `36d2a031b434c89e` (catálogo consultado 2026-08-20)
**Bead**: librisk-gyz (F1.1)

## Entries fetched (governed Brain, vía brain-retrieval MCP)

| ID | Capa/Dominio | tipo_conocimiento | Uso en el diseño |
|---|---|---|---|
| `capas/Capa2_RI_MetodologiaCredito.md` | 2 / riesgo / RI | guia (con secciones inviolables) | Canon metodológico del módulo: valida el handoff §1–§9. Confirma inviolables: PD es insumo no salida; distribución multimodal — "**nunca se representa como campana de Gauss**"; adaptación RD (equity/correlación/transición no observables); "el rating es el eje primario de drill-down (no prometer visualmente granularidad emisor-específica que el modelo no tiene) · el supuesto activo siempre visible (insignia con fuente de transición, método de correlación y ρ) · sensibilidad a supuestos con espacio de interfaz para barrer ρ (15/25/35%)". Diseño del módulo [guia]: 4 secciones núcleo, VaR pantalla por defecto, selector VaR·ES·Std solo VaR y Marginal ("cambia los datos, nunca el layout"), molde miga+selector+insignia+tabs+4 KPIs+rejilla 2×2 con tabla exportable, iso-risk con 3 overlays y fallen angels. Estado [libre]: nada desplegado hoy — la integración es roadmap. |
| `capas/Capa2_RI_PlataformaUX.md` | 2 / diseno / RI | guia (con secciones inviolables) | **RI es la única excepción de rebranding**: quien construye sobre RI sigue el baseline vigente (tokens `#eff3f8`/`#0d77bf`/`#1f2a4e`, Inter, semáforo Ok/Advertencia/Incumplimiento). Jerarquía Módulo→Sección→Tab→Visual [inviolable]; arquetipo 1 "dashboard dirigido por manifest (KPIs a la izquierda + grilla)" y arquetipo 2 simulador (riel de control persistente — patrón para Escenarios; "nunca convertir dashboard en simulador ni viceversa"). Contrato de navegación analítica [inviolable] (orden de controles; dominios de filtro autoritativos). "Extensión a otros riesgos [inviolable]: crédito, liquidez y operacional **copian el contrato completo del módulo de mercado**". Prohibiciones de construcción [inviolable]: no reasignar la terna del semáforo, no pintar series con semánticos, no ocultar corte de datos, N/D nunca cero, no métrica de riesgo sin contexto de límite, DD/MM/AAAA, "Futuro visible pero inactivo (Liquidez/Crédito/Operacional en gris)". |
| `capas/Capa2_RI_Producto.md` | 2 / riesgo / RI | guia (con secciones inviolables) | Roles RBAC: **Administrador, CRO, Analista, Lector** — audiencia del mock. Corte oficial EOD; metodología oficial única; localización RD del tenant (DOP, DD/MM/AAAA); límites con umbral advertencia + incumplimiento; "Una métrica nunca se expone sin su contexto de límite cuando existe". Estado del módulo Crédito [libre]: "librería cuantitativa avanzada; integración a plataforma en roadmap". |
| `capas/Capa1_Diseno_Principios.md` | 1 / diseno | guia (con inviolables) | Semántica de color [inviolable]: "TODAS las métricas de riesgo en neutro… umbral excedido = warning, no rojo; categórico, no semáforo, para riesgo/calificación/segmento". Cuatro estados UI canónicos; grados de certeza (Ausente = "sin valorar", nunca cero). Aplican como **destino/canon corporativo**; para RI gobierna el baseline de excepción (Capa2_RI_PlataformaUX) mientras dure el rebranding. |
| `capas/Capa1_Diseno_Tokens.md` | 1 / diseno | inviolable | Convenciones que sí aplican transversalmente al contenido: **MM = millones · M = miles (nunca K)**, DD/MM/AAAA, mono tabular para cifras, dataviz categórico 8+"Otros", DOP por defecto. Los tokens de color corporativos NO gobiernan RI hoy (excepción documentada). |

## Resolución de jerarquía (nota clave)

Capa 2 RI PlataformaUX declara explícitamente que RI está en excepción de
rebranding: el mock usa el **baseline visual vigente de RI** (tokens del front
actual), no los tokens corporativos de Capa 1. Las reglas de *uso* de color
(riesgo en neutro, semáforo solo estado de límite, N/D) son consistentes en
ambas fuentes y aplican.

## Evidencia de producción (precedente factual, no canon)

- `context-mercado/01-front-structure.md` — molde de pantalla, MenuSidebar, tabs pill, CardMetric, DataStatus badge, chart_types registrados, tokens y formatos del front.
- `context-mercado/02-dashboards-backend.md` — backend-driven (`components[]` + `chart_type`); view profiles diseñados para reutilizar market↔credit; nada de crédito implementado.
- `context-mercado/screenshots/*` — 10 capturas; `var-global.png` = molde de referencia; nav superior ya muestra **Crédito deshabilitado**.

## Gaps / avisos

- Ninguna contradicción Brain↔handoff detectada: `Capa2_RI_MetodologiaCredito.md` respalda el handoff punto por punto.
- Sin gaps declarados. Nota menor para PM (feedback-log): el handoff propone menú lateral con las 4 recomendadas "próximamente"; el Brain pide "futuro visible pero inactivo… en gris" a nivel de header/nav — consistente, se aplica el mismo patrón dentro del MenuSidebar de Crédito.

---

## A-phase — Bead librisk-xo9 (F1.2 User Journey)

**Corpus re-verificado 2026-08-20**: `36d2a031b434c89e` (sin cambios; entries de F1.1 siguen válidos).

### Spec del artefacto (02-user-journey.md)

- **Alcance**: happy path only del **Analista de riesgo** (rol RBAC canónico, `Capa2_RI_Producto.md`); CRO como lector del primer vistazo (KPIs); edge cases → Fase 2.
- **Secuencia pinneada por el bead**: entra a Crédito (default **VaR**, handoff §5) → lee KPIs (§7.2: Medida Total vs anterior · Medida/VM · Top Driver · Vol anualizada) → drill-down **rating→emisor** (§2/§6: rating eje primario; emisor solo por exposición, sin distribución propia) → **Marginal** iso-risk (§7.3: cuadrantes A/B/C, fallen angels, overlays de límite) → **Escenarios** con barrido de ρ ∈ {15,25,35}% (§7.4, §2).
- **Paridad Mercado citada**: MenuSidebar título "Crédito" (patrón `layout.tsx` Mercado), tabs pill `tabs.ts`, breadcrumb + badge DataStatus as_of, selector de medida solo VaR/Marginal (Brain `Capa2_RI_MetodologiaCredito.md` + `Capa2_RI_PlataformaUX.md` [inviolable: crédito copia el contrato completo de mercado]). Evidencia factual: `context-mercado/var-global.png`, `var-marginal.png`, `escenarios-impacto-riesgo.png`.
- **Escenarios = arquetipo simulador** (riel de control persistente, `Capa2_RI_PlataformaUX.md`): el paso de barrido de ρ usa panel de configuración → recálculo → comparación base/shock en la misma pantalla.
- **Portafolio**: sección núcleo visible en sidebar pero **fuera del happy path** (el bead no la incluye); se especifica en F1.3.
- **Badge de supuesto activo** presente en el estado inicial y verificado por el analista antes de leer cifras (tablero auditable, §2).
- **Decisiones abiertas resueltas**: (1) el cambio de medida VaR·ES·Std se modela como decisión opcional dentro del paso de lectura de VaR, no como paso propio (cambia datos, no flujo); (2) el drill-down rating→emisor ocurre dentro de la sección VaR (sub-vista/tab + tabla jerárquica BR), no navegando a otra sección; (3) ≤3 clics KPI Top Driver → vista Marginal (success criteria #3 del brief).

---

## A-phase — Bead librisk-8ag (F1.3 Navegación + molde transversal)

**Corpus re-verificado 2026-08-20**: `8b3bd636c070fe38` (cambió desde `36d2a031b434c89e`; se re-fetchearon `Capa2_RI_PlataformaUX.md` y `Capa2_RI_MetodologiaCredito.md` — contenido consistente con F1.1/F1.2, sin cambios que afecten decisiones previas).

### Spec del artefacto (03-wireframe-specs.md Parte 1 — Shell + 03-wireframe-diagram.mermaid)

- **Alcance del bead**: shell transversal — header global, MenuSidebar "Crédito", tabs por sección, molde de pantalla (tira KPI + rejilla 2×2), selector VaR·ES·Std, badge de supuesto activo, badge as_of, formatos. Los contenidos por sección (KPIs concretos, gráficos) van en beads siguientes.
- **Sidebar (8 ítems, orden narrativo de Mercado con Marginal insertado tras VaR)**: Visión General (gris) · Portafolio · Sensibilidades (gris) · VaR · Marginal · Factores de Riesgo (gris) · Escenarios · Backtesting (gris). Marginal es sección propia (handoff §5, sketch de 4 núcleo) aunque en Mercado es tab de VaR-y-ES — desviación documentada: el inviolable "copia el contrato completo" gobierna contrato (jerarquía, orden de controles, arquetipos), no el árbol IA literal.
- **Default**: entrar al módulo → `Crédito › VaR › Global` (handoff §5; Brain MetodologiaCredito "VaR/Riesgo — pantalla por defecto").
- **Resolución deferral #1 (tabs §6 vs sidebar)**: la tira "Tabs: VaR·Marginal·Portafolio·Escenarios" del molde §6 NO se implementa como tabs de sección — chocaría con la jerarquía inviolable Módulo→Sección→Tab. Tabs = sub-vistas por sección (patrón `tabs.ts`): VaR (Global · Por Calificación) · Marginal (Global) · Portafolio (Global · Concentración) · Escenarios (Impacto en Riesgo). Sets provisionales, confirmados en los beads por sección.
- **Molde dashboard (Portafolio, VaR, Marginal)**: breadcrumb Home/Sección/Tab + derecha [badge supuesto activo · DataStatus · dataset · Filtros] + selector medida (solo VaR/Marginal) → tabs pill → columna izquierda 4 tarjetas KPI (actual, anterior, Δ, Δ%, tendencia) → rejilla 2×2 con BR = tabla exportable. 4 KPIs (canon handoff §6/Brain) vs 5 empíricos en `var-global.png` — canon guia > precedente factual.
- **Escenarios = arquetipo simulador** (inviolable "nunca convertir dashboard↔simulador"): riel de control persistente izquierdo + área de resultados; sin selector de medida; badge de supuesto con 2 estados (pre/post-run).
- **Badge de supuesto activo**: presente en las 4 secciones, junto al DataStatus (§2 no negociable; Brain: "insignia con fuente de transición, método de correlación y ρ").
- **Formatos**: DOP con M/MM (nunca K), DD/MM/AAAA, N/D nunca cero, riesgo en neutro, semáforo solo estado de límite, drill-down canónico rating→emisor→sector→tipo (rating eje primario).
- **Deferral #2 (Top Driver no navegable)**: se mantiene — se anota en el molde como propiedad del componente KPI.

### Correcciones X ronda 1 (bead librisk-8ag)

1. **KPI de límite (FAIL)**: tira = **4 KPIs de contenido + 1 tarjeta fija "Uso Límite"** (5 total, dentro del "tira 4-5" del handoff §6). El inviolable "no métrica de riesgo sin contexto de límite" (`Capa2_RI_PlataformaUX.md`, `Capa2_RI_Producto.md`) gobierna sobre el molde guia; sin límite configurado → "N/D" (paridad `var-global.png`).
2. **Filtros (FAIL)**: el shell define `CreditoFiltersSidebar` (paridad `MercadoFiltersSidebar`) + orden inviolable de controles: (1) globales fecha/portafolio/dataset → (2) toggles de pestaña → (3) contextuales de crédito: **calificación · emisor · tipo de instrumento (bono/SBB/SBB garantía/CD) · seniority** → (4) "Vista por" (rating→emisor→sector→tipo) → (5) selectores de tiempo solo en visuales temporales. Dominios autoritativos de la capa de datos (mock: declarados del contrato backend, nunca inferidos del contenido visible). MenuSidebar auto-colapsa cuando el riel de Escenarios está abierto (paridad).
3. **Marginal sección propia (WARN)**: anclada al handoff §5 (fuente vinculante: sketch núcleo de 4); registrada como tensión guia-vs-inviolable para el PM en feedback-log (no reinterpretación unilateral).
4. **Secciones de un tab (WARN)**: se renderiza la barra con un solo pill (uniformidad de molde y breadcrumb Home/Sección/Tab); sin precedente empírico — anotado para PM.
5. **Formato DOP (WARN)**: paridad con el motor de formato de Mercado: símbolo `$`, escala M/MM, 2 decimales; la unidad **DOP explícita** en encabezados de columnas, ejes y subtítulo de KPIs (cartera 100% DOP, §2).
6. **Orden sidebar (WARN)**: se mantiene interlavado por paridad de orden con Mercado ("copia el contrato completo"); decisión documentada en el artefacto y feedback-log.
7. **Breadcrumb (WARN)**: pinneado `Home > Sección > Tab` (paridad empírica `Breadcrumb.tsx`; el módulo lo nombra el título del sidebar). La notación "Crédito › VaR" del journey es abreviatura editorial.
8. **Tabs provisionales (WARN)**: acotado — los beads por sección pueden **añadir** tabs, nunca renombrar/eliminar los pinneados (hrefs del MENU_ITEMS dependen del primer tab).
9. **Badge de supuesto en estados no felices (WARN)**: muestra el supuesto del último dataset publicado; en Preparando/No listo/Error → "Supuesto: N/D" — **nunca se oculta** (§2).
10. **Etiqueta de prorrateo (OK-note 12)**: elevada a formato transversal del shell: toda vista por emisor lleva la leyenda fija "Contribución prorrateada por exposición — el modelo opera a nivel rating".

---

## A-phase — Bead librisk-2v2 (F1.4 Wireframe spec — Portafolio)

**Corpus re-verificado 2026-08-20**: `8b3bd636c070fe38` (sin cambios). Re-fetch `Capa2_RI_MetodologiaCredito.md`: "Portafolio = composición y concentración **sin medida de riesgo** (HHI, top-N)" [guia]; drill-down canónico rating→emisor→sector→tipo; leyenda de prorrateo aplica a vistas por emisor.

### Spec del artefacto (sección Portafolio en 03-wireframe-specs.md)

- **Tabs pinneados por el shell**: Global · Concentración (no se renombran).
- **Tab Global** (handoff §7.1): KPIs de contenido = VM Total · N° Posiciones · N° Emisores · Calificación predominante (mayor share por rating; sin Δ% aritmético — muestra actual vs anterior como rating); + tarjeta fija "Límite de concentración" (HHI vs límite; N/D). 2×2: TL **área apilada temporal** VM por rating; TR **dona** composición con "Vista por" (Calificación default · Emisor · Tipo de instrumento); BL **barras divergentes** cambio por grupo vs corte anterior; BR **tabla** por rating (VM DOP, % Global, Var DOP, Var %) expandible rating→emisor (paridad tabla jerárquica `portafolio-global.png`).
- **Tab Concentración** (§7.1 métricas a destacar; paridad `portafolio-concentracion.png`): KPIs = **HHI** · Share Top-5 emisores · Mayor concentración (emisor + %VM) · N° emisores efectivos (1/HHI); + tarjeta límite (estado de límites de concentración). 2×2: TL barras horizontales top-N emisores %VM; TR evolución histórica del HHI / mayor concentración con línea de límite; BL barras divergentes cambio de concentración por emisor; BR tabla por emisor (VM DOP, %VM, HHI aporte, límite interno, holgura/exceso).
- **Sin selector VaR·ES·Std** (Portafolio no tiene medida de riesgo — canon).
- **Moneda**: tabla solo DOP (cartera 100% DOP, §2) — la partición DOP/USD de Mercado NO se replica; unidad DOP explícita en encabezados.
- **Leyenda de prorrateo** en toda vista por emisor (dona por emisor, top-N, tabla de concentración): aquí es *composición por exposición observada* — nota: la exposición SÍ es por emisor (matriz de Exposición, handoff §1); la leyenda del shell aplica solo a contribuciones de riesgo, no a VM. Decisión: en Portafolio NO se muestra la leyenda de prorrateo (no hay medida de riesgo que prorratear); se documenta para X.
- **Decisiones abiertas resueltas**: (1) treemap vs dona → dona (paridad empírica Mercado; treemap sin precedente en la librería de componentes del front); (2) el eje del área apilada = rating (no clase de activo como Mercado — rating es el eje primario §2); (3) KPI "Calificación predominante" con tendencia cualitativa (↑/↓/=) por migración del share.

---

## A-phase — Bead librisk-a66 (F1.5 Wireframe spec — VaR/Riesgo)

**Corpus re-verificado 2026-08-20**: `8b3bd636c070fe38` (sin cambios). Re-fetch `Capa2_RI_MetodologiaCredito.md`: "VaR = medida por dimensión y tiempo (sin contraste contra 'empírica': la distribución es simulada)" [guia]; selector VaR·ES·Std solo VaR y Marginal, "cambia los datos, nunca el layout"; "brecha Σ standalone − cartera = beneficio de diversificación"; leyenda de prorrateo (§2) aplica: contribuciones de riesgo por emisor son prorrateo por exposición.

### Spec del artefacto (sección VaR en 03-wireframe-specs.md)

- **Tabs pinneados por el shell**: Global · Por Calificación (no se renombran). Molde dashboard §4 íntegro + **selector VaR·ES·Std** (mismo set de visuales por medida; etiqueta `<Medida>` dinámica en títulos/KPIs/columnas).
- **Tab Global** (§7.2): KPIs = `<Medida>` Total (DOP, vs anterior) · Razón `<Medida>`/VM (%) · Top Driver (emisor mayor contribución prorrateada; informativo no navegable — deferral F1.2) · Volatilidad anualizada σ·√252 (**fija ante el selector** — es σ del libro; tooltip explícito) · + Uso Límite (fija). 2×2: TL **área apilada temporal** de la medida por rating (§7.2 métrica×tiempo + §9; paridad `var-global.png`, apilado por rating no clase); TR **dona por emisor** (top-7+"Otros"; leyenda de prorrateo); BL **divergentes de cambio** (Δ medida por grupo + Total; selector dimensión rating default/emisor); BR **tabla de descomposición jerárquica** rating→emisor exportable (VM DOP · `<Medida>` DOP · % del total · vs anterior).
- **Tab Por Calificación** (§7.2 métrica×calificación): KPIs = `<Medida>` Total · Rating de mayor aporte (categoría + monto) · Share del top rating · **Beneficio de diversificación** (Σ standalone − cartera; ancla Brain metodología) · + Uso Límite. 2×2: TL barras `<Medida>` por rating; TR **standalone vs contribución por rating** (barras agrupadas — visualiza la diversificación); BL divergentes Δ por rating; BR tabla por rating expandible rating→emisor.
- **Colapso top-7+"Otros"** en vistas gráficas por emisor (coherencia con la regla de sección de Portafolio; el "top-8+Otros" literal del §7.2 se registra como desviación para el PM). Tablas exentas.
- **Decisiones abiertas resueltas**: (1) TL Global apilado por rating (lee total + mezcla; evita duplicar con Por Calificación); (2) TR de Por Calificación = standalone vs contribución (no repite el área apilada); (3) Vol anualizada no conmuta con el selector — única tarjeta fija de contenido, tooltip; (4) sin histograma de distribución en esta sección (§7.2: no se contrasta contra "empírica"; la distribución vive en Escenarios).

---

## A-phase — Bead librisk-iq9 (F1.7 Wireframe spec — Escenarios)

**Corpus verificado 2026-08-20**: catálogo devuelve `36d2a031b434c89e` (distinto al `8b3bd636c070fe38` de F1.3–F1.5; contenido re-fetcheado de `Capa2_RI_MetodologiaCredito.md` idéntico en lo sustantivo — sin impacto). Anclas del fetch: "Stress de crédito [guia]: shocks del libro (subida de PD global/por emisor, N defaults forzados, N downgrades) como condicionamiento de la simulación; shocks de supuesto (fuente de transición, barrido de ρ, media/dispersión de recuperación). La sensibilidad a supuestos es entregable de primera clase"; "Escenarios = base vs shockeada (histograma post-shock con VaR superpuesto, cascada por instrumento)"; inviolable: distribución multimodal "nunca se representa como campana de Gauss"; espacio de UI para barrer ρ 15/25/35%.

### Evidencia empírica (verificada en este bead)

`escenarios-impacto-riesgo.png` (Mercado › Escenarios › Impacto en Riesgo): riel de configuración izquierdo (toggle de modo, medida VaR/CVaR, tipo de movimiento, curvas, tramo, magnitud, shock FX opcional, **Aplicar/Reset**); área de resultados = **columna de tarjetas apiladas** (VaR Pre Shock, VaR Post Shock, Delta VaR, Driver Principal, Impacto por familia) + **columna central de paneles** (dona/divergentes de impacto, tabla Delta por Factor) + **tabla ancha derecha** (Descomposición por Emisor e Instrumento: Pre/Post/Δ$/Δ%). Sin tarjeta de Uso Límite. Deltas con color de signo (rojo/verde).

### Spec del artefacto (sección Escenarios en 03-wireframe-specs.md)

- **Molde**: arquetipo simulador (shell §5, inviolable "nunca convertir dashboard↔simulador"): breadcrumb `Home > Escenarios > Impacto en Riesgo` + badge as_of + **badge de supuesto 2 estados** (pre-run base / post-run con barrido activo) + tab único pill; **sin selector VaR·ES·Std** (handoff §5); riel de control persistente izquierdo (MenuSidebar auto-colapsa); área de resultados con layout de paridad empírica: tarjetas KPI apiladas + paneles centrales + tabla ancha.
- **Riel de configuración** (§7.4): selector de **familia de shock** — **Libro** (subida PD global o por rating; N defaults forzados con selección de emisores; N downgrades por notch con alcance) / **Supuesto** (barrido ρ {15/25/35}%; fuente de transición S&P/Moody's; recovery (μ,σ) por seniority). Magnitudes + Aplicar/Reiniciar. Estado pre-run: resultados en vacío con instrucción.
- **KPIs post-run** (§7.4): VM Pre-Shock · VM Post-Shock · G/P Total (Δ y %) · Driver principal (emisor con mayor pérdida — prorrateo N/A: la pérdida por posición es salida directa de la revaluación, pero tooltip aclara que en shocks por rating los emisores del mismo rating comparten distribución, §2). **Sin tarjeta Uso Límite**: paridad empírica (no existe en Escenarios de Mercado) + el G/P de escenario no es métrica con límite configurado — desviación del molde dashboard documentada para PM.
- **Paneles de resultados**: (1) **divergentes P&L por rating** (shock−base); (2) **histograma post-shock** — silueta **asimétrica a la izquierda y multimodal** (jorobas 0/1/2/3 defaults), **línea de VaR**, overlay opcional de la base (outline), **zoom multinivel cuerpo/cola** (§9); anotación de artefacto: *nunca campana de Gauss* (inviolable); (3) **waterfall** de pérdida por instrumento (top-7 |G/P| + "Otros"); (4) **tabla por instrumento** exportable: VM Pre / VM Post / G-P (Δ y %).
- **Modo barrido de ρ**: chips ρ=15/25/35 sobre el área de resultados conmutan el escenario mostrado (paneles y KPIs); franja comparativa fija VaR/ES por ρ; el histograma superpone las 3 siluetas en outline al activar "Comparar".
- **Color**: G/P con semántica económica de signo (paridad empírica + Capa1 Principios "semántica de color por dominio económico"); las medidas de riesgo (VaR pre/post, franja por ρ) en neutro. Tensión con la regla del shell "deltas en neutro" documentada para PM.
- **Decisiones abiertas resueltas**: (1) layout resultados = paridad empírica (tarjetas apiladas + paneles + tabla), no la rejilla 2×2 del dashboard; (2) la línea de VaR del histograma usa el percentil de la metodología oficial (sin selector local de medida); (3) defaults forzados eligen emisores concretos (la exposición SÍ es por emisor, §1) sin violar §2 (la distribución sigue siendo por rating).

---

## A-phase — Bead librisk-mvx (F1.6 Wireframe spec — Marginal)

**Corpus verificado 2026-08-20**: `36d2a031b434c89e`. Re-fetch `Capa2_RI_MetodologiaCredito.md` [guia]: "**Marginal = dispersión riesgo-vs-tamaño (iso-risk)** — cuadrantes con los *fallen angels* (dimensionadas con rating alto luego degradadas) y **tres overlays de límite**: horizontal (% de riesgo), vertical (tamaño), y la **hipérbola iso-risk** (riesgo absoluto — la recomendada: topea la σ del portafolio)"; "σ standalone y marginal, VaR/ES marginal · contribución por dimensión (brecha Σ standalone − cartera = beneficio de diversificación)"; selector VaR·ES·Std solo VaR y Marginal, "cambia los datos, nunca el layout".

### Evidencia empírica (verificada en este bead)

`var-marginal.png` (Mercado › VaR › Marginal): 5 tarjetas apiladas (VaR Marginal Total + %VM · Mayor Aumento con driver · Mayor Reducción con driver · % VaR Explicable · Concentración Marginal Top-5), ranking horizontal por subclase con selector de dimensión, barras +/- de distribución con toggles Subclase/Top5 Emisores/Factores/Instrumentos, descomposición con selector, tabla jerárquica por Emisor expandible (VM DOP · VaR Marginal $ · VaR Marginal % · VaR Componental · % VaR Total), botón "Tabla VaR Marginal". Sin scatter iso-risk en Mercado — el iso-risk es aporte propio de Crédito (handoff §7.3 + Brain).

### Spec del artefacto (sección Marginal en 03-wireframe-specs.md)

- **Tab pinneado por el shell**: Global (único; barra con un pill). Molde dashboard §4 íntegro + **selector VaR·ES·Std** (etiqueta `<Medida>` dinámica).
- **KPIs (§7.3, fuente vinculante > 5 tarjetas empíricas)**: Marginal promedio · Mayor contribución (posición) · Posiciones sobre umbral · Concentración HHI de contribuciones · + Uso Límite (fija, conmutable).
- **2×2**: TL **scatter iso-risk** (X=VM DOP, Y=marginal % — cuadrantes A/B/C anotados, fallen angels en C, 3 overlays de límite h/v/hipérbola; hipérbola = recomendada); TR **dona** de contribución (top-7+Otros); BL **barras ranking** top posiciones por marginal; BR **tabla por posición** VM · marginal · standalone · % del total, jerárquica rating→emisor→instrumento, exportable.
- **Granularidad (§2)**: el marginal/standalone por posición es salida directa de la revaluación por escenario (no prorrateo) → nota de granularidad estilo §9.5, no la leyenda de prorrateo del shell.
- **Decisiones abiertas resueltas**: (1) scatter sin colapso top-7 (cada punto = posición; el colapso destruiría la lectura por cuadrantes) — puntos coloreados por **rating** (categórico neutro, eje primario §2); (2) los 3 overlays con límite no configurado → línea ausente + nota "Límite: N/D"; (3) fallen angels = anotación de cuadrante C + tooltip por punto (rating actual; el modelo no rastrea historial de rating — no inventar); (4) "Posiciones sobre umbral" = conteo sobre el límite del overlay activo (hipérbola por defecto); N/D sin límite.

### X/R — Bead librisk-mvx

X 2 rondas: R1 = 4 FAIL (dona/%-total con marginal no aditivo → componental Euler; negativos sin regla → dona positiva + nota diversificadoras + BL divergente con signo; KPI 3 acoplado al overlay activo → fijado a hipérbola; badge no declarado → explícito) + 9 WARN (Y≡marginal/VM; etiqueta hipérbola conmutada; leyendas de overlay siempre presentes; rating a letra ≤8; scatter fuera del alcance top-7; dona alineada con VaR; columnas Δ en BR; KPI 1 con signo; ranking con signo). R2 = 13/13 RESUELTO + 3 WARN nuevos cerrados (KPI 2 todo componental; HHI renormalizado sobre positivos; "Otros" divergentes partido por signo). R: PASS (1 MEDIA registrado en feedback-log; 2 BAJA corregidos: negativos en scatter bajo Y=0; KPI 3 N/D aunque existan h/v).

---

## A-phase — Bead librisk-dbv (F1.8 Visión General como entrada default — corrección PM)

**Corpus re-verificado 2026-08-21**: retrieval devolvió los mismos entries ya fetcheados (`Capa2_RI_MetodologiaCredito.md`, `Capa2_RI_PlataformaUX.md`, `Capa2_RI_Producto.md`, etc.) — sin cambios que afecten decisiones previas.

### Spec del artefacto (03-wireframe-specs.md §11 + shell §1/§2/§3 + mermaid)

- **Mandato del bead (feedback PM 2026-08-20)**: entrada default = Visión General (overview ejecutivo), no VaR; activar el ítem 1 del sidebar; wireframe con KPIs resumen del libro y del riesgo, estado de límites y mini-vistas hacia las secciones; paridad `vision-general.png`.
- **Arquetipo overview** (paridad empírica estructural `vision-general.png`: 4 cards → tabla límites + Top Drivers + Variación → 5 card_small): no molde 2×2 §4, sin barra de tabs (excepción acotada al overview; precedente empírico directo), sin selector VaR·ES·Std (medida canónica VaR etiquetada 99% · 1 año).
- **§2 garantizado**: badge de supuesto en cabecera con reglas de estado del shell §4; Top Drivers por emisor con leyenda de prorrateo fija visible; Variación por rating (eje primario); regla de comparabilidad de cortes (Δ = N/D si el supuesto del corte anterior difiere); DOP explícito en toda superficie; sin histograma (sin riesgo de Gauss).
- **Handoff §5 "VaR pantalla por defecto" sustituido por decisión del PM** — fuente: feedback-log 2026-08-20 (el PM es autoridad sobre el handoff en este punto; corrección explícita).
- **X adversarial**: 2 rondas — R1: 6 FAIL + 16 WARN; resoluciones aplicadas; R2: 22/22 RESUELTO. Observación no bloqueante: ratificación PM de deltas neutros (vs rojo/verde de Mercado) y de NavCards navegables.

---

## A-phase — Bead librisk-08x (F1.9 CORRECCIÓN PM — "Métricas de Riesgo" + as_of vs histórico)

**Corpus re-verificado 2026-08-21** (retrieval hybrid, filtro producto RI): sin entradas nuevas. `Capa2_RI_MetodologiaCredito.md` [guia] nombra la sección "VaR/Riesgo" y la fija como pantalla por defecto — ambas cosas ya sustituidas por decisión del PM (F1.8 default→Visión General; F1.9 nombre→"Métricas de Riesgo"). Guia admite desviación con razones explícitas: el PM es la autoridad de producto y su razón es de fondo (la medida VaR/ES/Std es el *selector*, no la identidad de la sección). Candidato a brain-gap junto con F1.8 (feedback-log).

### Spec del artefacto (rehacer §8 de 03-wireframe-specs.md)

- **Renombre integral**: sección "Métricas de Riesgo"; ruta `/metricas-de-riesgo/*`; breadcrumb `Home > Métricas de Riesgo > <Tab>`; sidebar ítem 4. "VaR" sobrevive SOLO como medida (selector VaR·ES·Std, KPI/card "VaR de Crédito Total" de Visión General, franja VaR/ES de Escenarios). Aceptación: ninguna pantalla se titula "VaR".
- **Separación estructural por tabs** (no toggle escondido): tabs pinneados **A la Fecha · Histórico**.
  - **A la Fecha** (default, href del sidebar): el riesgo AL CORTE — descomposición, drill-down, concentración de la medida. Absorbe: barras medida×rating (ex-8.2 TL), dona por emisor (ex-8.1 TR), standalone vs contribución (ex-8.2 TR), tabla jerárquica sin columnas de variación. KPIs: Medida Total · Razón Medida/VM · Top Driver · Beneficio de diversificación · +Uso Límite.
  - **Histórico**: la EVOLUCIÓN de la medida y los cambios de mezcla. Absorbe: área apilada temporal (ex-8.1 TL), divergentes de cambio vs corte anterior (ex-8.1/8.2 BL), tabla comparativa con Var DOP/Var %. Nuevo TR: evolución de la razón Medida/VM. KPIs: Medida Total (continuidad) · Δ Medida vs corte anterior · Volatilidad anualizada (propiedad histórica — se muda aquí desde ex-Global) · Rating de mayor Δ · +Uso Límite.
- **Excepción declarada a la regla del shell §3** ("nunca renombrar tabs pinneados"): la regla protegía hrefs internos entre beads; una corrección del PM la supera. Los hrefs se actualizan en el mismo bead (sidebar, NavCard 3 de Visión General, diagrama).
- **Propagación**: shell §1–§4 (menciones "solo VaR y Marginal" → "solo Métricas de Riesgo y Marginal"), §7/§10/§11 (referencias cruzadas, NavCard 3 → `/metricas-de-riesgo/a-la-fecha`), 02-user-journey (nombres de pantalla; además corrige el default obsoleto pre-F1.8), 03-wireframe-diagram.
- **KPIs conservan el patrón CardMetric completo (anterior, Δ, Δ%) en ambos tabs**: el chip Δ es contexto del molde §4, no análisis histórico; la separación estructural vive en los paneles y en las columnas de las tablas. Decisión documentada.
- **Regla de comparabilidad de cortes** (§11 F1.8) aplica a todos los Δ del tab Histórico (Δ jamás mezcla efecto cartera con efecto metodológico).

## F1.10 — Multi-moneda DOP/USD (bead librisk-eed, 2026-08-21)

**Brain fetch nuevo**: `capas/Capa2_RI_Consolidacion.md` [inviolable] — regla canónica 7: **"Moneda de consolidación: DOP único; otras monedas base = futuro"**. Ancla la regla de consolidación del mock.

**Evidencia Mercado (context dataset)**: `01-front-structure.md:34` — `Table.tsx` con **grupos de columnas DOP/USD**; `03-screenshots-index.md` `var-global.png` — tabla de descomposición **DOP/USD**. `formatMoneyCompact`: `$`, M/MM, 2 dec, "N/D".

**Spec A (corrección PM — la cartera NO es 100% DOP; instrumentos de crédito pueden denominarse en USD):**
1. **Se revierte la "excepción de paridad — moneda"** (§7 y §9.9 previos). Se sustituye por una **regla transversal de moneda** en el shell §4.
2. **Moneda del instrumento**: dimensión autoritativa de la capa de datos (DOP · USD). Visible en todo nivel hoja instrumento (chip/columna "Moneda") y **filtrable**: nuevo filtro contextual "Moneda" en el orden fijo de `CreditoFiltersSidebar` (bloque 3).
3. **Consolidación**: toda cifra agregada (KPIs, ejes, donas, áreas apiladas, medidas de riesgo) en **DOP consolidado**, USD convertido al **TC oficial del corte (as_of)**; regla **declarada** en subtítulo de KPI 1 de cada sección ("Consolidado en DOP · TC del corte") y en pie/export de tablas. Ancla: Consolidacion regla 7 [inviolable] + handoff §2 "moneda base DOP" (intacto: DOP sigue siendo la base).
4. **Tablas BR de composición/descomposición** (Portafolio Global, Métricas de Riesgo A la Fecha e Histórico): paridad Mercado — **grupos de columnas DOP · USD · Total (DOP consolidado)** para las columnas de monto. Tablas con nivel hoja instrumento (Marginal, Escenarios) y tabla de concentración por emisor: consolidado DOP + columna/chip Moneda en el nivel que corresponda + filtro.
5. **Dona de Portafolio**: "Vista por" gana opción **Moneda** (2 categorías — cabe en máx 8).
6. **Escenarios**: **sin shock FX** (pertenece a Mercado); posiciones USD se revalúan crediticiamente y se consolidan al TC del corte, **constante durante la simulación** — declarado en el riel y el export.
7. **Overview §11**: card 1 "Portafolio" agrega fila **"Exposición USD: $X MM DOP eq. · Y%"** (visibilidad USD sin romper el molde 4 cards ni el eje rating).
8. **Formato**: unidad explícita por grupo de columna ("DOP" / "USD" / "Total DOP"); jamás cifras de monedas distintas sin rótulo; N/D nunca cero.

---

## A-phase — Bead librisk-6rq (F1.11 AMPLIACIÓN PM — Factores de Riesgo activa)

**Brain re-verificado 2026-08-21** (retrieval hybrid producto RI, aviso "semantica degradado a lexical"): re-fetch `Capa2_RI_MetodologiaCredito.md` [guia] — ancla directa: "**Factores = gráfico de umbrales de Merton (densidad con fronteras Z y cola de default sombreada)**"; factores en clave de crédito: migración · default · correlación (ρ o cópula — el componente abierto en RD) · recuperación/LGD (Beta por seniority) · spread/curva por rating; inviolables §2 reconfirmados (rating eje primario, badge de supuesto, ρ barrible, "nunca campana de Gauss" **para la distribución de valor**).

**Evidencia empírica (verificada en este bead)**: `factores-mapa.png` (Mercado › Factores de Riesgo › Mapa de Factores): 4 tabs, 5 KPI cards (VaR Global · VaR Tasas · VaR FX · VaR RV · Factor Dominante), evolución VaR por factor (área), distribución por factor (dona+barras), cambio en composición (divergentes), tabla Breakdown por factor **con grupos DOP/USD** (no replicable en Crédito: F1.10 — medidas jamás partidas por moneda; desviación declarada).

### Spec del artefacto (§12 + shell §2/§3/§4 + §11.3 + screens + mermaid)

- Mandato PM: NO "próximamente" — las 8 se diseñan. Este bead activa **Factores de Riesgo** (`/factores-de-riesgo/mapa-de-factores`); Sensibilidades y Backtesting pasan a gris **"en diseño"** (estado de proceso, no promesa) y se activan en sus beads.
- Molde dashboard §4, tab único "Mapa de Factores", **sin selector** (medida canónica VaR 99%·1a etiquetada en KPI 1 y encabezado BR).
- KPIs 4+1: VaR Total · Factor dominante · **Efecto correlación** (VaR(ρ)−VaR(ρ=0), incremental) · Prob ≥1 default · Uso Límite.
- 2×2: TL barras **Euler aditivas** (migración·default·recovery·spread; correlación = overlay incremental rotulado — jamás barra: no es sumando Euler) · TR **umbrales de Merton** (variable latente; selector rating AAA…CCC, D excluido — absorbente; default = predominante por share VM §7.1; subtítulo fijo anti-Gauss) · BL **heatmap ρ** (anotación "matriz uniforme — ρ axiomático"; estado Alt 1 empírico definido — el panel audita el supuesto) · BR tabla breakdown factor→rating (DOP consolidado; fila correlación fuera del subtotal; pies F1.10 + convención).
- Desviación de paridad declarada: sin evolución temporal por factor (los 3 gráficos del §8 mandan; lo temporal vive en §8.2 con marcadores de supuesto).

### X/R — Bead librisk-6rq

X 2 rondas: R1 = 4 FAIL (Euler con correlación como sumando → overlay incremental; rating default sin criterio → share VM + D excluido; evolución temporal ausente sin justificar → desviación declarada; sidebar "activas sin spec" → gris "en diseño") + 8 WARN resueltos; R2 = 13/13 RESUELTO. R: **PASS** — 3 MEDIO corregidos (shell "5 secciones"→"todas las activas"; NavCard 6 hacia Factores en §11.3; pie F1.10 en BR §12); 2 BAJO diferidos a Fase 2 / gate PM (refuerzo visual anti-Gauss del TR; ratificación KPI Prob ≥1 default).

---

## A-phase — Bead librisk-yct (F1.12 AMPLIACIÓN PM — Sensibilidades activa)

**Brain re-verificado 2026-08-21** (retrieval hybrid producto RI, aviso "semantica degradado a lexical"): re-fetch `Capa2_RI_MetodologiaCredito.md` [guia] — anclas directas: "**Sensibilidades = tornado paramétrico a supuestos (a futuro CS01/spread duration)**"; "sensibilidades de PD con **common random numbers** para comparaciones no contaminadas por ruido"; "la sensibilidad a supuestos es entregable de primera clase: el Credit VaR se presenta con su dependencia de supuestos visible y barrible, no como cifra incuestionable"; inviolables §2 reconfirmados (badge de supuesto, ρ barrible 15/25/35, rating eje primario).

**Evidencia empírica (verificada en este bead)**: `sensibilidades-duracion.png` (Mercado › Sensibilidades › Duración): molde dashboard — 5 KPI cards apiladas, tabs pill (Duración · DV01 · Convexidad), dona+barras de composición, scatter YTM vs Duración, barras de contribución, tabla por tramo con drill. `03-screenshots-index.md` anota: "patrón de sensibilidades (futuro: tornado de supuestos)".

### Spec del artefacto (§13 + shell §2/§3 + §11.3 + screens + mermaid)

- Mandato PM F1.11/F1.12: activar **Sensibilidades** (`/sensibilidades/supuestos`, tab único "Supuestos"); Backtesting queda gris "en diseño".
- **Molde dashboard §4**, tab único, **sin selector VaR·ES·Std** (solo Métricas de Riesgo y Marginal): opera sobre la medida canónica **VaR — 99% · 1 año** etiquetada en KPI 1 y encabezado BR (mismo patrón que Factores §12).
- **Objeto de la sección (handoff §8)**: sensibilidad **paramétrica a los supuestos** del modelo — ρ, recovery (μ,σ) por seniority, fuente de transición. **CS01 / spread duration = extensión futura declarada, NO en el mock v1** (sin greeks por posición).
- **Convención OAT declarada**: barridos one-at-a-time alrededor del supuesto base del corte, con **common random numbers** (Brain [guia]) — los ΔVaR son atribuibles por supuesto y no contaminados por ruido MC; coherente con la regla de Escenarios "shocks de Supuesto excluyentes por run".
- **Frontera Escenarios/Sensibilidades (mandato del bead, sin solapamiento)**: Sensibilidades = **vista sistemática precomputada** del corte oficial (dashboard: mismos barridos en cada as_of, comparable en el tiempo, sin configuración del usuario, sin Aplicar, sin histogramas ni G/P); Escenarios §9 = **run puntual efímero** configurado por el usuario (simulador: riel, Aplicar, distribución post-shock, chips por ρ). El set de barridos de Sensibilidades pertenece a la **metodología oficial** (no editable); el preset de Escenarios sí es editable por run.
- **KPIs 4+1**: VaR base 99%·1a · Supuesto más influyente (|ΔVaR| máx del tornado) · Rango del VaR bajo supuestos (min–max del barrido) · Sensibilidad a ρ (VaR@35% − VaR@15%) · Uso Límite (fija).
- **2×2**: TL **tornado de supuestos** (barras horizontales centradas en el VaR base; extremo −/+ por barrido OAT) · TR **curva VaR vs ρ** (15/25/35 + marcador base + línea de límite si configurada — el ρ de §2 en primera clase) · BL **barras de impacto por recovery** (μ y σ por seniority, −/+) + fuente de transición (S&P→Moody's, un solo delta) · BR **tabla de barridos** exportable (supuesto · base · barrido · VaR− · VaR+ · ΔVaR máx DOP y % · Δ vs corte anterior bajo comparabilidad).
- **Reglas**: DOP consolidado, medida jamás partida por moneda (F1.10); impactos en **neutro** (son medida de riesgo, no P&L); comparabilidad de cortes (§11) extendida al supuesto más influyente (chip categórico); sin vistas por emisor → sin leyenda de prorrateo (§2 intacto); N/D nunca cero; badge de supuesto = **ancla del tornado** (el centro del tornado ES el supuesto del badge).
- **Propagación**: sidebar ítem 3 activo; shell §3 tabs; NavCard 7 en §11.3 (Supuesto más influyente — espeja KPI 2, anti-duplicación intacta); tabla screens; mermaid.

---

## A-phase — Bead librisk-o07 (F1.13 AMPLIACIÓN PM — Backtesting activa)

**Brain re-verificado 2026-08-21** (retrieval hybrid producto RI, aviso "semantica degradado a lexical"): fetch nuevo `Capa2_RI_MetodologiaMercado.md` [guia] — anclas directas de backtesting: **excepciones** (P&L realizado < −VaR del día; ~2.5/año esperadas al 99% en 250 días, parametrizable) · **Kupiec POF** (LR ~ χ²(1); rechaza demasiadas O sospechosamente pocas excepciones) · **Christoffersen** (independencia — no rachas — + cobertura, χ² conjunto) · **semáforo de Basilea** (verde 0–4 · amarilla 5–9 · roja 10+ en 250 días; multiplicador base 3 con recargo en amarilla). **[inviolable] Regla de interfaz**: el semáforo de Basilea es un **veredicto estadístico de validación del modelo** — no se confunde con el semáforo de cumplimiento de límites aunque compartan colores; si coexisten, se rotulan y no comparten componente visual sin etiqueta.

**Evidencia empírica (verificada en este bead)**: `backtesting-excepciones.png` = **placeholder "Contenido próximamente"** — Mercado NO tiene pantalla de Backtesting construida; la única evidencia es la **ruta** `/backtesting/resumen-excepciones` (`mercado_routes.txt` / `03-screenshots-index.md`) y el ítem 7 del sidebar (`layout.tsx:4-28`). Paridad aplicable: nombre de ruta/tab + molde dashboard §4; el layout interno es diseño propio anclado en handoff §8/§9 + Brain.

### Spec del artefacto (§14 + shell §2/§3 + §11.3 + screens + mermaid)

- Mandato PM F1.11/F1.13: activar **Backtesting** (`/backtesting/resumen-excepciones`, tab único "Resumen de Excepciones" — nombre de la ruta empírica de Mercado). Sidebar ítem 8 activo → 8/8 activas.
- **Molde dashboard §4**, sin selector VaR·ES·Std: se valida la **medida oficial VaR — 99% · 1 año** etiquetada (patrón §12/§13).
- **Dos lentes de validación (handoff §8 + catálogo §9)**: (1) **externa** — excepciones vs. realizado: serie + Kupiec + Christoffersen + semáforo Basilea; (2) **interna** — estabilidad Monte Carlo del estimador: traza de convergencia + bandas de confianza; **caveat de colas profundas (0.5%, 0.1% — bandas ~1/q) como elemento de UI** (subtítulo fijo + selector de cuantil), no nota al pie (aceptación del bead).
- **KPIs 4+1**: Excepciones 250d vs. esperadas · Kupiec POF (veredicto) · Christoffersen (veredicto) · Precisión MC de la cola (semiancho banda de confianza) · KPI 5 fija = **Estado de validación (semáforo Basilea)** — desviación declarada del "Uso Límite": el contexto-de-límite de la sección son los umbrales 0–4/5–9/10+ del veredicto estadístico; rotulado bajo la regla de interfaz [inviolable] (nunca el componente visual del semáforo de límites).
- **2×2**: TL serie de excepciones (P&L realizado vs. −VaR, marcadores de excepción + de cambio de supuesto) · TR panel de pruebas (Kupiec/Christoffersen: estadístico, p-value, veredicto; semáforo con multiplicador) · BL traza de convergencia + bandas por cuantil (selector 1% · 0.5% · 0.1%) · BR tabla de excepciones exportable.
- **Tensión metodológica anotada para PM (no gap declarado)**: el Brain define backtesting para VaR diario de mercado; el horizonte 1 año del Credit VaR exige definir la frecuencia/escala de observación — el mock declara "ventana de 250 cortes EOD; comparación según la metodología oficial del tenant" como valor del mock y registra la tensión en feedback-log.
- **Moneda (F1.10)**: P&L y VaR en DOP consolidado, jamás partidos por moneda; serie multi-corte → pie "Cada punto consolidado al TC de su fecha".
- **Propagación**: sidebar §2 (ítem 8 activo, nota "en diseño" eliminada); shell §3 tabs; NavCard 8 en §11.3 (estado de validación — anti-duplicación intacta); tabla screens; mermaid.

---

## A-phase — Bead librisk-bql (F2.1 Design System Mapping)

**Corpus re-verificado 2026-08-21**: `00dfc7c8353bacaf` (cambió desde `8b3bd636c070fe38`; re-fetch de `Capa2_RI_PlataformaUX.md` y `Capa1_Diseno_Tokens.md` — contenido consistente con F1.x, sin cambios que afecten decisiones previas).

### Spec del artefacto (04-design-system-mapping.md)

- **Fuente de tokens**: baseline visual vigente de RI (excepción de rebranding, `Capa2_RI_PlataformaUX.md` [guia] — RI es el único producto en excepción; el canon corporativo Capa 1 es el *destino*, no el vigente). Valores concretos verificados contra `context-mercado/01-front-structure.md` (`globals.css`, `colors-reports.tsx`): bg `#eff3f8` · primario `#0d77bf` · secundario `#1f2a4e` · error `#c10007` · éxito `#008236` · advertencia `#de560d` · hover `#d9e2ed` · contenedor blanco `rounded-[20px]` · card `#eff3f8` `rounded-lg` · Inter (H1 35 → body 13) · grid 4px · umbral 1280px. **Sin hex fuera de tokens** [inviolable].
- **Convenciones de contenido de Capa 1 que sí aplican** (transversales, `Capa1_Diseno_Tokens.md` [inviolable]): MM/M nunca K · DD/MM/AAAA · N/D nunca cero · dataviz máx 8+"Otros" · DOP por defecto · riesgo en neutro · semáforo solo estado de límite · color nunca canal único.
- **Tensión mono-tabular (declarada)**: Capa 1 exige IBM Plex Mono `tabular-nums` para cifras; el baseline RI es Inter puro. Resolución del mapping: **Inter + `font-variant-numeric: tabular-nums`** en toda celda/cifra (satisface la intención — alineación tabular — sin romper la coherencia local obligatoria del baseline). Registrada para PM.
- **Paleta de rating (AAA→CCC–D, 7 categorías ordinales)**: escala secuencial azul del front (`colors-reports.tsx`) usada como **ordinal neutra** — jamás semáforo, jamás semánticos; "Otros" en gris terciario.
- **Inventario de componentes**: barrido completo de §1–§14 del wireframe spec → ~34 componentes; base empírica = componentes reales del front (`CardMetric`, `DataStatus`, `TabsNavigation`, `Breadcrumb`, `MenuSidebar`, `Table.tsx` grupos DOP/USD, registro `DynamicComponentRenderer` con `loss_histogram`/`scatter`/`waterfall`/`heatmap`/`confidence_band`/`stacked_area_chart`). Nuevos propuestos: BadgeSupuestoActivo, NavCard, ScatterIsoRisk (overlays h/v/hipérbola), BadgeVeredictoBasilea, ChipsRho+FranjaVaRES, NotaFijaMetodologica, BannerResultadosObsoletos, PanelUmbralesMerton, TornadoSupuestos.
- **Plausibilidad backend**: cada gráfico mapeado a un `chart_type` del registro del front (mock plausible bajo el patrón backend-driven, `02-dashboards-backend.md`).

---

## Addendum F2.2 (bead librisk-zph) — Spec A del prototipo shell + Portafolio

**Artefacto**: Val Town HTTP val (`ri-credito-mock`), single-page HTML con hash-routing.
**Fuentes**: mapping 04 (tokens/componentes, Ledger L-1..L-14), wireframe §1–§7, handoff §2/§6/§7.1/§10; referencia visual = screenshots `portafolio-global.png`, `portafolio-concentracion.png`, `var-global.png` (dataset context-mercado cubre lo requerido; app viva no re-navegada — regla del dataset).

Alcance del bead:
- **Shell completo**: header global (Crédito activo; Mercado/Liquidez/Operacional grises e inertes en el mock), sidebar "Crédito" 8 ítems activos (orden F1.11), breadcrumb, cabecera de sección con BadgeSupuestoActivo (N-1, fuera de contenedores skeletonizables) + DataStatus "Datos 30/01/2026" + selector dataset + Filtros (panel derecho, orden inviolable).
- **Portafolio Global (§7.1)** y **Concentración (§7.2)** completos: 4+1 KPIs, rejilla 2×2, tabla jerárquica rating→emisor con partición v2 (DOP·USD·Total solo VM), pies de moneda.
- **Otras 6 secciones**: pantalla con chrome completo del molde + placeholder "contenido en la próxima iteración del prototipo" (nota de alcance del prototipo, NO estado de producto "próximamente" — las 8 son activas por mandato PM F1.11). Anotado para el PM: la descripción del bead ("4 tabs + próximamente") es anterior a F1.11; gobierna el wireframe aprobado en gate.
- **4 estados UI** por pantalla vía switcher flotante "Estado del prototipo": ok / loading (skeletons por panel; badge visible) / empty / error (Reintentar). En Preparando/No listo/Error → badge "Supuesto: N/D", nunca oculto.
- Datos mock coherentes: deuda dominicana DOP+USD (bonos, SBB, SBB c/garantía, CDs), ratings AA→B, TC 61.50, VM ≈ $8,4xx MM, HHI 4 dec, N/D nunca cero, "—" para no-aplica.
- Charts con ECharts CDN (paridad visual con producción); tokens solo por variables CSS de la tabla del mapping.

## A-phase — Bead librisk-qj3 (F2.3 Prototipo — Métricas de Riesgo)

**Corpus re-verificado 2026-08-21**: `8b3bd636c070fe38` (idéntico a F1.3–F2.2 — fetches previos de `Capa2_RI_MetodologiaCredito.md` [guia] y `Capa2_RI_PlataformaUX.md` [guia] siguen vigentes). Anclas activas: selector VaR·ES·Std "cambia los datos, nunca el layout"; "brecha Σ standalone − cartera = beneficio de diversificación"; leyenda de prorrateo §2 (contribuciones de riesgo por emisor = prorrateo por exposición, el modelo opera a nivel rating); rating eje primario; distribución simulada — sin histograma en esta sección.

### Spec del artefacto (iterar val `joselier3/ri-credito-mock`, no crear otro — aceptación del bead)

Fuente vinculante: `03-wireframe-specs.md` §8 (aprobado en gate librisk-tv6) + mapping `04-design-system-mapping.md` + patrón de implementación F2.2 (mismo shell, kpiCard, grid-2x2, estados, export).

- **Selector VaR · ES · Std**: segmented control en la cabecera de sección, visible SOLO en `metricas-de-riesgo` (y Marginal futuro). Estado `S.medida` (default VaR). Conmuta datos y etiqueta `<Medida>` en títulos/KPIs/encabezados — jamás la estructura (mismo set de paneles por medida, handoff §4/§7.2).
- **Modelo de datos mock (data.js)**: `RISK[medida] = { rate por rating (standalone, % del VM), divF por rating (contribución = standalone × divF) }` con ES ≈ 1.32×VaR y Std ≈ VaR/2.55 por rating (coherencia interna: ES>VaR>… no exigida entre Std y VaR — σ es dispersión, no cuantil; documentado). Contribución de cartera = Σ contribuciones por rating; emisor = prorrateo por exposición dentro del rating (§2). `LIMITES.medida = { VaR: 220 MM, ES: null, Std: null }` → Uso Límite "N/D" con tooltip bajo ES/Std (canon §4: es esperable que el límite viva en una sola medida). `SUPUESTO_MARKERS = [{ fecha: "03/01/2026", label: "ρ 20%→25% · S&P" }]` para los marcadores verticales de TL/TR de Histórico; el corte anterior (28/01) comparte supuesto con el as_of → los Δ son comparables (la regla de N/D por supuesto distinto queda representada en tooltip de los marcadores).
- **Tab A la Fecha** (§8.1): KPIs `<Medida>` Total (subtítulo consolidación DOP) · Razón `<Medida>`/VM · Top Driver (subtítulo visible con leyenda de prorrateo; chip categórico "anterior: X") · Beneficio de diversificación (con signo; negativo→"Penalización por concentración"+tooltip VaR no subaditivo) · Uso Límite fija. 2×2: TL barras `<Medida>` por rating (orden AAA→D, barra ausente+N/D si sin dato) · TR dona "Vista por" Emisor(default)/Tipo, top-7+Otros, leyenda de prorrateo en ambas vistas · BL standalone vs contribución por rating (agrupadas) · BR tabla jerárquica rating→emisor: VM en grupos DOP·USD·Total + `<Medida>` DOP consolidado (jamás partida) + % del total; SIN columnas Var; nota de prorrateo al pie + export.
- **Tab Histórico** (§8.2): KPIs `<Medida>` Total (mismo dato — continuidad) · Rating de mayor Δ (categórico) · Volatilidad anualizada del VM (fija ante el selector; frecuencia real de cortes ≈ 5 días → factor √(252/5); tooltip descriptivo) · Δ Razón `<Medida>`/VM (pp) · Uso Límite. 2×2: TL área apilada `<Medida>` por rating + marcadores de cambio de supuesto · TR línea razón `<Medida>`/VM + mismos marcadores · BL divergentes Δ por dimensión (Calificación default/Emisor top-7 |Δ|+Otros+prorrateo) · BR tabla comparativa con columnas Var(DOP)·Var% + pies de moneda F1.10.
- **Moneda (F1.10)**: filtro Moneda restringe el universo; las medidas se calculan sobre el universo filtrado y se consolidan SIEMPRE en DOP (partición v2: solo columnas VM se parten DOP·USD·Total).
- **Estados**: 5 (éxito/cargando/vacío/error/parcial — parcial = errBox en TR) por tab, patrón F2.2; KPIs N/D nunca cero; Uso Límite visible en todo estado.
- **Decisiones abiertas resueltas**: (1) límite configurado solo en VaR — ES/Std → N/D con tooltip (demuestra la regla del shell §4 sin inventar límites); (2) marcador de supuesto en 03/01/2026 con corte anterior comparable — la regla de comparabilidad se demuestra sin vaciar los Δ del mock; (3) vol anualizada con factor por frecuencia real (√(252/5)) y tooltip que lo declara.

## A-phase — Bead librisk-hh0 (F2.4 Prototipo — Marginal)

**Corpus re-verificado 2026-08-21** (retrieval hybrid producto RI, aviso "semantica degradado a lexical"): re-fetch `Capa2_RI_MetodologiaCredito.md` [guia] — anclas directas vigentes: "**Marginal = dispersión riesgo-vs-tamaño (iso-risk)** — cuadrantes con los *fallen angels* y **tres overlays de límite**: horizontal (% de riesgo), vertical (tamaño), **hipérbola iso-risk** (riesgo absoluto — la recomendada)"; selector VaR·ES·Std solo VaR y Marginal, "cambia los datos, nunca el layout"; §2 [inviolable]: rating eje primario, badge de supuesto siempre visible, no prometer granularidad emisor-específica.

### Spec del artefacto (iterar val `joselier3/ri-credito-mock` — pantalla `#/marginal/global`)

Fuente vinculante: `03-wireframe-specs.md` §10 (aprobado en gate librisk-tv6) + mapping 04 (ScatterIsoRisk = componente nuevo) + patrón F2.2/F2.3 (mismo shell, kpiCard, grid 2×2, 5 estados, export, `usoLimiteCard`).

- **SECTIONS**: quitar `placeholder:true` de `marginal`, añadir `medida:true` (selector visible; conmuta datos y `<Medida>`, jamás layout).
- **Datos (data.js)**: posiciones ganan `inst` (nombre de instrumento) + `mgF` (factor marginal/componental por posición, determinista) + flag `div` en 2 posiciones diversificadoras (BCRD CD AAA · BHD CD A — narrativa plausible: papel corto de bajo ρ). `MG_LIMITS` por medida: VaR = {h: %-riesgo, v: tamaño MM, hyp: MM riesgo absoluto}; ES/Std = {v solamente} → demuestra "Límite: N/D" por overlay y KPI 3 N/D aunque exista v/h (regla §10 KPI 3).
- **Derivación por posición (app.js)**: standalone_i = VM_DOP·rate[rating]; componental_i = standalone_i·divF[rating] con **ajuste de diversificadoras** (comp := −10%·standalone; el excedente se redistribuye proporcionalmente dentro del mismo rating) → **Σ componental = total de Métricas de Riesgo exacto** (coherencia inter-sección); marginal_i = componental_i·mgF_i (no aditiva por construcción). Prev análogo con vm prev (supuesto comparable — decisión F2.3 #2).
- **KPIs 4+1 (§10.1)**: Marginal promedio (media con signo, subtítulo consolidación) · Mayor contribución (componental, % del total válido; tooltip granularidad) · Posiciones sobre umbral (conteo vs hipérbola; N/D bajo ES/Std con subtítulo "Límite de riesgo absoluto: N/D"; sin semáforo) · HHI de contribuciones (positivas renormalizadas; subtítulo 1/HHI) · Uso Límite (usoLimiteCard, conmutable).
- **2×2**: TL **ScatterIsoRisk** (X=VM DOP MM; Y=marginal/VM %; puntos por posición coloreados por rating ordinal; cuadrantes A/B/C anotados + "fallen angels viven aquí" en C; 3 overlays con leyenda siempre presente; hipérbola y=hyp/x; Y<0 renderizado con línea y=0; dataZoom; opacidad 0.7; sin top-7; nota granularidad al pie) · TR dona componental "Vista por" Emisor(top-7+Otros)/Calificación/Tipo, solo positivas + nota fija "Diversificadoras: N posiciones, neto −$X" · BL divergentes top-7 |marginal| + Otros(+)/Otros(−) · BR tabla jerárquica 3 niveles rating→emisor→instrumento (chip Moneda en hoja, "Mixta" en emisor; columnas VM·Marginal·Componental·%total·Standalone·Benef.div·Var DOP·Var%; completa sin top-7; export CSV con notas).
- **Filtro Moneda deshabilitado** en marginal (misma regla F2.3: medidas leave-one-out sobre cartera consolidada; f-note).
- **Estados**: 5 (éxito/cargando/vacío/error/parcial=errBox TR); KPIs N/D; badge de supuesto en todo estado.
- **Decisiones abiertas resueltas**: (1) diversificadoras con componental negativo ajustado intra-rating para preservar Σ=total de Métricas; (2) hipérbola solo configurada en VaR (paridad con LIM_MEDIDA — demuestra los estados N/D sin inventar límites); (3) instrumento como campo de datos, no generado en render (export estable).

## A-phase — Bead librisk-6rn (F2.10 Prototipo — Backtesting)

**Brain re-verificado 2026-08-21** (retrieval hybrid, aviso "semantica degradado a lexical"): mismo corpus que F1.13 — `Capa2_RI_MetodologiaMercado.md` [guia] (excepciones, Kupiec POF LR~χ²(1), Christoffersen independencia+cobertura, semáforo Basilea verde 0–4/amarilla 5–9/roja 10+ en 250d, multiplicador base 3), `Capa2_RI_PlataformaUX.md` [guia c/ inviolables] (regla de interfaz del semáforo: veredicto estadístico ≠ cumplimiento de límites — jamás comparten componente visual sin rótulo; riesgo en neutro; N/D nunca cero), `Capa1_Diseno_Principios.md`. Sin entradas nuevas aplicables.

**Fuente de verdad del artefacto**: wireframe spec §14 (aprobado en gate PM) — KPIs 4+1 (Excepciones VaR99%·1a · Kupiec · Christoffersen · Precisión MC @99% · Uso Límite), 2×2 (TL serie excepciones · TR panel validación · BL convergencia+bandas con selector cuantil 1/0.5/0.1% y eje Y fijo común · BR tabla exportable con historia completa y fuera-de-ventana atenuadas), regla de sub-ventana homogénea, marcadores rombo un solo color de alerta, badge Basilea rectangular rotulado, chip contiguo "Ventana: N cambios de supuesto", sin selector VaR·ES·Std, DOP consolidado F1.10.

**Arquitectura del prototipo (evidencia leída en este bead)**: `app.js` IIFE con `SECTIONS` (entrada `backtesting` ya existe con `placeholder:true` — se activa quitándolo), router hash `parseHash()/nav()`, `bodyHtml()/bindBody()` dispatch, `kpiCard/usoLimiteCard/kpisNDMR/kpiSkeletons/panelSkeletons/statePanels/emptyBox/errBox`, `mkChart` (ECharts 5.5, tokens vía `TK()`, GRAY, riesgo en neutro), `exportCSV(which)` con BOM+`;`, switcher 5 estados (`ok/loading/empty/error/partial`). `data.js` → `window.RI_DATA` (AS_OF 30/01/2026, SUPUESTO ρ=25% S&P, SUPUESTO_MARKERS [03/01/2026 ρ20%→25%], TC 61.50, LIM_MEDIDA.VaR=220). **No existe clave BT** — se añade.

**Decisiones de diseño de datos (declaradas, para X y feedback-log)**:
1. **Frecuencia de cortes del mock: EOD diario** (desviación declarada del valor de mock "frecuencia mensual" escrito en §14): (a) el corte oficial de RI es EOD; (b) el canon de backtesting del Brain es ventana de 250 cortes diarios (~2.5 excepciones esperadas al 99%); (c) con cortes mensuales la ventana válida jamás alcanzaría 250 y toda la pantalla quedaría en N/D permanente — imposible evaluar el diseño de los veredictos en el gate. Las reglas de UI de §14 (las vinculantes) se preservan íntegras; solo cambia el valor ilustrativo de la frecuencia, re-rotulado en TL/TR/BR ("cortes EOD diarios — convención del mock").
2. **Historia BT**: ~270 cortes diarios hábiles terminando en AS_OF 30/01/2026; un único cambio de supuesto en la historia visible = el marcador compartido 03/01/2026 (ρ 20%→25%) → **ventana válida vigente = 19 cortes → Kupiec/Christoffersen/semáforo = "N/D — ventana incompleta (19/250)"** (regla §14 demostrada honestamente).
3. **Bloque de referencia "ventana anterior (cerrada)"** en el TR: la sub-ventana previa (S&P · ρ=20%, 251 cortes, cerrada el 03/01/2026) es homogénea y auditable — se muestra su veredicto archivado (4 excepciones → Kupiec Aceptado p=0.38 · Christoffersen Aceptado p=0.29 · zona VERDE, multiplicador 3.00) **atenuado y rotulado "ventana cerrada — referencia histórica, no es el veredicto vigente"**. Motivo: sin él, el PM no puede evaluar el diseño poblado de los veredictos (todo sería N/D); no cruza ningún cambio de supuesto (§2 intacto). Registrar para ratificación PM.
4. **Excepciones mock**: 5 en la historia visible — 4 en la ventana anterior (fuera de ventana → atenuadas en BR) + 1 en la vigente (26/01/2026) → KPI 1 "1 en 19 cortes (ventana válida, objetivo 250)", esperadas ~0.19.
5. **KPI 5 Uso Límite**: VaR base (forzado a medida VaR, no sigue S.medida global) vs LIM_MEDIDA.VaR=220 — mismo componente `usoLimiteCard` en variante fija; coherencia con el total de Métricas de Riesgo (mrAgg con medida VaR).
6. **BL convergencia**: banda de confianza vs N escenarios para cuantiles 1%/0.5%/0.1%, eje Y fijo común (min/max globales de las 3 series), semiancho final @99% = KPI 4 (cuadratura interna).

**Corrección post-X (bead librisk-6rn, hallazgo R-B2)**: la ronda X ajustó los números del mock — cambio de supuesto 03/01/2026 (sábado) es **efectivo desde el corte hábil 05/01/2026**; ventana válida vigente = **20 cortes** (esperadas ~0.20); ventana anterior = **250 cortes, cerrada el 02/01/2026** (Kupiec LR 0.755 p=0.385 · Christoffersen conjunto LR 2.47 χ²(2) p=0.29 · zona Verde 4/250). El bloque archivado lleva AMBOS rótulos (referencia histórica + veredicto estadístico ≠ límites, X-#1) y es no colapsable con el N/D vigente dominante (X-#12). Los valores desplegados gobiernan sobre los del plan A original.

---

## A-phase — Bead librisk-7vy (F2.8 Prototipo — Factores de Riesgo)

**Corpus re-verificado 2026-08-21**: `8b3bd636c070fe38` (sin cambios; entries de F1.1–F1.3 válidos). Fuente de diseño vinculante: **03-wireframe-specs.md §12** (spec F1.11 ya adversariada y aprobada por PM en el gate de Fase 1) + handoff §2/§8. Evidencia de producción: `context-mercado/factores-mapa.png` (precedente factual, no canon).

### Spec del artefacto (pantalla `/factores-de-riesgo/mapa-de-factores` sobre el val existente)

**Integración al shell existente** (patrón factual del val `joselier3/ri-credito-mock`): quitar `placeholder: true` del entry `factores-de-riesgo` en `SECTIONS`; branch en `bodyHtml`; trío `frHtml()`/`tablaFr()`/`chartsFr()`; branch en `bindBody` (selector de rating TR, drill factor→rating con `S.frExp`, retry, export); branch `"factores"` en `exportCSV`; `FR_TITLES()` para estados N/D. **Sin `medida: true`** (§12: sin selector VaR·ES·Std — medida canónica VaR 99%·1a etiquetada en KPI 1 y encabezado BR). **Filtro Moneda deshabilitado** — se añade `"factores-de-riesgo"` a la lista de `renderFilters` (§12/F1.10: la medida jamás se parte por moneda) con nota propia.

**Datos (data.js, `D.FR`)** — coherencia interna obligatoria:
- **VaR total = misma fórmula que Métricas de Riesgo / BT.VAR1A** (Σ vmDop·rate·divF ≈ $122.8MM): KPI 1 idéntico a mrAgg(VaR) — "mismo dato" §12. Prev = misma fórmula con `prev` y `TC_PREV` (mismo supuesto: cambio efectivo 05/01/2026 < corte anterior ⇒ Δ comparables, consistente con el resto del mock).
- **Atribución Euler**: pesos por rating y factor (migración/default/recovery/spread; Σ=1 por rating; monotónicos: ratings bajos más default-driven) aplicados a var_r ⇒ Σ factores×ratings = VaR total exacto. Factor dominante emergente ≈ **Default (~37%)**.
- **Efecto correlación** (incremental): `RHO_ZERO_FACTOR = 0.78` ⇒ VaR(ρ activo)−VaR(ρ=0) = VAR1A·0.22 ≈ +$27MM. Nunca barra: overlay anotado en TL + KPI 3 + fila BR fuera del subtotal.
- **Prob ≥1 default**: 86.9% (mock, "leída de los escenarios simulados").
- **Umbrales de Merton**: Z-boundaries por rating de partida (7: AAA…CCC; D excluido — absorbente) con bandas de llegada AAA…CCC, D y cola de default sombreada. Default del selector = **calificación predominante por share de VM = "A"** (misma definición que §7.1 KPI 4; verificado: VM_A ≈ 1,764MM > AA 1,328 > BBB 1,172…).
- **Matriz ρ**: 7×7 uniforme 25% (todas las celdas — bajo ρ axiomático uniforme el par intra-rating también es 25%; no es autocorrelación de un activo), escala secuencial neutra (azules), valor en celda, anotación fija "Matriz uniforme — ρ=25% axiomático (Alt 2)".

**KPIs 4+1** (§12): (1) VaR Crédito Total 99%·1a DOP, chips anterior/Δ/Δ%, sub "Consolidado en DOP · TC del corte"; (2) Factor dominante "Default" + % Euler, chip categórico "anterior: Default" (regla → N/D bajo supuesto distinto implementada en el código); (3) Efecto correlación DOP y % del VaR, tooltip convención incremental; (4) Prob ≥1 default % 1 dec, tooltip cruce al TR; (5) Uso Límite VaR (≈55.8%, cuadra con Backtesting), patrón `usoLimiteCard`.

**2×2** (§12): TL barras Euler 4 factores DOP + leyenda "Σ barras = VaR total" + overlay markLine "Efecto correlación: +$X (incremental, no aditivo)" + nota metodológica fija al pie (ambas convenciones, exportada) + conmutación a "Atribución parcial — residual no atribuido" si falta barra; TR Merton con selector 7 ratings, subtítulo fijo del panel "Retorno de activo estandarizado bajo Alt 2 — no es la distribución de valor del portafolio" (bloqueo anti-Gauss §2 — la curva normal es legítima aquí por ser la variable latente), **TR = panel designado del estado partial** (paridad con el resto del mock); BL heatmap ρ; BR tabla exportable factor→rating (rating eje primario dentro de factor), fila "Efecto correlación" rotulada "incremental" fuera del subtotal, fila "Total (Σ Euler)" = VaR total, columnas DOP consolidado jamás partidas por moneda, pies FX + convención (ambos en export).

**Decisiones abiertas resueltas**: (a) partial en TR aunque contiene el selector — paridad del mock domina, el subtítulo anti-Gauss vive en el cuerpo y en partial no hay curva que malinterpretar; (b) chips categóricos comparables porque el supuesto del corte anterior es el mismo (cambio efectivo 05/01) — la rama N/D existe en código y se documenta en tooltip; (c) sin serie temporal por factor (desviación ya declarada en F1.11/feedback-log).

### Correcciones X ronda 1 (bead librisk-7vy — 14 ataques: 3 bloqueantes, 8 advertencias, 3 notas)

1. **Medida global contaminante (BLOQUEANTE)**: FR jamás usa `mrAgg()`/`usoLimiteCard()` a pelo — `frAgg(prev)` fuerza `D.RISK.VaR` (misma fórmula, no depende de `S.medida`) y el Uso Límite se calcula contra `D.LIM_MEDIDA.VaR` con tarjeta propia rotulada "VaR 99%·1a" (precedente `btUsoLimite`).
2. **Subtítulo anti-Gauss en export (BLOQUEANTE)**: el branch `"factores"` de `exportCSV` incluye la línea `"Nota";"Retorno de activo estandarizado bajo Alt 2 — no es la distribución de valor del portafolio"`; en UI el subtítulo vive en el cuerpo del panel (capturable), no en tooltip.
3. **Fuente única del VaR total (BLOQUEANTE)**: `frAgg().total` = Σ vmDop·rate·divF sin redondear — idéntica a `mrAgg` con VaR y a la fórmula de `BT.VAR1A`; sin nuevas constantes. Uso Límite FR ≡ 55.8% de Backtesting.
4. **Default del selector Merton dinámico**: se computa con la misma definición de predominante de §7.1 (share de VM sobre cartera completa, `dop`), con rama `CCC–D → CCC` en código; no hardcode "A".
5. **Rama "Atribución parcial" no demostrable en mock**: se implementa la conmutación (helper con residual) pero ningún estado la dispara — registrada en feedback-log como no demostrable, para el PM.
6. **KPI 4 con rama tarjeta-completa N/D**: flag de comparabilidad (`D.FR.prevComparable`) con branch implementado; en el mock es comparable (cambio efectivo 05/01 < corte anterior).
7. **Diagonal 25% del heatmap**: tooltip por celda — "correlación entre pares de emisores de los ratings; no es autocorrelación de un activo (≠1 por diseño)".
8. **Monotonía de ρ declarada**: comentario/restricción en data.js — `RHO_ZERO_FACTOR 0.78 < RHO_PREV_FACTOR 0.93 < 1` (VaR crece con ρ).
9. **Zs derivadas de matriz de transición única**: `D.FR.TRANS` (7 orígenes × 8 destinos, filas Σ=100%, PD monotónica AAA→CCC: 0.01→22.73%); Z-boundaries vía Φ⁻¹ (Acklam) y **Prob ≥1 default computada** de las PDs por posición (≈14.3%) — coherencia por construcción, no cifra inventada.
10. **Redondeo del Total (Σ Euler)**: pie de tabla "totales calculados sobre valores sin redondear" (patrón estándar).
11. **Persistencia del selector en estados**: `S.frRating` persiste a través de partial/retry; selector = pills `.seg` existentes (data-frr).
12. **Cabecera del CSV con supuesto serializado**: heredada y explícita (patrón l.1325).
13. **Tooltip KPI 4 ajustado**: "mecanismo por rating de partida; la probabilidad agregada surge de la simulación conjunta".
14. **Dependencia hacia Visión General (NavCard 6 espeja KPI 2)**: anotada en feedback-log para el bead F2.7.

Convergencia X: 1 ronda — los 3 bloqueantes corregidos en el spec; sin requisitos en disputa.

## D-phase — Bead librisk-p1d (F2.9 Prototipo — Sensibilidades)
Canon aplicado del A-phase de librisk-yct (re-verificado entonces: tornado paramétrico a supuestos, CRN para comparaciones no contaminadas, sensibilidad a supuestos = entregable de primera clase, ρ barrible 15/25/35 [inviolable §2]). Sin retrievals nuevos: la implementación no abrió preguntas de canon fuera de lo ya fetched. Evidencia empírica: `sensibilidades-duracion.png` (molde), sin referente de tornado en Mercado — diseño propio anclado en spec §13.

---

## A-phase — Bead librisk-vyz (F2.7 Prototipo Visión General)

**Corpus re-verificado 2026-08-21**: `8b3bd636c070fe38` (sin cambios; entries F1.1–F1.3 válidos). Referencia visual: `context-mercado/screenshots/vision-general.png` (paridad estructural del overview).

### Spec del artefacto (pantalla Visión General en el val, spec §11)

- **Arquetipo overview** (no molde §4): fila 1 = 4 cards resumen · fila media = tabla "Límites y Métricas" (ancho) + Top Drivers + Variación divergente · fila inferior = **8 NavCards**. Sin barra de tabs (excepción overview, shell §3), sin selector VaR·ES·Std, **sin botón Filtros** (paridad `vision-general.png`; el overview ignora `S.moneda`). Entrada default del módulo (ya cableada: `SECTIONS[0]` + hash default).
- **Fuente única de cifras**: VaR total y por rating = `frAgg()` (≡ mrAgg-VaR ≡ BT.VAR1A — coherencia inter-sección por construcción); Top Drivers = `mrEmisores()` **con medida pinneada a VaR** (el overview no sigue el selector de otras secciones — mismo patrón que Backtesting §14); Marginal componental = `mgRows()` pinneado a VaR; HHI/mayor emisor sobre **cartera completa sin filtro** (helpers no-`filt()`); Sensibilidades = `sensAgg()`; Backtesting = `btWin()`.
- **Card 2**: 7 filas fijas AAA/AA/A/BBB/BB/B/CCC–D; grupos sin posiciones (CCC–D en el mock) muestran "— · Sin posiciones" (exposición nula real, no dato ausente — N/D reservado a dato faltante).
- **Card 4**: VaR 99%·1a, % VM, **% Patrimonio N/D** (patrimonio no configurado en el mock) + chip Δ% neutro + pill límite (LIM_MEDIDA.VaR=220).
- **Tabla límites** (4 filas): VaR total (interno 220, reg N/D) · HHI (interno 0.18) · Mayor emisor % (interno 15%) · Riesgo marginal por posición (interno hyp=8 MM, máx |marg| del libro). Semáforo solo en Estado.
- **Comparabilidad**: mock `FR.prevComparable=true` ⇒ Δ visibles; la rama del spec §11 ("supuesto del corte anterior distinto ⇒ TODOS los Δ N/D + tooltip") se demuestra con el estado **"Error parcial"** del switcher: card 4 chip, NavCard 1 Δ, NavCard 7 chip y panel Variación → N/D + banner; niveles y límites sobreviven.
- **NavCards**: datos distintivos exactos de la tabla §11.3 (anti-duplicación verificada contra filas 1–2); NavCard 8 con Kupiec vigente "N/D — ventana incompleta (20/250)" como TEXTO sin pill (regla [inviolable] §14).
- **Estados §6**: loading = skeletons por fila; empty/error = cards N/D + state-box con CTA; badges nunca ocultos (headHtml existente ya lo garantiza).
- **Decisiones abiertas resueltas**: (1) medida pinneada a VaR vía guardado/restauración temporal de `S.medida` en los helpers reutilizados — sin duplicar fórmulas; (2) tabla de límites sin export (el mandato BR-exportable es del molde §4, no del overview; Mercado tampoco exporta ahí); (3) "Error parcial" del overview = comparabilidad de cortes rota (rama distinta de la de Sensibilidades, documentada en el banner).

### X-phase (1 ronda, 12 ataques — correcciones al spec)

1. **Badge en loading** — ya garantizado por el shell (headHtml renderiza badges fuera de contenedores skeletonizables; loading solo skeletoniza el cuerpo). Declarado.
2. **Comparabilidad = condición de datos, no estado de fallo** — se implementa `ovComparable()` leyendo `FR.prevComparable` (dato); el estado "Error parcial" solo SIMULA prevComparable=false para demostrar la rama. La regla vive en la lógica de datos.
3. **Medida pinneada con señal visual** — "VaR — 99% · 1 año" rotulado en: título card 4, fila 1 de la tabla de límites, subtítulo de Top Drivers, título del panel Variación y NavCards 3/7; tooltip "medida fija — no sigue al selector de otras secciones" (patrón §14 Backtesting).
4. **Tabla de límites**: las 4 filas SÍ tienen límite interno en el mock (VaR 220 · HHI 0.18 · mayor emisor 15% · marginal/posición 8MM) ⇒ Uso y Estado computables en todas; Regulatorio N/D con tooltip "sin límite regulatorio configurado". Aclarado.
5. **Paridad** — desviaciones ya declaradas y aprobadas en Fase 1 (§11 wireframe + feedback-log): sin tabs/Filtros = paridad empírica; 8 NavCards navegables = mandato del bead, registrado. Se inventarían en 05-prototype-metadata.
6. **Fila "Mayor emisor"** se rotula "Mayor emisor (% del VM)" — exposición, no riesgo; fila marginal con tooltip de granularidad; leyenda de prorrateo al pie de la tabla no necesaria (no hay cifras de riesgo por emisor en ella).
7. **%Patrimonio N/D** con tooltip-CTA ("Patrimonio no configurado — configurarlo en Administración habilita esta razón").
8. **Panel Variación en N/D** = state-box propio con el tooltip de comparabilidad + referencia al banner (no hueco vacío).
9. **NavCard Backtesting** añade marco: "esperadas ~0.2 al 99% en 20".
10. **Card Portafolio**: línea "Exposición en USD (equiv. DOP): X MM · Y%".
11. **Chip NavCard Sensibilidades**: "vs corte anterior: ρ…", neutro, tooltip aclarando que es el supuesto más influyente del corte anterior (categórico, no Δ metodológico).
12. **Título Top Drivers**: se mantiene el título aprobado del wireframe §11.2; el subtítulo declara la lectura ("ranking de exposición ponderada por el riesgo de su rating — nivel rating") como ya exigía el spec aprobado.

## A-phase — Bead librisk-ykp (F2.5 Prototipo — Escenarios)

**Corpus verificado 2026-08-21**: `brain_catalog` devuelve `36d2a031b434c89e` — idéntico al verificado en F1.7/F2.x; canon vigente sin re-fetch necesario. Anclas aplicables ya fetchadas: `Capa2_RI_MetodologiaCredito.md` [guia con inviolables] (multimodal "nunca campana de Gauss"; barrido ρ 15/25/35 como espacio de UI de primera clase; shocks de libro = condicionamiento de la simulación; shocks de supuesto excluyentes-atribuibles), `Capa2_RI_PlataformaUX.md` [guia con inviolables] (arquetipo 2 simulador — riel persistente, "nunca convertir dashboard↔simulador"; N/D nunca cero; no ocultar corte; semáforo solo límite), `Capa1_Diseno_Principios.md` (semántica de color por dominio económico → P&L con signo; riesgo en neutro).

### Spec de implementación (sobre wireframe §9 aprobado + DS mapping #21/#22/#33/#35/#37)

- **Estado del simulador** (`S.esc*`): `escRun` (null=pre-run | objeto resultado), `escFam` (libro|supuesto), sub-config libro {pdBp, pdScope, nDef+emisores, nDown+notches+alcance — combinables}, supuesto radio {barrido ρ | fuente | recovery μ/σ — excluyentes}, `escStale` (banner obsoleto §9.6), `escFail` (error de run con Reintentar), `escChip` (ρ activo), `escCompare`, `escZoom` (cuerpo/banda/cola), `escExp` (drill tabla).
- **Fuente única de cifras**: VaR base ≡ `BT.VAR1A` (misma constante que Métricas de Riesgo/FR/SENS). Factores de ρ del set SENS/FR (0.885 / 1.0 / 1.13 — monotonía X-#8 heredada); fuente S&P→Moody's = ×1.036 (convención X-12 de SENS); recovery reutiliza fLo/fHi de SENS. ES por ρ = ES total (RISK.ES) × mismo factor — convención declarada del mock.
- **G/P del barrido de ρ**: VM medio casi invariante (−0.4/−0.5/−0.6MM aprox) — la lectura del barrido es la franja VaR/ES, no el G/P (nota corta en UI, §9.7). G/P de shocks de libro: pérdidas por posición = vm×rate[rating]×k(shock)×jitter determinista (realización simulada — nota §9.5).
- **Histograma**: mixture de jorobas 0/1/2/3+ defaults (silueta asimétrica izquierda, multimodal — inviolable anti-Gauss anotado en subtítulo); línea VaR @percentil oficial sin selector local; overlay base outline; toggle Comparar (3 siluetas ρ en outline); zoom 3 niveles cuerpo/banda/cola (presets de rango x + escala y).
- **Franja VaR/ES por ρ** fija (no conmuta con chips): neutro; límite VaR $220MM → "uso YY% @ρ=25%" (ρ base del set; si el set editado no lo contiene, el más cercano etiquetado).
- **Waterfall**: top-7 |G/P| + "Otros" + Total; semántica de signo. **Divergentes por rating** + barra Total; etiquetas Δ%.
- **Tabla jerárquica** rating→emisor→instrumento (completa, sin top-7), columnas Moneda(chip)·VM Pre·VM Post·G-P·G-P% (todo DOP consolidado, TC constante — línea fija en el riel); export CSV con notas §9.5 + consolidación.
- **Badge 2+ estados** §9.2 exactos (pre-run base / chip shock de libro / flecha supuesto efectivo / barrido / N/D en degradados).
- **Ciclo §9.6**: pre-run instructivo → Recalculando (skeletons por panel ~700ms, riel vivo) → post-run → obsoleto (banner + atenuado, jamás limpiar en silencio) → fallo con Reintentar (mock: botón de demo en el riel no — se simula con estado "partial"? NO: fallo de run se demuestra con un control del riel "simular fallo" descartado — en su lugar el 5º estado del switcher global "Error parcial" degrada el histograma post-run; el fallo-de-run completo se representa con `escFail` accionado por un checkbox discreto del riel de prototipo). — decisión: checkbox de prototipo en el riel para demo del fallo del run.
- **Auto-colapso del MenuSidebar** cuando la sección es Escenarios (clase CSS en body; paridad shell §2).
- **Estados globales del switcher**: loading → skeleton total; empty/error → KPIs N/D + state-box + badge Supuesto N/D (riel visible pero Aplicar deshabilitado — sin corte no hay run); partial → post-run con histograma en errBox (paridad parcial de otras secciones).
- **Decisiones abiertas resueltas**: (1) el fallo de run (§9.6) se demuestra con checkbox de prototipo "Simular fallo del recálculo" dentro del riel, rotulado como control del mock; (2) pre-run es el estado inicial al entrar (uiState ok); (3) selector de emisores para defaults forzados = checklist de top-6 emisores por VM.

### X-phase REVISE (librisk-ykp — 12 ataques, 5 bloqueantes corregidos)
1. **ES por ρ con factores propios más empinados** (0.86/1.0/1.17 → ES/VaR sube 1.245→1.445→1.496… en realidad razón = 1.445×(fE/fV): 1.404/1.445/1.496 monótona) — la cola engorda relativamente; fE@25%=1.0 preserva cuadratura con mrAgg(ES) (condición #14).
2. **Set de ρ NO editable en v1 del mock** — desviación declarada del wireframe §9.3 registrada en feedback-log para el gate (el editor exigiría modelo de interpolación; anclas 0.78@0/0.885@15/1.0@25/1.13@35 documentadas para implementación real). Tie-break del ρ-ancla (mayor=conservador) anotado para el handoff.
3. **Reparto por posición en familia Supuesto: drift uniforme intra-rating, sin jitter** — G/P% idéntico entre emisores del mismo rating (demuestra §2 en pantalla); Driver principal = mayor exposición del rating más castigado, tooltip lo declara.
4-5. **Nota §9.5 con 2 variantes por familia** (libro: "…comparten distribución — diferencias por exposición y realización simulada"; supuesto: "…diferencias exclusivamente por exposición") en la terna de ubicaciones: pie del área de resultados + pie de tabla (y export) + tooltip KPI Driver.
6. **Anti-Gauss estructural en zoom**: dataZoom slider con preview de la silueta completa siempre visible; presets cuerpo/banda/cola mueven la ventana sobre el minimapa — la multimodalidad nunca sale de pantalla.
7. **Fallo de run movido al switcher del prototipo** (control meta segregado, visible solo en Escenarios) — el riel queda superficie de producto pura.
8. **Error/empty globales**: escRun se invalida a pre-run (el run era de un corte que ya no está); errBox con Reintentar / emptyBox con CTA dataset (paridad); Aplicar deshabilitado con title explicativo.
9. **Partial** = histograma en errBox declarado "convención de demo del switcher, sin semántica de producto — defensa plausible: la distribución completa es payload separado y pesado" (nota en feedback-log).
10. **Badge: 6 plantillas literales §9.2**; recovery modifica UNA seniority por run (radio Senior/Subordinada).
11. **Chips ρ deshabilitados en estado obsoleto** (activo fijado, tooltip "Aplicar para recalcular").
12. **Franja con rótulo "DOP MM · consolidado"**. 13. KPI G/P en barrido: signo tipográfico con intensidad reducida (nota PM). Cifras base: VM 6,138.30 · VaR 122.79 (uso 55.8% @ρ25 vs límite 220) · ES 177.44.

## Addendum A-phase — bead librisk-hzu (F2.6 Auto-validación completa, 2026-08-21)

**Artefacto**: `05-prototype-metadata.md` consolidado (formato del output contract del skill fase 2) + capturas Playwright frescas `prototype-captures/f26-*.png` de las 8 secciones.

**Alcance de la validación (spec)**:
- **Grupo A (A1–A6)** sobre el módulo completo (9 pantallas / 8 secciones + Visión General default):
  - A1 marca: baseline RI (`Capa2_RI_PlataformaUX.md` [guia con inviolables]) — tokens `#eff3f8`/`#0d77bf`/`#1f2a4e`, Inter, semáforo rotulado.
  - A2 fintech: sin verde/rojo en series (inviolable "no pintar series con semánticos"), N/D nunca cero, métrica siempre con contexto de límite (`Capa2_RI_Producto.md`), anti-Gauss (handoff §4: distribución multimodal, nunca campana).
  - A3 flujo: 9 pantallas de `03-wireframe-specs.md` presentes; hash-routing = mermaid; 4 núcleo con contenido pleno + 4 recomendadas TAMBIÉN desplegadas (mandato PM F1.11 supera el alcance mínimo "próximamente" del prompt del loop).
  - A4: 5 estados por pantalla (ok/loading/empty/error/partial) + ciclo simulador §9.6 en Escenarios.
  - A5: Ledger L-1..L-14 y Financial Data Contract de `04-design-system-mapping.md` verificados en superficie; invariantes §2 (rating eje primario, badge de supuesto en TODA pantalla, DOP, granularidad emisor no prometida) y §6 (molde KPIs+2×2) y §10.
  - A6: lado a lado con dataset `context-mercado/screenshots/` (regla: dataset primero; app viva solo si el dataset no cubre).
- **Grupo B**: B1 JTBD del brief trazado click-a-click con captura por paso; B2 acción primaria por pantalla; B3 cero dead-ends en 9×5 estados; B4 roles RBAC del Brain — **Administrador, CRO, Analista, Lector** (`Capa2_RI_Producto.md` [guia], secciones RBAC [inviolable]): CRO→"¿cumplo hoy? ¿dónde?" (límites/uso%/semáforo), Analista→drill-down + supuestos + sensibilidad ρ, Lector→Visión General legible, Administrador→auditabilidad visible (badge, as_of, fuente) — la superficie de gobierno/config queda fuera del mock (declarar, no flag).
- **Coherencia transversal (chequeo propio del bead)**: VaR base único $122.79MM ≡ Métricas/Marginal/FR/SENS/BT/OV; límite $220MM y uso 55.8% consistentes; fecha de corte única DD/MM/AAAA; badge idéntico entre secciones salvo plantillas §9.2 en Escenarios.
- **Método de captura**: MCP Playwright del entorno exige Chrome del sistema (no disponible) → script chromium (`/tmp/opencode/`) como en beads previos; desviación ya documentada en metadata.

**Decisiones abiertas resueltas**: (1) el metadata se REESCRIBE al formato consolidado del skill en vez de seguir acreción por bead — las notas por bead se preservan como anexo de historia; (2) B4 se responde con los 4 roles RBAC del Brain, sin inventar "decision clusters" no documentados; (3) las desviaciones declaradas pendientes de ratificación PM (frecuencia BT diaria, límite fuera de escala en SENS, partial=rama badge, bloque archivado BT) se consolidan en una sección única "Desviaciones para ratificación del PM" visible para el gate.

### Ronda X (librisk-hzu) — 15 ataques, resolución
Aceptados 14/15 (todos los BLOQUEANTES): (1) matriz pantalla×invariante-§2 explícita; (2) sub-checklist DOP/F1.10 de 4 puntos; (3) anti-Gauss con 3 superficies nombradas (histograma Escenarios, subtítulo Merton UI+CSV, subtítulo doble BL Backtesting); (4) badge validado por estado (regla X-2: N/D solo degradación de dataset); (5) **valor cero de los ✅ per-bead — toda celda se re-verifica sobre el val desplegado hoy**; (6) lista transversal ampliada (VM total, VaR, ES, límite+uso, HHI, mayor emisor, USD%, TC, fecha, marcador supuesto); (7) regla de precedencia: fuente de verdad numérica = val desplegado + wireframes aprobados, addenda A-phase = historia; (8) B4 reformulado como tareas medibles por rol (CRO ≤2 clics a peor incumplimiento; Analista KPI→Marginal ≤3 clics + barrer ρ; Lector OV sin dead-end; Administrador auditabilidad badge/as_of/fuente en 10 pantallas); (9) exclusión RBAC-gating movida a ratificación PM; (10) plan de capturas enumerado por hash — **10 pantallas**, + estados + variantes de medida + ciclo simulador + secuencia B1; (11) capturas con el switcher del mock rotulado (ocultarlo donde sea viable); (12) A6 dos modos (referente directo / paridad estructural con cita §N); (13) barrido exhaustivo de desviaciones-para-PM con bead de origen; (14) tabla evidencia pantalla×estado×archivo + rechazos X preservados; (15) conteo cerrado: 10 hashes.
Matiz al (10): la matriz completa 10×5 estados se evidencia con **aserciones DOM programáticas** (script chromium) + capturas de muestra por tipo de estado; capturar 50 PNG no añade información y contamina el folder — decisión registrada para el PM.

## Bead librisk-hzu (F2.6) — Spec de auto-validación completa (fase A, 2026-08-21)

**Corpus re-verificado**: catálogo `dominio: diseno` devuelve `corpus_version 00dfc7c8353bacaf` (distinto a versiones previas del snapshot). Re-fetch completo de las 2 entradas que gobiernan la validación:
- `Capa2_RI_PlataformaUX.md` [guia con inviolables] — sin cambios sustantivos: jerarquía Módulo→Sección→Tab [inviolable], contrato de navegación (orden de controles, dominios autoritativos) [inviolable], "crédito copia el contrato completo de mercado" [inviolable], semáforo Ok/Advertencia/Incumplimiento nunca reasignado [inviolable], 13 prohibiciones de construcción [inviolable] (sin hex fuera de tokens, N/D nunca cero, DD/MM/AAAA, sin métrica de riesgo sin contexto de límite, no dashboard↔simulador, insignia "Datos {fecha}" siempre visible, semáforo Basilea ≠ semáforo de límites rotulados si coexisten), baseline RI excepción de rebranding (`#eff3f8`/`#0d77bf`/`#1f2a4e`, Inter).
- `Capa2_RI_MetodologiaCredito.md` [guia con inviolables] — sin cambios: rating eje primario (no prometer granularidad emisor-específica del modelo), badge de supuesto siempre visible (fuente transición + método correlación + ρ), ρ barrible 15/25/35, "nunca campana de Gauss", selector VaR·ES·Std solo VaR y Marginal ("cambia los datos, nunca el layout"), PD insumo no salida.

**Alcance de la validación (universo)**: 10 pantallas / 8 secciones del val `joselier3/ri-credito-mock`:
`#/vision-general` · `#/portafolio/global` · `#/portafolio/concentracion` · `#/metricas-de-riesgo/a-la-fecha` · `#/metricas-de-riesgo/historico` · `#/marginal/global` · `#/factores-de-riesgo/mapa-de-factores` · `#/sensibilidades/supuestos` · `#/escenarios/impacto-en-riesgo` · `#/backtesting/resumen-excepciones`.

**Protocolo de verificación (fase D del bead)**:
1. Captura Playwright fresca (chromium vía script — MCP exige Chrome de sistema, no instalable) de las 10 pantallas en estado éxito + verificación de estados vía switcher en muestreo dirigido; consola limpia (0 errores) como criterio duro.
2. Grupo A (A1–A6) evaluado sobre el módulo completo, no por bead: A5 incluye re-chequeo del Ledger L-1..L-14 del mapping contra el DOM real (hex fuera de :root, fechas, N/D, semáforo, badge). A6 contra los 10 screenshots de `context-mercado/`.
3. Grupo B: B1 traza JTBD del brief click-a-click (Playwright); B2 acción primaria por pantalla; B3 barrido de estados × pantallas sin dead-ends; B4 cobertura de roles RBAC de `Capa2_RI_Producto.md` (Administrador · CRO · Analista · Lector) — flag, no bloqueante.
4. Invariantes del handoff auditadas transversalmente: §2 (DOP, rating eje, badge, anti-Gauss, granularidad no prometida), §6 (molde KPIs+2×2), §10 (patrones UX transversales).
5. Salida: `05-prototype-metadata.md` reescrito como documento consolidado (URL, tokens, tabla de pantallas×estados, Grupo A+B formal, desviaciones declaradas acumuladas para ratificación del PM en el gate).

---

## A-phase — Bead librisk-k9s (F1.14 AMPLIACIÓN PM — Deterioro NIIF 9: Staging + Clasificación contable)

**Brain re-verificado 2026-09-02** (retrieval hybrid "NIIF 9 IFRS 9 deterioro ECL staging SICR" + capa 4 "provisiones REA categorías A-E"): **sin cobertura NIIF 9/ECL en el Brain** — `Capa2_RI_MetodologiaCredito.md` es solo Credit VaR; Capa 4 regulatorio cubre reportería SB/SIMV y liquidez-solvencia, no deterioro ni REA-vs-ECL. Gap ya registrado en feedback-log 2026-08-21 (pendiente aprobación PM — no declarado). **Fuente vinculante única del contenido: `06-handoff-ifrs9-ecl.md`** (§1 alcance, §2 stages, §3 SICR); molde/shell gobernados por los entries ya fetcheados (`Capa2_RI_PlataformaUX.md` [guia+inviolables], `Capa1_Diseno_Tokens.md` [inviolable]) y el wireframe aprobado §1–§6.

### Spec del artefacto (nuevo §15 en 03-wireframe-specs.md + propagación shell §2/§3 + §7.1 TR + mermaid)

- **Sección nueva**: sidebar ítem 9 **"Deterioro (NIIF 9)"**, href `/deterioro/staging`. Tabs pinneados: **Staging · ECL · Movimientos · Conciliación REA** (set completo fijado por el PM en feedback-log 2026-08-21; este bead spec-ea Staging; ECL → F1.15, Movimientos/Conciliación → F1.16 — tabs declarados "spec en bead Fx.x", nunca "próximamente" de producto).
- **Molde dashboard §4 íntegro, sin selector VaR·ES·Std** (la provisión ECL no es una medida del selector; es cifra contable única — patrón §12/§13: medida etiquetada en KPI y encabezados: "ECL — NIIF 9").
- **Badge de supuesto EXTENDIDO** (mandato del bead): en las pantallas de Deterioro el badge agrega el segmento NIIF 9 a los supuestos base: "S&P · ρ=25% · TC 61.50 · **NIIF 9: SICR ≥3 notches ó PD×2 · backstop 30d · 3 escenarios (60/25/15)**" — un solo badge, nunca dos componentes (auditable §2); reglas de estado del shell §4 intactas (N/D nunca oculto).
- **Tab Staging — KPIs 4+1**: (1) VM en alcance ECL (AC+FVOCI, DOP consolidado; subtítulo "FVTPL excluido: $X MM — riesgo ya en fair value" + declaración de consolidación) · (2) Provisión ECL total (DOP; anterior, Δ — continuidad con tab ECL F1.15) · (3) VM en Stage 2 (% del alcance — SICR sin default) · (4) VM en Stage 3 + N posiciones deterioradas · (5) Uso Límite (fija; límite de cobertura de provisión si configurado, si no N/D).
- **2×2**: TL **barras apiladas por rating × stage** (rating eje primario §2; toggle métrica VM · N posiciones · Provisión) · TR **Panel de criterios SICR activos** (componente nuevo `PanelCriteriosSICR`, auditable: cuantitativo = deterioro ≥N notches desde el origen [enfoque operable para cartera de inversión, 06 §3] con alternativa PD relativa declarada; backstop 30 días mora — presunción refutable, nota "en bonos bullet rara vez se activa antes del default"; cualitativos = watchlist · outlook · covenants · deterioro soberano/sectorial; **low credit risk expedient con flag de juicio RD**: "Soberano RD ≈ BB− sub-investment-grade — expedient NO automático (5.5.10); juicio documentado: [referencia a política]"; nota fija de **simetría**: "Staging simétrico — mejora del riesgo devuelve Stage 2 → 1") · BL **clasificación contable AC · FVOCI · FVTPL** (dona/barras VM por clasificación; FVTPL en gris terciario con rótulo fijo "Excluido de ECL — riesgo de crédito capturado en fair value"; FVOCI con nota "provisión contra ORI — no reduce el valor en balance") · BR **tabla por posición** exportable, jerárquica rating→emisor→instrumento: rating actual · rating en origen · Δ notches (el driver SICR) · clasificación (chip AC/FVOCI/FVTPL) · stage (1/2/3; FVTPL → "—") · criterio gatillado (categórico) · días mora · VM (grupos DOP·USD·Total v2 — montos) · Provisión ECL (solo DOP consolidado — es medida, jamás partida por moneda, F1.10).
- **Clasificación contable — decisión abierta resuelta**: NO es tab propio ni pantalla de Portafolio; vive como **panel BL de Staging** (donde la exclusión FVTPL es accionable) + **la dona de Portafolio §7.1 TR gana la opción "Vista por: Clasificación NIIF 9"** (3 categorías; misma mecánica que la opción Moneda F1.10 — la clasificación es atributo de composición observable, no riesgo modelado). Razón: el alcance del ECL se juzga en Deterioro; la composición se explora en Portafolio.
- **Color de stages**: categórico ordinal **neutro** (paleta secuencial tipo rating), **jamás semáforo** — Stage 3 no se pinta rojo; el semáforo queda reservado al estado de límite (inviolable shell §4). Documentado como regla de la sección.
- **Granularidad §2 intacta**: el staging es **regla por instrumento sobre datos observables** (rating actual vs origen, mora, clasificación contractual) — no es la distribución de riesgo del modelo; no aplica leyenda de prorrateo. El rating en origen es dato de registro del instrumento (reto "EIR original/legacy" del 06 §6 se anota para F1.15).
- **Coexistencia con Credit VaR declarada** (06 preámbulo): nota fija de sección "El Credit VaR responde el riesgo económico; esta sección responde la provisión contable ECL" — evita lectura de doble conteo.

### Correcciones X ronda 1 (bead librisk-k9s) — 2 FAIL + 8 WARN integrados

1. **SICR cuantitativo fijado (FAIL)**: criterio activo del mock = **deterioro ≥3 notches desde el origen** (enfoque operable para cartera de inversión con pocos emisores, 06 §3); la **PD lifetime relativa (×2)** queda como alternativa metodológica **declarada NO activa** en el panel TR (la metodología oficial del tenant elige una — paridad con "metodología oficial única" de RI). Badge muestra solo el activo. Dominio de la columna "criterio gatillado" del BR: `≥3 notches · backstop 30d · cualitativo (watchlist/outlook/covenants/soberano-sectorial) · —`.
2. **TR no-gráfico = desviación declarada del molde §4 (FAIL)**: precedente directo §14 Backtesting (TR = panel de pruebas Kupiec/Christoffersen, no gráfico). La auditabilidad §2 gobierna; desviación registrada en el artefacto y feedback-log para el PM.
3. **Badge sin ponderaciones de escenarios (WARN 3)**: "3 escenarios (60/25/15)" pertenece a la mecánica ECL (06 §5) → se difiere a F1.15. Badge de Deterioro: "… · NIIF 9: SICR ≥3 notches · backstop 30d (refutable)" — valores del mock marcados; los reales vienen del contrato de datos.
4. **Refutabilidad en el badge (WARN 4)**: "backstop 30d (refutable)".
5. **Expedient con rastro por posición (WARN 5)**: BR gana columna **"Expedient"** (chip "Sí — juicio doc." / "—") para Stage 1 bajo low-credit-risk; placeholder resuelto: "Política de Deterioro Crediticio v1" (valor del mock, documento del tenant).
6. **Base de interés visible (WARN 6)**: el panel TR incluye la mini-tabla de consecuencias por stage (ECL 12m/lifetime · interés sobre bruto/**neto**); tooltip del chip de stage en BR la repite.
7. **KPIs re-plantillados (WARN 7)**: KPI 4 = "VM en Stage 3" (valor grande, anterior/Δ) con subtítulo "N posiciones deterioradas"; KPI 1 subtítulo único "AC + FVOCI · Consolidado en DOP · TC del corte", exclusión FVTPL vive en tooltip del KPI 1 + rótulo fijo del BL.
8. **Sidebar 9 ítems (WARN 8)**: ítem 9 tras Backtesting (narrativa: medición → validación → traducción contable); se actualizan specs línea 6, §2 (conteo y tabla) y §3.
9. **Filtros extendidos (WARN 9)**: bloque 3 de `CreditoFiltersSidebar` gana **Clasificación NIIF 9 (AC·FVOCI·FVTPL)** y **Stage (1·2·3)** tras seniority, antes de moneda; "Vista por" no cambia (rating eje primario).
10. **Δ de provisión (WARN 10)**: tendencia del KPI 2 = impacto en deterioro (provisión ↑ = flecha ↑ deterioro), color neutro, tooltip explícito — regla "deltas comunican impacto, no signo".

Re-ataque (ronda 2) diferido al revisor R sobre el artefacto final (los 2 FAIL son de contrato interno, resueltos arriba; máx 3 rondas respetado).

### T — Checklist bead librisk-k9s (verificado sobre el artefacto final)

- [x] Aceptación: KPIs 4+1 (§15.1) · rejilla 2×2 · tabs Staging·ECL·Movimientos·Conciliación REA pinneados
- [x] Aceptación: distribución Stage 1/2/3 con VM · N posiciones · provisión (TL, toggle de métrica)
- [x] Aceptación: criterios SICR auditables en UI (PanelCriteriosSICR: cuantitativo activo ≥3 notches + alternativa PD×2 NO activa, backstop 30d refutable, cualitativos, mini-tabla de consecuencias, simetría 2→1)
- [x] Aceptación: expedient RD con juicio documentado visible (bloque 4 del TR + columna "Expedient" en BR + soberano BB− NO automático)
- [x] Aceptación: clasificación AC/FVOCI/FVTPL como dimensión visible; FVTPL excluido con motivo visible (BL + tooltip KPI 1); decisión tab-propio-vs-Portafolio resuelta y razonada (§15.2)
- [x] Handoff 00 §2: rating eje primario (TL por rating; BR rating→emisor→instrumento) · badge de supuesto extendido, nunca oculto · sin campana de Gauss (sin histogramas en el tab) · DOP consolidado; provisión jamás partida por moneda (F1.10)
- [x] Handoff 00 §6/§10: molde 4+1 + 2×2 + BR exportable; desviación TR-panel declarada con precedente §14; DD/MM/AAAA, N/D nunca cero, "—" no-aplica, M/MM, máx 8 categorías, stages neutros (jamás semáforo), deltas = impacto
- [x] Handoff 06 §1–§3 fieles: alcance AC/FVOCI/FVTPL con tratamiento ORI, 3 stages con horizonte ECL y base de interés bruto/neto, SICR relativo (no PD absoluta), backstop refutable, expedient 5.5.10 con juicio RD, simetría
- [x] Propagación: specs línea 6 (9 secciones) · §2 sidebar (ítem 9 + orden razonado) · §3 tabs · §4 badge + filtros (clasificación/stage) · §7.1 TR (Vista por: Clasificación NIIF 9) · tabla screens (fila 9) · mermaid (DT/DTS/DTE/DTM)
- [x] Correcciones X 1–10 integradas en el artefacto

## A-phase — Bead librisk-1ob (F1.15 — Deterioro NIIF 9: tab ECL — cálculo, curvas y escenarios macro)

**Brain re-verificado 2026-09-02** (retrieval hybrid "NIIF 9 IFRS 9 ECL escenarios macro PD lifetime EIR"): sigue **sin cobertura NIIF 9/ECL** — top hit `Capa2_RI_MetodologiaCredito.md` [guia] es Credit VaR (aporta: matriz de transición y paridad de módulo). Gap ya registrado (feedback-log 2026-08-21, pendiente aprobación PM). **Fuente vinculante: `06-handoff-ifrs9-ecl.md` §4–§5** (+§6 retos, §7 módulos); shell/molde por wireframe aprobado §1–§6 y F1.14 §15.

### Spec del artefacto (nuevo §15.3 tab ECL + propagaciones)

- **Tab ECL** (`/deterioro/ecl`), molde §4, sin selector (cifra contable "ECL — NIIF 9"). Badge extendido **gana el segmento de escenarios** (resuelve deferral WARN 3 F1.14): "… · NIIF 9: SICR ≥3 notches · backstop 30d (refutable) · **3 escenarios (60/25/15)**" (valores del mock).
- **KPIs 4+1**: (1) Provisión ECL total — NIIF 9 (misma cifra que Staging KPI 2, pinneada no recalculada; subtítulo "Ponderada por escenarios · Consolidado en DOP · TC del corte"; Δ = impacto, neutro) · (2) **Efecto no-linealidad**: ECL ponderado − ECL del escenario promedio (DOP y %; mandato del bead — ambos números visibles) · (3) ECL lifetime (Stage 2+3) $ + % del total (12m vs lifetime a nivel KPI) · (4) Cobertura: Provisión/VM en alcance (%; anterior, Δ) · (5) Uso Límite (fija).
- **2×2**: TL **Panel de escenarios macro ponderados** (elemento central del bead): 3 columnas base/adverso/favorable con chips de probabilidad, barras de ECL por escenario (neutro), mini-tabla de variables macro RD (PIB · DOP/USD · tasa BCRD) por escenario; líneas de referencia **ECL ponderado (oficial)** y **ECL del escenario promedio (rotulada "no usada — muestra la no-linealidad")** + Δ anotado; nota de calibración RD ("proxies regionales — escasez de defaults locales", 06 §5) · TR **barras apiladas rating × horizonte ECL (12m · lifetime)** — lente distinta del TL de Staging (stage) para no duplicar; toggle "Vista por: Rating · Clasificación (AC·FVOCI)"; cross-ref a Staging para la vista por stage · BL **Mecánica del cálculo** con selector local (KPIs jamás mutan — precedente §14 BL): **Curvas PD** (survival S(t) + marginal por rating, selector 7 letras D excluido, nota "derivadas de la matriz de transición del modelo — la misma de Factores §12, elevada a potencia t con absorción del default") · **Perfil EAD** (saldo esperado + devengados; bullet ≈ estable, amortizable proyectado) · **LGD PIT** (barras por seniority senior·subordinada, "point-in-time y forward-looking — no through-the-cycle"); **subtítulo fijo auditable: "Descuento a la EIR ORIGINAL del reconocimiento inicial — jamás a tasa de mercado actual"** + fórmula ECL = Σ PD_m(t)·EAD(t)·LGD(t)·DF(t) · BR **tabla ECL por posición** exportable rating→emisor→instrumento: Stage · Horizonte · Clasificación · PD (del horizonte) · LGD · EAD (DOP consolidado) · **EIR original (%)** — "N/D — no almacenada en origen (legacy)" posible (06 §6) · Provisión ECL (DOP, jamás partida) · Δ vs anterior. FVTPL fuera de la tabla (alcance).
- **Frontera declarada** (mandato): tabla ECL-escenarios vs Escenarios §9 (estrés efímero, run puntual del usuario) vs Sensibilidades §13 (barridos OAT del VaR): los escenarios macro del ECL son **parte del número contable oficial** (recurrentes, ponderados, gobernados por la metodología del tenant), no estrés ni sensibilidad del VaR.
- **NavCard 9** (deferral R#1 de F1.14 resuelto): §11.3 gana NavCard "Deterioro (NIIF 9)" con ancla Provisión ECL total; mermaid OV pasa a 9 NavCards + nodo DTE expandido.
- Granularidad §2: ECL calculado **por instrumento** (PD/EAD/LGD del instrumento) — prorrateo no aplica (misma exención que Staging). Provisión y ECLs por escenario **jamás partidos por moneda** (F1.10); stages/escenarios en paleta neutra (jamás semáforo).

### Correcciones X ronda 1 (bead librisk-1ob) — 6 FAIL + 6 WARN integrados (detalle en feedback-log 2026-09-02)

### T — Checklist bead librisk-1ob (verificado sobre el artefacto final)
- [x] Aceptación: ECL total y por stage con 12m vs lifetime visible (KPI 1/3; TR apilado 2 segmentos + nota S2+S3→Staging)
- [x] Aceptación: descomposición rating/emisor/clasificación (TR toggle; BR rating→emisor→instrumento)
- [x] Aceptación: curvas PD survival/marginal por rating desde la matriz de transición (§12), potencia t, absorción del default — render escalonado + guardarraíl anti-Gauss
- [x] Aceptación: perfil EAD · LGD PIT por seniority · EIR ORIGINAL como elemento auditable (fórmula BL + columna BR con ⚑/proxy)
- [x] Aceptación: ≥3 escenarios con probabilidades; ECL ponderado vs ECL del promedio AMBOS visibles con Δ (TL central + KPI 2); macro RD (PIB·DOP/USD·BCRD); ponderación central de UI, no nota
- [x] Aceptación: frontera declarada con Escenarios §9 y Sensibilidades §13 (tabla + nota fija TL)
- [x] Handoff 00 §2: rating eje primario · badge único seccional nunca oculto · sin campana de Gauss · DOP consolidado, provisión/ECLs jamás partidos por moneda
- [x] Handoff 00 §6/§10: molde 4+1 + 2×2 + BR exportable (desviaciones TL/BL declaradas con precedente) · N/D nunca cero · "—" no aplica · deltas neutros de impacto · semáforo solo límite · ≤8 categorías · comparabilidad (extendida a ponderaciones)
- [x] Propagación: specs línea 6 (Parte 11) · §11.3 (NavCard 9, 9 NavCards) · §15 badge seccional · deferral F1.14 marcado resuelto · mermaid (DTE expandido, edge NavCard, 9 NavCards)
- [x] R: PASS; observación menor #1 corregida

## A-phase — Bead librisk-arr (F1.16 — Deterioro NIIF 9: tabs Movimientos + Conciliación REA + FVOCI/ORI)

**Brain re-verificado 2026-09-02** (retrieval hybrid "provisiones REA SB categorías A-E conciliación NIIF 9", telemetría q_f5f82ad416): **sin cobertura** — Capa 4 regulatorio cubre reportería SB/SIMV (RTC1, RI01…) y liquidez-solvencia SIMV, no el REA de provisiones por categorías A-E ni la conciliación REA↔ECL. Gap ya registrado (feedback-log 2026-08-21, pendiente aprobación PM). **Fuente vinculante: `06-handoff-ifrs9-ecl.md` §6 ("Consistencia con normativa SB (REA)": ambos cálculos, NIIF prevalece para reporte financiero, regulatorio exige el mínimo REA, gestionar el "mayor de los dos"; FVOCI doble registro) + §7 (módulo 7 Reporte: roll-forward de stages, conciliación REA) + §1 (FVOCI: provisión contra ORI, no reduce balance, deterioro en resultados compensado en ORI)**. Shell/molde: wireframe aprobado §1–§6 + §15/§15.3.

### Spec del artefacto (nuevos §15.4 Movimientos y §15.5 Conciliación REA + mermaid)

**Tab Movimientos** (`/deterioro/movimientos`) — pregunta: *¿por qué cambió la provisión y el staging entre cortes?*
- Molde §4, badge seccional idéntico (regla F1.15: un badge por sección, idéntico entre tabs hermanos). Sin selector de medida.
- **Comparación de cortes es la naturaleza del tab** → regla propia: selector local "vs corte anterior (default) · vs corte a elegir"; si CUALQUIER componente del badge difiere entre los dos cortes, banner de no-comparabilidad y el bucket **"Cambio de medición"** del waterfall se rotula "incluye efecto metodológico — cortes no comparables" (no se blanquea el tab: el roll-forward sigue siendo contablemente válido; los Δ de cartera se marcan).
- KPIs 4+1: (1) Provisión ECL al corte (pinneada = Staging KPI 2/ECL KPI 1) · (2) Δ Provisión del período (DOP y %; neutro, impacto) · (3) VM deteriorado (migró a S2/S3) · (4) VM mejorado (S2→1, S3→2 — simetría 06 §2 visible a nivel KPI) · (5) Uso Límite.
- 2×2: TL **waterfall de roll-forward de provisión** (inicial → altas → bajas → migraciones netas por stage → cambio de medición → final; nota FVOCI/ORI) · TR **sankey de migraciones de stages** 1↔2↔3 + Altas/Bajas (VM; paleta neutra) · BL **Δ provisión por rating** (barras, rating eje primario §2, signo visible neutro) · BR **tabla de movimientos por posición** exportable (stage anterior→actual, provisión anterior/actual/Δ, motivo categórico, registro P&L/ORI).

**Tab Conciliación REA** (`/deterioro/conciliacion-rea`) — pregunta: *¿qué exige el regulador vs qué dice NIIF 9, cuál gobierna y por qué difieren?*
- KPIs 4+1: (1) Provisión ECL NIIF 9 (pinneada) · (2) Provisión REA SB (categorías A-E) · (3) **Provisión exigible = mayor de los dos** con chip de cuál gobierna (06 §6) · (4) Diferencia ECL − REA (DOP y %, signo visible, neutro) · (5) Uso Límite.
- 2×2: TL **barras pareadas ECL vs REA por categoría REA A-E** (≤5 categorías, ordinal neutro — jamás semáforo, misma regla que stages) · TR **panel de mapeo y reglas REA** (auditable, no gráfico — precedente §14/§15 TR): mapeo rating→categoría A-E declarado, % de provisión REA por categoría (valores del mock), y la regla "mayor de los dos" con ámbito declarado **a nivel cartera** (decisión del mock; el nivel real lo fija la política del tenant) · BL **bridge de la diferencia explicada** (waterfall REA→ECL por drivers: forward-looking/escenarios · lifetime vs 12m · LGD PIT vs % fijo REA · descuento a EIR) · BR **tabla de conciliación por instrumento** exportable (la aceptación exige tabla exportable): categoría REA · % REA · provisión REA · Stage NIIF · horizonte · ECL · diferencia · **Registro contable (chip P&L / ORI)**.
- **FVOCI/ORI sin ambigüedad (mandato c)**: columna "Registro contable" en BR de ambos tabs (AC → "provisión reduce valor en libros — P&L"; FVOCI → "ECL en ORI — balance permanece a fair value") + nota fija en el waterfall TL de Movimientos + fila informativa de doble registro en la tabla de conciliación (fair value en balance / ECL en ORI, 06 §1/§6).
- Granularidad §2: staging/ECL/REA son reglas por instrumento sobre datos observables — exención de prorrateo intacta. Moneda: provisiones ECL y REA **siempre DOP consolidado, jamás partidas por moneda** (F1.10).

### Correcciones X ronda 1 (bead librisk-arr) — 7 FAIL + 5 WARN integrados (detalle en feedback-log 2026-09-02)

### T — Checklist bead librisk-arr (verificado sobre el artefacto final)
- [x] Aceptación (a): roll-forward de stages y provisión entre cortes — waterfall TL (altas/bajas/migraciones/cambio de medición) + sankey TR 1↔2↔3 + altas/bajas + tabla BR con stage ant→act y motivo
- [x] Aceptación (b): conciliación REA como tabla exportable (BR §15.5), regla "mayor de los dos" visible (KPI 3 + chip gobierna + bloque TR + nota anti-suma-de-máximos), diferencia explicada (KPI 4 + bridge BL con cuadre)
- [x] Aceptación (c): FVOCI sin ambigüedad — chip P&L/ORI en ambos BR, nota fija waterfall, fila fija de doble registro en subtotal FVOCI (fair value en balance / ECL en ORI)
- [x] Handoff 00 §2: rating eje primario (BL Movimientos, jerarquía BR ambos tabs) · badge seccional único idéntico, jamás oculto · sin campana de Gauss · DOP consolidado, provisiones jamás partidas
- [x] Handoff 00 §6/§10: molde 4+1 + 2×2 + BR exportable jerárquica · desviaciones declaradas con precedente (§14/§15.1 TR; waterfall bajo divergencia con ancla 06 §7) · N/D nunca cero · "—" no aplica · deltas neutros · semáforo solo límite · ≤8 categorías · comparabilidad alineada con §15.3
- [x] Handoff 06 §1/§2/§6/§7 fieles: doble registro FVOCI/ORI, simetría de stages a 3 niveles, ambos cálculos + prevalencia NIIF + piso REA + mayor de los dos, roll-forward y conciliación como reportes
- [x] Cuadres declarados e incluidos en export: waterfall = KPI 2 = Σ BL = Σ Δ BR; bridge = KPI 4; Σ ECL/REA BR = KPIs 1/2; selector de corte jamás muta el KPI 1 pinneado
- [x] Propagación: specs línea 6 (Parte 12) · mermaid (DTM expandido + DTR nuevo)
- [x] R: PASS; hallazgos menores 1–3 corregidos

## Bead librisk-nqj — F2.11 Prototipo Deterioro (NIIF 9) — Fase A: spec de implementación (2026-09-02)

Contratos: 06-handoff-ifrs9-ecl.md (vinculante) + 03-wireframe-specs §15.1–§15.5 (aprobados AX-DTR-D en F1.14–F1.16). Canon Brain: reutiliza el snapshot vigente (tokens DS, molde 4+1/2×2, reglas §2/§4 del shell) — sin cambio de corpus declarado. Evidencia de patrón: app.js del val (secciones §12–§14 como precedente de panel-no-gráfico, tablas jerárquicas rating→emisor→instrumento, exportCSV, switcher 5 estados).

**Decisiones de implementación (A)**
1. `SECTIONS` gana `deterioro` (9º ítem sidebar, tras Backtesting — orden de la tabla de screens §15): tabs `staging (default) · ecl · movimientos · conciliacion-rea`. Rutas hash `#/deterioro/<tab>`.
2. **Badge seccional único**: headHtml agrega a `sup`, solo en deterioro, el segmento fijo " · NIIF 9: SICR ≥3 notches · backstop 30d (refutable) · 3 escenarios (60/25/15)" — idéntico en los 4 tabs; reglas de estado intactas (N/D degradado, jamás oculto).
3. **Nota fija de sección** bajo el breadcrumb en los 4 tabs e incluida en los 4 CSV: "El Credit VaR responde el riesgo económico; esta sección responde la provisión contable ECL (NIIF 9)".
4. **Filtros**: en deterioro el panel gana los grupos interactivos **Clasificación NIIF 9** (Todas·AC·FVOCI·FVTPL) y **Stage** (Todos·1·2·3); Stage activo excluye implícitamente FVTPL (regla §15.1, nota en el panel). Moneda solo afecta los grupos de VM; ECL/REA jamás se parten (F1.10).
5. **Datos (data.js → bloque `IFRS`)**: atributos por instrumento (clasif, rating en origen, seniority, plazo, mora, prevStage, cualitativo). Staging derivado por regla: impaired→3; Δ≥3 notches ∨ mora≥30d ∨ cualitativo→2; resto→1; expedient chip en Stage 1 IG con juicio doc. Mock: 2 FVTPL (SBB Popular 2026, CD BHD 90d), Stage 3 = SBB Caribe 2026 (impago de cupón, mora 95d, origen A), Stage 2 = EGE Haina 2028/2031 (≥3 notches, origen A), AES Andrés 2029 (cualitativo — deterioro sectorial), mejora CD Promerica S2→1, alta/baja sintéticas (CD BHD 60d nueva · Letra Hacienda 2025 vencida). PD desde `FR.TRANS` (fuente única de la matriz — coherencia VaR↔ECL por construcción); PD lifetime = 1−(1−PD12)^T (convención declarada del mock, ancla 06 §6 "elevar la matriz"); LGD por seniority desde `ESC.REC` (Senior 55% · Subordinada 70%), PIT con shift por escenario; EAD = VM DOP (mock declara "costo amortizado ≈ VM", ⚑); DF a EIR original omitido en cifras (EIR columna con N/D+proxy ⚑ según §15.3). Escenarios 60/25/15 con fPD 1.0/1.45/0.75 y dLGD 0/+6/−3 — la correlación positiva PD·LGD produce convexidad ≥0 por construcción (KPI 2 ECL).
6. **Movimientos — descomposición auditable por posición**: Δ_migración = ECL_hoy(stage hoy) − ECL_hoy(stage anterior); Δ_remedición = ECL_hoy(stage anterior) − ECL_ant(stage anterior); alta = +ECL; baja = −ECL_ant. Σ buckets = Δ total exacto (cuadre waterfall = KPI 2 = Σ BL = Σ Δ BR por construcción).
7. **REA (mock ⚑, norma SB fuera del Brain — gap ya registrado)**: mapeo rating→categoría A/A/A/B/C/D + override Stage 3→E; % por categoría {A .5, B 1.5, C 4, D 15, E 60}; exigible = max a nivel cartera, chip gobierna computado del dato. Bridge REA→ECL: buckets mock (forward-looking, lifetime, LGD PIT, % fijo REA vs modelo, EIR) con plug que cierra exacto con KPI 4 (⚑ descomposición del mock).
8. **Charts**: TL Staging barras apiladas rating×stage (toggle VM·N·ECL); BL dona clasif; TL ECL panel compuesto HTML/CSS (3 columnas escenario + 2 líneas de referencia — desviación declarada §15.3); TR ECL apiladas 12m/lifetime (toggle Horizonte/Clasificación, 2 segmentos siempre); BL ECL selector 3 vistas (curvas PD escalonadas + guardarraíl anti-Gauss, EAD escalonado, LGD barras); TL Mov waterfall ECharts (serie fantasma); TR Mov sankey ECharts (bundle completo del CDN la incluye); BL Mov barras con signo; TL Conc barras pareadas A–E; BL Conc bridge waterfall. Paleta stages = secuencial neutra ORDINAL existente; Stage 3/E/Bajas jamás rojo.
9. **Estados**: loading/empty/error patrón existente (kpisND + statePanels); **partial = corte anterior publicado bajo badge distinto** (precedente SENS X-7): Δ→N/D en los 4 tabs; en Movimientos KPIs 2–4 N/D, BL vacío con motivo, waterfall TL renderizado con bucket "Cambio de medición — incluye efecto metodológico ⚑" (regla §15.4).
10. **Overview**: NavCard 9 → Deterioro (ancla Provisión ECL total, aterriza `/deterioro/staging`); skeleton de 9 nav-cards.
11. **Export**: 4 casos CSV con footers de cuadre mandados (§15.3/§15.4/§15.5) + nota fija de sección.

## A-phase — Bead librisk-3vd (F2.12 Re-validación final incluye NIIF 9)

**Brain (2026-09-02, corpus `8b3bd636c070fe38`)**: catálogo RI re-consultado (7 entries, mismas coordenadas que F2.6/F2.11: `Capa2_RI_PlataformaUX.md` guía UX/baseline, `Capa2_RI_Producto.md` roles, `Capa2_RI_MetodologiaCredito.md` metodología). Sin cambios de estado que alteren los oráculos. Confirmado: NIIF 9/ECL sigue sin cobertura en el catálogo (gap 2026-08-21 vigente, sin declarar — pendiente PM).

**Spec de la re-validación F2.12** (artefacto = script `f212-validate.mjs` + resultados + capturas + metadata actualizada):

1. **Matriz completa 14 pantallas × 5 estados** (10 heredadas + 4 tabs Deterioro), oráculos F2.6 heredados sin cambio: badge presente/N-D-solo-degradado, `$X,XXX.XXMM`, `DD/MM/AAAA` sin ISO, sin K, CTA Reintentar, instrucción en vacío, N/D-nunca-cero, 0 hex inline fuera de `:root` (excl. `mock-only`).
2. **Oráculos NIIF 9 nuevos** (fuente: 03 §15, 06 §2–§7, feedback F2.11):
   - Badge seccional **idéntico** entre los 4 tabs y con segmento `NIIF 9: SICR ≥3 notches · backstop 30d (refutable) · 3 escenarios (60/25/15)` (sondeado en DOM vivo).
   - Provisión ECL **pinneada** `$78.53MM` en los 4 tabs (§15 mandato de cifra ancla).
   - Cuadres con dato vivo: `66.83` (waterfall = Δ provisión) en Movimientos; `51.50` (bridge REA→ECL = KPI 4) en Conciliación.
   - Anti-rojo Stage 3: color computado de los elementos con texto "Stage 3" no rojo-dominante (paleta secuencial neutra — 00 §2 semáforo solo límite).
   - Filtro activo ⇒ KPI 1 inmutable + nota "Filtro activo" visible (invariante F2.11 FAIL-2).
   - Convexidad: texto "onvexidad" + Δ anotado presentes en tab ECL.
3. **Coherencia transversal (regresión)**: `122.79` en las 5 secciones con medida (sin contaminación por la ampliación); `78.53` ausente de las secciones VaR (la provisión no invade el molde de riesgo económico).
4. **B1 re-trazado** (JTBD ≤3 clics VaR→Marginal) + captura.
5. **Consola 0 errores** en toda la sesión.
6. **Capturas** `f212-*`: los 4 tabs en éxito + estados en 1 tab de muestreo (Staging) + partial de Movimientos (cuadre suspendido).
7. **Metadata**: 05 reescrito a matriz consolidada de 9 secciones/14 pantallas con Auto-Validation Results F2.12 (A1–A6, B1–B4) por criterio PASS o desviación documentada.

**Decisión de alcance**: los oráculos NO re-asertan las fases del ciclo §9.6 de Escenarios ni los sets por-bead de estados (ya verificados F2.5/F2.6/F2.11) — desviación declarada, misma regla que F2.6.

**X-phase F2.12 (1 ronda, 12 FAIL + 8 WARN — todos integrados al spec):**
- Badge: se aserta el string COMPLETO (base `S&P · ρ=25% axiomático · TC 61.50` + segmento NIIF 9), idéntico entre los 4 tabs (X#1).
- Anti-Gauss en ECL: subtítulo-guardarraíl visible + serie escalonada (`step`) leída de la opción ECharts viva + guardarraíl en el CSV (X#2).
- Provisión jamás partida por moneda: aserción negativa sobre headers de los 4 BR (X#3).
- PD por rating uniforme: leaf rows del BR de ECL — mismo rating+horizonte ⇒ misma PD (X#4); coherencia dato: `FR.TRANS` única fuente, spot-check vía `window.RI_DATA` (X#5).
- Pinneo `$78.53MM` por SELECTOR del KPI correcto por tab (Staging KPI2 · ECL KPI1 · Mov KPI1 · Conc KPI1), no por substring del body (X#6).
- Cuadres aritméticos con signo: KPI2 Mov parseado = +66.83 = Σ buckets del waterfall (opción ECharts); KPI4 Conc = −51.50 = total del bridge (X#7).
- Negativos con rutas enumeradas: `78.53` ausente de métricas×2/marginal/factores/sensibilidades (permitido en OV NavCard 9 y Deterioro); `122.79` con tabla ruta→expectativa (BT y Escenarios pre-run excluidos, herencia F2.6) (X#8/#9).
- Paleta vía opciones ECharts: ninguna serie/color de Staging TL, sankey, waterfall y Conc TL es rojo-dominante; Stage 3/E/Bajas jamás rojo (X#10); limitación del hex-scan DOM a canvas declarada y cubierta por esta vía (X#14).
- Filtro que filtra: Stage=3 ⇒ BR se reduce y FVTPL desaparece, KPI1 inmutable + nota visible; Clasificación=FVTPL ⇒ Stage "—" (X#11).
- Convexidad: KPI2 numérico ≥0 + referencia "no usada"/Δ presente en la opción del chart, no substring del body (X#12).
- Partial de Movimientos con aserciones de régimen: KPIs 2–4 N/D, waterfall RENDERIZADO con bucket ⚑, cuadre "suspendido" (X#13).
- Deep-link frío: `page.goto` directo a las 4 rutas nuevas, consola limpia (X#15).
- Controles nuevos F2.11: toggle TL Staging, vistas BL de ECL, selector de período de Movimientos — KPI1 inmutable ante cada uno (X#16).
- CSV de los 4 tabs descargado y asertado: nota de sección, footers de cuadre, guardarraíl anti-Gauss (X#17).
- Metadata: desviaciones NIIF 9 fusionadas a la lista numerada del gate (12+ incl. gap Brain), B4 re-mapeado sobre Deterioro, tabla de evidencia extendida con filas 11–14 declarando re-verificado vs heredado (X#18/#19/#20).

## Bead librisk-8yh — F2.13 Corrección PM: densidad de texto (patrón ⓘ) — Fase A spec (2026-09-02)
- Inventario de texto explicativo en el val: 55 `.panel-foot`, 6 `.fr-sub`, 2 `.bt-sub2`, 5 `.f-note` (drawer), 2 `.esc-foot-note`, 1 `.mr-nota` (hallazgo R), 1 leyenda de prorrateo embebida en KPI Top Driver.
- Solución: pass post-render idempotente `applyInfoPattern()` (marca `data-info-applied`, `display:none` sobre la nota original — el HTML fuente no se toca) invocado al final de `render()` y `renderFilters()`. UN ⓘ por panel en `.panel-head` tras el `<h2>`; popover portal a `document.body` (fixed, z-60), segmentos con inviolables §2 primero (regex prorrate|granularidad|nivel rating).
- Exclusiones (visibles): `.info-keep` (nota empty-state simulador — B3), `.placeholder-note` (banners de estado), badges/pills, `.sub`/`.esc-sub`/`.bt-arch-sub`/`.nv-sub` (dato/controles cortos).
- CTA `a[data-goesc]` (Sensibilidades): nodo MOVIDO (listener preservado) a línea visible `.panel-foot-cta`.
- KPI Top Driver: leyenda larga → chip `prorr.` con title (patrón ya existente en celdas de tabla).
- Exports CSV: verificado que TODOS los exports ya llevan líneas "Nota" con los inviolables (§2, granularidad, FX, N/D≠0) — requisito (3) del bead satisfecho sin cambios.
- X adversarial: 5 BLOCKER + 9 MAJOR + 4 MINOR. Integrados: idempotencia+marca, portal al body, exclusión/extracción de CTAs, orden §2-primero, ARIA disclosure (aria-expanded/controls/haspopup, Esc devuelve foco), cambio atómico entre ⓘ, ⓘ individual en drawer, taxonomía escrita en specs §4, chip visible en KPI. Overruled por decisión PM explícita del bead: BLOCKERs #1/#2 (micro-copy visible obligatorio) — el PM sancionó "1 clic" para prorrateo/granularidad; se conserva chip corto donde ya existía. Deferral: paridad del patrón hacia Mercado (producción) — fuera de alcance del mock, anotado para PM.
- T (Playwright chromium local — MCP sin canal chrome): 14/14 rutas con 0 notas explicativas visibles; popover 1-clic con prorrateo; toggle/Esc/atómico/clic-fuera/scroll OK; CTA navega a Escenarios; drawer ⓘ z=60 sobre panel z=41; empty-state visible; chip prorr.; 0 errores consola. Capturas before/after ×4 + popover en prototype-captures/f2.13/.
- R: PASS. Hallazgo 1 (`.mr-nota` visible en Métricas) corregido añadiéndola a INFO_SEL y re-verificado (0 visibles, 5 ⓘ, 0 errores). Hallazgo 2 (banner de alcance de Deterioro "Credit VaR vs ECL", 1 línea con ⓘ inline) — se mantiene visible como banner de alcance (excepción declarada, taxonomía (a)). Hallazgo 3 (micro-texto en KPIs de Sensibilidades) — fuera de alcance, anotado.
