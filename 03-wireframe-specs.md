# Wireframe Specification — Sección Crédito (Mock UX/UI)

**App**: Risk Intelligence (RI)
**Date**: 2026-08-20
**Status**: Draft — awaiting PM gate (bead [GATE-PM] Fase 1)
**Screens**: Parte 1 — Shell de navegación + molde transversal (bead librisk-8ag / F1.3). Parte 2 — Sección Portafolio, tabs Global y Concentración (bead librisk-2v2 / F1.4, §7). Parte 3 — Sección Métricas de Riesgo (ex-VaR), tabs A la Fecha e Histórico (bead librisk-a66 / F1.5, §8; rehecha por corrección PM F1.9, bead librisk-08x). Parte 4 — Sección Escenarios, tab Impacto en Riesgo (bead librisk-iq9 / F1.7, §9). Parte 5 — Sección Marginal, tab Global (bead librisk-mvx / F1.6, §10). Parte 6 — Sección **Visión General** (entrada default, corrección PM F1.8, bead librisk-dbv, §11). Parte 7 — Sección **Factores de Riesgo**, tab Mapa de Factores (ampliación PM F1.11, bead librisk-6rq, §12). Parte 8 — Sección **Sensibilidades**, tab Supuestos (ampliación PM F1.12, bead librisk-yct, §13). Parte 9 — Sección **Backtesting**, tab Resumen de Excepciones (ampliación PM F1.13, bead librisk-o07, §14). **8 secciones activas** (mandato PM F1.11 cumplido: las 8 diseñadas — sin "próximamente"). Corrección PM **F1.10 multi-moneda DOP/USD** aplicada transversalmente (bead librisk-eed, 2026-08-21): regla de moneda en shell §4 + §7–§12. Parte 10 — Sección **Deterioro (NIIF 9)**, tab Staging + clasificación contable (ampliación PM F1.14, handoff `06-handoff-ifrs9-ecl.md`, bead librisk-k9s, §15): el módulo pasa a **9 secciones activas**; tabs ECL · Movimientos · Conciliación REA pinneados con spec en F1.15/F1.16. Parte 11 — **Tab ECL** de Deterioro (bead librisk-1ob / F1.15, §15.3): mecánica del cálculo, curvas PD/EAD/LGD, EIR original y escenarios macro ponderados; badge seccional completado y NavCard 9 agregada (§11.3). Parte 12 — **Tabs Movimientos y Conciliación REA** de Deterioro (bead librisk-arr / F1.16, §15.4–§15.5): roll-forward de stages y provisión, conciliación ECL↔REA SB (categorías A-E, "mayor de los dos") y tratamiento FVOCI/ORI (doble registro). **La cadena de tabs de Deterioro queda completa** — el módulo entra al gate de Fase 1 ampliada con 9 secciones y 4 tabs de Deterioro especificados.

---

## Production Reference

Grounding empírico: dataset `context-mercado/` (estructura del front `01-front-structure.md`, backend `02-dashboards-backend.md`, 10 screenshots `03-screenshots-index.md`). Referencia de molde: `screenshots/var-global.png` (verificada visualmente en este bead) — header global con 4 módulos (Crédito hoy **deshabilitado en gris**: ahí vive esta sección), sidebar "Mercado" con 7 ítems, breadcrumb `Home > VaR > Global`, derecha: badge "Datos 30/01/2026" + selector de dataset + botón Filtros, tabs pill, columna izquierda de 5 tarjetas KPI (la 5ª es "Uso Límite N/D"), rejilla derecha con área apilada, dona, barras de cambio y tabla de descomposición. No se navegó la app viva: el dataset cubre todo lo requerido por este bead.

**Fuentes canónicas**: `00-handoff-metodologico.md` (§2 no negociable, §5, §6, §10); Brain corpus `8b3bd636c070fe38`: `Capa2_RI_MetodologiaCredito.md`, `Capa2_RI_PlataformaUX.md`, `Capa2_RI_Producto.md`, `Capa1_Diseno_Tokens.md`. RI opera bajo la **excepción de rebranding**: baseline visual vigente del front, no tokens corporativos de Capa 1.

---

## 1. Shell — Header global y entrada al módulo

**Purpose**: el usuario entra a Crédito desde el header global y aterriza en la pantalla por defecto sin decisiones intermedias.

**Information Hierarchy**:
1. Tab de módulo **Crédito** activo en el header global (Mercado · Liquidez · **Crédito** · Operacional; Liquidez y Operacional permanecen en gris — "futuro visible pero inactivo", Brain [inviolable]).
2. Selector de tenant, búsqueda, notificaciones, avatar — sin cambios (paridad total con Mercado).

**Navegación**:
- **Inbound**: clic en "Crédito" en el header global.
- **Default**: redirección a **Crédito › Visión General** (`/dashboard/credito/vision-general`) — corrección PM F1.8 (bead librisk-dbv): la entrada al módulo aterriza en el overview ejecutivo, no en VaR. Paridad con Mercado, cuyo primer ítem y aterrizaje natural es Visión general (`vision-general.png`). El "VaR pantalla por defecto" del handoff §5 queda sustituido por decisión del PM (feedback-log 2026-08-20).
- Patrón de rutas [inviolable]: `/dashboard/[categoría]/[módulo]/[vista]`; vista nueva = pestaña, nunca pantalla suelta.

## 2. Shell — MenuSidebar "Crédito"

**Purpose**: el usuario elige la sección de análisis; ve el futuro del módulo sin poder activarlo.

**Componentes**:
| Componente | Tipo | Descripción |
|---|---|---|
| MenuSidebar título "Crédito" | navegación | colapsable con persistencia propia (`storageKey` de Crédito); versión móvil dropdown; activo por prefijo de ruta; **auto-colapsa cuando el riel de Escenarios está abierto** (paridad con el comportamiento de Mercado) |
| 9 ítems de menú | navegación | **las 9 activas** — mandato PM F1.11 cumplido y ampliado por F1.14 (handoff NIIF 9): cada sección se activó en el bead que entregó su spec (Backtesting: F1.13, §14; Deterioro NIIF 9: F1.14, §15); sin "próximamente" ni "en diseño" |

**Orden de ítems** (paridad empírica con el orden de Mercado — `MENU_ITEMS` en `layout.tsx:4-28` y sidebar de `var-global.png`; la enumeración en prosa del handoff §5 no es mandato de orden — con **Marginal** insertado inmediatamente después de Métricas de Riesgo por ser su satélite analítico):

| # | Ítem | Estado | Href (primer tab) |
|---|---|---|---|
| 1 | Visión General | **activa (default del módulo — corrección PM F1.8)** | `/vision-general` |
| 2 | Portafolio | activa | `/portafolio/global` |
| 3 | Sensibilidades | **activa (ampliación PM F1.12, §13)** | `/sensibilidades/supuestos` |
| 4 | Métricas de Riesgo | activa (renombre PM F1.9 — ex "VaR") | `/metricas-de-riesgo/a-la-fecha` |
| 5 | Marginal | activa | `/marginal/global` |
| 6 | Factores de Riesgo | **activa (ampliación PM F1.11, §12)** | `/factores-de-riesgo/mapa-de-factores` |
| 7 | Escenarios | activa | `/escenarios/impacto-en-riesgo` |
| 8 | Backtesting | **activa (ampliación PM F1.13, §14)** | `/backtesting/resumen-excepciones` |
| 9 | Deterioro (NIIF 9) | **activa (ampliación PM F1.14, §15)** | `/deterioro/staging` |

> **Orden del ítem 9 (decisión declarada)**: Deterioro (NIIF 9) cierra el sidebar tras Backtesting — narrativa medición → validación → **traducción contable**. Sin equivalente en Mercado (el deterioro es propio de crédito); la paridad de contrato (molde, jerarquía, orden de controles) se mantiene.

> **Desviación documentada — Marginal como sección propia.** En Mercado, Marginal es un tab de VaR-y-ES. En Crédito es sección de sidebar porque el handoff §5 (fuente vinculante: sketch núcleo de 4 secciones) la eleva a núcleo. El inviolable "crédito copia el contrato completo del módulo de mercado" se cumple en contrato (jerarquía, orden de controles, arquetipos, molde), no en árbol IA literal. Tensión registrada para el PM en `feedback-log.md`.

## 3. Shell — Tabs por sección (jerarquía Módulo→Sección→Tab [inviolable])

La tira "Tabs: VaR · Marginal · Portafolio · Escenarios" del molde §6 del handoff **no** se implementa literal (chocaría con la jerarquía inviolable: las secciones viven en el sidebar). Tabs = **sub-vistas por sección**, patrón `tabs.ts` + pills de Mercado:

| Sección | Tabs pinneados |
|---|---|
| Visión General | — (sin barra de tabs; ver excepción abajo) |
| Portafolio | Global · Concentración |
| Sensibilidades | Supuestos |
| Métricas de Riesgo | A la Fecha · Histórico |
| Marginal | Global |
| Factores de Riesgo | Mapa de Factores |
| Escenarios | Impacto en Riesgo |
| Backtesting | Resumen de Excepciones |
| Deterioro (NIIF 9) | Staging · ECL · Movimientos · Conciliación REA |

- Los beads por sección pueden **añadir** tabs; nunca renombrar ni eliminar los pinneados (los hrefs del menú apuntan al primer tab).
- Secciones de un solo tab **sí renderizan la barra** con un solo pill: uniformidad del molde y del breadcrumb. Sin precedente empírico en Mercado — anotado para el PM. **Excepción acotada al arquetipo overview**: Visión General **no** renderiza barra de tabs (precedente empírico directo: `vision-general.png` de Mercado no la tiene); su breadcrumb es `Home > Visión general` (dos niveles). El resto de secciones de un solo tab mantienen la regla del pill.
- **Breadcrumb**: `Home > Sección > Tab` (paridad empírica `Breadcrumb.tsx`; el módulo lo nombra el título del sidebar). La notación "Crédito › <Sección>" del journey es abreviatura editorial.

## 4. Molde transversal de pantalla (Portafolio · Métricas de Riesgo · Marginal)

**Purpose**: molde único reutilizable; el cambio de sección cambia contenido, nunca estructura.

**Estructura** (de arriba hacia abajo; paridad `var-global.png` + handoff §6):

```
┌─────────────────────────────────────────────────────────────────────┐
│ Home > <Sección> > <Tab>     [Supuesto: S&P · ρ=25% axiomático]      │
│                              [Datos DD/MM/AAAA] [dataset ▾] [Filtros]│
│                              [ VaR · ES · Std ]  ← solo Métricas de Riesgo y Marginal│
├─────────────────────────────────────────────────────────────────────┤
│ ( Tab 1 ) ( Tab 2 )                                   ← pills        │
├───────────────┬─────────────────────────────────────────────────────┤
│ KPI 1         │                                                     │
│ KPI 2         │   TL (gráfico)            TR (gráfico)              │
│ KPI 3         │                                                     │
│ KPI 4         │   BL (gráfico)            BR (tabla exportable)     │
│ KPI 5: límite │                                                     │
└───────────────┴─────────────────────────────────────────────────────┘
```

**Componentes del molde**:
| Componente | Tipo | Descripción |
|---|---|---|
| Badge de supuesto activo | feedback | **presente en toda pantalla del módulo (todas las secciones activas), en todo estado** (§2 no negociable). Contenido: fuente de transición · método de correlación · ρ · **TC de consolidación** (p.ej. "S&P · ρ=25% axiomático · TC 61.50 (BCRD venta, as_of)" — el 61.50 es **valor del mock**; el TC real viene del contrato de datos) — el TC usado para consolidar USD→DOP es un supuesto activo auditable (F1.10). En estados Preparando / No listo / Error del dataset muestra "Supuesto: N/D" — **nunca se oculta**. En Escenarios tiene 2 estados (ver §5). **En Deterioro (NIIF 9) se extiende con el segmento de supuestos NIIF 9 activos (ver §15)** — un solo badge, nunca dos componentes. |
| Badge as_of (`DataStatus`) | feedback | "Datos DD/MM/AAAA" + estados Desactualizados/Preparando/No listo/Error + selector de dataset (paridad Mercado) |
| Selector de medida VaR · ES · Std | acción | *segmented control* arriba a la derecha; **solo Métricas de Riesgo y Marginal** (ausente en Portafolio y Escenarios). Cambia los datos, **nunca el layout** (handoff §4/§10; Brain guia). σ → límites; VaR/ES → capital. |
| Tira de KPIs (5 tarjetas) | data display | patrón `CardMetric`: valor grande + (anterior, Δ, Δ%) + tendencia. **4 KPIs de contenido** (definidos por sección) **+ 1 tarjeta fija de contexto de límite** — inviolable "no métrica de riesgo sin contexto de límite": en Métricas de Riesgo y Marginal = "Uso Límite" (de la medida activa); en Portafolio = "Límite de concentración" (HHI / top-N). Sin límite configurado → "N/D" (paridad `var-global.png`). Los KPIs son **informativos, no navegables** (incluye Top Driver — deferral F1.2 mantenido). |
| Rejilla 2×2 | data display | TL/TR/BL = gráficos por sección; **BR = tabla detallada y exportable** (handoff §6; paridad `var-global.png`) |

**Formatos transversales** (Brain `Capa1_Diseno_Tokens.md` [inviolable] + baseline RI):
- **Regla transversal de moneda (F1.10 — corrección PM: la cartera NO es 100% DOP; hay instrumentos denominados en USD):**
  - **Motor de formato**: paridad Mercado — símbolo `$` uniforme, escala **M/MM (nunca K)**, 2 decimales; la desambiguación de moneda vive **exclusivamente en encabezados de grupo/columna, ejes y subtítulos** ("DOP" / "USD" / "Total DOP"); prohibido mezclar `RD$`/`US$` en celdas; jamás cifras de monedas distintas sin rótulo.
  - **Consolidación**: toda cifra agregada (KPIs, ejes, donas, áreas apiladas y **toda medida de riesgo**) en **DOP consolidado**, USD convertido al **TC BCRD venta del as_of** (campo del contrato de datos — dominio autoritativo de la capa de datos). Ancla: Brain `Capa2_RI_Consolidacion.md` [inviolable] regla 7 "moneda de consolidación: DOP único" — **intacta**: las columnas DOP/USD muestran **denominación nativa**, no una consolidación alternativa; y handoff §2 "moneda base DOP" (intacto). Portador de la declaración por sección: dashboards (Portafolio, Métricas de Riesgo, Marginal) → **subtítulo del KPI 1** ("Consolidado en DOP · TC del corte"); Escenarios → **línea fija en el riel de control**; Visión General → **subtítulo de la card Portafolio**.
  - **Partición de moneda v2** (paridad Mercado, `var-global.png` tabla DOP/USD + `Table.tsx` grupos de columnas): grupos de columnas **DOP · USD · Total (DOP consolidado)** SOLO en columnas de **VM (montos de valor)**. Toda **medida de riesgo** (VaR/ES/Std, marginal, componental, standalone, G/P de escenarios) va SIEMPRE en DOP consolidado y **jamás se parte por moneda** — el VaR no es aditivo entre monedas; una columna "Total" junto a parciales invitaría a una suma falsa.
  - **Moneda del instrumento**: dimensión autoritativa (DOP · USD); **visible** como chip/columna en todo nivel hoja instrumento; a nivel emisor solo si es unívoca — emisor con ambas monedas → chip **"Mixta"**; **filtrable** (ver Filtros).
  - **Celdas de grupo sin posiciones** en esa moneda → **"—"** (no aplica); el 0 queda reservado a valor nulo real. Bajo filtro de moneda, ratings sin posiciones en la moneda filtrada se muestran con "—", **nunca 0, nunca ocultos** (el eje primario rating no pierde categorías).
  - **Variaciones y series**: pie fijo en toda tabla con columnas Δ: *"Variaciones al TC de cada corte; incluyen efecto FX"*; en **toda visual o tabla de naturaleza temporal multi-corte** (no solo el tab Histórico §8.2 — incluye el área apilada de Portafolio §7.1 y la evolución del HHI §7.2) además: *"Cada punto consolidado al TC de su fecha"*. Los visuales de Δ (barras divergentes) quedan cubiertos por el pie de la tabla BR de su misma pantalla — decisión declarada, no omisión. Ambas leyendas se incluyen en el export.
  - **Sin shock FX en todo el módulo** (el estrés FX pertenece a Mercado).
- Moneda (formato): unidad del grupo explícita en encabezados de columnas, ejes y subtítulo de KPIs.
- Fechas **DD/MM/AAAA**; valores ausentes **"N/D", nunca cero**; cifras en mono tabular.
- Color: métricas de riesgo en **neutro**; el semáforo Ok/Advertencia/Incumplimiento solo para estado de límite; series nunca pintadas con semánticos; deltas comunican impacto en riesgo, no signo aritmético.
- Dataviz categórico: máx **8 categorías + "Otros"**.
- **Leyenda de prorrateo (transversal)**: toda vista con desglose por emisor lleva la leyenda fija *"Contribución prorrateada por exposición — el modelo opera a nivel rating"* (§2 no negociable: no prometer granularidad emisor-específica; rating = eje primario del drill-down canónico rating → emisor → sector → tipo de instrumento).

