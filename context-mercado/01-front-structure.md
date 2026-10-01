# Frontend — risk-intelligence-front_v3 (evidencia explore, 2026-08-20)

Todas las rutas relativas a `risk-intelligence-front_v3/`.

## 1. Stack

- **Framework**: Next.js 16 (App Router) + React 19 + TypeScript — `package.json:15-18`. Estado global con **Jotai** (`package.json:14`), auth con next-auth, export a Excel con `xlsx`.
- **Gráficos**: **ECharts 6** vía `echarts-for-react` — `package.json:12-13`. Registro central de tipos en `components/charts/core/DynamicComponentRenderer.tsx:39-69`. Un chart de línea simple en Canvas propio: `components/charts/canvas/SimpleLineChart.tsx` (mapeado a `line`).
- **UI/estilos**: **Tailwind CSS v4** (config vía CSS, no hay tailwind.config.js) — tokens en `app/globals.css`. Sin librería de componentes externa: todo en `components/`.

## 2. Navegación

- **Layout de sección**: `app/dashboard/mercado/layout.tsx:35-58` — `<MenuSidebar title="Mercado">` a la izquierda + contenedor blanco `rounded-[20px]` + `<MercadoFiltersSidebar />` a la derecha.
- **MENU_ITEMS** en `app/dashboard/mercado/layout.tsx:4-28`: Visión general, Portafolio, Sensibilidades, VaR, Factores de Riesgo, Escenarios, Backtesting. Cada ítem: `label`, `icon`, `href` (primera sub-tab), `match` (prefijo para estado activo).
- **MenuSidebar** (`components/MenuSidebar/MenuSidebar.tsx`): colapsable con persistencia (`storageKey`, `useSidebarCollapsed.ts`), ancho `w-60.5` / colapsado `w-[40px]`, versión móvil dropdown, activo por prefijo de ruta, auto-colapsa cuando el panel de filtros de Escenarios está abierto.
- **Tabs por subsección**: cada carpeta define `tabs.ts` (ej. `var-y-es/tabs.ts`: Global, Renta Fija, Renta Variable, Marginal, Comparativa Metodológica) renderizadas con `components/TabsNavigation.tsx` (pill activo blanco con borde, tooltip por portal).
- **Breadcrumbs**: `components/Breadcrumb.tsx` — `Home > Sección > Tab` (ej. `var-y-es/global/GlobalSection.tsx:74-84`).
- **Rutas**: cada una con `page.tsx` (server) + `XxxSection.tsx` (client) + `loading.tsx`. Lista completa en `../../mercado_routes.txt` (39 rutas).

## 3. Patrón de pantalla (repetido en cada `*Section.tsx`)

1. **Cabecera**: Breadcrumb izquierda; derecha spinner + badge `DataStatus` (as_of/dataset) + `MercadoFiltersBar` — `GlobalSection.tsx:73-92`.
2. **TabsNavigation** (`GlobalSection.tsx:94`).
3. **Cuerpo backend-driven**: la respuesta trae `components[]`, cada uno se pinta con `DynamicComponentRenderer` según `chart_type` (`DynamicComponentRenderer.tsx:86-127`). Layout con mapa de clases grid por índice:
   - Visión General: `grid-cols-12`, filas `[217px_371px]` — 4 KPIs/lines arriba, tabla + 2 charts abajo, fila de 5 `card_small` — `VisionGeneralSection.tsx:18-28, 113-130`.
   - VaR Global: columna izquierda de 5 tarjetas KPI (`xxl:max-w-54.25 xxl:flex-col`) + rejilla derecha — `GlobalSection.tsx:96-117`, `getGridClasses` (33-41).
4. **Filtros y refetch**: `hooks/useMercadoFilters.tsx` + `hooks/useFiltersRefetch.ts` → server action → nuevo `BackendResponse`. Filtros por chart: `components/charts/core/ChartFilterBar.tsx`.

## Componentes reutilizables

