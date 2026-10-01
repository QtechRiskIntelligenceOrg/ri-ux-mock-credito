# Prototype Metadata — Sección Crédito (Mock UX/UI) — CONSOLIDADO F2.6

**App**: Risk Intelligence (RI)
**Date**: 2026-08-21 (validación completa, bead librisk-hzu)
**Status**: Auto-validación completa PASS — **pendiente gate de PM de Fase 2** (no aprobado)

## Prototype
- **Type**: Live (Val Town)
- **URL**: https://joselier3--64f125fa9d7611f1b5491607ee4eb77e.web.val.run/
- **Val Name**: joselier3/ri-credito-mock
- **Val File ID (main.ts)**: 64f125fa-9d76-11f1-b549-1607ee4eb77e
- **Rutas**: hash routing `#/<seccion>/<tab>` con deep-link a nivel tab
- **Archivos**: main.ts (http) · index.html · styles.css · app.js · data.js
- **Entrada default**: `#/vision-general` (mandato PM F1.11: 8 secciones activas)

## Design Tokens Used
Tabla completa en `04-design-system-mapping.md` (baseline RI — excepción de rebranding documentada en `Capa2_RI_PlataformaUX.md`). Claves: fondo `#eff3f8`, primario `#0d77bf`, navy `#1f2a4e`, Inter + `tabular-nums`, radios 20/10/8, skeleton `#d9e2ed`, semánticos solo en pastillas de límite. **Re-verificado en F2.6: 0 nodos con hex inline fuera de `:root` en las 10 pantallas (scan DOM, excluye controles `mock-only` del switcher).**

## Screens Prototyped (10 pantallas / 8 secciones — módulo completo)
| # | Screen | Ruta | Estados | Bead |
|---|---|---|---|---|
| 1 | Visión General (default) | `#/vision-general` | ok·loading·empty·error·partial (=comparabilidad rota) | F2.7 |
| 2 | Portafolio › Global | `#/portafolio/global` | 5 estados | F2.2 |
| 3 | Portafolio › Concentración | `#/portafolio/concentracion` | 5 estados | F2.2 |
| 4 | Métricas de Riesgo › A la Fecha | `#/metricas-de-riesgo/a-la-fecha` | 5 estados + selector VaR·ES·Std | F2.3 |
| 5 | Métricas de Riesgo › Histórico | `#/metricas-de-riesgo/historico` | 5 estados + selector | F2.3 |
| 6 | Marginal › Global | `#/marginal/global` | 5 estados + selector | F2.4 |
| 7 | Factores de Riesgo › Mapa | `#/factores-de-riesgo/mapa-de-factores` | 5 estados | F2.8 |
| 8 | Sensibilidades › Supuestos | `#/sensibilidades/supuestos` | 5 estados (partial = rama badge↔barridos) | F2.9 |
| 9 | Escenarios › Impacto en Riesgo | `#/escenarios/impacto-en-riesgo` | 5 estados + ciclo §9.6 (pre-run·recalculando·post-run·obsoleto·fallo) | F2.5 |
| 10 | Backtesting › Resumen de Excepciones | `#/backtesting/resumen-excepciones` | 5 estados | F2.10 |

## Verificación Playwright (F2.6)
El MCP de Playwright del entorno exige Chrome del sistema (no instalable sin sudo); la verificación se hizo con **Playwright chromium vía script** (`prototype-captures/f26-validate.mjs`, resultados en `prototype-captures/f26-results.json`). Referencia visual de producción: dataset pre-cocinado `context-mercado/screenshots/` (regla: app viva solo para lo que el dataset no cubre).