**Patrón transversal InfoButton ⓘ / InfoPopover (corrección PM F2.13 — densidad de texto)**:
- **Taxonomía de texto**: (a) *estado/acción* — badges (supuesto, as_of, NIIF 9), pills/chips de estado, banners de estado (corte no comparable, barridos pendientes, dataset no listo) y notas de empty-state que evitan dead-ends → **siempre visibles**; (b) *metodología/explicación* — pies de panel, leyendas largas, caveats, notas de granularidad/prorrateo, subtítulos explicativos → **detrás de UN botón ⓘ por panel**, junto al título en el panel-head; (c) *calificadores §2 en celdas/KPIs* → chip corto visible ("prorr.") con detalle en el popover del panel.
- **Los textos no se eliminan**: viven a 1 clic en el popover (segmentos separados, **inviolables §2 primero**) y permanecen como líneas "Nota" en todos los exports CSV (el CSV no es UI). Decisión PM explícita (bead librisk-8yh): 1 clic satisface el §2 para prorrateo/granularidad; el badge de supuesto sigue siempre visible.
- **Comportamiento** (componente nuevo propuesto — pendiente de alta en DS): botón real con `aria-expanded`/`aria-controls`/`aria-haspopup`; popover en portal al body (nunca hijo del panel — evita clipping por overflow y stacking del canvas), max-width min(420px, 90vw), uno abierto a la vez con cambio atómico entre ⓘ, cierre por clic fuera / Esc (devuelve foco) / scroll / re-render.
- **CTAs jamás enterrados**: cualquier enlace de navegación dentro de una nota (p.ej. "Explorar → Escenarios") se extrae a una línea visible propia del panel antes de mover el resto al popover.
- **Notas del drawer de Filtros**: ⓘ individual inline por nota (no se concatenan a nivel drawer).

**Filtros** (contrato de navegación analítica [inviolable]):
- Panel derecho `CreditoFiltersSidebar` (paridad `MercadoFiltersSidebar`): contexto, no navegación; se cierra al navegar; superpuesto <1280px.
- Orden fijo de controles: (1) filtros globales — fecha, portafolio, dataset → (2) toggles de pestaña → (3) filtros contextuales de crédito — **calificación · emisor · tipo de instrumento (bono / SBB / SBB con garantía / CD) · seniority · clasificación NIIF 9 (AC · FVOCI · FVTPL — F1.14) · stage (1 · 2 · 3 — F1.14) · moneda** (control segmentado Todas · DOP · USD, default **Todas**, último del bloque — F1.10; con filtro de moneda activo, el subtítulo de consolidación pasa a "Solo instrumentos USD · Consolidado en DOP · TC del corte" — simétrico para DOP; las filas de emisores "Mixta" recalculan solo con sus instrumentos de la moneda filtrada y su chip conmuta a esa moneda) → (4) "Vista por" — dimensión de agregación rating → emisor → sector → tipo (no es filtro) → (5) selectores de tiempo solo en visuales temporales.
- **Dominios autoritativos**: los valores válidos vienen de la capa de datos (en el mock, declarados del contrato backend); jamás se infieren del contenido visible.

## 5. Molde de Escenarios — arquetipo simulador (excepción al molde §4)

**Purpose**: configurar → aplicar → leer. Escenarios **no hereda** la tira KPI + 2×2 del dashboard: es el arquetipo 2 del Brain [inviolable] ("nunca convertir dashboard en simulador ni viceversa"; paridad `escenarios-impacto-riesgo.png`).

**Estructura**: breadcrumb + badges (as_of y supuesto, igual que §4, **sin selector de medida**) → barra de tabs (un pill) → **riel de control persistente izquierdo** (tipo de shock: libro / supuesto; magnitud; parámetro a barrer; Aplicar / Reiniciar; el MenuSidebar auto-colapsa mientras esté abierto) → área de resultados (layout definido en el bead de Escenarios).

**Badge de supuesto con estados**: pre-run "S&P · ρ=25% (base)"; post-run refleja el supuesto **efectivo** por familia de shock — tabla completa en §9.2.

## 6. Estados de interfaz (transversal)

`loading · refreshing · component_refreshing · warming · ready · failed · stale` (Brain [guia]): overlay completo solo al arranque del módulo; luego skeletons por panel (patrón `MercadoSkeletons`); las fallas de un componente no tumban el dashboard; vacíos por gráfico; sin toasts; todo estado con marca y en español. Detalle por sección en Fase 2 (prototipo: happy path + 4 estados UI).

---

## 7. Sección Portafolio — *composición y concentración* (bead librisk-2v2 / F1.4)

Molde dashboard §4 heredado íntegro: breadcrumb `Home > Portafolio > <Tab>`, **badge de supuesto activo** + DataStatus + dataset + Filtros (el badge lo garantiza el shell en toda pantalla, §2), tabs pill, tira 4+1 KPIs, rejilla 2×2 con BR exportable. **Sin selector VaR·ES·Std**: Portafolio es composición y concentración **sin medida de riesgo** (handoff §7.1; Brain `Capa2_RI_MetodologiaCredito.md` [guia]). La sensibilidad a ρ (§2) no vive aquí: su espacio de UI es Escenarios (§7.4) y Sensibilidades (recomendada).

**Asignación tab-a-métrica del §7.1** (decisión explícita): la *composición* (área apilada, dona, cambio, tabla por rating) vive en **Global**; las *métricas destacadas* HHI y top-N emisores viven en **Concentración**. Juntas cubren §7.1 completo.

**Regla transversal de la sección**: toda vista **gráfica** por emisor (dona en "Vista por: Emisor", top-N, divergentes por emisor) colapsa a **top-7 + "Otros"** (formato transversal máx 8 categorías, §4); en barras divergentes "Otros" = Δ agregado del residual. Las **tablas** quedan exentas (listan completo). Todas las cifras de Portafolio son **VM observado** (matriz de Exposición, handoff §1), no riesgo modelado → la leyenda de prorrateo del shell (§4) **no aplica** aquí; ninguna celda de esta sección contiene riesgo prorrateado.

### 7.1 Tab Global — ¿de qué está hecho el libro y cómo cambió?

**Purpose**: el usuario lee la mezcla de calidad crediticia del libro y su variación vs. el corte anterior.

**Information Hierarchy**: 1) VM Total y su variación · 2) mezcla por rating (hoy y en el tiempo) · 3) cambio por grupo vs. referencia · 4) detalle exportable.

**KPIs (4 contenido + 1 límite)** — patrón `CardMetric`:
| # | KPI | Formato | Ancla |
|---|---|---|---|
| 1 | VM Total (DOP) | $ M/MM, 2 dec; anterior, Δ, Δ%; subtítulo **"Consolidado en DOP · TC del corte"** (regla de moneda §4; con filtro de moneda activo conmuta a "Solo instrumentos USD/DOP · …") | §7.1; F1.10 |
| 2 | N° Posiciones | entero; anterior, Δ | §7.1 |
| 3 | N° Emisores | entero; anterior, Δ | §7.1 |
| 4 | Calificación predominante | valor categórico (p.ej. "AA"); subtítulo "share XX.X% (ant. YY.Y%)"; **flecha = dirección del share del rating predominante** (↑ share sube), **color neutro siempre** (semáforo solo para límites); tooltip define la semántica | §7.1 |
| 5 | **Límite de concentración** (fija) | HHI actual vs. límite configurado; sin límite → "N/D" | shell §4 (inviolable "no métrica sin contexto de límite") |

**Rejilla 2×2**:
| Panel | Gráfico | Detalle |
|---|---|---|
| TL | **Área apilada temporal** — VM por **rating** | eje del apilado = rating (eje primario §2; *no* clase de activo como Mercado); selector de temporalidad al pie (paridad `portafolio-global.png`); eje Y en DOP MM |
| TR | **Dona de composición** | selector "Vista por": **Calificación (default)** · Emisor · Tipo de instrumento (bono / SBB / SBB con garantía / CD) · **Moneda (DOP · USD — F1.10)** · **Clasificación NIIF 9 (AC · FVOCI · FVTPL — F1.14; atributo de composición observable, misma mecánica que Moneda; la narrativa de exclusión FVTPL del ECL vive en §15, no aquí)**; participación siempre sobre **DOP consolidado**; paleta categórica neutra (la moneda no es semáforo); caso de 2 categorías aceptado explícitamente; leyenda lateral con montos (paridad `portafolio-global.png`); vista Emisor → top-7 + "Otros" |
| BL | **Barras divergentes de cambio** | Δ VM por grupo vs. corte anterior + barra "Total"; mismo selector de dimensión que TR; etiquetas Δ% sobre barra (paridad); vista Emisor → top-7 por \|Δ\| + "Otros" |
| BR | **Tabla de composición** (exportable) | filas por **rating**, expandibles **rating → emisor** (drill-down canónico §2; composición observada, no riesgo). Columnas: **VM en grupos DOP · USD · Total (DOP consolidado)** (partición de moneda v2 §4, paridad `var-global.png`) · % Global (sobre Total) · Var (DOP) · Var % — §7.1 + F1.10. Emisor con ambas monedas → chip "Mixta"; celda de grupo sin posiciones → "—"; Var/Var % sin corte anterior → "N/D", nunca 0; pie: *"Variaciones al TC de cada corte; incluyen efecto FX"* |

**Regla de moneda**: aplica la regla transversal del shell §4 (F1.10) — la anterior "excepción de paridad — moneda" (cartera 100% DOP) queda **revertida por corrección del PM** (feedback-log 2026-08-21).

**Navegación**: Inbound — sidebar "Portafolio" o breadcrumb. Outbound — tab Concentración; drill-down en tabla; Filtros (§4).

### 7.2 Tab Concentración — HHI y top-N emisores

**Purpose**: el usuario evalúa si el libro está concentrado en pocos nombres — *la* motivación del enfoque de cartera en crédito (§7.1) — y su posición frente a los límites.

**Information Hierarchy**: 1) nivel de concentración (HHI) y su tendencia · 2) quiénes concentran (top-N, mayor emisor) · 3) posición frente a límites (estado, holgura/exceso) · 4) evolución y detalle exportable.

**Paridad empírica**: espejo estructural de `portafolio-concentracion.png` (Mercado › Portafolio › Concentración Prudencial): tarjetas de mayor concentración con holgura/exceso, top-5 por emisor, evolución histórica con línea de límite, divergentes de cambio, tabla por emisor con columnas de límite.

**KPIs (4 contenido + 1 límite)**:
| # | KPI | Formato | Ancla |
|---|---|---|---|
| 1 | **HHI** | valor (0–1, 4 dec); anterior, Δ; subtítulo "≈ N emisores efectivos (1/HHI)" con tooltip explicativo | §7.1 "métricas a destacar" |
| 2 | Share Top-5 emisores | % del VM; anterior, Δ | §7.1 top-N |
| 3 | Mayor concentración | emisor + % VM; subtítulo Holgura/Exceso vs. límite | paridad `portafolio-concentracion.png` |
| 4 | Δ HHI vs. corte anterior | Δ en **puntos de HHI (4 dec)**, neutro; tooltip: "HHI al alza = mayor concentración" (sin color semántico) | derivada de §7.1 (tendencia de concentración) |
| 5 | **Estado de Límites** (fija) | conteo Alertas · Incumplimientos de límites de concentración; sin límites → "N/D" | shell §4 + paridad screenshot |

> Fuente única del dato de límite: la tarjeta fija (5). El KPI 3 referencia la misma configuración; jamás divergen (si límite N/D, la holgura del KPI 3 también es N/D).

**Rejilla 2×2**:
| Panel | Gráfico | Detalle |
|---|---|---|
| TL | **Barras horizontales top-N emisores** | top-7 + "Otros" por % VM; toggle % VM / VM DOP (paridad selector "% Patrimonio") |
| TR | **Evolución histórica de la concentración** | serie del HHI (toggle: HHI / mayor concentración %) con **línea punteada de límite** (paridad "Límite Regulatorio" del screenshot); sin límite → sin línea, nota "Límite: N/D" |
| BL | **Barras divergentes de cambio** | Δ VM de los top-7 emisores por \|Δ\| + "Otros" + Total, vs. corte anterior (paridad) |
| BR | **Tabla de concentración por emisor** (exportable) | Emisor · **Moneda** (chip: DOP / USD / "Mixta" si el emisor tiene ambas — F1.10) · VM (DOP consolidado) · % VM · aporte al HHI · Límite interno · Holgura/Exceso. Bajo filtro de moneda, la fila recalcula solo con los instrumentos de esa moneda (consolidados en DOP) y el chip conmuta a la moneda filtrada. Columnas de límite ancladas en paridad `portafolio-concentracion.png` (Límite Interno/Reg) + inviolable "no métrica sin contexto de límite"; son límites de **exposición** (VM observado), no granularidad de riesgo emisor (§2 intacto). Sin límite → "N/D". **Exenta de la regla top-7+"Otros"**: lista todos los emisores (paginada/scroll); un emisor en alerta o exceso jamás puede quedar oculto |

**Navegación**: Inbound — tab desde Global o href directo. Outbound — tab Global; Filtros.

**Formatos por columna (ambos BR)**: montos $ M/MM (nunca K) con la moneda del grupo en encabezado (DOP / USD / Total DOP — regla de moneda §4); % con 2 dec; fechas DD/MM/AAAA; ausentes "N/D" nunca cero (celda de grupo sin posiciones → "—"); cifras mono tabular; deltas en neutro (sin verde/rojo semántico — semáforo solo en Holgura/Exceso como estado de límite).

---

## 8. Sección Métricas de Riesgo — *la medida al corte y su historia* (bead librisk-a66 / F1.5; rehecha por corrección PM F1.9, bead librisk-08x)

> **Renombre (corrección PM F1.9)**: la sección se llama **Métricas de Riesgo** — la medida (VaR / ES / Std) es el *selector*, no el nombre. "VaR" sobrevive en la UI solo como **medida**: en el selector, en labels dinámicos `<Medida>`, en la card "VaR de Crédito Total" de Visión General (§11.1) y en la franja VaR/ES de Escenarios (§9.7). **Ninguna pantalla, sección ni tab se titula "VaR".** El nombre "VaR/Riesgo" del handoff §7.2 y del Brain [guia] queda sustituido por decisión del PM (feedback-log 2026-08-20 #2).

Molde dashboard §4 heredado íntegro: breadcrumb `Home > Métricas de Riesgo > <Tab>`, badge de supuesto activo + DataStatus + dataset + Filtros, tabs pill, tira 4+1 KPIs, rejilla 2×2 con BR exportable. **Con selector VaR · ES · Std** (handoff §7.2; Brain `Capa2_RI_MetodologiaCredito.md` [guia]): conmuta los datos y la etiqueta `<Medida>` en títulos, KPIs y encabezados, **nunca la estructura del layout**. La sección no contrasta la distribución contra una "empírica" (es simulada, §7.2); **sin histograma aquí** — la silueta multimodal vive en Escenarios (§9.8).

**Separación estructural por modo de análisis (corrección PM F1.9)** — dos tabs pinneados, no un toggle:

| Tab | Pregunta | Contenido |
|---|---|---|
| **A la Fecha** (default) | ¿cuánto puedo perder **al corte**, dónde se concentra y cuánta diversificación tengo? | descomposición, drill-down y concentración de la medida en el as_of; **sin columnas ni paneles de variación temporal** |
| **Histórico** | ¿cómo **evolucionó** la medida y cómo cambió la mezcla? | series temporales, cambios vs. corte anterior, cambios de mezcla |

- **Excepción declarada a la regla del shell §3** ("nunca renombrar tabs pinneados"): esa regla protegía hrefs internos entre beads; la corrección del PM la supera y este bead actualiza todos los hrefs (sidebar §2, NavCard §11.3, diagrama). Ruta: `/metricas-de-riesgo/a-la-fecha` · `/metricas-de-riesgo/historico`.
- **Deep-link manda > default**: URL con tab explícito gana; sin tab → A la Fecha. Sin persistencia de tab entre sesiones (paridad Mercado).
- **Chips de los KPIs**: ambos tabs conservan el patrón `CardMetric` completo (anterior, Δ, Δ%) — el chip es **contexto del molde §4**, no análisis histórico; la separación estructural vive en los paneles y en las columnas de las tablas (la tabla as_of no tiene columnas Var). Decisión documentada para el PM. KPIs **categóricos** (Top Driver, Rating de mayor Δ) usan la variante categórica ya precedentada (§7.1 KPI 4): "anterior: X" como categoría, sin Δ% aritmético.

**Reglas transversales de la sección**:
- Toda vista **gráfica** por emisor colapsa a **top-7 + "Otros"** (regla de §7; el "top-8 + Otros" literal del handoff §7.2 sigue registrado como desviación en `feedback-log.md`). Tablas exentas.
- **Leyenda de prorrateo** (*"Contribución prorrateada por exposición — el modelo opera a nivel rating"*, shell §4, §2 no negociable) presente en: dona TR de A la Fecha en **todas sus vistas** (Emisor y Tipo de instrumento — ambas derivan del riesgo modelado a nivel rating), BL de Histórico cuando la dimensión activa es Emisor, filas de emisor de ambas tablas BR (nota al pie incluida en el export) y **subtítulo visible** (no solo tooltip) del KPI Top Driver.
- **Uso Límite (tarjeta fija, ambos tabs): siempre visible; refleja la medida activa; sin límite configurado para esa medida → "N/D" con tooltip; jamás 0% ni oculta** (canon §4: σ→límites, VaR/ES→capital — es esperable que el límite viva en una sola medida).
- **Regla de comparabilidad de cortes** (§11, transversal): si el supuesto activo difiere del supuesto del corte anterior, **todo Δ muestra "N/D"** + tooltip *"corte anterior calculado bajo otro supuesto"*. En KPIs cuyo dato principal es un Δ (Rating de mayor Δ, Δ Razón), la **tarjeta completa** pasa a estado N/D con ese tooltip.
- **Barras sin dato**: barra **ausente** + marca "N/D" en la categoría — nunca altura cero (TL de A la Fecha, BL de Histórico, standalone-vs-contribución).
- Cifras en DOP consolidado ($ M/MM; regla de moneda §4: subtítulo del KPI 1 "Consolidado en DOP · TC del corte"; **las medidas de riesgo jamás se parten por moneda** — VaR no aditivo); Δ en neutro; semáforo solo en Uso Límite; N/D nunca cero.

### 8.1 Tab A la Fecha — el riesgo al corte: descomposición, drill-down, concentración

**Purpose**: el usuario lee la medida de riesgo del libro **a la fecha del corte**, la descompone por rating y emisor, y evalúa la diversificación — sin mezclar lectura temporal.

**Information Hierarchy**: 1) `<Medida>` Total al corte · 2) descomposición por rating (¿qué calificación conduce el riesgo?) · 3) quién lo conduce (Top Driver, dona) y diversificación (standalone vs. contribución) · 4) detalle jerárquico exportable.