- **Tarjeta KPI**: `components/charts/core/CardMetric.tsx` (título bold 14px, valor xl bold, `DeltaBadge`/`StatusBadge`, fondo `#eff3f8`). Compacta: `CardMetricCompact.tsx`.
- **Badges**: `components/Badges/DeltaBadge.tsx`, `StatusBadge.tsx` (positive/negative/warning/neutral en `CardMetric.tsx:14-62`).
- **Badge as_of/dataset**: `components/DataStatus.tsx` — píldora "Datos DD/MM/YYYY" + estados Desactualizados/Preparando/No listo/Error; selector global `components/GlobalDatasetSelector.tsx` + `state/datasetSelectionAtoms.ts`.
- **Tablas**: `components/charts/core/TableGeneric.tsx`, `TableTabs.tsx`, `components/Table.tsx` (grupos de columnas DOP/USD, `Table.tsx:12`).
- **Vacíos/error**: `ChartErrorState.tsx` + `ChartErrorBoundary.tsx`; "N/D" estándar de los formatters (`utils/format.ts:24,57,75`); `SectionUnavailable.tsx`, `ServiceUnavailable.tsx`.
- **Loading**: skeletons compartidos `app/dashboard/mercado/_components/MercadoSkeletons.tsx` (pulse `bg-[#d9e2ed]`).
- **Inputs**: `components/inputs/{Select, MultiSelect, Calendar, RangeCalendar, Checkbox, RadioButton}.tsx`.

## 4. Tipos de gráficos (registro `DynamicComponentRenderer.tsx:39-69`)

`card`, `card_small`, `table`, `table_tabs`, `line` (canvas), `bar`/`chart_horizontal_bar`/`chart_vertical_bar`/`waterfall`/`stacked_bar`, `heatmap`, `timeseries`, `scatter`, `confidence_band`, `loss_histogram`, `bubble`, `pyramid`, `pie`, `stacked_area_chart`, `multi_chart`, `dual_chart`. Option builders en `components/charts/echarts/optionBuilders/` (`lossHistogram.ts:85` tiene marklines VaR/ES).

## 5. Tokens visuales (`app/globals.css`, Tailwind v4 `@theme`)

- **Colores**: `--primary #0d77bf`, `--secondary #1f2a4e`, `--error #c10007`, `--success #008236`, `--alert #de560d`, `--grey-hover #d9e2ed`, fondos semánticos `--fondo-ok/error/alerta` — `globals.css:10-53`; dark por clase `.dark`.
- **Paleta Tailwind**: brand `#0d77bf`/`#1f2a4e`, escala de grises, semánticos — `globals.css:74-104`.
- **Tipografía**: Inter + Roboto; H1 35/800 → body 13/400, utilidades `.font-h1..h6/.font-body` — `globals.css:105-220`.
- **Espaciado**: grid 4px, `--spacing-01..10`; breakpoints `xxl` 1400px, `3xl` 1600px.
- **Colores de gráficos**: fuente única `components/charts/colors-reports.tsx` (brandBlue `#0D77BF`, escala azul para pies, paleta categórica ECharts).
- **Superficies**: contenedores blancos `rounded-[20px]`, cards `#eff3f8` `rounded-lg`, fondo app `#eff3f8` / dark `#0c131c`.

## 6. Formatos

- **Moneda**: `utils/format.ts` → `formatMoneyCompact` (20-51): `$` por defecto, escalado `M`/`MM`, 2 decimales, locale en-US, `"N/D"` para null/NaN. DOP como etiqueta/código en datos (grupos DOP/USD en tablas), no `Intl currency`.
- **Porcentajes/números**: `formatPercent`, `formatNumber` (`utils/format.ts:53-99`).
- **Fechas**: `utils/formatDate.ts` (DD/MM/YYYY); badge dataset usa locale es-ES.

## Receta para replicar en "Crédito"

Crear `app/dashboard/credito/layout.tsx` clonando el de mercado (MenuSidebar `title="Crédito"`, `storageKey` propio, MENU_ITEMS), subcarpetas por tab con `tabs.ts` + `page.tsx` (server action) + `Section.tsx` (Breadcrumb + DataStatus + FiltersBar + TabsNavigation + grid de `DynamicComponentRenderer`) + `loading.tsx` con skeletons compartidos. El nav superior global ya muestra el tab **Crédito** deshabilitado (ver screenshots).