- **Matriz 10 pantallas × 5 estados verificada por aserción DOM** (146 aserciones: 144 PASS, 2 artefactos de oráculo resueltos abajo). Oráculos: badge de supuesto visible con contenido (`S&P · CreditMetrics-Merton · ρ=25%`; "N/D" **solo** en degradación empty/error), montos `$X,XXX.XXMM`, fechas `DD/MM/AAAA` sin ISO visible, sin abreviación K, CTA "Reintentar" en error, instrucción en vacío, KPIs degradados en N/D nunca "0", coherencia VaR base `$122.79MM` entre secciones, 0 hex inline.
- **Capturas frescas**: `prototype-captures/f26-*.png` — las 10 pantallas en éxito + estados completos en 3 pantallas de muestreo (Visión General, Métricas A la Fecha, Escenarios) + `f26-b1-marginal.png`. Las capturas por estado de las demás pantallas viven en los sets por bead (`ov-*`, `mr-*`, `f24-*`, `fr-*`, `sens-*`, `esc-*`, `bt-*`, capturas F2.2).
- **Consola: 0 errores** acumulados en toda la sesión (navegación 10 rutas × 5 estados + interacciones).
- **Artefactos de oráculo (no violaciones)**: (1) Escenarios pre-run sin montos `$#.##MM` — por diseño del arquetipo simulador §9.6 (configurar→aplicar→leer); **re-asertado en F2.6 post-run** (`f26-postrun.mjs`): montos `$X,XXX.XXMM` presentes, `$122.79MM` presente, badge `.badge-supuesto` visible con plantilla §9.2 "Base: S&P · ρ=25% → Barrido activo: ρ=15/25/35%" (el rótulo cambia de "Supuesto:" a "Base:→Activo:" por diseño F2.5 — el badge nunca miente sobre el supuesto efectivo), consola limpia; captura `f26-esc-postrun.png`. Las fases obsoleto/fallo del ciclo §9.6 quedan verificadas en F2.5 (`esc-stale.png`, `esc-runfail.png`), no re-asertadas en F2.6 — desviación declarada. (2) Backtesting no muestra el string `122.79` — el VaR de la serie es diario (escalado raíz-de-tiempo **declarado en pie de panel**); la derivación desde el VaR base anual es coherencia de datos, ya validada en F2.10.
- **Granularidad emisor no prometida (§2)**: aserción de presencia de la nota de prorrateo/realización en TODAS las superficies con cifra de riesgo a nivel emisor — Visión General (Top Drivers), Métricas (drill), Marginal (scatter y tabla), Escenarios (tabla §9.5). Todas presentes.

## Auto-Validation Results (formal, módulo completo)

### Group A — Design Quality
| # | Criterio | Estado | Nota |
|---|---|---|---|
| A1 | Marca / baseline RI | ✅ Pass | Tokens del mapping en las 10 pantallas; Inter; molde de Mercado; 0 hex fuera de `:root` (scan DOM F2.6). Baseline de excepción re-verificado contra Brain (corpus `00dfc7c8353bacaf`). |
| A2 | Convenciones fintech | ✅ Pass | Series y deltas en neutro; semáforo Ok/Advertencia/Incumplimiento solo estado de límite; semáforo Basilea rotulado como veredicto estadístico [inviolable]; N/D nunca cero (aserción); DOP MM/M, DD/MM/AAAA (aserción). |
| A3 | Flujo | ✅ Pass | 10/10 pantallas del wireframe spec presentes; navegación sidebar+tabs conforme al mermaid; deep-link por hash verificado. |
| A4 | 4 estados UI | ✅ Pass | 5 estados (4 canónicos + error parcial) × 10 pantallas verificados por aserción; Escenarios añade el ciclo §9.6 completo. |
| A5 | DS y canon | ✅ Pass | Ledger L-1..L-14 del mapping re-chequeado sobre DOM real; Financial Data Contract implementado (formatter único, TC del corte declarado, fuentes en pies, exports con supuesto serializado); invariantes §2 verificadas con oráculos (badge, anti-Gauss, granularidad, DOP). |
| A6 | Consistencia con producción | ✅ Pass | Comparación por pantalla contra `context-mercado/screenshots/`: OV↔`vision-general.png`, Portafolio↔`portafolio-*.png`, Métricas↔`var-global.png`, Marginal↔`var-marginal.png`, Escenarios↔`escenarios-impacto-riesgo.png`, Sensibilidades↔`sensibilidades-duracion.png` (molde). BT y FR sin referente construido en Mercado (placeholders del dataset) → paridad = molde §4 + contrato de navegación, justificación por pantalla en beads F2.10/F2.8. |