**KPIs (4 contenido + 1 límite)** — patrón `CardMetric`; 1–3 y 5 conmutan con el selector:
| # | KPI | Formato | Ancla |
|---|---|---|---|
| 1 | `<Medida>` Total (DOP) | $ M/MM, 2 dec; chips (anterior, Δ, Δ%); subtítulo **"Consolidado en DOP · TC del corte"** (regla de moneda §4) | §7.2; F1.10 |
| 2 | Razón `<Medida>`/VM | % 2 dec; chips | §7.2 (paridad "% VM Global" `var-global.png`) |
| 3 | **Top Driver** | emisor + `<Medida>` del top + % contribución; **informativo, no navegable** (deferral F1.2); **subtítulo visible con la leyenda de prorrateo** (no solo tooltip); chip categórico "anterior: X" | §7.2 |
| 4 | **Beneficio de diversificación** | Σ `<Medida>` standalone − `<Medida>` cartera (DOP y % de la suma standalone), **con signo**; si negativo → label "Penalización por concentración" + tooltip *"VaR no es subaditivo"* (cambio de label por signo = dato, no layout) | Brain [guia] "brecha Σ standalone − cartera" |
| 5 | **Uso Límite** (fija) | regla de la sección (siempre visible; medida activa; N/D con tooltip) | shell §4 (inviolable) |

**Rejilla 2×2**:
| Panel | Gráfico | Detalle |
|---|---|---|
| TL | **Barras `<Medida>` por rating** | métrica × calificación al corte (§7.2 literal); orden por escala AAA→D, no por magnitud; color categórico neutro; rating sin dato → barra ausente + "N/D" |
| TR | **Dona de contribución** | selector "Vista por": **Emisor (default, §7.2 literal)** · Tipo de instrumento — la opción Calificación se **elimina** (duplicaría TL); vista Emisor → top-7 + "Otros"; **leyenda de prorrateo en ambas vistas** (ambas derivan del modelo a nivel rating); leyenda lateral con montos |
| BL | **Standalone vs. contribución por rating** | barras agrupadas: `<Medida>` standalone vs. contribución a cartera; la brecha visible = diversificación (la vista **por posición** vive en Marginal §10 — sin solapamiento) |
| BR | **Tabla de descomposición jerárquica** (exportable) | filas por **rating**, expandibles **rating → emisor** (drill-down canónico §2). Columnas: **VM en grupos DOP · USD · Total (DOP consolidado)** (partición v2 §4 — solo el VM se parte) · `<Medida>` (DOP consolidado, **nunca partida por moneda**) · `<Medida>` % del total. Emisor con ambas monedas → chip "Mixta"; celda de grupo sin posiciones → "—". **Sin columnas de variación** — viven en Histórico (separación estructural F1.9). Nota de prorrateo al pie (filas emisor), incluida en el export |

**Navegación**: Inbound — sidebar "Métricas de Riesgo", NavCard "Métricas de Riesgo" del overview (§11.3), breadcrumb, deep-link. Outbound — tab Histórico; drill-down en tabla; Filtros (§4).

### 8.2 Tab Histórico — la evolución de la medida y los cambios de mezcla

**Purpose**: el usuario lee cómo evolucionó la medida en el tiempo, qué cambió vs. el corte anterior y cómo se movió la mezcla por rating.

**Information Hierarchy**: 1) evolución temporal de la medida y su mezcla por rating · 2) qué cambió vs. el corte anterior y quién condujo el cambio · 3) evolución de la intensidad de riesgo (razón `<Medida>`/VM) · 4) detalle comparativo exportable.

**KPIs (4 contenido + 1 límite)** — 1, 2, 4 y 5 conmutan con el selector:
| # | KPI | Formato | Ancla |
|---|---|---|---|
| 1 | `<Medida>` Total (DOP) | $ M/MM; chips (anterior, Δ, Δ%) — mismo dato que A la Fecha (continuidad entre tabs); subtítulo **"Consolidado en DOP · TC del corte"** (§4; en este tab el pie de sección añade *"Cada punto consolidado al TC de su fecha"*) | §7.2; F1.10 |
| 2 | **Rating de mayor Δ** | categoría (p.ej. "BBB") + Δ `<Medida>` (DOP) de ese rating vs. corte anterior; chip categórico "anterior: X"; color neutro. Supuesto distinto en el corte anterior → tarjeta completa N/D + tooltip (regla de comparabilidad) | §7.2 cambio por grupo (derivada) |
| 3 | Volatilidad anualizada | σ de la serie histórica de **VM del libro**, anualizada **según la frecuencia real de cortes** (√252 solo si diaria), en % — **no conmuta con el selector**; tooltip: *"volatilidad descriptiva del valor del libro, no la distribución de la medida"*. Sin serie suficiente → "N/D" | §7.2 |
| 4 | **Δ Razón `<Medida>`/VM** | Δ en puntos porcentuales vs. corte anterior; separa efecto nivel de efecto tamaño del libro (no derivable de los chips del KPI 1 — requiere VM); supuesto distinto → tarjeta N/D + tooltip. Atribución formal mezcla/nivel: candidata Fase 2 | derivada §7.2 (mandato PM "cambios de mezcla") |
| 5 | **Uso Límite** (fija) | regla de la sección | shell §4 |

**Rejilla 2×2**:
| Panel | Gráfico | Detalle |
|---|---|---|
| TL | **Área apilada temporal** — `<Medida>` por **rating** | métrica × tiempo (§7.2) apilada por rating (eje primario §2; paridad `var-global.png` con rating en lugar de clase); selector de temporalidad al pie (paridad `portafolio-global.png`); eje Y en DOP MM; cima del apilado = `<Medida>` Total; **marcadores verticales de cambio de supuesto** + tooltip con el supuesto vigente en cada corte (la serie jamás se lee como continua bajo supuestos distintos, §2) |
| TR | **Evolución de la razón `<Medida>`/VM** | línea temporal de la intensidad de riesgo del libro; mismos **marcadores de cambio de supuesto** que TL; eje Y en % |
| BL | **Barras divergentes de cambio** | Δ `<Medida>` por grupo vs. corte anterior + barra "Total"; selector de dimensión: **Calificación (default)** · Emisor; vista Emisor → top-7 por \|Δ\| + "Otros" + leyenda de prorrateo; etiquetas Δ% sobre barra; grupo con Δ no comparable (cambio de supuesto) → barra ausente + "N/D" |
| BR | **Tabla comparativa jerárquica** (exportable) | filas por **rating**, expandibles **rating → emisor** (drill-down canónico §2). Columnas: **VM en grupos DOP · USD · Total (DOP consolidado)** (partición v2 §4) · `<Medida>` (DOP consolidado, nunca partida por moneda) · **Var (DOP) vs. anterior · Var %** — las columnas de variación viven aquí, no en A la Fecha. Encabezados con `<Medida>` dinámica; nota de prorrateo al pie; pies de moneda (§4): *"Variaciones al TC de cada corte; incluyen efecto FX"* y *"Cada punto consolidado al TC de su fecha"*; sin corte anterior o supuesto distinto → "N/D", nunca 0 |

**Navegación**: Inbound — tab desde A la Fecha o deep-link. Outbound — tab A la Fecha; Filtros.
---

## 9. Sección Escenarios — *estrés del libro y de los supuestos* (bead librisk-iq9 / F1.7)

Arquetipo **simulador** (shell §5, Brain [inviolable] "nunca convertir dashboard en simulador ni viceversa"): configurar → aplicar → leer. **No hereda** la tira 4+1 + rejilla 2×2 del molde dashboard §4. **Sin selector VaR·ES·Std** (handoff §5). Paridad empírica: `escenarios-impacto-riesgo.png` (Mercado › Escenarios › Impacto en Riesgo) — riel de configuración izquierdo con Aplicar/Reset, columna de tarjetas de resultado apiladas, paneles centrales, tabla ancha derecha; el MenuSidebar auto-colapsa mientras el riel está abierto (shell §2).

**Purpose**: el usuario configura un shock —del libro o de los supuestos del modelo—, lo aplica, y lee el impacto en valor y en la cola de la distribución.

**Information Hierarchy**: 1) configuración del shock (el riel — sin shock no hay lectura) · 2) impacto agregado (KPIs VM Pre/Post, G/P) · 3) forma de la cola post-shock (histograma + VaR; en barrido, la franja VaR/ES por ρ) · 4) dónde pega (divergentes por rating, waterfall) · 5) detalle exportable.

**Formatos de la sección** (los "Formatos transversales" del shell §4 aplican aquí íntegros aunque el layout sea de simulador — declaración explícita): moneda con $ M/MM (nunca K), 2 dec, unidad explícita en tarjetas, ejes del histograma/waterfall y encabezados de la tabla; DD/MM/AAAA; **N/D nunca cero**; mono tabular. **Regla de moneda (F1.10)**: en Escenarios **todo monto es DOP consolidado al TC del as_of, constante durante la simulación** (base y estresado — coherente con la ausencia de shock FX); las posiciones USD **se revalúan crediticiamente** y se consolidan a ese TC; el chip de moneda es solo etiqueta de denominación. La declaración vive como **línea fija en el riel de control** ("Consolidado en DOP · TC 61.50 del corte, constante" — 61.50 = valor del mock) y en el export. **El "Shock FX" del screenshot de Mercado NO se replica** (el estrés FX pertenece a Mercado — corrección PM F1.10; la exposición USD sí es visible y filtrable, §4).

**Regla de color de la sección (frontera explícita)**: los paneles de **P&L** (divergentes por rating, waterfall, columnas G-P de la tabla, KPI G/P Total) usan **semántica económica de signo** (ganancia/pérdida) — anclada en Capa1 `Capa1_Diseno_Principios.md` "semántica de color por dominio económico" + paridad empírica del screenshot. Las **medidas de riesgo** (VaR/ES pre/post, franja por ρ) permanecen en **neutro** (regla del shell §4: deltas de medida en neutro). Tensión shell-vs-sección registrada para el PM en `feedback-log.md`; mientras el gate no falle, gana esta regla de frontera.

### 9.1 Estructura de pantalla

```
┌──────────────────────────────────────────────────────────────────────────┐
│ Home > Escenarios > Impacto en Riesgo   [Supuesto: <2 estados, §9.2>]     │
│                                         [Datos DD/MM/AAAA] [dataset ▾]    │
├──────────────────────────────────────────────────────────────────────────┤
│ ( Impacto en Riesgo )                                    ← un pill        │
├────────────┬─────────────────────────────────────────────────────────────┤
│ RIEL DE    │  [chips ρ: 15% · 25% · 35%]  [franja VaR/ES por ρ + límite]  │← solo modo barrido
│ CONFIG     │ ┌──────────┐ ┌──────────────────────┐ ┌────────────────────┐ │
│ (persist.) │ │ KPI 1    │ │ C1 Divergentes P&L   │ │  Tabla jerárquica  │ │
│  familia   │ │ KPI 2    │ │    por rating        │ │  rating → emisor   │ │
│  de shock  │ │ KPI 3    │ ├──────────────────────┤ │  → instrumento     │ │
│  params    │ │ KPI 4    │ │ C2 Histograma post-  │ │  (exportable)      │ │
│  [Aplicar] │ │(apiladas)│ │    shock (multimodal) │ │                    │ │
│  [Reinic.] │ └──────────┘ ├──────────────────────┤ │                    │ │
│            │              │ C3 Waterfall pérdida │ │                    │ │
│            │              └──────────────────────┘ └────────────────────┘ │
└────────────┴─────────────────────────────────────────────────────────────┘
```

Área de resultados = **columna de 4 tarjetas KPI apiladas + columna central de 3 paneles (divergentes, histograma, waterfall) + tabla ancha derecha** (paridad empírica; no es la rejilla 2×2 del dashboard).

### 9.2 Badge de supuesto activo — estados por familia de shock (§2 no negociable)

El badge está presente en **todo** estado y nunca miente sobre el supuesto efectivo:

