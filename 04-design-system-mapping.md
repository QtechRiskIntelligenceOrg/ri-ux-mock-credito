# Design System Mapping — Sección Crédito (Mock UX/UI)

**App**: Risk Intelligence (RI)
**Date**: 2026-08-21
**Bead**: librisk-bql (F2.1)
**Fuentes**: Brain corpus `00dfc7c8353bacaf` — `Capa2_RI_PlataformaUX.md` [guia, con inviolables], `Capa1_Diseno_Tokens.md` [inviolable], `Capa2_RI_MetodologiaCredito.md`, `Capa1_Diseno_Principios.md`; evidencia empírica `context-mercado/01-front-structure.md` (`globals.css`, `colors-reports.tsx`, componentes reales de Mercado); wireframe spec aprobado `03-wireframe-specs.md` (gate librisk-tv6 cerrado por PM).

> **Régimen de tokens — excepción RI (decisión de jerarquía).** RI es el único producto en excepción de rebranding: quien construye sobre RI sigue el **baseline visual vigente** (coherencia local obligatoria), no los tokens corporativos de Capa 1 (`#0A1628`/`#00C2FF`/IBM Plex Mono son el *destino*, no el vigente). Las convenciones de **contenido** de Capa 1 sí aplican transversalmente (MM/M, DD/MM/AAAA, N/D, 8+"Otros", riesgo en neutro, semáforo solo límite, color nunca canal único).

---

## Design Tokens Resolved

Todos los valores provienen del baseline RI vigente (Brain `Capa2_RI_PlataformaUX.md` § baseline) verificados contra `globals.css` del front (evidencia factual). **Prohibido hex fuera de esta tabla** [inviolable] — el prototipo declara estas variables en `:root` y solo las consume por nombre.

| Token | Valor | Fuente |
|---|---|---|
| `--bg-app` (fondo de aplicación) | `#eff3f8` | Brain baseline RI + `globals.css` |
| `--primary` (acción/interacción) | `#0d77bf` | Brain baseline RI |
| `--secondary` (navy institucional) | `#1f2a4e` | Brain baseline RI |
| `--text` / `--text-2` | `#000` / `#434343` | Brain baseline RI |
| `--border` | `#dfdfdf` | Brain baseline RI |
| `--hover` (interacción) | `#d9e2ed` | Brain baseline RI |
| `--skeleton` | **alias de `#d9e2ed`** — alias declarado: un hex, dos semánticas (interacción/carga) hoy en el front; el alias evita la deriva (corrección X-10) | `MercadoSkeletons.tsx` (factual) |
| `--sem-error` / fondo pastilla | `#c10007` / `--fondo-error` | Brain baseline RI (semánticos) |
| `--sem-ok` / fondo pastilla | `#008236` / `--fondo-ok` | Brain baseline RI |
| `--sem-warn` / fondo pastilla | `#de560d` / `--fondo-alerta` — **token único**: el naranja del semáforo Y el de "Advertencia" son el mismo (corrección X-10) | Brain baseline RI |
| `--surface-container` | `#ffffff`, `border-radius: 20px` (contenedor de pantalla) | `globals.css` + `var-global.png` |
| `--surface-card` | `#eff3f8`, `border-radius: 8px` (`rounded-lg`) — tarjetas KPI | `CardMetric.tsx` (factual) |
| Tipografía | **Inter** — H1 35/800 → body 13/400 (escala `.font-h1..h6/.font-body` del front) | Brain baseline RI + `globals.css` |
| Cifras | **Inter + `font-variant-numeric: tabular-nums`**, alineadas a la derecha | resolución de tensión (ver Ledger L-9) |
| Espaciado | base **4px** (`--spacing-01..10`) | Brain baseline RI |
| Radios | 20 (contenedor) / 10 (paneles) / 8 (cards) / 4 (badges rectangulares, p.ej. N-9) / pill (badges de estado) — set del baseline (20/10/4/16 + usos del front) sin sistema formal: deuda RI conocida [libre], se usan tal cual | Brain baseline RI |
| Breakpoints | Tailwind + `xxl` 1400 / `3xl` 1600; **umbral 1280px** para paneles laterales — jerarquía: 1280 gobierna superposición de paneles, 1400/1600 gobiernan densidad de grid; tres quiebres coexistentes del baseline (deuda documentada, no se corrige en el mock — corrección X-13) | Brain baseline RI |
| `--data-neutral` (serie única / barras de riesgo) | azul de marca `#0d77bf` de `colors-reports.tsx` — el riesgo se pinta con azules de marca, jamás con semánticos | `colors-reports.tsx` (factual) + Capa 1 "riesgo en neutro" |
| Paleta rating (ordinal 7: AAA/AA/A/BBB/BB/B/CCC–D) | **escala secuencial azul** de `colors-reports.tsx` usada como ordinal (oscuro=AAA → claro=CCC–D); "Otros" en gris terciario; nunca semáforo | `colors-reports.tsx` + Capa 1 dataviz |
| Paleta categórica (tipo instrumento, moneda, factor) | paleta categórica ECharts de `colors-reports.tsx` (máx 8) | `colors-reports.tsx` (factual) |
| Semántica de signo P&L (solo Escenarios §9) | `--sem-ok` / `--sem-error` sobre G/P — **única superficie donde verde/rojo pinta datos** (juicio económico); frontera del wireframe §9 | Capa 1 "rojo/verde solo juicio económico" |