### Group B — Usability & Actionability
| # | Criterio | Estado | Nota |
|---|---|---|---|
| B1 | JTBD completable | ✅ Pass | Criterio del brief: "desde VaR, identificar top driver y llegar a Marginal en ≤3 clics" → trazado con Playwright: driver legible en la propia vista (tabla por calificación) + **1 clic** de sidebar a Marginal. Captura `f26-b1-marginal.png`. |
| B2 | Acción primaria dominante | ✅ Pass | Dashboards: export de la tabla BR como acción primaria única por pantalla; simulador: "Aplicar" primario del riel (deshabilitado hasta validez). Sin CTAs de peso igual. |
| B3 | Sin dead-ends | ✅ Pass | 50 celdas pantalla×estado + 5 fases del ciclo de Escenarios: error→Reintentar, vacío→instrucción con selector visible, N/D con redacción explicativa, obsoleto→re-run, fallo de run→Reintentar (aserción DOM en toda la matriz). |
| B4 | Cobertura de roles | ⚠️ Flag PM | Roles RBAC (`Capa2_RI_Producto.md`): **CRO** — estado global + límites en Visión General (1 pantalla, 0 clics desde entrada); **Analista** — drill rating→emisor en Métricas/Marginal + simulador; **Lector** — export CSV en toda tabla BR; **Administrador** — sin superficie propia en el mock (configuración de límites/supuestos fuera de alcance del mock, es módulo de Configuración). Flag: el PM decide si el mock necesita señalizar el punto de entrada de configuración (hoy: N/D regulatorio con tooltip-CTA). |

## Desviaciones y decisiones para ratificación del PM (gate de Fase 2 — consolidado)
Origen y detalle en `feedback-log.md`; ninguna se auto-aprueba.

1. **Filtro Moneda deshabilitado en Métricas de Riesgo, Marginal y Sensibilidades** (desviación del filtro transversal F1.10): las medidas se calculan sobre la cartera consolidada completa; nota explicativa en el panel de filtros.
2. **Backtesting con cortes EOD diarios** (desviación del valor ilustrativo "mensual" del handoff §14): con mensual la pantalla sería N/D permanente; convención re-rotulada en TL/TR/BR.
3. **Backtesting: bloque archivado "ventana anterior (cerrada)"** para que los veredictos poblados sean evaluables; doble rótulo inviolable Basilea≠límites.
4. **Sensibilidades: recovery barrido por seniority** (no "por rating" literal del §8; ancla handoff §3 Beta por seniority); límite del TR como anotación fuera de escala; KPI 4 renombrado "Rango del barrido de ρ (15%→35%)"; rama badge↔barridos como estado "Error parcial".
5. **Factores: correlación como efecto incremental** (VaR(ρ)−VaR(0)), no barra Euler (Σ=VaR con 4 factores); KPI "Probabilidad de ≥1 default" (aporte propio); rama "residual no atribuido" implementada pero no demostrable desde el switcher.
6. **Visión General: NavCards navegables** (6→8, distinto de card_small informativas de Mercado); deltas del overview en neutro (contra el rojo/verde de producción — gobierna el shell §4); exención de contexto de límite en Top Drivers/Variación (descomposiciones del VaR Total).
7. **Marginal: glosario ⓘ como franja visible** (no tooltip); hipérbola iso-risk en `--sem-warn` (precedente markline HHI); terminología "componental" (deferral F1.6 abierto).
8. **Marginal como sección propia del sidebar** (en Mercado es tab de VaR): el inviolable "copia el contrato completo" gobierna contrato, no árbol IA literal (handoff §5).
9. **Escenarios: convención de demo del fallo de run** (payload de distribución separado); chip "⚡ Shock de libro" auditable.
10. **Diferidos menores de F2.2** (3 BAJOS del revisor, en feedback-log) y ataque desestimado de Marginal (filtro moneda visual).
11. **B4**: sin superficie de Administrador en el mock (configuración fuera de alcance) — confirmar.

## Reglas clave del prototipo (heredadas de los beads, vigentes)
- **BadgeSupuestoActivo** en cabecera, fuera de contenedores skeletonizables; "Supuesto: N/D" **solo** en degradación de dataset (vacío/error); intacto en cargando y error de panel (resolución X-2).
- **Fuente única de límites** (hallazgo R-1): el KPI de límite de Portafolio Global refleja el peor estado agregado con referencia a Concentración.
- **Aviso de universo filtrado** (hallazgo R-4): con filtro Moneda activo, "límites evaluados sobre el universo filtrado".
- Semáforo con texto (Ok/Advertencia/Incumplimiento) solo en límites; series/deltas en neutro; paleta ordinal azul AAA→B; N/D nunca cero; "—" solo grupo sin posiciones.