| Estado | Contenido del badge |
|---|---|
| Pre-run | `Supuesto: S&P · ρ=25% (base)` |
| Post-run, shock de **libro** | `Base: S&P · ρ=25%` + chip contiguo `Shock de libro: <resumen>` (p.ej. "PD +200bp global", "3 defaults forzados") — los supuestos del modelo **no cambian** con un shock de libro; el chip lo hace auditable |
| Post-run, **fuente de transición** | `Base: S&P · ρ=25% → Activo: Moody's · ρ=25%` (el badge refleja la fuente **efectiva**; nunca muestra "S&P" si el escenario corre con Moody's) |
| Post-run, **barrido de ρ** | `Base: S&P · ρ=25% → Barrido activo: ρ=15/25/35%` (shell §5) |
| Post-run, **recovery** | `Base: S&P · ρ=25% → Recovery: μ=X/σ=Y (<seniority>)` |
| Dataset Preparando/No listo/Error | `Supuesto: N/D` — nunca se oculta (shell §4) |

### 9.3 Riel de configuración de shock (handoff §7.4)

| Control | Tipo | Detalle |
|---|---|---|
| Familia de shock | toggle segmentado | **Libro** / **Supuesto** — las dos familias del §7.4; cambiar de familia con resultados en pantalla los **invalida** (§9.6). **Composición**: los sub-tipos de **Libro** son combinables entre sí (p.ej. PD +bp **y** 2 defaults forzados — condicionamientos acumulables de la simulación); los de **Supuesto** son **excluyentes por run** (radio: se barre/cambia UN supuesto a la vez — la sensibilidad por supuesto debe ser atribuible, §2). El chip del badge en shocks de libro lista los sub-tipos activos concatenados |
| — Libro: Subida de PD | input + alcance | magnitud en bp; alcance **global o por rating** (rating = eje primario §2; el "por emisor" del Brain queda cubierto vía defaults forzados) |
| — Libro: N defaults forzados | stepper + selector de emisores | elegir emisores concretos es legítimo: la **exposición** sí es por emisor (handoff §1); la distribución sigue siendo por rating (§2 intacto) |
| — Libro: N downgrades | stepper + notches + alcance | rebaja de *notch* (1–3), alcance global / por rating / emisores seleccionados |
| — Supuesto: Barrido de ρ | preset editable | set default {15% · 25% · 35%} (§2: espacio de UI de primera clase para barrer ρ); si el usuario edita el set, **badge, chips y franja reflejan el set efectivo**; la referencia de límite de la franja se ancla al **ρ base (25%)** si pertenece al set, si no al ρ más cercano al base (etiquetado "@ρ=X%") |
| — Supuesto: Fuente de transición | radio | S&P / Moody's |
| — Supuesto: Recovery (μ, σ) | inputs por seniority | media y dispersión de la Beta de recovery |
| Aplicar / Reiniciar | acciones | Aplicar dispara el recálculo (§9.6); Reiniciar vuelve a pre-run |

**Desviaciones de paridad documentadas** (feedback-log): el riel de Mercado tiene toggle "Impacto Económico / Impacto en Riesgo" y radio de medida VaR/CVaR — Crédito v1 **no los tiene**: un solo tab que lee P&L (valor) **y** efecto en la cola (VaR) juntos, y sin selector de medida (handoff §5). Las tarjetas empíricas "VaR Pre/Post/Delta" se sustituyen por **VM Pre/Post/G-P** (handoff §7.4, fuente vinculante > precedente).

### 9.4 KPIs post-run (4 tarjetas apiladas — §7.4)

| # | KPI | Formato | Ancla |
|---|---|---|---|
| 1 | VM Pre-Shock (DOP) | $ M/MM, 2 dec — constante ante chips de ρ (la base no depende del barrido) | §7.4 |
| 2 | VM Post-Shock (DOP) | $ M/MM; conmuta con el chip de ρ activo en modo barrido | §7.4 |
| 3 | G/P Total | Δ DOP y Δ% con semántica de signo (§9 regla de color) | §7.4 |
| 4 | Driver principal | emisor con mayor pérdida + G/P (DOP); **con la nota de granularidad §9.5** | §7.4 |

Pre-run: las 4 tarjetas se renderizan con **"N/D"** (regla shell §4 — nunca ocultas, nunca cero). **Sin tarjeta "Uso Límite"**: paridad empírica (Escenarios de Mercado no la tiene) + el G/P de escenario no es métrica con límite configurado; el **contexto de límite del VaR vive en la franja por ρ** (§9.7) — desviación del molde dashboard registrada para el PM.

### 9.5 Nota de granularidad (§2 no negociable — excepción declarada a la leyenda de prorrateo)

Las cifras por emisor/instrumento de esta sección (waterfall, tabla, Driver principal) **no son prorrateo**: son salidas directas de la revaluación por posición. La leyenda de prorrateo del shell §4 **no aplica literal**; en su lugar, la sección lleva una **nota fija de granularidad** visible en el pie del área de resultados (no solo tooltip): *"En shocks por rating, los emisores de una misma calificación comparten distribución — las diferencias por emisor provienen de su exposición y realización simulada"*. Aparece también como nota al pie de la tabla exportable (incluida en el export) y en el tooltip del KPI Driver principal. Así la pantalla no promete granularidad emisor-específica que el modelo no tiene (§2).

### 9.6 Ciclo de estados del simulador (extiende §6)

- **Pre-run**: paneles con estado vacío e instrucción ("Configura un shock y pulsa Aplicar"); KPIs en N/D; badge en estado base.
- **Recalculando** (tras Aplicar): `component_refreshing` — skeletons **por panel** del área de resultados; el riel y los badges permanecen interactivos/visibles; sin overlay completo.
- **Post-run**: resultados + badge en estado post-run (§9.2).
- **Cambio de configuración post-run** (incluye cambiar de familia): los resultados se marcan **obsoletos** (banner "Configuración modificada — Aplicar para recalcular", resultados atenuados); nunca se limpian en silencio.
- **Fallo del recálculo**: estado de error del área de resultados con acción Reintentar; el badge de dataset/as_of no se toca (el fallo es del run, no del corte de datos).

### 9.7 Modo barrido de ρ (solo familia Supuesto → Barrido)

- **Chips ρ = 15% · 25% · 35%** sobre el área de resultados (visibles **solo** post-run de un barrido): conmutan el escenario mostrado en KPIs, paneles y tabla — mismo layout, distintos datos.
- **Franja comparativa fija** (no conmuta): VaR y ES por cada ρ, lado a lado, en neutro; incluye la **referencia de límite de VaR** si está configurada ("Límite: $X — uso YY% @ρ=25%"), si no → "Límite: N/D" (restituye el contexto de límite del inviolable del shell en la única métrica con límite de la pantalla).
- **Toggle "Comparar"** en el histograma: superpone las 3 siluetas post-shock en outline (+ base). Lectura clave: cómo ρ **engorda la cola** — el VM medio apenas se mueve; por eso la franja VaR/ES, no el G/P, es la lectura principal del barrido (nota corta en la UI).

### 9.8 Paneles de resultados

| Panel | Gráfico | Detalle |
|---|---|---|
| Central-1 | **Barras divergentes P&L por rating** | (shock − base) por rating (eje primario §2) + barra "Total"; semántica de signo; etiquetas Δ% (paridad divergentes del molde) |
| Central-2 | **Histograma post-shock** | distribución de **valores del portafolio** chocado: silueta **asimétrica a la izquierda y multimodal** (jorobas = escenarios con 0/1/2/3… defaults — handoff §4, Brain [inviolable]: **nunca campana de Gauss**); **línea de VaR** al percentil de la metodología oficial (sin selector local); overlay opcional de la base en outline; **zoom multinivel cuerpo/banda/cola** (§9 catálogo: la cola vive ~200× más abajo que el cuerpo); eje X en DOP MM |
| Central-3 | **Waterfall de pérdida** | descomposición aditiva del G/P por instrumento: top-7 por \|G/P\| + "Otros" + Total (regla top-7+Otros de §7/§8); semántica de signo; nota de granularidad §9.5 al pie |
| Derecha | **Tabla jerárquica de impacto** (exportable) | filas por **rating**, expandibles **rating → emisor → instrumento** (drill-down canónico §2; corrige la lectura plana "por instrumento" del handoff §7.4 manteniendo su granularidad en el nivel hoja — paridad con la tabla empírica "por Emisor e Instrumento" del screenshot). Columnas: **Moneda** (chip en nivel instrumento: DOP/USD; nivel emisor "Mixta" si aplica — F1.10) · VM Pre (DOP consolidado) · VM Post (DOP consolidado) · G-P (DOP consolidado) · G-P % — G/P jamás partido por moneda (partición v2 §4); TC constante del as_of declarado en el riel. **Exenta de top-7+Otros** (lista completo). Sin corte/valor → "N/D". Nota §9.5 al pie, incluida en el export |

**Navegación**: Inbound — sidebar "Escenarios" (`/escenarios/impacto-en-riesgo`) o breadcrumb. Outbound — riel (reconfigurar); breadcrumb Home. Sin panel de Filtros del shell §4: en el simulador el riel **es** el contexto (paridad empírica: el screenshot no muestra el botón Filtros en Escenarios); registrado para PM.

---

## 10. Sección Marginal — *contribución por posición* (bead librisk-mvx / F1.6)

Molde dashboard §4 heredado íntegro: breadcrumb `Home > Marginal > Global`, **badge de supuesto activo** explícito (presente en todo estado; contenido fuente de transición · método de correlación · ρ, p.ej. "S&P · ρ=25% axiomático"; estados N/D del shell §4 — nunca se oculta, §2 no negociable), DataStatus + dataset + Filtros, barra de tabs con **un pill** ("Global", shell §3), tira 4+1 KPIs, rejilla 2×2 con BR exportable. **Con selector VaR · ES · Std** (handoff §5/§7.3; Brain `Capa2_RI_MetodologiaCredito.md` [guia]): conmuta datos y etiqueta `<Medida>`, **nunca el layout**.

**Pregunta de la sección (§7.3)**: ¿qué posición **añade** más riesgo al portafolio en el margen (no en aislamiento)?

**Las tres métricas de la sección (glosario único — tooltip "ⓘ Definiciones" en el encabezado de la sección, mismo texto en tooltips de KPIs y encabezados de columna):**
| Métrica | Definición | Propiedad | Dónde se usa |
|---|---|---|---|
| **Marginal** | riesgo(cartera) − riesgo(cartera sin la posición) — leave-one-out (§7.3) | **no aditiva** (Σ marginales ≠ riesgo total) | scatter TL (eje Y), KPI 1, KPI 3, BL, columna BR |
| **Contribución (componental)** | descomposición Euler de la medida: **Σ componentales = `<Medida>` total** | aditiva | dona TR, "% del total", HHI (KPI 4), KPI 2, columna BR |
| **Standalone** | riesgo de la posición en aislamiento; brecha vs. su contribución = **beneficio de diversificación** | — | columna BR (la vista por **rating** vive en Métricas de Riesgo §8.1, panel BL — frontera sin solapamiento) |

Ancla de la separación marginal/componental: paridad empírica `var-marginal.png` (columnas "VaR Marginal $" y "VaR Componental" coexisten en la tabla de Mercado) + Brain [guia] "σ standalone y marginal, VaR/ES marginal · contribución por dimensión".

**Granularidad (§2 no negociable — misma solución que Escenarios §9.5)**: las cifras por posición de esta sección (marginal, componental, standalone) son **salidas directas de la revaluación por escenario, no prorrateo** → la leyenda de prorrateo del shell §4 **no aplica**; en su lugar, **nota fija de granularidad** al pie del scatter TL y de la tabla BR (incluida en el export) y en el tooltip del KPI 2: *"En el modelo, los emisores de una misma calificación comparten distribución — las diferencias por posición provienen de su exposición y de la realización simulada de su escenario"*. La pantalla no promete granularidad emisor-específica que el modelo no tiene.

### 10.1 Tab Global — ¿qué posición añade más riesgo en el margen?

**Purpose**: el usuario identifica las posiciones que conducen el riesgo del portafolio, las lee por cuadrantes tamaño-vs-riesgo, y evalúa concentración de contribuciones y beneficio de diversificación.

**Information Hierarchy**: 1) el mapa iso-risk (¿quién vive en el cuadrante C?) · 2) magnitud y concentración de contribuciones (KPIs, dona) · 3) ranking con signo (¿quién añade, quién diversifica?) · 4) detalle exportable por posición.

**KPIs (4 contenido + 1 límite)** — patrón `CardMetric`; 1–5 conmutan con el selector:
| # | KPI | Formato | Ancla |
|---|---|---|---|
| 1 | **Marginal promedio** | media aritmética **con signo** (incluye negativos) del `<Medida>` marginal por posición; $ M/MM, 2 dec; anterior, Δ, Δ%; subtítulo **"Consolidado en DOP · TC del corte"** (§4, F1.10); tooltip con la definición leave-one-out | §7.3 |
| 2 | **Mayor contribución** | posición (instrumento + emisor) con mayor **contribución componental** + monto (DOP) + **% del total** (válido: la componental es aditiva); **informativo, no navegable** (coherencia con Top Driver de Métricas de Riesgo — deferral F1.2); tooltip con la nota de granularidad | §7.3 |
| 3 | **Posiciones sobre umbral** | conteo de posiciones que exceden el **límite de riesgo absoluto (hipérbola)** — fijado a ese límite, **independiente de la interacción del scatter**; sin hipérbola configurada → "N/D" **aunque existan los límites h/v** (no se sustituye el umbral en silencio; subtítulo "Límite de riesgo absoluto: N/D"); **sin semáforo** (el semáforo solo vive en Uso Límite) | §7.3 |
| 4 | **Concentración HHI de contribuciones** | HHI (0–1, 4 dec) sobre los pesos de contribución componental **positivos, renormalizados a suma 1**; subtítulo "≈ N posiciones efectivas (1/HHI)"; tooltip: "sobre contribuciones positivas" | §7.3 |
| 5 | **Uso Límite** (fija) | uso de la **medida activa** vs. su límite; conmuta con el selector; sin límite → "N/D" | shell §4 (inviolable "no métrica sin contexto de límite") |

**Rejilla 2×2**:
| Panel | Gráfico | Detalle |
|---|---|---|
| TL | **Scatter iso-risk "riesgo-vs-tamaño"** | Cada punto = **instrumento** (posición). Eje X = VM de la posición (DOP MM); **eje Y ≡ `<Medida>` marginal de la posición / VM de la posición (%)** — así X·Y = marginal en DOP y la hipérbola es una curva de nivel de riesgo absoluto geométricamente correcta. **Cuadrantes anotados** (CMTD §12.1, §7.3): **A** inferior-derecha = mayor tamaño absoluto ("un default pega fuerte en DOP") · **B** superior-izquierda = mayor % de riesgo · **C** superior-derecha (**recomendado**) = mayor riesgo absoluto — anotación fija *"fallen angels viven aquí"* (exposición dimensionada con rating alto, luego degradada). **3 overlays de límite** con entrada de leyenda **siempre presente** (layout estable ante el selector): línea **horizontal** (límite %-riesgo ≈ piso de rating) · línea **vertical** (límite de tamaño de exposición) · **hipérbola iso-risk** (límite de riesgo absoluto — **la recomendada**; etiqueta conmutada: "topea el `<Medida>` total del portafolio"); límite no configurado → línea ausente + leyenda "Límite: N/D". Color de punto por **rating agrupado a letra** (AAA/AA/A/BBB/BB/B/CCC–D — 7 ≤ máx 8; categórico neutro, jamás semáforo). Tooltip por punto: instrumento · emisor · **moneda del instrumento** (F1.10) · **rating actual** (sin insinuar migración detectada — el modelo no rastrea historial) · VM · marginal % · marginal DOP. **Fuera del alcance de la regla top-7+"Otros"** (esa regla gobierna vistas por emisor; aquí el colapso destruiría la lectura por cuadrantes); mitigación de sobreplot: opacidad 0.7 + zoom/brush. **Marginales negativos** (posiciones diversificadoras): se renderizan bajo el eje X (Y<0) con la línea Y=0 marcada; los cuadrantes A/B/C y la hipérbola solo anotan el semiplano Y>0 — la lectura de diversificadoras vive en BL. Nota de granularidad al pie |
| TR | **Dona de contribución (componental)** | título "Contribución (componental)" — terminología declarada en la UI; selector "Vista por": **Emisor (default)** · Calificación · Tipo de instrumento (alineado con la dona de Métricas de Riesgo §8.1 — que en A la Fecha omite Calificación por duplicar su TL; aquí Calificación se mantiene: el TL de Marginal es el scatter, no barras por rating); vista Emisor → top-7 + "Otros"; **solo contribuciones positivas** (una dona no representa negativos); posiciones con componental negativo agrupadas fuera de la dona en **nota fija**: "Diversificadoras: N posiciones, neto −$X"; leyenda lateral con montos |
| BL | **Barras divergentes ranking** | top-7 posiciones por \|`<Medida>` marginal\| + "Otros", **mostrando signo** (recupera la lectura "Mayor Aumento / Mayor Reducción" de Mercado `var-marginal.png`); "Otros" partido por signo: **"Otros (+)" y "Otros (−)"** separados (un neto ocultaría magnitudes de ambos signos) | 
| BR | **Tabla por posición** (exportable) | jerárquica **rating → emisor → instrumento** (drill-down canónico §2; "por posición" del §7.3 preservado en el nivel hoja — paridad tabla jerárquica de `var-marginal.png`). Columnas: **Moneda** (chip en nivel instrumento; "Mixta" en nivel emisor si aplica — F1.10) · VM (DOP consolidado) · `<Medida>` **Marginal** (DOP) · **Contribución componental** (DOP) · % del total (base componental) · **Standalone** (DOP) · Beneficio diversificación (standalone − componental) · **Var Marginal (DOP)** y **Var %** vs. corte anterior (los Δ refieren al Marginal — declarado en encabezado y export; pie §4: *"Variaciones al TC de cada corte; incluyen efecto FX"*). Las medidas de riesgo jamás se parten por moneda (partición v2 §4). **Exenta de top-7+"Otros"** (lista completo). Sin corte/valor → "N/D". Nota de granularidad al pie, incluida en el export |

**Desviación de paridad documentada** (feedback-log): la tira empírica de Mercado (VaR Marginal Total · Mayor Aumento · Mayor Reducción · % VaR Explicable · Concentración Marginal) se sustituye por los 4 KPIs del handoff §7.3 (fuente vinculante > precedente); las lecturas Aumento/Reducción se recuperan en BL (divergentes con signo). El **scatter iso-risk no existe en Mercado** — es aporte propio de Crédito (handoff §7.3 + Brain [guia]), ocupa TL como panel principal.

**Navegación**: Inbound — sidebar "Marginal" (`/marginal/global`) o breadcrumb. Outbound — drill-down en tabla BR; Filtros (§4); breadcrumb Home.

---

## 11. Sección Visión General — *overview ejecutivo de riesgo de crédito* (bead librisk-dbv / F1.8, corrección PM)

Arquetipo **overview** — paridad estructural con `vision-general.png` de Mercado (grid-cols-12: fila de 4 cards resumen → fila media de tabla de límites + 2 paneles → fila de 5 card_small). **No hereda** la tira 4+1 + rejilla 2×2 del molde dashboard §4 ni el riel del simulador §5. Es la **entrada default del módulo** (shell §1). **Sin barra de tabs** (excepción overview, shell §3) y **sin selector VaR·ES·Std** (solo Métricas de Riesgo y Marginal, shell §4): las cifras de riesgo del overview se muestran en la **medida canónica VaR**, con percentil y horizonte etiquetados.

**Purpose**: el CRO/Analista lee en un vistazo el estado del libro y del riesgo de crédito, la posición frente a límites, y salta a la sección donde profundizar.

**Information Hierarchy**: 1) resumen del libro y VaR total con su estado de límite · 2) estado de límites configurados (tabla) · 3) quién conduce el riesgo y qué cambió vs. el corte anterior · 4) puertas de entrada a las 4 secciones de análisis.

**Cabecera**: breadcrumb `Home > Visión general` · derecha: **badge de supuesto activo** ("S&P · ρ=25% axiomático"; reglas de estado del shell §4 — dataset Preparando/No listo/Error → "Supuesto: N/D", **nunca oculto**; durante skeletons por panel no cambia; al cambiar dataset muestra N/D hasta ready y luego el supuesto del dataset entrante) · badge as_of `DataStatus` + selector de dataset. Sin botón Filtros (paridad empírica: el overview de Mercado no lo muestra; el overview es lectura fija, el recorte vive en las secciones).

**Reglas transversales de la pantalla**:
- **Moneda (F1.10)**: toda cifra en **DOP consolidado** ($ M/MM, nunca K; regla de moneda §4); el portador de la declaración en esta pantalla es el **subtítulo de la card Portafolio** ("Consolidado en DOP · TC del corte"). El **badge de supuesto** de la cabecera incluye el TC (§4).
- **Color**: todos los Δ y métricas de riesgo en **neutro**; semáforo solo en pills de estado de límite (regla shell §4 — desviación deliberada del rojo/verde de signo visible en `vision-general.png`; registrada para ratificación del PM).
- **Comparabilidad de cortes**: si el supuesto activo difiere del supuesto del corte anterior, **todos los Δ vs. corte anterior de la pantalla** muestran "N/D" + tooltip *"corte anterior calculado bajo otro supuesto (\<detalle\>)"* — un Δ jamás mezcla efecto de cartera con efecto metodológico (§2 auditable).
- N/D nunca cero; DD/MM/AAAA; mono tabular.

### 11.1 Fila 1 — 4 cards resumen

**Desviación de paridad declarada**: las cards 2–3 de Mercado (Renta Fija DOP / USD) se sustituyen — Crédito no recorta por clase de activo; su primer recorte es el **rating (eje primario §2)** y el tipo de instrumento. La visibilidad de la exposición USD (F1.10) se resuelve **dentro de la card Portafolio** (fila "Exposición USD"), sin romper el molde de 4 cards ni el eje rating.

| # | Card | Contenido | Ancla |
|---|---|---|---|
| 1 | **Portafolio** | VM Total (DOP) grande, subtítulo "Consolidado en DOP · TC del corte" (§4) + filas: N Posiciones · N Emisores · Calificación predominante (mayor share de **VM**, §7.1 KPI 4) con share % · **"Exposición USD: X MM DOP eq. (Y% del portafolio)"** (F1.10) | paridad card "Portafolio" + §7.1 + F1.10 |
| 2 | **Composición por Calificación** | 7 filas fijas por rating agrupado a letra (AAA/AA/A/BBB/BB/B/CCC–D — misma agrupación que el scatter §10.1; ≤8, sin "Otros"): VM (DOP) \| % | §2 rating eje primario |
| 3 | **Exposición por Tipo de Instrumento** | filas por tipo → VM (DOP) \| %. Dominio **autoritativo de la capa de datos** (hoy: bono / SBB / SBB con garantía / CD); si el dominio creciera >8 → top-7 + "Otros" | handoff §2; shell §4 dominios |
| 4 | **VaR de Crédito Total — 99% · 1 año** | percentil y horizonte de la metodología oficial visibles en el título (paridad "95%, 1D" de Mercado; ancla: handoff §1 horizonte típico 1 año y §4 percentil p.ej. 1% ⇒ confianza 99% — valores del mock, la metodología oficial del tenant gobierna). Filas: $ (DOP) · % VM · % Patrimonio (N/D si patrimonio no configurado) · chip Δ% vs corte anterior (**neutro**) · **pill de estado de límite** (Ok/Advertencia/Incumplimiento); sin límite configurado → sin pill + "Límite: N/D" | paridad card "VaR Total" + inviolable contexto de límite |