**Reglas de color no negociables del mapping** (síntesis; detalle en Ledger):
- Métricas de riesgo (VaR/ES/Std, marginal, componental, HHI, Δ de medida): **siempre `--data-neutral` / azules**. El semáforo pinta **solo** estado de límite en pastilla.
- **DeltaBadge en KPIs de riesgo usa la variante neutra** (gris/azul, sin verde/rojo) — el `DeltaBadge` de Mercado colorea por signo; esa conducta queda **excluida** del módulo Crédito para deltas de medida (corrección X-4; wireframe shell §4; deuda #12 del baseline: "pantallas nuevas siguen el canon").
- Color nunca canal único: todo estado/juicio lleva texto o ícono además del color.

---

## Component Mapping

Estatus: ✅ `exists` (componente real del front, uso directo) · 🔄 `adapt` (existe, requiere variante/props) · 🆕 `new` (propuesto — pendiente de adición al DS).
"Screen" referencia §§ del wireframe spec. Todo gráfico se ancla a un `chart_type` del registro `DynamicComponentRenderer` (plausibilidad backend-driven).

### Shell y navegación

| # | Wireframe Component | Screen | DS Component | Variante / adaptación | Tokens clave | Status |
|---|---|---|---|---|---|---|
| 1 | Header global (módulos, tenant, avatar) | todas | header de Mercado | Crédito activo; Liquidez/Operacional en gris ("futuro visible pero inactivo" [inviolable]) | `--secondary`, `--primary` | ✅ |
| 2 | MenuSidebar "Crédito" (8 ítems) | todas | `MenuSidebar` | `storageKey` propio; auto-colapso con riel de Escenarios abierto | `--surface-container` | ✅ |
| 3 | Tabs pill por sección | todas menos Visión General | `TabsNavigation` + `tabs.ts` | pill activo blanco con borde; secciones de 1 tab renderizan 1 pill | `--border`, `--hover` | ✅ |
| 4 | Breadcrumb `Home > Sección > Tab` | todas | `Breadcrumb` | dos niveles en Visión General | `--text-2` | ✅ |
| 5 | Badge as_of + estados de dataset | todas | `DataStatus` + `GlobalDatasetSelector` | estados Desactualizados/Preparando/No listo/Error | pastilla, `--fondo-*` | ✅ |
| 6 | **Badge de supuesto activo** | todas, todo estado | — | — (ver New Components N-1) | pastilla neutra | 🆕 |
| 7 | Panel de filtros derecho | dashboards | `MercadoFiltersSidebar` → `CreditoFiltersSidebar` | orden inviolable de controles (§4); control segmentado de moneda Todas·DOP·USD; "Vista por" | `--surface-container` | 🔄 |
| 8 | Selector de medida VaR·ES·Std | Métricas de Riesgo, Marginal | selector VaR↔CVaR de Mercado (`vision_general_dashboard.py` toggle) | segmented control de 3 opciones; cambia datos + etiqueta `<Medida>`, jamás layout (corrección X-8a: mapeado explícito) | `--primary` activo | 🔄 |
| 9 | Chip de moneda (DOP / USD / Mixta) | tablas, tooltips | `StatusBadge` | variante **neutra categórica** (la moneda no es estado ni semáforo) | gris, texto `--text-2` | 🔄 |

### KPIs y tarjetas

| # | Wireframe Component | Screen | DS Component | Variante / adaptación | Tokens clave | Status |
|---|---|---|---|---|---|---|
| 10 | Tarjeta KPI (valor + anterior, Δ, Δ%, tendencia) | dashboards §7–§14 | `CardMetric` | **DeltaBadge variante neutra** para medidas de riesgo (X-4); subtítulos portadores ("Consolidado en DOP · TC del corte", leyenda de prorrateo) | `--surface-card` | 🔄 |
| 11 | Tarjeta KPI categórica (Top Driver, Kupiec, Factor dominante) | §7.1, §8, §12–§14 | `CardMetric` | valor categórico + chip "anterior: X"; sin Δ% aritmético; estado tarjeta-completa-N/D (comparabilidad) | ídem | 🔄 |
| 12 | Tarjeta fija Uso Límite / Estado de Límites | dashboards | `CardMetric` + `StatusBadge` | semáforo Ok/Advertencia/Incumplimiento **solo aquí**; "N/D" sin límite, jamás 0% | `--sem-*` + `--fondo-*` | 🔄 |
| 13 | Cards resumen de Visión General (fila 1) | §11.1 | `card` (chart_type) | filas internas de detalle; pill de límite en card VaR | `--surface-card` | ✅ |
| 14 | **NavCard** (card_small navegable) | §11.3 | `card_small` | **variante de `card_small`** con prop `href` + chevron + hover elevación — no fork del registro (X-11) | `--hover` | 🆕 |

### Gráficos (registro `DynamicComponentRenderer`)

| # | Wireframe Component | Screen | chart_type | Variante / adaptación | Status |
|---|---|---|---|---|---|
| 15 | Área apilada temporal por rating | §7.1 TL, §8.2 TL | `stacked_area_chart` | paleta ordinal rating; selector de temporalidad al pie; **marcadores de cambio de supuesto** (ver N-6) | 🔄 |
| 16 | Dona de composición / contribución | §7.1, §8.1, §10.1 TR | `pie` | selector "Vista por" (`ChartFilterBar`); top-7+"Otros"; leyenda lateral con montos | ✅ |
| 17 | Barras divergentes de cambio / P&L / ranking | §7, §8.2, §9.8, §10.1, §11.2 | `chart_horizontal_bar` | barra "Total"; etiquetas Δ% sobre barra; neutro (P&L de Escenarios: semántica de signo); barra sin dato → ausente + "N/D" | 🔄 |
| 18 | Barras `<Medida>` / contribución por factor / top-N | §8.1 TL, §12 TL, §7.2 TL | `chart_vertical_bar` / `chart_horizontal_bar` | orden AAA→D; Euler + overlay incremental anotado (§12); toggle % VM / VM DOP en §7.2 TL (patrón `ChartFilterBar`) | 🔄 |
| 18b | Descomposición por rating del ΔVaR (selector de supuesto + toggle extremo −/+) | §13 BL | `chart_vertical_bar` + `ChartFilterBar` | dos controles intra-panel (precedente "Vista por" de donas); barras Δ de contribución Euler, aditivas al ΔVaR del extremo; subtítulo declarativo (N-4) | 🔄 |
| 19 | Barras agrupadas standalone vs. contribución | §8.1 BL | `bar` (serie doble) | dos series neutras diferenciadas por tono azul + dash | 🔄 |
| 20 | Línea con límite (HHI, razón, curva VaR-vs-ρ) | §7.2 TR, §8.2 TR, §13 TR | `timeseries` / `line` | **markline punteada de límite** (patrón Concentración de Mercado); marcador "base" en curva de ρ; marcadores de supuesto (N-6) | 🔄 |
| 21 | Histograma de pérdidas post-shock (multimodal) | §9.8 C2 | `loss_histogram` | ya trae marklines VaR (`lossHistogram.ts:85`); + overlay base outline, toggle "Comparar" 3 siluetas, **zoom multinivel cuerpo/banda/cola** (X-8c) | 🔄 |
| 22 | Waterfall de pérdida | §9.8 C3 | `waterfall` | top-7+"Otros"+Total; semántica de signo (P&L) | ✅ |
| 23 | **Scatter iso-risk** | §10.1 TL | `scatter` | — (ver N-3) | 🆕 |
| 24 | Heatmap matriz ρ | §12 BL | `heatmap` | escala **secuencial neutra** (jamás divergente semafórica); valor en celda; anotación de método | 🔄 |
| 25 | Tornado de supuestos | §13 TL | `chart_horizontal_bar` | — (ver N-8) | 🆕 |
| 26 | Traza de convergencia + bandas | §14 BL | `confidence_band` | selector local de cuantil; eje Y fijo común; subtítulo doble anti-Gauss | 🔄 |
| 26b | Panel de validación estadística (Kupiec · Christoffersen · Basilea) | §14 TR | `card` compuesto (3 bloques rotulados) | encabezado "Ventana válida: N cortes…"; p-values y veredictos en texto; contiene N-9 como badge; ventana <250 → "N/D — ventana incompleta" | 🔄 |
| 27 | Serie de excepciones (P&L vs −VaR) | §14 TL | `timeseries` (2 series) | marcadores de excepción por **forma** (rombo) en un único color de alerta rotulado, jamás terna; marcadores de supuesto (N-6) | 🔄 |
| 28 | Panel Umbrales de Merton | §12 TR | `line` + markArea | — (ver N-7) | 🆕 |

### Tablas

| # | Wireframe Component | Screen | DS Component | Variante / adaptación | Status |
|---|---|---|---|---|---|
| 29 | **Tabla jerárquica exportable** (BR de todo dashboard) | §7–§14 BR | `Table.tsx` + `TableGeneric` | Filas expandibles **hasta 3 niveles** (rating → emisor → instrumento — el front tiene expandibles de 2; se extiende a 3, X-3/X-8). **Regla de partición v2 codificada en el componente** (X-1): los grupos de columnas DOP·USD·Total **solo admiten columnas de VM**; toda columna de medida de riesgo (VaR/ES/Std, marginal, componental, standalone, G/P) se declara `consolidada: true` y el componente la renderiza fuera de los grupos de moneda — la violación es imposible por construcción, no por disciplina. Columnas Var → "N/D" bajo supuesto distinto. Pies metodológicos fijos **incluidos en el export** (X-8d): el export (patrón `xlsx` del front) serializa pies y notas como filas finales de la hoja | 🔄 |
| 30 | Tabla "Límites y Métricas" | §11.2 | `table` | columnas Métrica·Valor·Límite Int·Límite Reg·Uso·Estado; semáforo solo en Estado | ✅ |

### Estados y feedback

| # | Wireframe Component | Screen | DS Component | Variante / adaptación | Status |
|---|---|---|---|---|---|
| 31 | Skeletons por panel | todas | `MercadoSkeletons` | pulse `--skeleton`; overlay completo solo al arranque del módulo. **Los badges (supuesto, as_of) viven en la cabecera de sección, fuera de todo contenedor skeletonizable** (X-2) | ✅ |
| 32 | Estados vacío / error por gráfico | todas | `ChartErrorState`, `SectionUnavailable` | vacíos con instrucción y siguiente acción; error con Reintentar; sin toasts | ✅ |
| 33 | **Banner resultados obsoletos** | §9.6 | — (ver N-5) | | 🆕 |
| 34 | **Nota fija metodológica** (pies de panel/leyendas §2) | §9.5, §10, §12–§14 | — (ver N-4) | | 🆕 |
| 35 | **Chips de ρ + Franja VaR/ES** | §9.7 | — (ver N-2) | | 🆕 |
| 36 | **Badge veredicto Basilea** | §14 TR | — (ver N-9) | | 🆕 |

### Simulador (Escenarios)

| # | Wireframe Component | Screen | DS Component | Variante / adaptación | Status |
|---|---|---|---|---|---|
| 37 | Riel de configuración de shock | §9.3 | riel del simulador de Mercado (arquetipo 2 [inviolable]) + inputs del front (`Select`, `RadioButton`, `Checkbox`, inputs numéricos) | toggle segmentado Libro/Supuesto; steppers; selector de emisores (`MultiSelect`); preset editable de ρ; Aplicar (primario `--primary`, deshabilitado hasta validez — arquetipo 6) / Reiniciar (secundario); línea fija de consolidación TC (F1.10) | 🔄 |

---

## New Components

### N-1 · BadgeSupuestoActivo
- **Type**: feedback (chrome de sección).
- **Anatomía**: pastilla neutra (fondo `--surface-card`, borde `--border`, texto `--text-2`, ícono Info) contigua a `DataStatus`. Contenido: fuente de transición · método de correlación · ρ · TC de consolidación. Estados: base · post-run por familia de shock (§9.2) · **"Supuesto: N/D"** en Preparando/No listo/Error.
- **Regla estructural (X-2)**: vive en la **cabecera de la sección** (fila del breadcrumb), un nivel por encima de los paneles — jamás dentro de un contenedor que se skeletonice, vacíe o falle. Presente en las 8 pantallas y en los 4 estados UI. Admite **chips contiguos** (shock activo §9.2; "Ventana: N cambios de supuesto" §14). En exports de tabla, el supuesto activo se serializa como fila de encabezado (junto al as_of).
- **Fuente de verdad de ρ**: este badge. Los ChipsRho (N-2) **derivan** su estado de él (X-7).
- **Rationale**: §2 no negociable del handoff; no existe nada equivalente en Mercado.
- **Status**: Pending DS addition. **Candidato a retro-porte a Mercado** (transversal, no crediticio — X-9; anotado en feedback-log para el PM).

### N-2 · ChipsRho + FranjaVaRES
- **Type**: acción (chips) + data display (franja). Solo Escenarios post-run de barrido.
- **Anatomía**: grupo de chips (patrón chip activo del front: fondo `--primary`, texto blanco) con los valores del **set efectivo del run** (nunca hardcodeado en el componente — X-7: el default {15/25/35} es dato del riel, no del DS); franja fija con VaR y ES por ρ en neutro + referencia de límite ("Límite: $X — uso YY% @ρ=base" / "Límite: N/D").
- **Rationale**: §9.7; sin precedente en Mercado.
- **Status**: Pending DS addition.

### N-3 · ScatterIsoRisk
- **Type**: data display (`scatter` extendido).
- **Anatomía**: scatter ECharts + 3 overlays de límite con leyenda **siempre presente** (h: piso %-riesgo · v: tamaño · hipérbola iso-risk; ausente → "Límite: N/D"), cuadrantes A/B/C anotados + nota "fallen angels viven aquí", color por rating (paleta ordinal), opacidad 0.7, zoom/brush, semiplano Y<0 con línea Y=0.
- **Rationale**: §10.1 TL; no existe en Mercado (aporte propio de Crédito).
- **Status**: Pending DS addition.

### N-4 · NotaFijaMetodologica
- **Type**: feedback (texto fijo de panel/tabla).
- **Anatomía**: pie de panel en `--text-2` 12px, **parte del componente del panel, no del layout** (X-6: sobrevive a capturas/exports del componente); variantes: leyenda de prorrateo (shell §4), nota de granularidad (§9.5/§10), convención de atribución (§12), OAT+CRN (§13), convención de escala (§14), pies de moneda/TC (F1.10). Siempre incluida en el export.
- **Rationale**: §2 auditable; el front no tiene componente de pie metodológico.
- **Status**: Pending DS addition. **Candidato a retro-porte a Mercado** (X-9).

### N-5 · BannerResultadosObsoletos
- **Type**: feedback (estado del simulador).
- **Anatomía**: banner inline sobre el área de resultados (fondo `--fondo-alerta`, texto warning, sin auto-dismiss): "Configuración modificada — Aplicar para recalcular"; resultados atenuados (opacidad), nunca limpiados en silencio. **Variante dashboard** (§13): "Barridos calculados bajo otro supuesto — pendiente de recálculo del corte" — mismo componente, copy por contexto.
- **Rationale**: §9.6; el simulador de Mercado no declara este estado.
- **Status**: Pending DS addition. Candidato a retro-porte (X-9).

### N-6 · MarcadorCambioSupuesto (variante de series temporales)
- **Type**: data display (markline vertical + tooltip).
- **Anatomía**: markline vertical punteada gris en cada corte donde cambió el supuesto, tooltip con el supuesto vigente; aplica a `stacked_area_chart`, `timeseries` y `line` multi-corte (§8.2, §14 TL). **Sin él, ninguna serie histórica del módulo es publicable** (X-8b: una serie que cruza un cambio de ρ/TC sin marcar es engañosa — roza §2).
- **Rationale**: §8.2/§14; regla de comparabilidad.
- **Status**: Pending DS addition (variante de charts existentes).

### N-7 · PanelUmbralesMerton
- **Type**: data display (`line` + markArea).
- **Anatomía**: densidad normal de la **variable latente** con bandas Z etiquetadas y cola de default sombreada; selector de rating de partida (7 letras, D excluido). **El subtítulo anti-lectura-errónea es parte del componente** (X-6): *"Retorno de activo estandarizado bajo Alt 2 — no es la distribución de valor del portafolio"* se renderiza dentro del panel y se incluye en export/captura — el componente no puede instanciarse sin él (prop obligatoria).
- **Rationale**: §12 TR; única curva normal legítima del módulo (variable latente, no valor).
- **Status**: Pending DS addition.

### N-8 · TornadoSupuestos
- **Type**: data display (`chart_horizontal_bar` extendido).
- **Anatomía**: barras horizontales centradas en línea vertical del VaR base (etiquetada con monto), extremos −/+, máx 7 barras + fila de texto "N supuestos más — ver tabla"; barras unilaterales para supuestos categóricos; neutro; subtítulo OAT+CRN (N-4 embebida).
- **Rationale**: §13 TL; sin precedente en Mercado.
- **Status**: Pending DS addition.

### N-9 · BadgeVeredictoBasilea
- **Type**: feedback (veredicto estadístico).
- **Anatomía**: badge **rectangular** (radio 4, no pill) con rótulo fijo *"Veredicto estadístico de validación del modelo — no es cumplimiento de límites"* + zona y conteo en texto ("Zona verde — 2 excepciones / 250"). **Color (resolución X-5)**: el Brain permite el semáforo estadístico de Basilea como elemento distinto **si se rotula** ("nunca se confunde con el semáforo de límites; si coexisten, se rotulan" [inviolable]); el badge usa los mismos tokens semánticos (`--sem-ok/warn/error`) pero en **forma rectangular etiquetada con el nombre de la zona siempre en texto** (color nunca canal único) — la distinción canónica es rótulo + silueta + contexto, y queda prohibido instanciarlo fuera del panel TR de Backtesting. En NavCard (§11.3) el veredicto es **texto sin color**.
- **Rationale**: §14 (regla de interfaz [inviolable]).
- **Status**: Pending DS addition.

---

## Financial Data Contract

| Concern | Applies | Concrete Implementation | Status |
|---|---|---|---|
| Unidades y precisión | sí | Formateador único (paridad `utils/format.ts`): $ + escala M/MM (nunca K), montos 2 dec, HHI 4 dec, % 1–2 dec, cifras `tabular-nums` alineadas a la derecha. **Codificado en `CardMetric`/`Table` vía el formatter, no por pantalla** (X-12) | applied |
| Moneda | sí | DOP consolidado en todo agregado; grupos DOP·USD·Total solo en VM (partición v2, codificada en Table #29); chip de moneda (#9) en nivel instrumento; subtítulo del KPI 1 "Consolidado en DOP · TC del corte" (portador por arquetipo: riel en Escenarios, card Portafolio en Visión General) | applied |
| Corte, fecha y timezone | sí | `DataStatus` "Datos DD/MM/AAAA" siempre visible [inviolable "no ocultar corte"]; DD/MM/AAAA en toda fecha; pies "Cada punto consolidado al TC de su fecha" en series multi-corte | applied |
| Fuente o metodología | sí | BadgeSupuestoActivo (N-1) en toda pantalla/estado; NotaFijaMetodologica (N-4) por panel; convenciones del mock rotuladas ("convención del mock — la metodología oficial del tenant gobierna") | applied |
| Certeza y frescura | sí | Estados Desactualizados/Preparando/No listo/Error del `DataStatus`; regla de comparabilidad (Δ → "N/D" bajo supuesto distinto, tarjeta completa N/D en KPIs-Δ); ventana válida rotulada en Backtesting | applied |
| Estados vacío/degradado/error | sí | 4 estados UI por pantalla (mandato Fase 2); `ChartErrorState` con Reintentar; vacíos con instrucción; N/D nunca cero; "—" solo para no-aplica; barras sin dato ausentes + "N/D"; fallas por componente no tumban el dashboard. Matriz pantalla×estado se materializa en el prototipo (F2.2) — los componentes de estado quedan mapeados aquí (#31–#33) (X-8e) | applied |
| Actualización / motion | sí | Números de tabla se actualizan secos (sin tween); skeleton pulse; `component_refreshing` por panel; nunca animar color de dato | applied |
| Equivalente accesible | sí | Toda tabla BR es el equivalente tabular de los gráficos de su pantalla (exportable); color nunca canal único (forma+texto en excepciones, signo+etiqueta en divergentes); foco visible en controles (no suprimir foco [prohibición]) | applied |

## Canon Compliance Ledger

| # | Source | Constraint | Applicability | Concrete Implementation | Status |
|---|---|---|---|---|---|
| L-1 | Handoff §2 / Brain MetodologiaCredito [inviolable] | Rating eje primario; jamás granularidad emisor-específica | aplicable | Drill-down rating→emisor→instrumento en Table #29; leyenda de prorrateo / nota de granularidad (N-4) en toda superficie por emisor; scatter colorea por rating | applied |
| L-2 | Handoff §2 [inviolable] | Badge de supuesto activo visible en toda pantalla y estado | aplicable | N-1 en la cabecera fuera de contenedores skeletonizables; "Supuesto: N/D" en estados degradados; serializado en exports | applied |
| L-3 | Brain MetodologiaCredito [inviolable] | Distribución de valor jamás campana de Gauss | aplicable | `loss_histogram` multimodal (#21); curvas normales solo en N-7 (variable latente) y N-26 bandas MC, ambas con subtítulo anti-Gauss embebido en el componente (N-7 y fila #26) | applied |
| L-4 | Handoff §2 / F1.10 | DOP consolidado; medida de riesgo jamás partida por moneda | aplicable | Partición v2 codificada por construcción en Table #29; TC en badge N-1 | applied |
| L-5 | Brain PlataformaUX [inviolable] | No reasignar la terna del semáforo; semáforo solo estado de límite | aplicable | `--sem-*` solo en Uso Límite (#12), tabla de límites (#30), pills de estado; **DeltaBadge neutro para medidas de riesgo** (#10); Basilea rotulado y rectangular (N-9); excepciones por forma+color-alerta-único (#27) | applied |
| L-6 | Brain Capa1 Tokens [inviolable] | Riesgo en neutro; series jamás con semánticos; color nunca canal único | aplicable | `--data-neutral` + paleta ordinal azul; semántica de signo solo en P&L de Escenarios (frontera §9, registrada para PM); texto/forma acompañan todo color | applied |
| L-7 | Brain PlataformaUX [inviolable] | No hex fuera de tokens | aplicable | Tabla de tokens única; el prototipo consume solo variables | applied |
| L-8 | Brain PlataformaUX [inviolable] | Jerarquía Módulo→Sección→Tab; contrato de navegación; dominios autoritativos; no dashboard↔simulador | aplicable | Componentes #1–#8; Escenarios con riel (arquetipo 2); filtros con orden fijo y dominios declarados del contrato | applied |
| L-9 | Brain Capa1 Tokens [inviolable] vs. baseline RI [guia] | IBM Plex Mono para cifras (corporativo) vs. Inter (baseline RI) | **conflicto de régimen resuelto por la excepción documentada** | RI en excepción de rebranding → Inter + `tabular-nums` satisface la intención (alineación tabular); tensión registrada en feedback-log para el PM; migración = decisión del dueño de producto | applied |
| L-10 | Brain Capa1 Tokens [inviolable] | MM/M nunca K; DD/MM/AAAA; N/D nunca cero; máx 8+"Otros"; DOP | aplicable | Formatter único (#Contract fila 1); top-7+"Otros" en vistas por emisor; N/D y "—" diferenciados | applied |
| L-11 | Brain PlataformaUX [inviolable] | No métrica de riesgo sin contexto de límite | aplicable | Tarjeta fija Uso Límite (#12) en todo dashboard; franja VaR/ES con límite en Escenarios (N-2); markline de límite en series (#20) | applied |
| L-12 | Brain PlataformaUX [inviolable] | Crédito copia el contrato completo de Mercado | aplicable | Todo componente base es el componente real de Mercado (#1–#5, #10, #15–#22, #29–#32); desviaciones documentadas en el wireframe spec y feedback-log | applied |
| L-13 | Brain Motion [inviolable] | Nunca animar color de dato; reduced-motion | aplicable | Números secos; pulse solo en skeleton; el prototipo respeta `prefers-reduced-motion` | applied |
| L-14 | Brain PlataformaUX [inviolable] | Estados de sistema con marca y en español; sin toasts; no spinner único | aplicable | #31–#32; overlay solo al arranque; feedback = cambio de estado visible | applied |

**Auditoría de consistencia final**: ninguna fila `applied` es debilitada por otra parte del artefacto; el único conflicto real (L-9) está resuelto por la regla de excepción explícita del propio Brain, no por juicio del agente. Ningún ítem aplicable queda sin implementación concreta.

## Codebase References (Supplementary)

Evidencia factual (no canon) de `context-mercado/01-front-structure.md`: `globals.css` (tokens), `colors-reports.tsx` (paletas de gráficos), `CardMetric.tsx`, `DataStatus.tsx`, `TabsNavigation.tsx`, `Table.tsx` (grupos de columnas), `MercadoSkeletons.tsx`, `utils/format.ts` (formatter), registro `DynamicComponentRenderer.tsx:39-69`. Backend: view profiles diseñados para reutilización market↔credit (`02-dashboards-backend.md`) — el mapping mantiene todo gráfico dentro del catálogo de `chart_type` para plausibilidad de implementación.

## Gaps para brain-gap-reporting (pendientes de aprobación del PM — no declarados)

1. **Componentes transversales sin canon**: BadgeSupuestoActivo, NotaFijaMetodologica y BannerResultadosObsoletos son patrones de auditabilidad transversales (aplicarían a Mercado); el Brain no los documenta como componentes del DS de RI. Candidatos a entrada de plataforma + retro-porte (X-9).
2. **Paleta ordinal de rating**: el Brain corporativo define "pasos de calificación ordinal a ΔE≥25" para el sistema destino, pero el baseline RI no define paleta ordinal — el mapping la deriva de la escala azul del front. Vacío del baseline.
3. **Variante neutra de DeltaBadge**: el DS vigente de RI colorea deltas por signo (deuda #12 reconocida); la variante neutra requerida por el canon no existe como componente documentado.

---
**Estado**: mapping completo — documento de trabajo para F2.2 (assembly). No es gate formal; el PM puede ajustar antes o durante el prototipo.