## Historia por bead (trazabilidad AX-DTR-D)
- **F2.2** (librisk-zph) — shell + Portafolio: X 19 ataques (15 integrados, #4 rechazado con evidencia, #5 diferido) → R PASS (4 MEDIOS corregidos; 6 BAJOS: 3 corregidos, 3 diferidos). Capturas F2.2 + `14/15/16-*.png`.
- **F2.3** (librisk-qj3) — Métricas: X 14 ataques (6 bloqueantes resueltos) → R PASS (2 rondas). Límite solo VaR; ES/Std → Uso Límite N/D sin semáforo. Capturas `mr-*.png`.
- **F2.4** (librisk-hh0) — Marginal: X 20 ataques → R PASS. Iso-risk con hipérbola/cuadrantes/fallen angels; Σ componental = total Métricas. Capturas `f24-marginal-*.png`.
- **F2.10** (librisk-6rn) — Backtesting: X 14 ataques (3 bloqueantes) → R PASS. Kupiec/Christoffersen/Basilea rotulados; convergencia MC anti-Gauss. Capturas `bt-*.png`.
- **F2.8** (librisk-7vy) — Factores: X 14 ataques (3 bloqueantes) → R PASS. Merton 7 ratings; PD y Z de matriz de transición única. Capturas `fr-*.png`.
- **F2.9** (librisk-p1d) — Sensibilidades: X 12 ataques (7 bloqueantes) → R PASS. Tornado OAT+CRN; curva VaR vs ρ; Euler Σ=ΔVaR. Capturas `sens-*.png`.
- **F2.7** (librisk-vyz) — Visión General: X 12 ataques (6 bloqueantes) → R PASS. Medida pinneada a VaR sin contaminar el selector. Capturas `ov-*.png`.
- **F2.5** (librisk-ykp) — Escenarios: X 12 ataques (5 bloqueantes) → R PASS. Barrido ρ 15/25/35 comparativo; histograma multimodal anti-Gauss con zoom; ciclo §9.6. Capturas `esc-*.png`.
- **F2.6** (librisk-hzu) — esta validación: X 1 ronda de **12 ataques al spec** (3 bloqueantes: #1 oráculos sin definir, #2 exención del badge de Escenarios demasiado ancha, #3 test operativo de granularidad emisor — los tres integrados como aserciones DOM; 7 MEDIOS integrados al protocolo; 2 BAJOS: B4→desviación PM, exclusión `mock-only` del scan L-7) → matriz ejecutada → R **PASS** (0 bloqueantes; M-2 corregido con aserción post-run + `f26-esc-postrun.png`; M-3 corregido con mapeo de evidencia; M-1 descartado: premisa errónea del revisor — la ronda X de este bead fue de 12 ataques, no 15).

### Mapeo de evidencia por pantalla (M-3)
| Pantalla | Éxito (F2.6) | Estados completos | Aserciones |
|---|---|---|---|
| Visión General | `f26-vision-general-ok.png` | `f26-vision-general-{loading,empty,error,partial}.png` | `f26-results.json` |
| Portafolio Global / Concentración | `f26-portafolio-*-ok.png` | set F2.2 (`05/06/08/09/14/15/16-*.png`) | ídem |
| Métricas A la Fecha | `f26-metricas-de-riesgo-a-la-fecha-{ok,loading,empty,error,partial}.png` | ídem | ídem |
| Métricas Histórico | `f26-metricas-de-riesgo-historico-ok.png` | set `mr-hist-*.png` | ídem |
| Marginal | `f26-marginal-global-ok.png` | set `f24-marginal-*.png` | ídem |
| Factores | `f26-factores-de-riesgo-mapa-de-factores-ok.png` | set `fr-*.png` | ídem |
| Sensibilidades | `f26-sensibilidades-supuestos-ok.png` | set `sens-*.png` | ídem |
| Escenarios | `f26-escenarios-impacto-en-riesgo-{ok,loading,empty,error,partial}.png` + `f26-esc-postrun.png` | ciclo §9.6: set `esc-*.png` | ídem + `f26-postrun.mjs` |
| Backtesting | `f26-backtesting-resumen-excepciones-ok.png` | set `bt-*.png` | ídem |
| B1 (JTBD) | `f26-b1-marginal.png` | — | `summary.b1` |

## Coherencia transversal verificada (F2.6)
- **VaR base $122.79MM** (fuente única `frAgg`) presente y idéntico en Métricas, Factores, Sensibilidades, Visión General y Escenarios post-run; Backtesting deriva la serie diaria del mismo ancla con convención declarada.
- **Badge de supuesto idéntico** (`S&P · CreditMetrics-Merton · ρ=25%`) en las 9 pantallas dashboard; Escenarios pre-run "S&P · ρ=25% (base)" e interpola el ρ activo post-run (plantillas §9.2, verificado en `esc-barrido-*.png`).
- **Formatter único**: $X,XXX.XXMM y DD/MM/AAAA por aserción en las 10 pantallas; sin fechas ISO visibles; sin K.

## Lo que el mock NO muestra (para el gate)
- Datos reales / API / cálculo del motor (todo `data.js` determinista).
- Autenticación, RBAC efectivo, configuración de límites y supuestos.
- Las secciones de otros riesgos del header (Mercado/Liquidez/Operacional) — decorativas.
- El switcher de estados y el botón de fallo de run son **controles del mock**, no del producto (rotulados).

---
**Pendiente**: gate [GATE-PM] de Fase 2 — el PM revisa el prototipo con este documento y las desviaciones 1–11.

---

## Ampliación F2.11 — Sección Deterioro (NIIF 9) completa (bead librisk-nqj, 2026-09-02)

**Screens agregadas (módulo pasa a 9 secciones / 14 pantallas; sidebar 9 ítems):**
| # | Screen | Ruta | Estados |
|---|---|---|---|
| 11 | Deterioro › Staging (default) | `#/deterioro/staging` | 5 estados (partial = Δ N/D) |
| 12 | Deterioro › ECL | `#/deterioro/ecl` | 5 estados + 3 vistas BL + escenarios expandibles |
| 13 | Deterioro › Movimientos | `#/deterioro/movimientos` | 5 estados (partial = KPIs 2–4 N/D, waterfall con bucket ⚑, cuadre "suspendido") |
| 14 | Deterioro › Conciliación REA | `#/deterioro/conciliacion-rea` | 5 estados |

**Reglas implementadas (§15 + handoff 06):** badge seccional único con segmento NIIF 9 idéntico entre los 4 tabs; nota fija de sección bajo el breadcrumb e incluida en los 4 CSV; provisión ECL **pinneada** ($78.53MM idéntico en Staging KPI2 / ECL KPI1 / Mov KPI1 / Conc KPI1 — verificado por DOM); convexidad ≥0 con ambas líneas de referencia y Δ anotado; DF a EIR original (EIR mock por posición; 2 proxy ⚑); cuadres verificados con dato vivo: waterfall = KPI 2 = Σ BL = Σ Δ BR (66.83) y bridge REA→ECL cierra con KPI 4 (−51.50); "mayor de los dos" a nivel cartera con chip Gobierna: REA (computado del dato); FVOCI/ORI con chip de registro y fila fija de doble registro; filtros Clasificación NIIF 9 + Stage (Stage excluye FVTPL implícitamente) con KPIs siempre globales y nota de filtro activo; paleta secuencial neutra (Stage 3/E/Bajas jamás rojo); NavCard 9 en Visión General.

**Coherencia VaR↔ECL:** PD desde la MISMA matriz de transición de Factores de Riesgo (fuente única); LGD desde recovery de Escenarios (Senior 55 / Sub 70); mismos emisores/ratings/VM. Narrativa del período: default de SBB Caribe 2026 (S2→S3) domina el Δ provisión (+571% — evento de default real del mock, auditable en el waterfall).

**AX-DTR-D:** X = 7 FAIL + 5 WARN corregidos pre-implementación (feedback-log 2026-09-02). R = **PASS** (3 menores: empty sin CTA — patrón del shell heredado; redondeo de etiquetas BL ±0.01 — el cuadre se cumple en el dato; charts canvas sin capa accesible — observación). Verificación Playwright chromium vía script: 4 tabs × estados, 0 errores de consola; capturas `prototype-captures/f211-*.png`.

**Valores del mock ⚑ pendientes de contrato de datos:** mapeo A-E y % REA (norma SB fuera del Brain — gap registrado), fracciones LGD/EIR del bridge + residual rotulado, convención notches (1 letra = 3), EAD ≈ VM, política EIR proxy.

---

## Re-validación final F2.12 — módulo consolidado 9 secciones / 14 pantallas (bead librisk-3vd, 2026-09-02)

**Esta sección supersede los "Auto-Validation Results" de F2.6 como validación vigente del gate.** Script: `prototype-captures/f212-validate.mjs` · resultados: `prototype-captures/f212-results.json` · **283 checks: 282 aserciones PASS + 1 exención declarada** (formato-MM en Escenarios pre-run por diseño §9.6, re-asertada post-run) · **0 errores de consola** (matriz 14×5 + oráculos NIIF 9 + deep-link frío + CSV + post-run de Escenarios). Playwright chromium vía script (MCP exige Chrome del sistema — misma convención F2.6/F2.11).

### Qué se re-verificó en F2.12 vs qué se hereda
- **Re-verificado sobre el val desplegado**: toda la matriz 14×5 con oráculos F2.6 (badge/N-D, formatos DOP MM y DD/MM/AAAA, CTA, N/D-nunca-cero, hex-scan), coherencia 122.79 (5 rutas + OV + Escenarios post-run), negativos de invasión 78.53, B1, y TODOS los oráculos NIIF 9 nuevos (abajo).
- **Heredado adicional**: nota de granularidad emisor (§2) en superficies VaR — asertada en F2.6 sobre las 4 superficies (Visión General, Métricas drill, Marginal, Escenarios §9.5); sin cambios en esas pantallas desde entonces.
- **Heredado con evidencia previa** (desviación declarada): fases obsoleto/fallo del ciclo §9.6 (F2.5 `esc-stale/esc-runfail.png`), sets de estados por bead de las pantallas 2–10, rama "residual no atribuido" de Factores (no demostrable desde el switcher). El hex-scan DOM es ciego a canvas — cubierto en F2.12 leyendo las opciones ECharts vivas (paleta).

### Oráculos NIIF 9 endurecidos por ronda X (12 FAIL + 8 WARN integrados — detalle en feedback-log)
| Oráculo | Resultado |
|---|---|
| Badge COMPLETO (base `S&P · ρ=25% axiomático · TC 61.50` + `NIIF 9: SICR ≥3 notches · backstop 30d (refutable) · 3 escenarios (60/25/15)`) e **idéntico** entre los 4 tabs | ✅ (string único, DOM) |
| Provisión pinneada `$78.53MM` por **selector del KPI correcto** (Staging KPI2 · ECL KPI1 · Mov KPI1 · Conc KPI1) | ✅ |
| Cuadres aritméticos con signo: Mov KPI2 = **+66.83** = waterfall final−inicial (opción ECharts, buckets Altas/Bajas presentes); Conc KPI4 = **−51.50** = bridge REA→ECL (endpoints 130.04→78.53) | ✅ |
| Paleta vía opciones ECharts: 0 colores rojo-dominantes en Staging TL, sankey, waterfall, Conc TL/BL; series Stage 3/E/Bajas neutras | ✅ |
| Anti-Gauss ECL: BL escalonado (`line:end`) + guardarraíl "no es la distribución" visible y en CSV | ✅ |
| Convexidad: KPI2 **+0.28MM** positivo = Δ de la referencia "no usada — muestra la no-linealidad"; ambas referencias viven en el panel TL (HTML, no chart — el TL de ECL es panel por desviación §15.3), por eso el oráculo lee el DOM y no la opción ECharts (ajuste declarado sobre X#12) | ✅ |
| PD uniforme en leaf rows del BR de ECL — clave rating × base ECL (12m/lifetime) × madurez T (la PD mostrada es acumulada al horizonte EFECTIVO: 21 leafs incl. pseudo-posición de alta, 20 claves, **0 conflictos**); `FR.TRANS` única fuente y LGD = `ESC.REC` (55/70) vía `RI_DATA` | ✅ |
| Provisión jamás partida por moneda: 0 headers `(Provisión|ECL|REA)×USD` en los 4 BR | ✅ |
| Filtro que filtra: Stage=3 reduce BR (9→4 filas visibles de la jerarquía), FVTPL desaparece, KPI global inmutable + nota "Filtro activo"; Clasificación=FVTPL ⇒ columna Stage = "—" en todas las leaf rows (verificado por índice de header tras expandir) | ✅ (`f212-staging-filtro-stage3.png`) |
| Partial de Movimientos: KPIs 2–4 N/D + waterfall RENDERIZADO con ⚑ + "cuadre suspendido" | ✅ (`f212-mov-partial.png`) |
| Controles nuevos F2.11: toggle TL Staging y vistas BL de ECL con **existencia y efecto en el chart asertados** + KPIs inmutables; el selector de período de Movimientos NO es interactivo (decisión F2.11: solo vs corte anterior) — se aserta el rótulo del período fijo | ✅ |
| CSV de los 4 tabs: nota de sección + supuesto serializado (ASCII `>=`) + footers de cuadre + guardarraíl | ✅ |
| Deep-link frío (`goto` directo) a las 4 rutas nuevas, consola limpia | ✅ |
| Nota cura S3→S2 en sankey; chip "Gobierna: REA"; fila FVOCI/ORI; nota anti-suma-de-máximos | ✅ |

### Auto-Validation Results F2.12 (vigente para el gate)

#### Group A — Design Quality
| # | Criterio | Estado | Nota |
|---|---|---|---|
| A1 | Marca / baseline RI | ✅ Pass | 14 pantallas con tokens del mapping; 0 hex inline fuera de `:root` (re-scan F2.12); baseline de excepción vigente en Brain (corpus `8b3bd636c070fe38`, catálogo re-consultado 2026-09-02). |
| A2 | Convenciones fintech | ✅ Pass | Neutro en series/deltas; semáforo solo límite; **paleta de stages/sankey/waterfall verificada sin rojo leyendo las opciones ECharts** (Stage 3/E/Bajas); N/D nunca 0; DOP MM, DD/MM/AAAA (aserción 14 pantallas). |
| A3 | Flujo | ✅ Pass | 14/14 pantallas presentes; sidebar 9 ítems; deep-link por hash re-verificado **incluida carga fría** de las 4 rutas nuevas. |
| A4 | Estados UI | ✅ Pass | 5 estados × 14 pantallas por aserción DOM (70 celdas) + régimen partial específico de Movimientos + ciclo §9.6 (post-run re-asertado en F2.12; obsoleto/fallo heredados F2.5). |
| A5 | DS y canon | ✅ Pass | Ledger del mapping vigente sobre las 14 pantallas; Financial Data Contract en Deterioro: EIR original con proxy ⚑, cuadres aritméticos verificados con dato vivo, CSVs con supuesto+notas; invariantes 00 §2 por oráculo F2.12 (badge completo, anti-Gauss, DOP); la nota de granularidad emisor en superficies VaR es **herencia declarada de F2.6** (aserción en las 4 superficies, ver línea F2.6 arriba) — Deterioro está exento por §15 (ECL por instrumento sobre observables, sin prorrateo). |
| A6 | Consistencia con producción | ✅ Pass | Sin cambios vs F2.6 para pantallas 1–10. Deterioro no tiene referente en Mercado (sección contable nueva) → paridad = molde §4 + jerarquía de tabla canónica; desviaciones TL/TR-panel declaradas con precedente (§14/§15). |

#### Group B — Usability & Actionability
| # | Criterio | Estado | Nota |
|---|---|---|---|
| B1 | JTBD completable | ✅ Pass | Re-trazado F2.12: driver legible en la vista + 1 clic sidebar → Marginal (objetivo ≤3). `f212-b1-marginal.png`. |
| B2 | Acción primaria | ✅ Pass | Sin cambios: export único por dashboard (incl. 4 tabs Deterioro); "Aplicar" en simulador. |
| B3 | Sin dead-ends | ✅ Pass | 70 celdas verificadas: error→Reintentar, vacío→instrucción, partial→explicación de régimen ("cuadre suspendido — no es un descuadre"). Menor heredado de F2.11: empty sin CTA dedicado (patrón del shell, igual en todo el mock). |
| B4 | Cobertura de roles | ⚠️ Flag PM | Re-mapeado incluyendo Deterioro: **CRO** → provisión exigible + "Gobierna: REA" en Conciliación (2 clics desde entrada; NavCard 9 en OV con ancla $78.53MM); **Analista** → auditoría SICR (criterios+Δnotches en Staging), mecánica PD/EAD/LGD/EIR y escenarios expandibles en ECL, waterfall auditable en Movimientos; **Lector** → export CSV en los 4 BR con cuadres serializados; **Administrador** → sigue sin superficie (config de límites/supuestos/escenarios contables fuera del alcance del mock) — flag original de F2.6 se mantiene, ahora también cubre la no-editabilidad de ponderaciones 60/25/15. |

### Desviaciones y decisiones para el gate — extensión NIIF 9 (se suman a las 1–11 de F2.6)
12. **Valores REA del mock ⚑**: mapeo rating→categoría A-E y % REA por categoría son invenciones del mock — la norma SB no está en el Brain (**gap Brain registrado 2026-08-21, aún sin declarar — requiere aprobación PM**). Todo valor REA lleva ⚑ en pantalla y CSV.
13. **"Mayor de los dos" evaluado a nivel cartera** (no por instrumento) — nota fija anti-suma-de-máximos; ámbito REA = AC+FVOCI por política del tenant ⚑.
14. **Criterio SICR del mock = ≥3 notches desde el origen** (06 §3); PD×2 visible como alternativa NO activa; convención de escala 1 letra = 3 notches (chip declarado).
15. **Escenarios contables 60/25/15 no editables en UI** (gobernanza del tenant); variables macro ilustrativas; EAD ≈ VM ⚑; política EIR proxy (2 posiciones) ⚑; PD lifetime `1−(1−PD12)^T` del mock.
16. **Bridge REA→ECL con residual rotulado** "base regulatoria (% fijo REA) — residual del mock ⚑" (driver económico real del gap); fracciones LGD/EIR mock ⚑.
17. **TL de ECL y TR de Movimientos/Conciliación como paneles no-gráficos** — desviación del molde §4 con precedente §14/§15 declarado.
18. **Fila fija FVOCI** al pie de Conciliación en vez de subtotal por clasificación (gana la jerarquía canónica rating→emisor→instrumento).
19. **Menores aceptados por R (F2.11)**: empty sin CTA (patrón shell); redondeo etiquetas BL ±0.01 (cuadre se cumple en el dato); charts canvas sin capa accesible (observación para producción).

### Mapeo de evidencia — filas 11–14 (extiende la tabla M-3)
| Pantalla | Éxito (F2.12) | Estados completos | Aserciones |
|---|---|---|---|
| Deterioro › Staging | `f212-deterioro-staging-ok.png` | `f212-deterioro-staging-{loading,empty,error,partial}.png` + filtro `f212-staging-filtro-stage3.png` | `f212-results.json` |
| Deterioro › ECL | `f212-deterioro-ecl-ok.png` | set F2.11 `f211-ecl-*.png` (heredado) + oráculos F2.12 (convexidad, anti-Gauss, PD, vistas BL, CSV) | ídem |
| Deterioro › Movimientos | `f212-deterioro-movimientos-ok.png` | `f212-mov-partial.png` (régimen asertado) + set F2.11 | ídem |
| Deterioro › Conciliación REA | `f212-deterioro-conciliacion-rea-ok.png` | set F2.11 `f211-conc-*.png` (heredado) + oráculos F2.12 (bridge, gobierna, FVOCI, CSV) | ídem |
| Escenarios post-run | `f212-esc-postrun.png` | — | `f212-results.json` |

---
**Pendiente**: gate [GATE-PM] de Fase 2 — el PM revisa el prototipo con este documento: desviaciones **1–11 (F2.6) + 12–19 (NIIF 9)** y el flag B4.

## Corrección F2.13 — densidad de texto: patrón InfoButton ⓘ (bead librisk-8yh, 2026-09-02)
- **Feedback PM del gate**: mock demasiado text-heavy. Aplicado patrón transversal **InfoButton ⓘ / InfoPopover** en las 14 pantallas: todo texto explicativo (69 notas: 55 panel-foot, 6 fr-sub, 2 bt-sub2, 5 f-note, 1 mr-nota + leyenda en KPI) movido detrás de UN ⓘ por panel — popover a 1 clic, portal al body (z-60), inviolables §2 primero, ARIA disclosure completo (Esc devuelve foco, clic fuera/scroll cierran, cambio atómico entre ⓘ).
- **Visible permanece**: títulos, ejes/series, valores, badges (supuesto/as_of/NIIF9), pills, banners de estado (.placeholder-note), nota de empty-state del simulador (anti dead-end B3), chips calificadores `prorr.` (tabla + KPI Top Driver), CTA "Explorar → Escenarios" (extraído a línea visible, listener preservado).
- **Textos no eliminados**: 1 clic vía ⓘ + líneas "Nota" en TODOS los exports CSV (verificado — ya presentes).
- **Componente nuevo propuesto**: `InfoButton` + `InfoPopover` (feedback/disclosure) — pendiente de alta en DS; taxonomía estado-visible / metodología-ⓘ / calificador-chip documentada en 03-wireframe-specs.md §4.
- **Verificación Playwright**: 14/14 rutas con 0 notas explicativas visibles; interacción completa del popover OK; 0 errores de consola. Capturas before/after ×4 pantallas + popover: `prototype-captures/f2.13/`.
- **Review independiente**: PASS (hallazgo .mr-nota corregido y re-verificado; banner de alcance de Deterioro se mantiene como excepción declarada).
- Los conteos de la validación F2.12 sobre texto visible de notas quedan superseded por este patrón: el contenido de las notas sigue asertable vía popover/CSV.