### 11.2 Fila media — límites y lectura del riesgo

| Panel | Componente | Detalle |
|---|---|---|
| Izquierda (ancho) | **Tabla "Límites y Métricas"** | columnas **Métrica · Valor · Límite Interno · Límite Regulatorio · Uso · Estado** (paridad literal de columnas con Mercado; regulatorio sin valor → N/D). Filas = límites de crédito configurados (VaR total, concentración HHI / mayor emisor, riesgo absoluto marginal). Sin límites → estado vacío "Sin límites configurados" (N/D, nunca fila en cero). Semáforo solo en columna Estado |
| Centro | **Top Drivers del VaR — contribución prorrateada por emisor** | barras horizontales top-5 emisores con montos (DOP); **leyenda fija visible al pie** (no tooltip): *"Contribución prorrateada por exposición — el modelo opera a nivel rating"* (§2 no negociable); el subtítulo del panel declara la lectura: ranking de exposición ponderada por el riesgo de su rating |
| Derecha | **Variación vs corte anterior** | barras divergentes **Δ VaR por rating** + barra "Total" (eje primario §2 — no por emisor, a diferencia de Mercado); barras en Δ DOP (MM), etiquetas Δ% sobre barra (mismo patrón que los BL divergentes §7/§8), **en neutro**; grupo sin corte anterior → sin barra + marca "N/D" en la categoría |

**Exención de contexto de límite (declarada)**: Top Drivers y Variación son **descomposiciones** del VaR Total; su contexto de límite está presente en la misma pantalla (pill de la card 4 + fila VaR de la tabla de límites) — mismo patrón que las rejillas 2×2 de las secciones (el límite vive en el KPI, no en cada gráfico).

### 11.3 Fila inferior — card_small de navegación (NavCard, una por sección activa)

Mandato del bead: **mini-vistas hacia las demás secciones**. Componente **NavCard**, distinto de `CardMetric`: dato distintivo + pie con affordance **"Ir a \<Sección\> →"** (chevron) + elevación al hover. **Desviación de paridad declarada**: en `vision-general.png` las card_small de Mercado son informativas (VaR Tasas/RV/FX, Concentración, MtM); aquí son navegables por mandato del bead — registrada para el PM. El deferral F1.2 (KPIs de la tira no navegables) queda **intacto**: estas no son la tira KPI del molde §4. **Regla anti-duplicación**: una card_small nunca repite una cifra ya mostrada en filas 1–2. **La fila crece con las secciones activas** (F1.11–F1.15: **9 NavCards**) — desviación del conteo de 5 card_small de Mercado registrada en feedback-log.

| # | NavCard | Dato distintivo | Destino |
|---|---|---|---|
| 1 | Portafolio | Δ VM vs corte anterior (Δ DOP, Δ%) — la fila 1 muestra el nivel, no el cambio | `/portafolio/global` |
| 2 | Concentración | HHI + pill estado de límite; sin límite → sin pill + "Límite: N/D" | `/portafolio/concentracion` |
| 3 | Métricas de Riesgo | **Rating de mayor aporte** + su VaR (DOP), rotulado "VaR total del rating, DOP" — legible en el TL de A la Fecha §8.1; contexto de límite: exención §11.2 (el límite del VaR vive en la card 4 y la tabla de límites de esta misma pantalla) | `/metricas-de-riesgo/a-la-fecha` |
| 4 | Marginal | **Mayor contribución (componental)** — espeja el KPI 2 de §10.1 (salida directa por posición, no prorrateo); subtítulo "por posición, no emisor-específico" + tooltip con la nota de granularidad §10 | `/marginal/global` |
| 5 | Escenarios | contenido fijo *"Simulador de estrés — configura un shock y aplícalo"*; **sin estado de último run** (los escenarios son efímeros por sesión; no se persisten ni se muestran como dato institucional) | `/escenarios/impacto-en-riesgo` |
| 6 | Factores de Riesgo | **Factor dominante** + % de contribución al VaR (base Euler — espeja el KPI 2 de §12; no repetido en filas 1–2: regla anti-duplicación intacta); chip categórico bajo la regla de comparabilidad (§12) | `/factores-de-riesgo/mapa-de-factores` |
| 7 | Sensibilidades | **Supuesto más influyente** + su ΔVaR máx (DOP) — espeja el KPI 2 de §13 (regla anti-duplicación intacta: no aparece en filas 1–2); chip categórico "anterior: X" → "anterior: N/D" bajo supuesto distinto (regla de comparabilidad, hereda §13) | `/sensibilidades/supuestos` |
| 8 | Backtesting | **"Excepciones: X en N cortes" + veredicto Kupiec como TEXTO, sin pill de color** (regla de interfaz [inviolable] §14: el veredicto estadístico jamás comparte el componente visual de los pills de límite de las demás NavCards); ventana insuficiente → "Kupiec: N/D — ventana incompleta (N/250)" | `/backtesting/resumen-excepciones` |
| 9 | Deterioro (NIIF 9) | **Provisión ECL total — NIIF 9** (DOP) + chip Δ vs corte anterior (impacto, neutro — hereda la regla de comparabilidad extendida a escenarios §15.3: badge de Deterioro distinto → "Δ: N/D"); regla anti-duplicación intacta (la provisión no aparece en filas 1–2 — el ECL es cifra contable, no la medida VaR de la card 4) | `/deterioro/staging` |

**Terminología**: en esta pantalla "contribución prorrateada" (Top Drivers) y "contribución (componental)" (NavCard Marginal) son cosas distintas y así se rotulan — componental queda reservado a Marginal (Euler por posición; confirmación PM pendiente, feedback-log F1.6 #1).

**Sin histograma de distribución** en el overview: la silueta (asimétrica/multimodal, jamás campana de Gauss) vive en Escenarios §9.8.

**Estados**: hereda §6 (overlay solo al arranque del módulo — que ahora ocurre aquí—, luego skeletons por panel); pre-datos todas las cifras "N/D", badges nunca ocultos.

**Navegación**: Inbound — entrada al módulo (default), sidebar "Visión General", breadcrumb Home. Outbound — 9 NavCards hacia las secciones; sidebar.

---

## 12. Sección Factores de Riesgo — *el desglose del VaR por factor crediticio y el mecanismo del modelo* (bead librisk-6rq / F1.11, ampliación PM)

Molde dashboard §4 heredado íntegro: breadcrumb `Home > Factores de Riesgo > Mapa de Factores`, **badge de supuesto activo** (contenido y estados del shell §4 — nunca se oculta, §2 no negociable), DataStatus + dataset + Filtros, barra de tabs con **un pill** ("Mapa de Factores", shell §3), tira 4+1 KPIs, rejilla 2×2 con BR exportable. **Sin selector VaR·ES·Std** (solo Métricas de Riesgo y Marginal, handoff §5): el desglose opera sobre la **medida canónica VaR — 99% · 1 año**, etiquetada en el **título del KPI 1** y en el **encabezado de la tabla BR** (mismo patrón que la card 4 de Visión General §11.1); los títulos de paneles usan "VaR" literal, sin `<Medida>` dinámica.

**Pregunta de la sección (handoff §8)**: ¿qué factor crediticio —migración, default, correlación, recovery, spread— conduce el VaR, y cómo funciona el mecanismo que lo genera?

**Convención de atribución (regla de la sección — declarada en UI y export)**: la sección usa **dos convenciones rotuladas, nunca mezcladas**:
- **Atribución Euler (aditiva)** — migración (non-default) · default · recovery · spread: Σ de las 4 barras = VaR total.
- **Efecto correlación (incremental, no aditivo)** — VaR(ρ activo) − VaR(ρ=0), por método de diferencias: la correlación es la **estructura** que acopla los factores, no un sumando Euler. Vive como overlay del TL + KPI 3 + heatmap BL; jamás como barra dentro de la suma.
Nota metodológica fija al pie del TL (incluida en el export) declara ambas convenciones. Así el "factor correlación" del handoff §8 queda cubierto sin prometer una aditividad matemáticamente falsa.

**Reglas transversales de la sección**:
- Sin vistas por **emisor** → la leyenda de prorrateo del shell §4 **no aplica** aquí (el drill es factor → rating; §2 intacto: rating eje primario, ninguna granularidad emisor prometida).
- **Comparabilidad de cortes** (§11): todo Δ → "N/D" + tooltip si el supuesto del corte anterior difiere; **extendida a chips categóricos**: "anterior: X" → "anterior: N/D" + tooltip bajo supuesto distinto (un factor dominante calculado bajo otro ρ no es comparable).
- Cifras en **DOP consolidado** ($ M/MM; subtítulo del KPI 1 "Consolidado en DOP · TC del corte", §4); **las medidas de riesgo jamás se parten por moneda** — *desviación de paridad declarada*: la tabla breakdown de Mercado (`factores-mapa.png`) parte el VaR en grupos DOP/USD; en Crédito la regla F1.10 (medida jamás partida) prevalece sobre el precedente — tabla BR íntegra en DOP consolidado.
- Riesgo en **neutro**; semáforo solo en Uso Límite; N/D nunca cero; barra sin dato → ausente + "N/D".

**KPIs (4 contenido + 1 límite)** — patrón `CardMetric`:
| # | KPI | Formato | Ancla |
|---|---|---|---|
| 1 | **VaR de Crédito Total — 99% · 1 año** (DOP) | $ M/MM, 2 dec; chips (anterior, Δ, Δ%); subtítulo "Consolidado en DOP · TC del corte" (§4). Mismo dato que Métricas de Riesgo y Visión General (coherencia entre secciones) | §8; paridad "VaR Global" `factores-mapa.png` |
| 2 | **Factor dominante** | categoría (p.ej. "Default") + % de contribución al VaR (base Euler); chip categórico "anterior: X" (→ "anterior: N/D" bajo supuesto distinto); color neutro | paridad "Factor Dominante" `factores-mapa.png`; §8 |
| 3 | **Efecto correlación** | VaR(ρ activo) − VaR(ρ=0) en DOP y % del VaR; tooltip con la convención incremental ("método de diferencias — no aditivo con las barras Euler"); comparabilidad de cortes aplica | §2 no negociable (sensibilidad a ρ = entregable de primera clase); convención de la sección |
| 4 | **Probabilidad de ≥1 default** | % con 1 decimal (100% se muestra tal cual); leída de los escenarios simulados; tooltip con referencia cruzada al TR ("la cola de default sombreada es su mecanismo"); supuesto distinto en corte anterior → **tarjeta completa N/D** + tooltip | handoff §3 nota visual ("el riesgo lo conduce el conteo de defaults") + §4 (jorobas = N defaults) |
| 5 | **Uso Límite** (fija) | uso del **VaR** vs. su límite; sin límite → "N/D" con tooltip; jamás 0% ni oculta | shell §4 (inviolable "no métrica sin contexto de límite") |

**Rejilla 2×2**:
| Panel | Gráfico | Detalle |
|---|---|---|
| TL | **Barras de contribución por factor (atribución Euler)** | 4 barras aditivas: **migración (non-default) · default · recovery · spread**, en DOP; leyenda "Atribución Euler — Σ barras = VaR total"; **overlay/anotación "Efecto correlación: +$X (incremental, no aditivo)"** visualmente separado de las barras (línea/marcador anotado, no barra); color categórico neutro; barra sin dato → ausente + "N/D" y la leyenda conmuta a **"Atribución parcial — residual no atribuido: $X"** (residual = VaR − Σ barras visibles; jamás se afirma Σ=VaR con datos incompletos); nota metodológica fija al pie (ambas convenciones), incluida en el export | 
| TR | **Umbrales de Merton — variable latente del modelo** | densidad normal estándar del **retorno de activo estandarizado** con las **fronteras Z** del rating de partida: bandas de llegada etiquetadas (AAA…CCC, D) y **cola de default sombreada** (banda inferior). **Selector de rating de partida**: 7 letras AAA·AA·A·BBB·BB·B·CCC — **D excluido** (estado absorbente, sin migración de salida); default del selector = **calificación predominante por share de VM** (misma definición que §7.1 KPI 4); si el grupo predominante es CCC–D → CCC. **Subtítulo fijo del panel** (no footnote; incluido en export/captura): *"Retorno de activo estandarizado bajo Alt 2 — no es la distribución de valor del portafolio"* — la silueta multimodal del valor vive solo en Escenarios §9.8 (inviolable "nunca campana de Gauss" para la distribución de valor: esta curva es legítimamente normal porque es la variable latente, y el subtítulo bloquea la lectura errónea) | 
| BL | **Heatmap de la matriz ρ asumida** | matriz rating × rating (7×7, letras AAA…CCC–D); valor numérico en celda; escala de color **secuencial neutra** (jamás semáforo — la correlación no es estado de límite); **anotación fija**: *"Matriz uniforme — ρ=25% axiomático (Alt 2)"* cuando el método activo es ρ axiomático (el mock muestra este estado). **Estado alternativo definido** (Alt 1 — cópula empírica): la matriz muestra la co-migración empírica por par de ratings (no uniforme) y la anotación conmuta a *"Co-migración empírica (Alt 1)"*. Función del panel: **auditar el supuesto** — uniforme ⇒ axiomático vigente; no uniforme ⇒ empírico activo (§2: el tablero es auditable; tangibiliza el supuesto, handoff §8) | 
| BR | **Tabla breakdown por factor** (exportable) | encabezado "Contribución al VaR — 99% · 1 año (DOP consolidado)"; filas por **factor** (migración · default · recovery · spread + fila separada **"Efecto correlación"** fuera del subtotal, rotulada "incremental"), expandibles **factor → rating** (rating = eje primario §2 dentro de cada factor). Columnas: Contribución (DOP consolidado, **jamás partida por moneda** — F1.10) · % del VaR · Var (DOP) vs. anterior · Var %. Fila "Total (Σ Euler)" = VaR total. Comparabilidad de cortes: Var/Var % → "N/D" bajo supuesto distinto, nunca 0. Pies (regla §4, F1.10): *"Variaciones al TC de cada corte; incluyen efecto FX"* + la convención de atribución (Euler vs. incremental); ambos incluidos en el export |

**Desviación de paridad declarada — sin evolución temporal por factor** (feedback-log): la pantalla espejo de Mercado (`factores-mapa.png`) incluye "Evolución del VaR por Factor" y "Cambio en la Composición"; aquí los 3 gráficos mandatados por el handoff §8 (fuente vinculante) + la tabla BR ocupan la rejilla 2×2. La lectura temporal de la medida vive en **Métricas de Riesgo › Histórico** (§8.2 TL: área apilada con marcadores de cambio de supuesto — dependencia satisfecha); una serie temporal por factor nacería mayormente "N/D" bajo la regla de comparabilidad cada vez que el supuesto cambie. Candidato futuro: tab "Histórico por Factor" (los beads pueden añadir tabs, shell §3).

**Navegación**: Inbound — sidebar "Factores de Riesgo" (`/factores-de-riesgo/mapa-de-factores`) o breadcrumb. Outbound — drill-down factor → rating en tabla BR; Filtros (§4); breadcrumb Home.

---

## 13. Sección Sensibilidades — *sensibilidad paramétrica del VaR a los supuestos del modelo* (bead librisk-yct / F1.12, ampliación PM)

Molde dashboard §4 heredado íntegro: breadcrumb `Home > Sensibilidades > Supuestos`, **badge de supuesto activo** (contenido y estados del shell §4 — nunca se oculta, §2 no negociable), DataStatus + dataset + Filtros, barra de tabs con **un pill** ("Supuestos", shell §3), tira 4+1 KPIs, rejilla 2×2 con BR exportable. **Sin selector VaR·ES·Std** (solo Métricas de Riesgo y Marginal, handoff §5): opera sobre la medida canónica **VaR — 99% · 1 año**, etiquetada en el **título del KPI 1**, en los **títulos de paneles** ("… impacto en el VaR 99%·1a") y en el **encabezado de la tabla BR** (mismo patrón que Factores §12).

**Pregunta de la sección (handoff §8)**: ¿cuánto se mueve el VaR si cambian los supuestos del modelo — ρ, recovery (μ,σ) por seniority, fuente de transición? **Desviación declarada**: el handoff §8 dice recovery "(μ,σ) por rating"; esta sección usa **por seniority** — ancla metodológica del propio handoff §3 ("distribución Beta por seniority (μ,σ)") y coherencia con el riel de Escenarios §9.3 (registrada en feedback-log). La sensibilidad más **defendible** en crédito es la paramétrica a los supuestos (§2: entregable de primera clase). **CS01 / spread duration = extensión futura declarada, NO en el mock v1** (sin greeks por posición; candidato: tab "CS01 / Spread" cuando existan — los beads pueden añadir tabs, shell §3). No aparece en la UI v1.

**Information Hierarchy**: 1) ¿qué supuesto mueve más el VaR? (tornado, KPI 2) · 2) ¿cuánto pesa ρ y cruza el límite? (curva VaR vs ρ, KPIs 3–4) · 3) ¿dónde pega dentro del libro? (Δ contribución por rating) · 4) detalle exportable por barrido.

**Frontera Escenarios/Sensibilidades (declarada — sin solapamiento)**:
| | **Sensibilidades (§13)** | **Escenarios (§9)** |
|---|---|---|
| Naturaleza | vista **sistemática precomputada** del corte oficial EOD: mismos barridos en cada as_of, **comparable en el tiempo** | **run puntual efímero** configurado por el usuario en sesión |
| Configuración | set de barridos de la **metodología oficial** — no editable por el usuario | riel de control; preset de ρ **editable** por run (§9.3) |
| Lectura | impacto en la **medida** (ΔVaR por supuesto) — sin histogramas, sin G/P, sin Aplicar | distribución post-shock, G/P, franja VaR/ES, chips por ρ |
| Arquetipo | dashboard §4 | simulador §5 |

Cross-link declarado: nota fija al pie del TR con enlace discreto *"Explorar un barrido configurable → Escenarios"* (affordance de panel, no KPI navegable — deferral F1.2 intacto; registrado para PM en feedback-log).

**Convenciones de la sección (declaradas en UI y export)**:
- **OAT + CRN** — subtítulo fijo del panel TL (incluido en el export): *"Barridos one-at-a-time con números aleatorios comunes — cada barra mueve un supuesto; el resto permanece en base"* (Brain [guia]: comparaciones no contaminadas por ruido MC; coherente con la regla de Escenarios §9.3 "shocks de Supuesto excluyentes por run"). Supuestos **categóricos** (fuente de transición): barra **unilateral** desde el centro, rotulada "Fuente: S&P → Moody's (alternativa única)" — convención incluida en la misma nota.
- **Ancla badge↔barridos**: los barridos se computan en el **mismo run EOD bajo la config del badge del corte** — el centro del tornado ES el supuesto del badge. Si la config de los barridos publicados difiere del badge (desfase de publicación), **los paneles y KPIs derivados de barridos (KPIs 2–4, TL, TR, BL, BR) pasan a N/D** con banner *"Barridos calculados bajo otro supuesto — pendiente de recálculo del corte"*; **KPI 1 (VaR base) y KPI 5 (Uso Límite) sobreviven** — provienen del corte oficial válido y son el mismo dato de Métricas de Riesgo (coherencia entre secciones); el badge **nunca** se altera para "cuadrar" (§2 auditable).
- **Set oficial de ρ**: {15% · 25% · 35%} ∪ {ρ base} — si el ρ base ∈ {15,25,35}, la curva TR muestra 3 puntos con el marcador "base" sobre el que corresponda; si ∉, muestra 4 puntos con el marcador en base.
- **TC**: base y barridos consolidados al **mismo TC del as_of** (declarado en el pie de la tabla BR y en el export — F1.10). Cifras en DOP consolidado ($ M/MM; subtítulo del KPI 1 "Consolidado en DOP · TC del corte"); **las medidas de riesgo jamás se parten por moneda**.
- **Color**: los ΔVaR son medida de riesgo, no P&L → **neutro** (dirección −/+ por posición geométrica y etiqueta, jamás verde/rojo); semáforo solo en Uso Límite.
- **Sin vistas por emisor** → la leyenda de prorrateo del shell §4 no aplica (el drill es supuesto → rating; §2 intacto: rating eje primario, ninguna granularidad emisor prometida).
- **Comparabilidad de cortes (§11) — global**: si el badge del corte anterior difiere en **cualquier** componente, **todos los Δ de la pantalla** → "N/D" + tooltip; extendida a chips categóricos ("anterior: N/D").
- N/D nunca cero; celda de lado inexistente en filas unilaterales → **"—"** (no aplica, precedente F1.10); barra sin dato → ausente + "N/D".

**KPIs (4 contenido + 1 límite)** — patrón `CardMetric`:
| # | KPI | Formato | Ancla |
|---|---|---|---|
| 1 | **VaR de Crédito Total — 99% · 1 año** (DOP) | $ M/MM, 2 dec; chips (anterior, Δ, Δ%); subtítulo "Consolidado en DOP · TC del corte" (§4). Mismo dato que Métricas de Riesgo, Visión General y Factores (coherencia entre secciones) | §8; patrón §12 KPI 1 |
| 2 | **Supuesto más influyente** | categoría (p.ej. "ρ") + su \|ΔVaR\| máx (DOP y % del VaR base); chip categórico "anterior: X" (→ "anterior: N/D" bajo supuesto distinto); color neutro | §8 tornado (lectura ejecutiva) |
| 3 | **Supuestos que cruzan el límite** | conteo de barridos cuyo VaR− o VaR+ excede el límite de VaR configurado (filas unilaterales: se evalúa solo el lado existente); número en **neutro** (el semáforo solo vive en Uso Límite); sin límite → "N/D" + subtítulo "Límite de VaR: N/D" | inviolable contexto de límite, extendido a los barridos |
| 4 | **Amplitud del VaR por ρ (15%→35%)** | VaR@35% − VaR@15% en DOP y % del VaR base; subtítulo "@base ρ=X%"; tooltip de distinción cruzada: *"distinto del 'Efecto correlación' de Factores de Riesgo (VaR(ρ activo)−VaR(ρ=0), incremental); esta amplitud es el rango del barrido oficial de ρ"* | §2 no negociable (ρ = sensibilidad de primera clase); frontera con §12 KPI 3 |
| 5 | **Uso Límite** (fija) | uso del **VaR base** (medida oficial del corte) vs. su límite — subtítulo "sobre VaR base"; el cruce del límite por los barridos se lee en TR y KPI 3; sin límite → "N/D"; jamás 0% ni oculta | shell §4 (inviolable) |

**Rejilla 2×2**:
| Panel | Gráfico | Detalle |
|---|---|---|
| TL | **Tornado de supuestos — impacto en el VaR 99%·1a** | barras horizontales centradas en el **VaR base** (línea vertical etiquetada con el monto), ordenadas por \|ΔVaR\| desc; extremos − / + por barrido OAT de cada supuesto (ρ · μ recovery por seniority · σ recovery por seniority · fuente de transición — dominio de seniorities **autoritativo de la capa de datos**; el mock v1 ilustra 2: senior · subordinada — valores del mock ⇒ 6 barras, dentro del máx 7); **máx 7 barras individuales**; los restantes NO se dibujan como barra agregada (una barra de N supuestos no tiene lectura OAT): fila de texto al pie *"N supuestos más — ver tabla"*; subtítulo fijo OAT+CRN (convención, incluida en export); barras en neutro; barra sin dato → ausente + "N/D" |
| TR | **Curva VaR vs ρ** | puntos del set oficial {15/25/35} ∪ {ρ base} unidos por línea; **marcador diferenciado en el ρ base** (relleno + etiqueta "base"); eje Y en DOP MM; **línea punteada de límite de VaR** si configurada (el cruce se lee aquí) — sin límite → sin línea + nota "Límite: N/D" (precedente §7.2 TR); nota fija al pie con el cross-link *"Explorar un barrido configurable → Escenarios"* |
| BL | **Descomposición por rating del ΔVaR del supuesto seleccionado** | selector de supuesto (default = supuesto más influyente) + toggle de extremo −/+ (default = extremo de mayor \|ΔVaR\|); barras **Δ de la contribución componental (Euler) por rating** = contribución Euler al VaR bajo el extremo − contribución Euler bajo base (ambas del mismo run EOD con CRN) — **aditiva: Σ barras = ΔVaR del extremo mostrado** (subtítulo fijo que lo declara); ratings agrupados a letra (AAA…CCC–D, ≤8, mismo agrupamiento que §10.1); rating = eje primario §2; neutro; barra sin dato → ausente + "N/D". El selector intra-panel sigue el precedente "Vista por" de las donas (§7.1/§8.1) |
| BR | **Tabla de barridos** (exportable) | encabezado "Sensibilidad del VaR — 99% · 1 año (DOP consolidado)"; **lista TODOS los barridos** (exenta del máx 7 del tornado — precedente de tablas del módulo); filas expandibles **supuesto → rating** (Δ de contribución Euler por rating, misma definición que BL; rating = eje primario §2). Columnas: Supuesto · Valor base · Barrido (−/+) · VaR− · VaR+ · ΔVaR máx (DOP) · ΔVaR máx (% del VaR base) · Var de ΔVaR máx vs corte anterior (DOP). Filas unilaterales (fuente de transición): VaR− → "—" (no aplica). Comparabilidad global: Var → "N/D" bajo supuesto distinto, nunca 0. Pies (incluidos en el export): *"Base y barridos consolidados al TC del as_of (mismo TC)"* + la convención OAT+CRN + *"Variaciones al TC de cada corte; incluyen efecto FX"* (F1.10) |

**Navegación**: Inbound — sidebar "Sensibilidades" (`/sensibilidades/supuestos`), NavCard 7 del overview (§11.3), breadcrumb. Outbound — cross-link del TR hacia Escenarios; drill-down supuesto → rating en tabla BR; Filtros (§4); breadcrumb Home.

---

## 14. Sección Backtesting — *validación estadística del VaR oficial* (bead librisk-o07 / F1.13, ampliación PM)

Molde dashboard §4 heredado íntegro: breadcrumb `Home > Backtesting > Resumen de Excepciones`, **badge de supuesto activo** (regla del shell §4 intacta — supuesto vigente del as_of, estados N/D, nunca se oculta, §2 no negociable; la sección añade un **chip contiguo "Ventana: N cambios de supuesto"** cuando la historia visible los contiene), DataStatus + dataset + Filtros, barra de tabs con **un pill** ("Resumen de Excepciones", shell §3 — nombre tomado de la ruta empírica de Mercado `/backtesting/resumen-excepciones`), tira 4+1 KPIs, rejilla 2×2 con BR exportable. **Sin selector VaR·ES·Std** (solo Métricas de Riesgo y Marginal, handoff §5): se valida la **medida oficial VaR — 99% · 1 año**, etiquetada en el título del KPI 1 y en el encabezado de la tabla BR (patrón §12/§13).

**Sin referente construido en Mercado (evidencia)**: `backtesting-excepciones.png` es un placeholder "Contenido próximamente" — la paridad aplicable se limita al **nombre de ruta/tab y al molde §4**; el layout interno es diseño propio anclado en handoff §8 (excepciones, Kupiec POF, Christoffersen, semáforo), §9 catálogo (serie de excepciones + semáforo; traza de convergencia + bandas) y Brain `Capa2_RI_MetodologiaMercado.md` [guia]. Registrado para el PM en feedback-log.

**Pregunta de la sección (handoff §8)**: ¿el VaR oficial predice bien las pérdidas realizadas (validación externa) y es estadísticamente estable el estimador Monte Carlo que lo produce (validación interna)? El **caveat de muestreo de colas profundas es elemento de UI** (mandato del bead): vive como subtítulo fijo + comportamiento visual del panel BL, no como nota al pie.

**Convención de escala (valor del mock — declarada, no silenciosa)**: la comparación P&L-vs-VaR exige conmensurar el horizonte 1 año del Credit VaR con el intervalo entre cortes EOD; el mock usa **VaR escalado al horizonte entre cortes (regla raíz de tiempo), con cortes de frecuencia mensual declarada** — rotulado en el TL y en la columna BR: *"convención del mock — la metodología oficial del tenant gobierna la comparación"*. El panel TR hereda el caveat (nota: *"excepciones contadas bajo la convención de escala del mock"*). Tensión metodológica registrada para el PM en feedback-log (el Brain define backtesting para VaR diario de mercado; la variante de crédito no está canonizada).

**Regla de sub-ventana homogénea (auditabilidad §2)**: conteo de excepciones, Kupiec, Christoffersen y semáforo de Basilea se computan **solo sobre la sub-ventana homogénea vigente** (desde el último cambio de supuesto), rotulada *"Ventana válida: N cortes desde DD/MM/AAAA (objetivo 250)"* — **las pruebas jamás cruzan un cambio de supuesto** (un veredicto sobre supuestos mixtos no es auditable). N insuficiente → veredicto **"N/D — ventana incompleta (N/250)"** (redacción única para KPIs, TR y NavCard). La serie TL sí muestra toda la historia, con marcadores de cambio de supuesto (precedente §8.2).

**Regla de interfaz del semáforo (Brain [inviolable])**: el **semáforo de Basilea es un veredicto estadístico de validación del modelo — no es cumplimiento de límites**. Vive **solo en el panel TR**, como badge rectangular etiquetado propio (jamás el pill de estado de límite), con rótulo fijo *"Veredicto estadístico de validación del modelo — no es cumplimiento de límites"*. La tarjeta fija KPI 5 sigue siendo **Uso Límite** (molde §4 intacto). Fuera de la sección (NavCard 8, §11.3) el veredicto se muestra como **texto sin pill de color**.

**Reglas transversales de la sección**: sin vistas por emisor → la leyenda de prorrateo del shell §4 **no aplica** (la unidad de análisis es el corte, no la posición; §2 intacto). Cifras en **DOP consolidado** ($ M/MM; subtítulo del KPI 1 "Consolidado en DOP · TC del corte"; **VaR y P&L jamás partidos por moneda** — F1.10); serie multi-corte → pie *"Cada punto consolidado al TC de su fecha"*. Comparabilidad de cortes (§11) **extendida a categóricos**: los chips "anterior" de KPIs 1–3 comparan contra la ventana del corte anterior; supuesto distinto → "anterior: N/D" + tooltip (precedente §12). **El KPI 4 queda exento del chip de comparabilidad** (declarado): es diagnóstico del estimador MC del run vigente, no un dato del corte comparable en el tiempo. N/D nunca cero; pre-datos → KPIs y paneles en N/D, badges nunca ocultos (§6).

**KPIs (4 contenido + 1 límite)** — patrón `CardMetric`:
| # | KPI | Formato | Ancla |
|---|---|---|---|
| 1 | **Excepciones — VaR 99% · 1 año** | "X en N cortes **(ventana válida, objetivo 250)**" + subtítulo "esperadas ~E al 99% en N" (**E prorrateado a N**, no 2.5 fijo) y "Consolidado en DOP · TC del corte" (§4); chip "anterior: X" (comparabilidad) | §8; Brain [guia] ~2.5/año al 99% en 250d |
| 2 | **Kupiec POF** | veredicto categórico (Aceptado/Rechazado) + p-value; **variante categórica** (chip "anterior: X", sin Δ% — precedente §7.1/§8.2); ventana insuficiente → "N/D — ventana incompleta (N/250)"; tooltip: "razón de verosimilitud de proporción de fallas, LR ~ χ²(1); rechaza demasiadas o sospechosamente pocas excepciones" | §8; Brain [guia] |
| 3 | **Christoffersen** | veredicto categórico conjunto (independencia + cobertura) + p-value; misma variante y estados que KPI 2; tooltip: "detecta rachas — síntoma de modelo que reacciona tarde" | §8; Brain [guia] |
| 4 | **Precisión MC de la cola** | semiancho de la banda de confianza del VaR **@99% fijo (cuantil oficial, rotulado "@99%")**, en % del VaR; subtítulo-caveat "colas más profundas requieren ~1/q escenarios"; no sigue al selector del BL (los KPIs jamás mutan por controles de panel) | bead (caveat como UI); §9 catálogo |
| 5 | **Uso Límite** (fija) | uso del **VaR base** vs. su límite configurado — mismo dato y componente que las demás secciones (coherencia); sin límite → "N/D"; jamás 0% ni oculta. **El semáforo Basilea NO vive aquí** (regla de interfaz) | shell §4 (inviolable "no métrica sin contexto de límite") |

**Rejilla 2×2**:
| Panel | Gráfico | Detalle |
|---|---|---|
| TL | **Serie de excepciones** | línea de P&L realizado entre cortes + línea **−VaR escalado** (ambas en **neutro**); **marcadores de excepción por FORMA (rombo relleno) en un único color de alerta rotulado en leyenda ("Excepción") — jamás la terna semafórica** (tres rojos con tres significados quedan prohibidos en esta pantalla); marcadores verticales de **cambio de supuesto** + tooltip con el supuesto vigente (precedente §8.2); rótulo de convención de escala (mock); eje Y en DOP MM; pie *"Cada punto consolidado al TC de su fecha"* | 
| TR | **Panel de validación estadística** | tres bloques rotulados: **Kupiec POF** (LR, χ²(1), p-value, veredicto) · **Christoffersen** (independencia + cobertura, χ² conjunto, veredicto) · **Semáforo de Basilea** (zona verde 0–4 / amarilla 5–9 / roja 10+ normalizada a 250; conteo N/umbrales; **multiplicador base 3 + recargo, rotulado "(referencia ilustrativa del marco de mercado)"**) como **badge rectangular etiquetado propio** con el rótulo fijo *"Veredicto estadístico de validación del modelo — no es cumplimiento de límites"* (Brain [inviolable]); encabezado del panel: *"Ventana válida: N cortes desde DD/MM/AAAA (objetivo 250)"*; nota: *"excepciones contadas bajo la convención de escala del mock"*; ventana <250 → zona "N/D — ventana incompleta (N/250)" | 
| BL | **Traza de convergencia + bandas de confianza** | VaR estimado vs. N escenarios acumulados, con banda de confianza; **selector local "cuantil de diagnóstico": 1% · 0.5% · 0.1%** (rotulado — no cambia la medida oficial ni ningún KPI); **eje Y fijo común entre cuantiles y bandas a escala real** (sin recorte ni reescala que oculte el ensanchamiento — el caveat ES el comportamiento visual); **subtítulo fijo doble** (incluido en export/captura): *"Colas profundas: la banda de confianza escala ~1/q en escenarios"* + *"Bandas del estimador Monte Carlo — no es la distribución de valor del portafolio"* (guardarraíl anti-Gauss, patrón §12 TR) | 
| BR | **Tabla de excepciones** (exportable) | lista **todas las excepciones de la historia visible** (no solo la ventana válida — auditabilidad), con las **fuera de ventana atenuadas y rotuladas**; columnas: Fecha (DD/MM/AAAA) · P&L realizado (DOP consolidado) · **VaR 99%·1a (escalado, convención mock)** (DOP) · Exceso (DOP) · Supuesto vigente del corte · **Ventana válida (sí/no)**; encabezado "Excepciones del VaR — 99% · 1 año (DOP consolidado)"; VaR/P&L jamás partidos por moneda; sin valor → "N/D", nunca 0; pies (incluidos en el export): convención de escala del mock + *"Cada punto consolidado al TC de su fecha"* + *"Variaciones al TC de cada corte; incluyen efecto FX"* (F1.10) |

> **Cuadratura KPI 1 ↔ tabla BR (declarada)**: el KPI cuenta solo la **ventana válida**; la tabla lista la historia completa con la columna "Ventana válida" — ambos rotulados para que la diferencia sea legible, no un descuadre.

**Navegación**: Inbound — sidebar "Backtesting" (`/backtesting/resumen-excepciones`), NavCard 8 del overview (§11.3), breadcrumb. Outbound — Filtros (§4); breadcrumb Home.

---

## 15. Sección Deterioro (NIIF 9) — *staging y clasificación contable de la provisión ECL* (bead librisk-k9s / F1.14, ampliación PM)

> **Contrato vinculante propio**: `06-handoff-ifrs9-ecl.md` (complementa, no sustituye, el handoff 00). **Nota fija de sección** (visible bajo el breadcrumb, incluida en export): *"El Credit VaR responde el riesgo económico; esta sección responde la provisión contable ECL (NIIF 9)"* — evita la lectura de doble conteo entre Métricas de Riesgo y Deterioro (06, preámbulo).

Molde dashboard §4 heredado: breadcrumb `Home > Deterioro (NIIF 9) > Staging`, badge de supuesto activo **extendido** (abajo), DataStatus + dataset + Filtros (bloque 3 gana **Clasificación NIIF 9** y **Stage**, shell §4), tabs pill **Staging (default) · ECL · Movimientos · Conciliación REA** (set completo fijado por el PM, feedback-log 2026-08-21; este bead especifica **Staging**; ECL → F1.15, Movimientos y Conciliación REA → F1.16 — los tabs se renderizan pinneados desde ya, con contenido especificado en sus beads). **Sin selector VaR·ES·Std** (handoff §5: solo Métricas de Riesgo y Marginal): la cifra de la sección es la **provisión ECL — NIIF 9**, contable y única, etiquetada en el KPI 2 y encabezados (patrón §12/§13; "medida" se usa aquí como préstamo terminológico declarado — es una cifra contable, no una medida de la distribución simulada).

**Badge de supuesto extendido — SECCIONAL (mandato F1.14; completado en F1.15, corrección X#2)**: en TODAS las pantallas de Deterioro el badge agrega **un único segmento NIIF 9 idéntico entre tabs hermanos** — *"S&P · ρ=25% axiomático · TC 61.50 (BCRD venta, as_of) · NIIF 9: SICR ≥3 notches · backstop 30d (refutable) · 3 escenarios (60/25/15)"*. **Un solo badge, jamás dos componentes ni dos textos distintos dentro de la sección** (§2: tablero auditable; el deferral WARN 3 de F1.14 queda resuelto — las ponderaciones de escenarios forman parte del supuesto activo de Deterioro y viven en el badge desde Staging). Los valores son **del mock**; los reales vienen del contrato de datos. Reglas de estado del shell §4 intactas ("Supuesto: N/D" en Preparando/No listo/Error, nunca oculto).

**Criterio SICR cuantitativo del mock (decisión declarada)**: el criterio activo es **deterioro ≥3 notches de rating desde el origen** — el enfoque por notches es el más operable para una cartera de inversión con pocos emisores (06 §3). La alternativa **PD lifetime relativa (×2, cambio RELATIVO no absoluto)** se muestra en el panel TR como alternativa metodológica **declarada NO activa** (paridad con "metodología oficial única" de RI: el tenant elige una). El badge muestra solo el criterio activo.

**Color de stages (regla de la sección)**: Stage 1/2/3 es un **categórico ordinal en paleta secuencial neutra** (misma familia que la paleta de rating) — **Stage 3 jamás se pinta rojo**; el semáforo queda reservado al estado de límite (shell §4 [inviolable]). FVTPL (fuera de alcance) → gris terciario, patrón "Otros".

**Granularidad §2 (declarada, sin violación)**: el staging es **regla por instrumento sobre datos observables** — rating actual vs. rating en origen (dato de registro del instrumento), días de mora, clasificación contractual. No es la distribución de riesgo del modelo → la leyenda de prorrateo del shell §4 **no aplica** (análogo a la exención de Portafolio §7). El reto de datos "rating/EIR en origen no almacenados en legacy" (06 §6) se registra para F1.15.

**Moneda (F1.10)**: VM en grupos **DOP · USD · Total (DOP consolidado)** (montos, partición v2); la **provisión ECL va SIEMPRE en DOP consolidado y jamás se parte por moneda** (misma regla que toda medida). Subtítulo KPI 1: "AC + FVOCI · Consolidado en DOP · TC del corte".

### 15.1 Tab Staging — ¿dónde está la cartera en el modelo de tres stages y por qué?

**Purpose**: el usuario lee la distribución de la cartera en alcance ECL por stage, audita los criterios SICR que la producen y ve la clasificación contable que define el alcance.

**Information Hierarchy**: 1) cuánto del libro está en alcance ECL y cuánta provisión carga · 2) cuánto migró a Stage 2/3 (SICR/deterioro) · 3) qué reglas SICR están activas y cómo operan (auditabilidad) · 4) clasificación contable y exclusión FVTPL · 5) detalle por posición exportable.

**KPIs (4 contenido + 1 límite)** — patrón `CardMetric`:
| # | KPI | Formato | Ancla |
|---|---|---|---|
| 1 | **VM en alcance ECL** | $ M/MM DOP (AC + FVOCI); anterior, Δ, Δ%; subtítulo único "AC + FVOCI · Consolidado en DOP · TC del corte"; tooltip: "FVTPL excluido del ECL: $X MM — riesgo de crédito capturado en fair value" | 06 §1 |
| 2 | **Provisión ECL total — NIIF 9** | $ M/MM DOP; anterior, Δ, Δ%; **tendencia = impacto en deterioro (provisión ↑ = flecha ↑), color neutro**, tooltip explícito (regla "deltas comunican impacto, no signo", shell §4). Cifra idéntica a la del tab ECL (F1.15 la pinnea, no la recalcula) | 06 §2/§4; continuidad F1.15 |
| 3 | **VM en Stage 2** | $ M/MM DOP + "% del alcance"; anterior, Δ — SICR sin default | 06 §2 |
| 4 | **VM en Stage 3** | $ M/MM DOP (valor grande); anterior, Δ; subtítulo "N posiciones deterioradas" | 06 §2 |
| 5 | **Uso Límite** (fija) | uso vs. límite de cobertura de provisión si el tenant lo configura; sin límite → "N/D", jamás 0% ni oculta | shell §4 (inviolable) |

**Rejilla 2×2**:
| Panel | Contenido | Detalle |
|---|---|---|
| TL | **Barras apiladas rating × stage** | eje X = rating (eje primario §2, letra, orden AAA→CCC−D); apilado por Stage 1/2/3 en paleta secuencial neutra; **toggle de métrica: VM (default) · N posiciones · Provisión ECL** (la aceptación del bead exige las tres); eje Y en DOP MM (VM/provisión) o entero (posiciones); FVTPL fuera del gráfico (no tiene stage) — nota al pie "Alcance: AC + FVOCI" |
| TR | **Panel de criterios SICR activos** (`PanelCriteriosSICR`, componente nuevo) | panel auditable, no gráfico — **desviación declarada del molde §4** (precedente directo: §14 TR panel de pruebas; la auditabilidad §2 gobierna). Bloques rotulados: **(1) Cuantitativo — ACTIVO**: "Deterioro ≥3 notches desde el origen" + alternativa rotulada **NO activa**: "PD lifetime ×2 (cambio relativo, no PD absoluta)" (06 §3); **(2) Backstop — obligatorio**: "30 días de mora → SICR (presunción **refutable**; en bonos bullet rara vez se activa antes del default)"; **(3) Cualitativos**: watchlist · cambio de outlook · breach de covenants · deterioro sectorial/soberano; **(4) Low credit risk expedient (5.5.10) — flag de juicio RD**: *"Soberano RD ≈ BB− / Ba3, sub-investment-grade — el expedient NO es automático; exige juicio documentado: Política de Deterioro Crediticio v1 (valor del mock)"*; **(5) Mini-tabla de consecuencias por stage** (06 §2): Stage 1 → ECL 12 meses · interés sobre bruto | Stage 2 → ECL lifetime · interés sobre bruto | Stage 3 → ECL lifetime · interés sobre valor **neto** (bruto − provisión); **nota fija de simetría**: *"El staging es simétrico — si el riesgo mejora, la posición regresa Stage 2 → 1"* (06 §2) |
| BL | **Clasificación contable AC · FVOCI · FVTPL** | dona (3 categorías) de VM por clasificación sobre el libro completo, DOP consolidado; **FVTPL en gris terciario con rótulo fijo "Excluido de ECL — riesgo de crédito capturado en fair value"** (06 §1, motivo visible = aceptación del bead); FVOCI con nota "provisión contra ORI — no reduce el valor en balance" (mecánica completa en F1.16); leyenda lateral con montos; clasificación = atributo contractual observable (test SPPI + modelo de negocio — tooltip) |
| BR | **Tabla de staging por posición** (exportable) | jerárquica **rating → emisor → instrumento** (drill-down canónico). Columnas: Instrumento · **Rating actual · Rating en origen · Δ notches** (el driver del criterio cuantitativo) · Clasificación (chip AC/FVOCI/FVTPL) · **Stage** (chip 1/2/3 neutro; FVTPL → "—", tooltip "fuera de alcance ECL"; tooltip del chip repite la consecuencia del stage: horizonte ECL + base de interés) · **Criterio gatillado** (categórico: `≥3 notches · backstop 30d · cualitativo (subtipo) · —`) · **Expedient** (chip "Sí — juicio doc." solo en Stage 1 bajo low-credit-risk / "—") · Días mora · **VM en grupos DOP · USD · Total (DOP consolidado)** · **Provisión ECL (DOP)** — jamás partida por moneda. Sin corte anterior → "N/D" nunca 0; celda de grupo sin posiciones → "—"; pies F1.10 |

**Navegación**: Inbound — sidebar "Deterioro (NIIF 9)" (`/deterioro/staging`), breadcrumb. Outbound — tabs ECL · Movimientos · Conciliación REA (contenido F1.15/F1.16); Filtros (§4); drill-down en BR.

> **Reglas de filtro (F1.14)**: el filtro **Stage** opera sobre el alcance ECL — las posiciones FVTPL (stage "—") quedan **excluidas implícitamente** con cualquier valor de Stage activo; para verlas se usa el filtro Clasificación NIIF 9. Regla declarada para Fase 2.
>
> **Deferral a F1.15 (hallazgo R #1) — RESUELTO en F1.15**: NavCard 9 → Deterioro (NIIF 9) agregada en §11.3 con ancla Provisión ECL total (del tab ECL §15.3).

### 15.2 Clasificación contable — decisión de arquitectura (mandato del bead)

**Decisión**: la clasificación AC/FVOCI/FVTPL **no es tab propio ni pantalla de Portafolio** — vive en dos portadores complementarios:
1. **Panel BL de Staging** (arriba): donde la exclusión FVTPL del ECL es accionable y su motivo es visible (aceptación del bead).
2. **Portafolio §7.1 TR**: la dona gana la opción **"Vista por: Clasificación NIIF 9"** — la clasificación es un atributo de composición observable (misma mecánica que la opción Moneda F1.10); la narrativa ECL no viaja a Portafolio.

**Razón**: el alcance del ECL se **juzga** en Deterioro; la composición se **explora** en Portafolio. Un tab propio duplicaría la dona BL sin pregunta analítica adicional.

### 15.3 Tab ECL — ¿cuánta provisión carga el libro, cómo se calcula y qué escenarios la ponderan? (bead librisk-1ob / F1.15)

**Purpose**: el usuario lee la provisión ECL final, audita la mecánica que la produce (PD·EAD·LGD·DF a EIR original) y ve que el número oficial es el **promedio ponderado de los ECL por escenario — no el ECL del escenario promedio** (06 §4–§5).

**Information Hierarchy**: 1) provisión ECL final y cómo la producen los escenarios ponderados (la ponderación es elemento central de UI, mandato del bead) · 2) efecto de la no-linealidad (ambos números visibles) · 3) 12m vs lifetime y su descomposición por rating/clasificación · 4) mecánica del cálculo auditable (curvas PD, EAD, LGD, EIR original) · 5) detalle por posición exportable con cuadre.

**Ruta**: `/deterioro/ecl` (tab pill "ECL"). Molde §4 heredado; sin selector de medida (cifra contable "ECL — NIIF 9" etiquetada, §15). Badge seccional de Deterioro (arriba) — idéntico al de Staging.

**Regla de comparabilidad de cortes — extendida a escenarios (corrección X#1)**: el **vector de probabilidades y el set de escenarios forman parte del supuesto activo** de Deterioro (viven en el badge). Si entre cortes difiere cualquier componente del badge — incluidas las ponderaciones o el set de escenarios — **todos los Δ del tab** (KPIs 1–4 y columna Δ del BR) muestran "N/D" + tooltip (§11; un Δ jamás mezcla efecto de cartera con efecto metodológico).

**KPIs (4 contenido + 1 límite)** — patrón `CardMetric`:
| # | KPI | Formato | Ancla |
|---|---|---|---|
| 1 | **Provisión ECL total — NIIF 9** | $ M/MM DOP; anterior, Δ, Δ% (tendencia = impacto en deterioro, neutro — misma regla que Staging KPI 2); subtítulo "Ponderada por escenarios · Consolidado en DOP · TC del corte"; **misma cifra que Staging KPI 2 — pinneada, jamás recalculada**; tooltip de descomposición: ECL base · adverso · favorable × probabilidad (corrección X#7 — la ponderación es auditable desde el KPI) | 06 §4–§5; continuidad §15.1 |
| 2 | **Convexidad de escenarios** | ECL ponderado − ECL del escenario promedio, en DOP y % del ECL; **signo siempre visible, color neutro forzado**; tooltip: *"positivo esperado por la no-linealidad del ECL — no es un error del modelo ni un colchón adicional; el número oficial es el promedio ponderado de los ECL, nunca el ECL del promedio"* (corrección X#4) | 06 §5 (mandato: ambos números y su diferencia) |
| 3 | **ECL lifetime (Stage 2+3)** | $ M/MM DOP + "% del ECL total"; anterior, Δ; subtítulo "el resto es ECL a 12 meses (Stage 1)" | 06 §2/§4 (12m vs lifetime visible) |
| 4 | **Cobertura** | Provisión ECL / **saldo en alcance (costo amortizado + devengados)** en %; anterior, Δ; tooltip: "numerador y denominador en base costo amortizado — consistente con la mecánica EAD del §4; no es cobertura sobre valor de mercado" (corrección X#12) | 06 §4 |
| 5 | **Uso Límite** (fija) | idéntica a §15.1 KPI 5 | shell §4 (inviolable) |

**Rejilla 2×2**:
| Panel | Contenido | Detalle |
|---|---|---|
| TL | **Panel de escenarios macro ponderados** — elemento central del tab | **Desviación declarada del molde §4** (panel compuesto, no gráfico simple; precedente §14/§15 TR — aquí la ponderación ES la mecánica del número oficial, 06 §5; corrección X#6). Tres columnas **Base · Adverso · Favorable**, cada una con: chip de **probabilidad** (60% · 25% · 15% — valores del mock), **barra de ECL del escenario** (DOP, neutro), y fila expandible de **variables macro RD** (PIB · DOP/USD · tasa BCRD — colapsada por defecto, se abre por escenario; corrección X#6). Overlay de dos líneas de referencia horizontales: **"ECL ponderado (oficial)"** (sólida, etiquetada con el monto = KPI 1) y **"ECL del escenario promedio"** (punteada, rotulada *"no usada — muestra la no-linealidad"*), con el **Δ anotado entre ambas** (= KPI 2). **Nota fija del panel** (corrección X#10, incluida en export): *"Escenarios contables NIIF 9 — fijados por la gobernanza metodológica del tenant, no editables aquí; para estrés ad-hoc → Escenarios; para barridos de supuestos del VaR → Sensibilidades"*. Pie de calibración: *"Calibración macro con proxies regionales / benchmarks de soberanos comparables — escasez de defaults locales"* (06 §5) |
| TR | **Barras apiladas rating × horizonte ECL** | eje X = rating (eje primario §2; letras AAA→CCC–D, ≤8 barras); apilado de **exactamente 2 segmentos: ECL 12m · ECL lifetime** (paleta secuencial neutra); el toggle **"Vista por: Horizonte (default) · Clasificación (AC · FVOCI)" reemplaza la apilación, jamás la multiplica** (2 segmentos en ambas vistas; corrección X#8); eje Y en DOP MM; **nota fija**: *"lifetime incluye Stage 2 y Stage 3 — para separarlos por stage, ver el tab Staging"* (lente distinta del TL de Staging: horizonte/clasificación aquí, stage allá — sin duplicación); FVTPL fuera del alcance (no aparece) |
| BL | **Mecánica del cálculo** (selector local de 3 vistas) | encabezado fijo: *"Vista pedagógica del cálculo — no afecta KPIs ni tabla"* (corrección X#9; los KPIs jamás mutan por selectores de panel, precedente §14 BL). Vistas: **(a) Curvas PD (default)** — survival S(t) y PD marginal(t) = S(t−1) − S(t) por rating, **selector de rating 7 letras (D excluido; default = calificación predominante por share de VM**, misma definición que §12 TR); **render escalonado por período anual, jamás curva suavizada tipo densidad** + subtítulo-guardarraíl fijo (incluido en export): *"Eje X = tiempo — probabilidad acumulada/marginal de default por período; NO es la distribución de valor del portafolio"* (corrección X#3, patrón anti-Gauss §12 TR); nota de origen: *"derivadas de la matriz de transición del modelo — la misma de Factores de Riesgo §12 — elevada a potencia t con absorción del default"* (06 §6) · **(b) Perfil EAD** — línea escalonada del saldo esperado (costo amortizado + devengados) del alcance en el tiempo; nota "bullet ≈ estable; amortizable se proyecta" (06 §4) · **(c) LGD PIT** — barras por seniority (senior · subordinada — dominio autoritativo de la capa de datos, mock 2 valores) con nota fija *"point-in-time y forward-looking — no through-the-cycle"* (06 §4). **Subtítulo fijo del panel** (todas las vistas, incluido en export): *"ECL = Σ_t PD_marginal(t) × EAD(t) × LGD(t) × DF(t) — descuento a la EIR ORIGINAL del reconocimiento inicial, jamás a tasa de mercado actual"* (06 §4 — elemento auditable, mandato del bead) |
| BR | **Tabla ECL por posición** (exportable) | jerárquica **rating → emisor → instrumento**; encabezado "ECL por posición — NIIF 9 (DOP consolidado)". Columnas: Instrumento · Stage (chip neutro) · Horizonte (12m / lifetime) · Clasificación (chip AC/FVOCI) · **PD acumulada del horizonte — escenario base** (tooltip: *"la provisión NO sale de esta PD: es el promedio ponderado de los ECL por escenario — ver KPI 2"*; corrección X#11) · LGD (%) · EAD (DOP consolidado; pie declara la consolidación) · **EIR original (%)** — sin dato de origen (legacy) → *"N/D — no almacenada en origen"* con flag ⚑ y **política declarada: EIR proxy documentada por la metodología del tenant, jamás tasa de mercado** (06 §6; corrección X#5) · **columnas expandibles ECL base · adverso · favorable** (por posición; corrección X#7) · **Provisión ECL (DOP — jamás partida por moneda**, F1.10) · Δ vs anterior (regla de comparabilidad del tab). **FVTPL fuera de la tabla** (alcance AC+FVOCI). **Footer de conciliación obligatorio** (incluido en export): *"Σ tabla = KPI 1 (Provisión ECL total) · posiciones con EIR proxy: N (⚑)"* — el cuadre es visible, no un descuadre silencioso (corrección X#5). N/D nunca cero; "—" no aplica; pies F1.10 |

**Frontera con Escenarios (§9) y Sensibilidades (§13) — declarada (mandato del bead)**:
| | **ECL — escenarios macro (§15.3)** | **Escenarios (§9)** | **Sensibilidades (§13)** |
|---|---|---|---|
| Naturaleza | parte del **número contable oficial** — recurrente en cada corte | estrés **efímero** de sesión | barridos **OAT precomputados** del VaR |
| Quién configura | gobernanza metodológica del tenant (no editable en UI) | el usuario, por run | metodología oficial (set fijo) |
| Salida | provisión ECL ponderada (P&L/ORI) | distribución post-shock, G/P | ΔVaR por supuesto |

**Navegación**: Inbound — tab "ECL" desde Staging (default de la sección; la NavCard 9 del overview aterriza en `/deterioro/staging`, §11.3), breadcrumb `Home > Deterioro (NIIF 9) > ECL`. Outbound — tabs Staging · Movimientos · Conciliación REA; Filtros (§4 — Clasificación NIIF 9 y Stage aplican); drill-down en BR; nota TL → Escenarios / Sensibilidades (referencia textual, no link de KPI — deferral F1.2 intacto).

### 15.4 Tab Movimientos — ¿por qué cambió la provisión y el staging entre cortes? (bead librisk-arr / F1.16)

**Purpose**: el usuario audita el roll-forward de la provisión ECL y de los stages entre dos cortes — qué entró, qué salió, qué migró y qué se re-midió — con cierre exacto contra el Δ de provisión.

**Information Hierarchy**: 1) cuánto cambió la provisión y por qué buckets (roll-forward que cierra) · 2) cómo migró la cartera entre stages (1↔2↔3, altas/bajas — simetría 06 §2 visible) · 3) dónde (por rating) se concentró el cambio · 4) detalle por posición exportable con registro contable P&L/ORI · 5) comparabilidad metodológica del período.

**Ruta**: `/deterioro/movimientos` (tab pill "Movimientos"). Molde §4 heredado; sin selector de medida (cifra contable "ECL — NIIF 9" etiquetada, §15). **Badge seccional de Deterioro explícito e idéntico a Staging/ECL** (un solo badge, §15; reglas de estado del shell §4 intactas — "Supuesto: N/D" en estados no listos, jamás oculto) (corrección X#2).

**Selector local de período** (encabezado del tab): *"vs corte anterior (default) · vs corte a elegir"*. **El selector solo define el corte de comparación; el corte base del tab es SIEMPRE el corte oficial activo — KPI 1 jamás cambia con este selector** (corrección X#11).

**Regla de comparabilidad — alineada con §15.3 (corrección X#3)**: si CUALQUIER componente del badge difiere entre los dos cortes, los **Δ de los KPIs 2–4, el panel BL y la columna Δ del BR muestran "N/D" + tooltip** (§11 — un Δ jamás mezcla efecto de cartera con efecto metodológico). El **waterfall TL sí se renderiza** — desviación declarada con justificación: el roll-forward es una **descomposición contable del cambio, no una comparación de medidas** (06 §7: reporte exige roll-forward siempre); bajo divergencia su bucket "Cambio de medición" se rotula *"incluye efecto metodológico — cortes no comparables"* y lleva flag ⚑.

**KPIs (4 contenido + 1 límite)** — patrón `CardMetric`:
| # | KPI | Formato | Ancla |
|---|---|---|---|
| 1 | **Provisión ECL al corte — NIIF 9** | $ M/MM DOP; **misma cifra pinneada que Staging KPI 2 / ECL KPI 1, jamás recalculada**; subtítulo "Corte oficial · Consolidado en DOP · TC del corte" | continuidad §15.1/§15.3 |
| 2 | **Δ Provisión del período** | $ M/MM DOP y % (denominador: provisión del corte de comparación); tendencia = impacto en deterioro, **color neutro**; **cierra exactamente con el waterfall TL y con Σ del BL** (corrección X#6); N/D bajo divergencia de badge | 06 §7 |
| 3 | **VM deteriorado** | $ M/MM DOP — sufijo de unidad fijo "**(VM, DOP)**" (corrección X#9); VM que migró a Stage 2/3 en el período; N/D bajo divergencia | 06 §2 |
| 4 | **VM mejorado** | $ M/MM DOP "(VM, DOP)"; VM que regresó S2→1 o S3→2 — la **simetría del staging** (06 §2) visible a nivel KPI; N/D bajo divergencia | 06 §2 |
| 5 | **Uso Límite** (fija) | idéntica a §15.1 KPI 5 | shell §4 (inviolable) |

**Rejilla 2×2**:
| Panel | Contenido | Detalle |
|---|---|---|
| TL | **Waterfall de roll-forward de provisión** | eje rotulado "**Provisión (DOP MM)**" (corrección X#7); buckets: Saldo inicial → **Altas** (compras/originación) → **Bajas** (ventas/vencimientos/write-offs) → **Migraciones netas por stage** (a S2, a S3, mejoras — 3 sub-buckets, simetría visible) → **Cambio de medición** (remedición PD/LGD/EAD/escenarios sobre cartera constante; bajo divergencia de badge: rótulo + ⚑, arriba) → Saldo final. **Invariante de cuadre obligatoria (incluida en export)**: *"Saldo final − Saldo inicial = KPI 2 = Σ panel BL = Σ columna Δ del BR"*; **dos regímenes distintos, no confundir (hallazgo R#3)**: divergencia metodológica del badge → el waterfall se renderiza con el bucket "Cambio de medición" rotulado + ⚑; **dato ausente** (algún bucket N/D) → el waterfall completo pasa a estado vacío con motivo — jamás cuadre parcial silencioso (corrección X#6). Nota fija FVOCI: *"los movimientos de ECL de posiciones FVOCI se registran contra ORI — no reducen el valor en balance"* (06 §1/§6) |
| TR | **Sankey de migraciones de stages** | eje rotulado "**VM (DOP MM)**" + nota fija *"el sankey mueve VM; el waterfall mueve provisión — magnitudes distintas que no cuadran entre sí"* (corrección X#7); nodos: Stage 1·2·3 del corte de comparación → Stage 1·2·3 del corte base, + nodo **Altas** (entradas) y **Bajas** (salidas) — 8 nodos, en el tope §4; **paleta secuencial neutra fijada en spec** (misma familia que rating; Stage 3 y Bajas jamás rojo — semáforo reservado al límite, corrección X#8); tooltip por flujo: VM, N posiciones, criterio dominante de la migración |
| BL | **Δ provisión por rating** | barras con signo (positivo = más provisión), **rating eje primario §2** (letras, orden AAA→CCC−D, ≤8 barras); color neutro, signo visible (regla "deltas = impacto"); **Σ BL = KPI 2** (cuadre X#6); N/D bajo divergencia de badge (estado vacío con motivo) |
| BR | **Tabla de movimientos por posición** (exportable) | **jerárquica rating → emisor → instrumento con agregados por nivel** (corrección X#1 — jerarquía canónica intacta). Columnas: Instrumento · Clasificación (chip AC/FVOCI) · **Stage anterior → Stage actual** (chips neutros; sin movimiento → "="; alta → "Alta"; baja → "Baja") · **Motivo** (categórico: `≥3 notches · backstop 30d · cualitativo (subtipo) · remedición · alta · baja · —`) · Provisión anterior · Provisión actual · **Δ Provisión (DOP)** (N/D bajo divergencia) · **Registro contable** (chip **P&L** para AC / **ORI** para FVOCI — mandato c del bead) · VM en grupos DOP · USD · Total (montos, F1.10) — **provisiones jamás partidas por moneda**. Footer de cuadre: *"Σ Δ = KPI 2"*. N/D nunca cero; "—" no aplica; pies F1.10 |

**Navegación**: Inbound — tab "Movimientos" desde Staging/ECL, breadcrumb `Home > Deterioro (NIIF 9) > Movimientos`. Outbound — tabs Staging · ECL · Conciliación REA; Filtros (§4 — Clasificación NIIF 9 y Stage aplican); drill-down en BR.

### 15.5 Tab Conciliación REA — ¿qué exige el regulador vs qué dice NIIF 9, cuál gobierna y por qué difieren? (bead librisk-arr / F1.16)

**Purpose**: el usuario compara la provisión ECL NIIF 9 con la provisión REA SB (categorías A-E), ve la regla "el mayor de los dos" operando y audita la explicación de la diferencia — trabajo real de la entidad regulada (06 §6).

**Information Hierarchy**: 1) las dos cifras y cuál gobierna (mayor de los dos) · 2) la diferencia y sus drivers explicados · 3) el mapeo rating→categoría A-E y las reglas REA auditables · 4) detalle por instrumento exportable con registro contable · 5) tratamiento FVOCI sin ambigüedad.

**Ruta**: `/deterioro/conciliacion-rea` (tab pill "Conciliación REA"). Molde §4; sin selector de medida. **Badge seccional de Deterioro idéntico a los tabs hermanos** (X#2; el REA no altera los supuestos ECL — no agrega segmento al badge).

**Ámbito REA del mock — decisión declarada (corrección X#5)**: la provisión REA se calcula en el mock sobre **todo el alcance ECL (AC + FVOCI)** como política del tenant (valor del mock, flag ⚑); el mapeo regulatorio real de inversiones a fair value lo fija la norma SB y viene del contrato de datos — **la norma REA no está en el Brain** (gap registrado, feedback-log 2026-08-21). FVTPL fuera de ambos cálculos. Las filas FVOCI del BR llevan el chip ORI y la fila de doble registro (abajo).

**Regla "mayor de los dos" — ámbito declarado**: opera **a nivel cartera** (decisión del mock; el nivel real lo fija la política del tenant, rotulado en el TR). **Nota fija en el BR (incluida en export)**: *"El exigible se determina a nivel cartera — la suma de los máximos por instrumento NO es la provisión exigible"* (corrección X#4; sin columna 'gobierna' por instrumento).

**KPIs (4 contenido + 1 límite)** — patrón `CardMetric`:
| # | KPI | Formato | Ancla |
|---|---|---|---|
| 1 | **Provisión ECL — NIIF 9** | $ M/MM DOP; **pinneada** (= Staging KPI 2); subtítulo "Reporte financiero — NIIF prevalece" | 06 §6 |
| 2 | **Provisión REA — SB (A-E)** | $ M/MM DOP; subtítulo "Mínimo regulatorio · categorías A-E"; valores del mock ⚑ (norma del contrato de datos) | 06 §6 |
| 3 | **Provisión exigible** | $ M/MM DOP = **max(KPI 1, KPI 2) a nivel cartera**; **chip de cuál gobierna** ("Gobierna: NIIF 9" / "Gobierna: REA"); tooltip: *"NIIF prevalece para reporte financiero; el regulatorio exige el mínimo REA — la gestión cubre el mayor de los dos"* (06 §6) | 06 §6 |
| 4 | **Diferencia ECL − REA** | $ M/MM DOP y **% sobre REA (denominador declarado en subtítulo y tooltip**, corrección X#12); signo siempre visible, color neutro | 06 §6 |
| 5 | **Uso Límite** (fija) | idéntica a §15.1 KPI 5 | shell §4 (inviolable) |

**Rejilla 2×2**:
| Panel | Contenido | Detalle |
|---|---|---|
| TL | **Barras pareadas ECL vs REA por categoría REA A-E** | eje X = categoría A→E (5 categorías, ordinal); dos barras por categoría (ECL agregado vía mapeo · REA), DOP MM; **paleta secuencial neutra — la categoría E jamás roja** (misma regla que stages, semáforo solo límite); nota al pie: "ECL asignado a categorías vía el mapeo del TR" |
| TR | **Panel de mapeo y reglas REA** (auditable, no gráfico) | **Desviación declarada del molde §4 con precedente §14 TR (panel de pruebas) y §15.1 TR (PanelCriteriosSICR)** (corrección X#10). Bloques: **(1) Mapeo rating → categoría A-E** (tabla compacta; valores del mock ⚑) · **(2) % de provisión REA por categoría** (A…E; valores del mock ⚑ — la norma SB viene del contrato de datos) · **(3) Regla vigente**: *"Provisión exigible = mayor(ECL NIIF 9, REA SB) — evaluado a nivel cartera (política del tenant)"* · **(4) Nota de prevalencia** (06 §6): NIIF para reporte financiero, REA como piso regulatorio |
| BL | **Bridge de la diferencia explicada** | waterfall REA → ECL, eje "DOP MM": REA SB → **+ Forward-looking / escenarios ponderados** → **+ Lifetime vs 12m (Stage 2/3)** → **± LGD PIT vs % fijo REA** → **± Descuento a EIR original** → ECL NIIF 9; drivers del 06 §4–§6; **el bridge cierra exactamente con KPI 4** (invariante de cuadre, incluida en export); descomposición del mock — los drivers reales vienen del motor (⚑) |
| BR | **Tabla de conciliación por instrumento** (exportable — aceptación del bead) | **jerárquica rating → emisor → instrumento con agregados por nivel** (corrección X#1). Columnas: Instrumento · Clasificación (chip AC/FVOCI) · **Categoría REA** (chip A-E neutro) · **% REA** · **Provisión REA (DOP)** · **Stage NIIF** (chip neutro) · Horizonte (12m/lifetime) · **ECL (DOP)** · **Diferencia ECL − REA (DOP**, signo visible, neutro) · **Registro contable** (chip **P&L** / **ORI**). **Fila fija de doble registro FVOCI en el subtotal de clasificación (incluida en export)**: *"FVOCI: valor en balance a fair value · ECL reconocido en ORI — la provisión no reduce el balance"* (06 §1/§6 — mandato c sin ambigüedad contable). Footer: nota fija del exigible (arriba) + *"Σ ECL = KPI 1 · Σ REA = KPI 2"*. Provisiones jamás partidas por moneda (F1.10); N/D nunca cero; "—" no aplica |

**Navegación**: Inbound — tab "Conciliación REA" desde los tabs hermanos, breadcrumb `Home > Deterioro (NIIF 9) > Conciliación REA`. Outbound — tabs Staging · ECL · Movimientos; Filtros (§4 — Clasificación NIIF 9 y Stage aplican; el filtro Stage excluye implícitamente FVTPL, regla §15.1); drill-down en BR.

---

## Screens del shell (resumen)

| # | Screen | Molde | Selector medida | Tabs |
|---|---|---|---|---|
| 1 | Crédito › Visión General (**default**) | overview §11 | no | — (sin barra) |
| 2 | Crédito › Portafolio | dashboard §4 | no | Global · Concentración |
| 3 | Crédito › Métricas de Riesgo | dashboard §4 | sí | A la Fecha · Histórico |
| 4 | Crédito › Marginal | dashboard §4 | sí | Global |
| 5 | Crédito › Escenarios | simulador §5 | no | Impacto en Riesgo |
| 6 | Crédito › Factores de Riesgo | dashboard §4 | no (VaR 99%·1a etiquetado) | Mapa de Factores |
| 7 | Crédito › Sensibilidades | dashboard §4 | no (VaR 99%·1a etiquetado) | Supuestos |
| 8 | Crédito › Backtesting | dashboard §4 | no (VaR 99%·1a etiquetado) | Resumen de Excepciones |
| 9 | Crédito › Deterioro (NIIF 9) | dashboard §4 | no (ECL — NIIF 9 etiquetado) | Staging · ECL · Movimientos · Conciliación REA |

**Diagrama de navegación**: `03-wireframe-diagram.mermaid`.

---
**Approved by PM**: pendiente — gate [GATE-PM] de Fase 1
