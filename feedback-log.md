# Feedback Log — Sección Crédito (append-only)

## 2026-08-20 — Bead librisk-gyz (F1.1 Brief estructurado)

- **X (adversarial, ronda 1)**: 2 FAIL — (a) ambigüedad Sección-vs-Tab entre el molde §6 del handoff (que lista las 4 secciones como tabs) y la jerarquía inviolable Módulo→Sección→Tab→Visual; (b) regla anti-Gauss sobregeneralizada y mal atribuida a §2 (chocaría con Umbrales de Merton §8) + SC1 no verificable.
- **Correcciones aplicadas**: (a) resolución explícita — sidebar = 4 secciones núcleo, tabs = sub-vistas por sección (patrón `tabs.ts` de Mercado); (b) anti-Gauss acotada a la silueta de la distribución de valor del portafolio, citada a §4, con excepción explícita de Merton (fuera de alcance); SC1 convertida a checklist de elementos vs `var-global.png`.
- **R (revisor independiente)**: PASS.
- **Nota para el PM**: el patrón "próximamente" del sidebar de Crédito sigue el inviolable del Brain "futuro visible pero inactivo… en gris" (`Capa2_RI_PlataformaUX.md`); consistente con el handoff §5. No hay gaps de Brain que declarar en este bead.
- **Decisión de jerarquía documentada**: el mock usa el baseline visual vigente de RI (excepción de rebranding, `Capa2_RI_PlataformaUX.md`), no los tokens corporativos de Capa 1; las reglas de USO de color (riesgo en neutro, semáforo solo en límite, N/D) aplican de ambas fuentes.

## 2026-08-20 — Bead librisk-xo9 (F1.2 User Journey)

- **X (adversarial, 2 rondas)**: 17 ataques R1 + 4 nuevos R2; todos resueltos en el artefacto. Decisiones clave:
  - Emisor reencuadrado como "desglose de exposición" con etiqueta fija (no nivel analítico) — §2.
  - Drill-down rating→emisor in-place en VaR›Global; sin cross-filter (no evidenciado en Mercado); tab "Por Calificación" fuera del happy path → definir en F1.3.
  - KPI Top Driver NO navegable (paridad); camino canónico a Marginal = sidebar (2 clics ≤3).
  - Barrido ρ: selector de ρ-activo en el riel; comparaciones base(25%) vs ρ-activo; tabla con 3 columnas.
  - Badge de Escenarios con dos estados (pre/post-run).
  - Ambas siluetas del histograma (base y shock) asimétricas/multimodales; densidad simétrica prohibida.
- **R (revisor independiente)**: PASS. Deferrals para F1.3:
  1. Resolver la tira "Tabs" del molde §6 vs. navegación por sidebar (evitar navegación duplicada).
  2. Mantener el KPI Top Driver como informativo no navegable (frontera §2).
- **Corrección post-R**: cita de fuente del presupuesto ≤3 clics (success criteria #3 del brief).

## 2026-08-20 — Bead librisk-8ag (F1.3 Shell: navegación + molde transversal)

- **X (adversarial, 2 rondas)**: R1 = 2 FAIL + 7 WARN; R2 = 0 FAIL + 2 WARN residuales. Correcciones clave:
  - **Tira KPI = 4 de contenido + 1 tarjeta fija de contexto de límite** (inviolable "no métrica de riesgo sin contexto de límite" > molde guia de 4): VaR/Marginal = "Uso Límite"; Portafolio = "Límite de concentración (HHI/top-N)"; N/D sin límite.
  - **Filtros definidos como contrato de shell**: `CreditoFiltersSidebar`, orden inviolable de 5 bloques, dominios contextuales de crédito (calificación, emisor, tipo de instrumento, seniority), dominios autoritativos de la capa de datos.
  - Badge de supuesto en estados no felices → "Supuesto: N/D", nunca oculto (§2).
  - Leyenda de prorrateo elevada a formato transversal.
  - Formato DOP pinneado: `$` + M/MM + unidad DOP explícita en encabezados/ejes/subtítulos.
  - Tabs: los beads por sección pueden añadir, nunca renombrar/eliminar los pinneados.
- **R (revisor independiente)**: PASS.
- **Tensiones/decisiones para el PM (gate de Fase 1)**:
  1. **Marginal como sección propia del sidebar** (en Mercado es tab de VaR-y-ES). Anclada al handoff §5 (sketch núcleo de 4); el inviolable "copia el contrato completo" se lee como contrato (jerarquía/arquetipos/molde), no árbol IA literal. Confirmar.
  2. **Secciones de un solo tab renderizan la barra con un pill** (uniformidad del molde) — sin precedente empírico en Mercado. Confirmar.
  3. La tira "Tabs: VaR·Marginal·Portafolio·Escenarios" del molde §6 del handoff se reinterpreta como sub-vistas por sección (jerarquía inviolable Módulo→Sección→Tab). Consistente con la decisión de F1.1.
- Sin gaps de Brain que declarar (corpus cambió a `8b3bd636c070fe38`; entries re-verificados, contenido consistente).

## 2026-08-20 — Bead librisk-2v2 (F1.4 Wireframe spec — Portafolio)

**AX-DTR-D**: X 2 rondas (ronda 1: 2 FAIL — límites por emisor sin ancla → anclados en paridad `portafolio-concentracion.png` + inviolable de límites; dona por emisor sin colapso → regla top-7+"Otros" gráfica, tablas exentas; ronda 2: PASS con 2 WARN corregidos — Δ HHI en puntos 4 dec con tooltip; tabla de límites exenta del colapso). R: PASS (obs. de simetría corregida).

**Para el PM (decisiones y excepciones a validar en el gate):**
1. **Excepción de paridad — moneda**: la tabla de Portafolio de Mercado parte DOP/USD; en Crédito se omite la partición (cartera 100% DOP, handoff §2). "DOP" explícito en encabezados/ejes/subtítulos.
2. **Eje del área apilada = rating** (no clase de activo como Mercado): rating es el eje primario del §2.
3. **Dona en vez de treemap** (§7.1 permite ambos): paridad empírica con Mercado; treemap sin precedente en la librería del front.
4. **Leyenda de prorrateo NO aplica en Portafolio**: todas las cifras son VM observado (matriz de Exposición), no riesgo prorrateado; compromiso: ninguna celda de la sección contiene riesgo modelado.
5. **KPI "Calificación predominante"**: valor categórico con flecha = dirección del share, siempre neutro (sin semáforo), tooltip con semántica.
6. **Tab Concentración** extiende §7.1 con paridad empírica (evolución histórica con línea de límite, holgura/exceso, estado de límites) — extensiones ancladas en screenshot de Mercado, no invención.

## 2026-08-20 — Bead librisk-a66 (F1.5 Wireframe spec — VaR/Riesgo)

**AX-DTR-D**: X 1 ronda (0 FAIL, 8 WARN — todos resueltos en el artefacto); R: PASS (1 hallazgo MEDIA corregido: esta entrada del log; 3 BAJA documentados en el spec).

**Correcciones X incorporadas**: leyenda de prorrateo extendida a BR (nota al pie, incluida en export), BL en vista Emisor y tooltip del KPI Top Driver; KPI "Share del top rating" (sin ancla) reemplazado por Razón `<Medida>`/VM (§7.2); Uso Límite conmuta con la medida activa y muestra N/D si esa medida no tiene límite configurado (canon §4: σ→límites); Vol anualizada con fuente definida (σ diaria del VM del libro ×√252, no conmuta, tooltip pinneado); BR de Por Calificación = mismo componente que BR Global (columnas pinneadas); dona TR con selector "Vista por" (Emisor default) por uniformidad de componente.

**Para el PM (decisiones y desviaciones a validar en el gate):**
1. **Top-7 + "Otros"** en vistas gráficas por emisor, en lugar del "top-8 + Otros" literal del §7.2 — coherencia con la regla de sección de Portafolio (F1.4). Confirmar la interpretación (8 categorías totales).
2. **TR de Por Calificación = "standalone vs. contribución por rating"** y KPI "Beneficio de diversificación": anclados en Brain `Capa2_RI_MetodologiaCredito.md` [guia] ("contribución por dimensión; brecha Σ standalone − cartera = beneficio de diversificación"). La vista standalone **por posición** queda en Marginal (§7.3) — frontera declarada, sin solapamiento. Confirmar que analítica puede computar standalone por rating bajo VaR/ES (no solo σ); si no, el panel degrada a N/D.
3. **Vol anualizada** definida como σ observada del VM del libro (no conmuta con el selector) — interpretación del §7.2; confirmar fuente de la serie.
4. **Uso Límite conmutable con N/D** por medida sin límite configurado — confirmar contra la configuración real de límites del tenant.
5. **"Sector" fuera del selector local de la dona** (se alcanza vía Filtros "Vista por") — misma omisión que Portafolio; paridad empírica.
6. Nota: el snapshot A (`brain-context-snapshot.md`, bead a66) conserva el KPI pre-adversarial "Share del top rating"; el artefacto final (specs §8.2) es el vigente.

## 2026-08-20 — Bead librisk-iq9 (F1.7 Wireframe spec — Escenarios)

**AX-DTR-D**: X 2 rondas (ronda 1: 2 FAIL — moneda DOP no declarada en la sección; badge post-run indefinido fuera del barrido de ρ — + 7 WARN, todos corregidos; ronda 2: 9/9 RESUELTO + 2 WARN nuevos N1/N2 corregidos). R: PASS.

**Decisiones y tensiones para el PM (gate de Fase 1)**:
1. **Sin tarjeta "Uso Límite" en Escenarios** — paridad empírica (Mercado Escenarios no la tiene) + el G/P de escenario no es métrica con límite; el contexto de límite del VaR se restituye en la franja por ρ (§9.7), que **solo existe en modo barrido**: en shocks de libro no hay contexto de límite en pantalla. Punto que más merece atención del PM (señalado por el revisor R).
2. **Color de P&L con semántica económica de signo** (divergentes, waterfall, G/P) vs. regla del shell "deltas en neutro" — regla de frontera declarada en §9 (P&L=signo; medidas de riesgo=neutro); decide el PM.
3. **Sin toggle "Impacto Económico / Impacto en Riesgo" ni radio VaR/CVaR** del riel de Mercado — Crédito v1 lee valor y cola en un solo tab, sin selector de medida (handoff §5). Tarjetas empíricas VaR Pre/Post/Delta sustituidas por VM Pre/Post/G-P (§7.4, fuente vinculante > precedente).
4. **Sin panel de Filtros del shell** en Escenarios: el riel de configuración es el contexto (paridad empírica); implica que no hay filtro de portafolio/fecha fuera del selector de dataset — confirmar en el gate.
5. **Leyenda de prorrateo sustituida por nota de granularidad** (§9.5): las cifras por emisor aquí son revaluación directa, no prorrateo; la nota fija protege el §2 sin mentir sobre el mecanismo.
6. **Composición de shocks**: sub-tipos de Libro combinables; los de Supuesto excluyentes por run (atribuibilidad de la sensibilidad, §2).
7. Observación no bloqueante del revisor: el catálogo §9 del handoff menciona líneas VaR/**ES** en el histograma; el spec dibuja solo VaR (criterio del bead) — confirmar con PM si ES merece línea propia.

## 2026-08-20 — Bead librisk-mvx (F1.6 Wireframe spec — Marginal)

**AX-DTR-D**: X 2 rondas (R1: 4 FAIL + 9 WARN, todos corregidos; R2: 13/13 RESUELTO + 3 WARN nuevos cerrados). R: PASS (1 MEDIA registrado aquí; 2 BAJA + 1 cosmético corregidos en el artefacto).

**Decisiones y desviaciones para el PM (gate de Fase 1):**
1. **Separación marginal / componental / standalone** (glosario de sección): la dona, el "% del total" y el HHI usan **contribución componental (Euler, aditiva)** — el marginal leave-one-out del §7.3 no es aditivo y presentarlo como porciones sería analíticamente falso. Ancla: tabla empírica de Mercado (VaR Marginal $ / VaR Componental coexisten) + Brain "contribución por dimensión". Confirmar que analítica computa componental bajo VaR/ES (no solo σ); si no, dona/%-total degradan a N/D.
2. **Beneficio de diversificación = standalone − componental** (no standalone − marginal, la lectura literal del §7.3): matemáticamente coherente con el KPI de VaR §8.2 (Σ standalone − cartera) y con la aditividad. Desviación de fuente vinculante señalada por el revisor R — confirmar.
3. **KPIs del §7.3 sustituyen la tira empírica de Mercado** (Mayor Aumento/Reducción, % VaR Explicable): fuente vinculante > precedente; las lecturas de signo se recuperan en el ranking divergente BL.
4. **Scatter iso-risk sin colapso top-7** (cada punto = posición; fuera del alcance de la regla, que gobierna vistas por emisor); sobreplot mitigado con opacidad+zoom. Rating de color agrupado a letra (7 categorías).
5. **KPI "Posiciones sobre umbral" anclado exclusivamente a la hipérbola** (límite de riesgo absoluto, la recomendada del §7.3); N/D si no está configurada aunque existan límites h/v. Confirmar contra la configuración real de límites.
6. **Marginales negativos**: scatter los muestra bajo Y=0 (cuadrantes/hipérbola solo anotan Y>0); dona excluye negativos con nota "Diversificadoras: N, neto −$X"; HHI sobre pesos positivos renormalizados.

---

## 2026-08-20 — Feedback PM sobre wireframe specs (revisión pre-gate Fase 1)

Revisión del PM sobre `03-wireframe-specs.md` (resumen presentado en sesión):

1. **Entrada default rechazada**: aterrizar en VaR Global no hace sentido. La entrada
   debe ser una **Visión General / overview de riesgo de crédito**. → bead `librisk-dbv` (F1.8).
2. **Nombre "VaR" rechazado** para la sección: es un error heredado de Mercado. La
   sección es **"Métricas de Riesgo"** (la medida es el selector, no el nombre).
   Además, **separar estructuralmente** el análisis del riesgo *a una fecha* (as_of)
   del *análisis histórico* del riesgo. → bead `librisk-08x` (F1.9).
3. (item 4 del resumen) **Multi-moneda**: correcto no tener shock FX, pero la cartera
   SÍ puede tener instrumentos de crédito en USD — revertir la excepción "100% DOP";
   exposición USD visible y filtrable, partición DOP/USD como Mercado. → bead `librisk-eed` (F1.10).
4. Item 5 (Escenarios sin tarjeta Uso Límite; contexto de límite en la franja VaR/ES
   por ρ): explicado al PM; **sin objeción** por ahora.
5. Desviaciones 1-3, 6-7 del feedback-log: sin objeción del PM en esta ronda.

Los 3 beads de corrección bloquean el gate `librisk-tv6`.

---

## 2026-08-21 — Bead librisk-dbv (F1.8): Visión General como entrada default

**AX-DTR-D**: X 2 rondas (R1: 6 FAIL + 16 WARN → 22 resoluciones; R2: 22/22 RESUELTO). R: ver cierre del bead.

**Decisiones y desviaciones para el PM (se suman al gate de Fase 1):**
1. **NavCards navegables** (fila inferior de Visión General): en Mercado las card_small son informativas; aquí son atajos "Ir a <Sección> →" por mandato del propio feedback del PM ("mini-vistas hacia las demás secciones"). Componente NavCard distinto de CardMetric; el deferral F1.2 (KPIs de tira no navegables) queda intacto. Ratificar.
2. **Deltas y variaciones en neutro** en todo el overview (chip Δ% de la card VaR y panel Variación): Mercado usa rojo/verde de signo en `vision-general.png`; gana la regla del shell §4 (métricas de riesgo en neutro; semáforo solo estado de límite). Ratificar.
3. **Fila 1 sustituye las cards RF DOP/USD de Mercado** por Composición por Calificación y Exposición por Tipo de Instrumento (rating = eje primario §2). F1.10 (multi-moneda) podrá reintroducir una card de exposición USD.
4. **Sin barra de tabs en Visión General** (precedente empírico directo de Mercado); la regla "un solo pill" del shell §3 queda acotada a las demás secciones de un tab.
5. **Regla de comparabilidad de cortes** (nueva, transversal a la pantalla): si el supuesto activo difiere del supuesto del corte anterior, todos los Δ muestran N/D + tooltip. Evita Δ que mezclen efecto cartera con efecto metodológico. Candidata a regla de shell para las demás secciones en Fase 2 — confirmar alcance.
6. **Card_small Escenarios sin "último run"**: los escenarios son efímeros por sesión; la NavCard es acceso, no estado institucional.
7. **Exención de contexto de límite en Top Drivers/Variación** (§11.2): son descomposiciones del VaR Total, cuyo límite vive en la card VaR y en la tabla de límites de la misma pantalla — misma interpretación que las rejillas 2×2. Ratificar la interpretación del inviolable.
8. **Handoff §5 desactualizado** ("pantalla por defecto VaR"): sustituido por la corrección del PM; el handoff no se edita (contrato original), la sustitución queda documentada en shell §1.

---

## 2026-08-21 — Bead librisk-08x (F1.9): "Métricas de Riesgo" + as_of vs histórico

**AX-DTR-D**: X 2 rondas (R1: 7 FAIL + 8 WARN → 15 resoluciones + 3 WARN nuevos de redacción, todos incorporados; R2: 15/15 RESUELTO). R: FAIL (7 hallazgos de propagación en el journey) → corregido → PASS.

**Decisiones y desviaciones para el PM (se suman al gate de Fase 1):**
1. **Renombre aplicado**: sección "Métricas de Riesgo" (ruta `/metricas-de-riesgo/*`); "VaR" sobrevive solo como medida. El nombre "VaR/Riesgo" del Brain [guia] y del handoff §7.2 queda sustituido — candidato a brain-gap junto con F1.8.
2. **Tabs A la Fecha · Histórico** sustituyen Global · Por Calificación (excepción declarada a la regla del shell "nunca renombrar tabs pinneados": la corrección del PM la supera; hrefs actualizados en el mismo bead).
3. **Partición de contenido**: A la Fecha = barras×rating, dona (Emisor/Tipo — opción Calificación eliminada por duplicar TL), standalone vs contribución, tabla SIN columnas Var. Histórico = área apilada temporal, evolución razón Medida/VM, divergentes de cambio, tabla CON Var DOP/Var %. Volatilidad anualizada se muda a Histórico.
4. **KPI nuevo en Histórico — Δ Razón Medida/VM** en lugar del "Δ Medida vs corte anterior" del plan A (era redundante con los chips del KPI 1); atribución formal mezcla/nivel → candidata Fase 2. Ratificar.
5. **Chips CardMetric se conservan en ambos tabs** (contexto del molde, no análisis histórico); KPIs categóricos usan la variante "anterior: X". Ratificar.
6. **Marcadores verticales de cambio de supuesto** en los gráficos temporales de Histórico (la serie jamás se lee continua bajo supuestos distintos — extiende la regla de comparabilidad F1.8 a series).
7. **Beneficio de diversificación con signo**: si negativo → label "Penalización por concentración" + tooltip "VaR no es subaditivo".
8. **NavCard 3 de Visión General** renombrada "Métricas de Riesgo", destino `/metricas-de-riesgo/a-la-fecha`, cifra rotulada "VaR total del rating, DOP". Redirect de rutas viejas = detalle de implementación fuera del mock (nota para handoff a ingeniería).
9. Journey actualizado (nombres, tabs, default F1.8 en tabla Screens, orden AAA→D, top-7).

## 2026-08-21 — F1.10 aplicada (bead librisk-eed): multi-moneda DOP/USD

**Corrección PM ejecutada**: revertida la "excepción de paridad — moneda" (cartera 100% DOP). Nueva **regla transversal de moneda** en shell §4: instrumentos DOP·USD visibles (chip nivel instrumento; "Mixta" a nivel emisor) y filtrables (filtro segmentado Todas·DOP·USD); consolidación **DOP único** al TC BCRD venta del as_of (canon `Capa2_RI_Consolidacion.md` [inviolable] regla 7 — intacto: columnas nativas = denominación, no consolidación alternativa); **partición v2**: grupos DOP·USD·Total solo en columnas de VM — las medidas de riesgo jamás se parten (VaR no aditivo); TC entra al **badge de supuesto activo**; pies FX en tablas Δ y series multi-corte; **sin shock FX** (pertenece a Mercado); Overview: fila "Exposición USD" en card Portafolio.

**AX-DTR-D**: X = 2 rondas (17 ataques adoptados → PASS); R = PASS con 3 refinamientos menores aplicados (alcance de leyenda temporal, divergentes cubiertos por pie de tabla vecina como decisión declarada, TC 61.50 rotulado valor del mock).

**Para decisión del PM (anotado, NO declarado como gap)**:
1. **Posible gap del Brain**: `Capa2_RI_Consolidacion.md` regla 7 ("DOP único") fue escrita sin contemplar denominación multi-moneda visible; convendría reformular a "consolidación DOP único; denominación nativa multi-moneda visible". Requiere aprobación PM antes de declarar vía brain-gap-reporting.
2. El handoff §2 dice "la cartera real es deuda dominicana en DOP" — premisa enmendada por esta corrección del PM; "moneda base DOP" sigue intacta.

## 2026-08-21 — Feedback PM: sin "próximamente", las 8 secciones activas

El PM rechaza el patrón "futuro visible pero inactivo" para este mock: **las 8
secciones del sidebar se diseñan y prototipan todas**. Se amplía el alcance:
- Fase 1: `librisk-6rq` (F1.11 Factores de Riesgo), `librisk-yct` (F1.12
  Sensibilidades), `librisk-o07` (F1.13 Backtesting) — bloquean el gate.
- Fase 2: `librisk-vyz` (F2.7 Visión General), `librisk-7vy` (F2.8), `librisk-p1d`
  (F2.9), `librisk-6rn` (F2.10).
Pendientes de ratificación previos (overview en neutro, NavCards navegables): sin
objeción explícita aún.

## 2026-08-21 — Bead librisk-6rq (F1.11 AMPLIACIÓN PM — Factores de Riesgo activa)

**Feedback PM aplicado**: NO hay secciones "próximamente" — las 8 se diseñan todas. Factores de Riesgo activada y especificada (§12); Sensibilidades y Backtesting quedan en gris **"en diseño"** hasta sus beads (decisión X-R1#10: ítems activos sin spec serían "próximamente" encubierto).

**Decisiones y deferrals para el PM**:
1. **Correlación no es barra Euler** (§12): la atribución aditiva Σ=VaR usa 4 factores (migración·default·recovery·spread); la correlación se muestra como "Efecto correlación" incremental (VaR(ρ)−VaR(ρ=0)) en overlay + KPI 3 + heatmap. Desviación defendida del literal §8 del handoff (que lista 5 factores) — ratificación PM en el gate.
2. **Sin evolución temporal por factor**: paridad rota vs `factores-mapa.png` de Mercado, justificada (los 3 gráficos del §8 + tabla ocupan la 2×2; la serie nacería mayormente N/D bajo la regla de comparabilidad al cambiar supuestos; lo temporal vive en Métricas de Riesgo › Histórico). Candidato futuro: tab "Histórico por Factor".
3. **KPI "Probabilidad de ≥1 default"**: aporte propio (ancla handoff §3/§4, no §8 literal) — ratificación PM.
4. **NavCards de Visión General pasan de 5 a 6** (una por sección activa; crecerán a 8): desviación del conteo de card_small de Mercado — ratificación PM.
5. **TR Merton dibuja una normal** (mandato §8): es la variable latente, no la distribución de valor; subtítulo fijo anti-confusión. Fase 2 debe reforzar visualmente la distinción vs los histogramas de valor (§9.8) — deferral R-BAJO-1.
6. **Tabla breakdown sin grupos DOP/USD** (a diferencia de Mercado): F1.10 — medidas de riesgo jamás partidas por moneda.

## 2026-08-21 — Bead librisk-yct (F1.12 AMPLIACIÓN PM — Sensibilidades activa)

**AX-DTR-D**: X 2 rondas (R1: 7 FAIL + 8 WARN → todos resueltos; R2: 18/18 RESUELTO + 3 WARN nuevos resueltos en spec: N1 BL definido como Δ contribución Euler por rating — aditiva; N2 sin barra agregada "Otros" en el tornado — fila de texto; N3 filas categóricas con "—" en el lado inexistente). R: **PASS** — 1 MEDIO corregido (M-1: desviación declarada recovery "por seniority" vs handoff §8 "por rating"; ancla: handoff §3 Beta por seniority + coherencia con riel §9.3) y 3 BAJO corregidos (B-1: KPI 1/5 sobreviven al desfase badge↔barridos; B-2: mock ilustra 2 seniorities; B-3: caso ρ base ∈ set explicitado).

**Decisiones y avisos para el PM**:
1. **Frontera Escenarios/Sensibilidades**: Sensibilidades = vista sistemática precomputada del corte oficial (barridos de la metodología, no editables); Escenarios = run efímero configurable. Cross-link discreto en el TR ("Explorar un barrido configurable → Escenarios") — primera affordance de navegación en pie de panel del módulo (deferral F1.2 sobre KPIs intacto); ratificación PM en el gate.
2. **KPI "Amplitud del VaR por ρ (15%→35%)"** convive con el "Efecto correlación" de Factores (§12, VaR(ρ)−VaR(ρ=0)): definiciones distintas, distinción declarada en tooltip cruzado.
3. **CS01 / spread duration**: fuera del mock v1 (sin greeks por posición); candidato a tab futuro "CS01 / Spread".
4. **Desviación declarada**: recovery barrido por **seniority** (no "por rating" literal del §8) — ver arriba.
5. Deferral a Fase 2: estados del banner de desfase badge↔barridos y variantes visuales del tornado (happy path + 4 estados UI).

## 2026-08-21 — Bead librisk-o07 (F1.13 AMPLIACIÓN PM — Backtesting activa)

**Artefacto**: §14 de `03-wireframe-specs.md` (Backtesting › Resumen de Excepciones) + propagación (sidebar 8/8 activas, tabs §3, NavCard 8 §11.3, tabla screens, mermaid). AX-DTR-D: X 2 rondas (R1: 2 VIOLACIONES + 15 hallazgos → corregidos; R2: 17/17 RESUELTO + 6 menores incorporados) → R **PASS** (1 MEDIO + 2 BAJO corregidos en el mismo bead).

**Decisiones / tensiones para el PM**:
1. **Convención de escala del mock (registrada, no resuelta en silencio)**: el Credit VaR es de horizonte 1 año; compararlo con P&L entre cortes exige una regla de escala. El mock usa VaR escalado al horizonte entre cortes (raíz de tiempo, cortes mensuales declarados), rotulado en TL, BR y heredado al panel TR ("excepciones contadas bajo la convención de escala del mock"). **La metodología oficial del tenant gobierna** — el Brain define backtesting para VaR diario de mercado; la variante de crédito no está canonizada. *Candidato a gap del Brain (anotado; no declarado sin aprobación del PM).*
2. **Regla de sub-ventana homogénea**: Kupiec/Christoffersen/semáforo jamás cruzan un cambio de supuesto (un veredicto sobre supuestos mixtos no es auditable, §2). Ratificación PM.
3. **Semáforo de Basilea** vive solo en el panel TR como badge propio rotulado "veredicto estadístico — no es cumplimiento de límites" (Brain [inviolable]); KPI 5 sigue siendo Uso Límite; NavCard 8 muestra el veredicto como texto sin pill. El ataque X descartó ponerlo en la tira KPI (colisión posicional con la semántica de límites).
4. **Multiplicador Basilea** rotulado "(referencia ilustrativa del marco de mercado)" — no promete consecuencia de capital sobre el Credit VaR.
5. **Sin referente construido en Mercado**: `backtesting-excepciones.png` es placeholder "Contenido próximamente"; la paridad se limita a nombre de ruta/tab + molde. Layout interno = diseño propio anclado en handoff §8/§9 + Brain.
6. Marcadores de excepción por **forma** (rombo) con un único color de alerta rotulado — nunca la terna semafórica (tres rojos con tres significados quedarían en una misma pantalla).

## 2026-08-21 — Bead librisk-bql (F2.1 Design System Mapping)

- **AX-DTR-D**: X 1 ronda (5 FAIL + 8 WARN, todos integrados: partición v2 codificada por construcción en la tabla, badge de supuesto fuera de contenedores skeletonizables, DeltaBadge neutro para riesgo, Basilea rotulado, aliases de token) → R **PASS** (0 bloqueantes; 3 MEDIO + 5 BAJO corregidos post-review: filas §13 BL y §14 TR, radio 4 declarado, referencia N-26→#26, variante de banner §13, chips contiguos del badge).
- **Tensión para PM (L-9)**: Capa 1 exige IBM Plex Mono tabular para cifras; el baseline RI (excepción de rebranding) es Inter puro. El mapping usa Inter + `tabular-nums`. Migración = decisión del dueño de producto.
- **Deriva neutra del DeltaBadge**: el DeltaBadge de Mercado colorea por signo (deuda #12 del baseline reconocida por el Brain); Crédito usa variante neutra para deltas de medida. Pantalla nueva sigue el canon.
- **Gaps candidatos a brain-gap-reporting (NO declarados — requieren aprobación PM)**: (1) componentes transversales de auditabilidad sin canon (BadgeSupuestoActivo, NotaFijaMetodologica, BannerResultadosObsoletos — candidatos a retro-porte a Mercado); (2) paleta ordinal de rating inexistente en el baseline RI; (3) variante neutra de DeltaBadge no documentada. Listados en 04-design-system-mapping.md § Gaps.

## 2026-08-21 — Bead librisk-zph (F2.2 Prototipo Val Town: shell + Portafolio)

**URL viva**: https://joselier3--64f125fa9d7611f1b5491607ee4eb77e.web.val.run/

**Decisiones para el PM**:
1. **Alcance del bead vs. mandato F1.11**: la descripción del bead ("4 tabs + próximamente") es anterior a la ampliación F1.11 (8 secciones activas). Gobierna el wireframe aprobado en gate: el sidebar muestra las 8 activas; las 6 no construidas llevan placeholder "contenido en la próxima iteración del prototipo" (nota de alcance del mock, no estado de producto).
2. **Degradación del badge de supuesto** (ronda X): "Supuesto: N/D" SOLO en degradación de dataset (vacío/error); un error de panel aislado NO degrada el badge (violaría aislamiento por componente y falsearía información). Se añadió estado "Error parcial" al switcher para demostrarlo.
3. **Breadcrumb con ícono Home** (ataque X-4 rechazado): paridad empírica con producción (`Breadcrumb.tsx`, `var-global.png`) — el módulo lo nombra el título del sidebar.
4. **KPI "Límite de concentración" (Global) refleja el peor estado agregado** (HHI + límites por emisor) con referencia a Concentración — evita lectura "todo Ok" con incumplimientos por emisor vivos (hallazgo R-1). El mock muestra deliberadamente 2 incumplimientos (Ministerio de Hacienda 21.6%, BCRD 15.4% vs límite 15%) para demostrar el semáforo.
5. **Límites bajo filtro de moneda**: aviso "límites evaluados sobre el universo filtrado" en KPIs de límite (hallazgo R-4).

**Deferrals registrados (no bloqueantes)**:
- Etiquetas Δ% sobre barras con eje en $MM: paridad exacta con producción (`portafolio-global.png` hace lo mismo); se mantiene.
- Estado vacío sin botón accionable hacia el selector de dataset (la instrucción lo referencia; el selector es visible en cabecera) — candidato a mejora transversal, aplicaría también a Mercado.
- Filtro "Emisor" del panel global: en beads de secciones de riesgo evaluar deshabilitarlo o acompañarlo de la leyenda de prorrateo (ataque X-5).
- Δ HHI mostrado deriva de valores completos (no de los redondeados 4-dec); posible discrepancia visual de ±0.0001.
- MCP Playwright requiere Chrome del sistema (sin sudo); verificación hecha con chromium vía script — anotar para el entorno del loop.

## 2026-08-21 — X-phase bead librisk-qj3 (F2.3 Prototipo — Métricas de Riesgo)

Ronda 1 (14 ataques): 6 BLOQUEANTES, 4 MEDIOS, 4 MENORES. Resoluciones:
- **X1 (BLOQ, aceptado)**: tooltip "VaR no es subaditivo" era falso bajo ES (coherente/subaditiva) y Std (σ subaditiva). Corrección: tooltip condicional por medida; divF≤1 en todas las medidas del mock (beneficio siempre ≥0); el label "Penalización por concentración" solo puede activarse bajo VaR.
- **X2 (BLOQ, aceptado)**: escalares fijos ES=1.32×VaR / Std=VaR/2.55 volvían el selector cosmético (proporciones idénticas). Corrección: multiplicadores por rating — ES/VaR de 1.15 (AAA) a 1.60 (B), coherente con colas más pesadas en ratings bajos; Std/VaR también variable; divF distinto por medida.
- **X3+X4 (BLOQ, aceptado con decisión de diseño)**: el filtro Moneda aplicado al cálculo de la medida = partición prohibida por cuotas + Uso Límite engañoso. Decisión: en Métricas de Riesgo el filtro Moneda queda **deshabilitado** con nota "no aplica: las medidas de riesgo se calculan sobre la cartera consolidada"; medidas y Uso Límite siempre sobre cartera completa. Desviación del filtro transversal F1.10 registrada para el PM.
- **X5 (BLOQ, ya aplicado)**: badge de supuesto vive en la cabecera del shell, fuera del área degradable, en los 5 estados (patrón F2.2 verificado).
- **X6 (BLOQ, aceptado parcial)**: BL/BR comparan as_of (30/01) vs corte anterior (28/01) — mismo supuesto, no cruzan el marcador de 03/01. Se añade pie explícito: "cortes previos a 03/01 no comparables punto a punto (supuesto distinto)" + tooltip en marcadores. La mecánica completa de N/D por pareja de cortes queda demostrada en copy, no en datos (el mock no tiene Δs que crucen el marcador).
- **X7 (MEDIO, deferral)**: KPI 1 de Histórico duplica el Total — es mandato literal del wireframe aprobado §8.2 ("continuidad entre tabs", gate PM cerrado). Se mantiene; atacado registrado para el PM.
- **X8 (MEDIO, aceptado)**: vol anualizada con Δt promedio real de los cortes + tooltip ampliado "incluye efecto FX de la consolidación".
- **X9 (MEDIO, aceptado)**: leyenda de prorrateo del Top Driver reforzada: "…el modelo no diferencia emisores dentro del rating".
- **X10 (MEDIO, aceptado)**: Uso Límite N/D bajo ES/Std sin pill/semáforo; tooltip explícito "solo existe límite configurado para VaR — no interpretar N/D como holgura".
- **X11 (MENOR, aceptado)**: cero real = barra en 0 con etiqueta; N/D = barra ausente + marca (regla implementada aunque el mock tenga tenencias en todos los ratings).
- **X12 (MENOR, aceptado)**: chips Δ/Δ% declarados en neutro (clase trend del shell — ya neutra).
- **X13 (MENOR, aceptado)**: export de Histórico serializa el supuesto de ambos cortes.
- **X14 (MENOR, aceptado)**: Rating de mayor Δ — desempate por |Δ| y luego orden de escala; N/D bajo regla de comparabilidad.

## 2026-08-21 — R-phase bead librisk-qj3 (F2.3 Prototipo — Métricas de Riesgo)

Ronda 1: FAIL — 1 bloqueante (chip "prorr." no visible en el drill-down: artefacto de captura, la columna vivía en el overflow de la tabla; corregido con recaptura a 1920px + verificación DOM: 3 chips) + 1 MEDIO (eje Y con etiquetas duplicadas "$-1MM" en BL Histórico vista Emisor; corregido el formatter). Ronda 2: **PASS**.

Deferrals/notas para el PM de este bead:
- **Filtro Moneda deshabilitado en Métricas de Riesgo** (X-3/X-4): las medidas se calculan siempre sobre la cartera consolidada completa; el filtro queda con nota explicativa. Desviación del filtro transversal F1.10 — a validar en el gate de Fase 2.
- **KPI 1 de Histórico duplica el Total de A la Fecha** (X-7): mandato literal del wireframe aprobado §8.2 ("continuidad entre tabs"); el crítico propone sustituirlo por una lectura temporal (máx/mín o Δ acumulado). Decisión del PM.
- **Badge de supuesto en error total muestra "Supuesto: N/D"** (hallazgo INFO del revisor): confirmar si en fallo se prefiere el último supuesto conocido + marca de staleness.
- El widget "Estado del prototipo" (esquina inferior derecha) puede tapar pies de tabla en capturas — es herramienta del mock, no parte del diseño.

## 2026-08-21 — Bead librisk-hh0 (F2.4 Prototipo — Marginal)

**X adversarial (1 ronda, 20 ataques: 8 FAIL + 12 WARN — resueltos o desestimados con razón):**
- Diversificadoras: atribuidas a la *realización simulada* (coherente con la nota de granularidad §2, que ella misma atribuye diferencias por posición a la realización) — no atributo del emisor; elegidas en ratings con receptoras suficientes (BHD CD · Promerica CD) para que la redistribución intra-rating preserve exacto el subtotal por rating y el total de Métricas de Riesgo.
- Nota de granularidad anclada en los 4 puntos del §10 (pie TL, pie BR, tooltip KPI 2, export) + tooltip de cada punto del scatter.
- Cuadrantes A/B/C = anotaciones fijas del lienzo, independientes de los overlays → layout estable bajo ES/Std (donde h/hyp = N/D).
- Hipérbola y(%) = 100·límite/x (unidades verificadas visualmente: 4% en X=$200MM para límite $8MM).
- mgF ∈ [1.02, 1.10] ⇒ componental ≤ marginal ≤ standalone en contribuidoras; Σ marginales ($131.64MM) visiblemente ≠ total ($122.79MM), declarado en el glosario.
- Dos límites distintos rotulados: hipérbola = "Iso-risk (por posición)"; Uso Límite = límite de cartera $220MM.
- **Ataque desestimado (para el PM):** el crítico propuso mantener el filtro Moneda activo como filtro visual; se mantiene deshabilitado con f-note — paridad con la decisión F2.3 ya aplicada en Métricas de Riesgo (leave-one-out definido contra la cartera consolidada completa). Ratificación PM en el gate.

**R (revisor independiente): PASS.** 3 BAJO — (1) glosario ⓘ como franja visible en vez de tooltip del encabezado: desviación deliberada (definiciones críticas para leer la pantalla; mayor accesibilidad) — ratificación PM en gate; (2) hipérbola en `--sem-warn`: sigue el precedente del propio prototipo (línea de límite del HHI en Portafolio › Concentración) — declarado; (3) signo ASCII en eje Y del BL: **corregido** (signo tipográfico −).

**Tensiones/deferrals vigentes:** ratificación PM del filtro Moneda deshabilitado en Marginal; terminología "componental" (deferral F1.6 #1 sigue abierto).

## 2026-08-21 — Bead librisk-6rn (F2.10 Prototipo — Backtesting)

**Artefacto**: pantalla `#/backtesting/resumen-excepciones` desplegada sobre el mismo val (sección activada, 8ª con contenido pendiente de F2.5/F2.7–F2.9). AX-DTR-D: X 1 ronda (14 ataques: 3 bloqueantes corregidos — rótulo inviolable en el badge archivado, fecha de cambio en sábado → "efectivo corte 05/01/2026", aritmética de ventana 19→20; + formato DOP MM en BR, "4/250" reconciliado con ventana de 250, Christoffersen rotulado "conjunto χ²(2)", VaR base = constante única compartida con Métricas, N/D vigente dominante sobre el verde archivado) → R **PASS** (0 bloqueantes; 1 MEDIO condicionado a ratificación PM + 3 BAJO: snapshot actualizado, capturas con overlay del switcher, comportamiento del chip declarado abajo).

**Decisiones / desviaciones para ratificación del PM en el gate de Fase 2**:
1. **Frecuencia de cortes EOD diaria (desviación declarada del valor de mock "mensual" de §14)**: con cortes mensuales la ventana válida jamás alcanzaría 250 y TODA la pantalla quedaría en N/D permanente — inevaluable. El corte oficial de RI es EOD y el canon de backtesting del Brain es 250 cortes diarios. Solo cambia el valor ilustrativo; todas las reglas de UI de §14 se preservan y la convención va re-rotulada en TL/TR/BR.
2. **Bloque "Ventana anterior (cerrada)" en el TR (adición declarada)**: la sub-ventana previa (S&P·ρ=20%, 250 cortes, cerrada el 02/01/2026) es homogénea — su veredicto archivado (Kupiec Aceptado p=0.385 · Christoffersen Aceptado p=0.29 · zona Verde 4/250) se muestra atenuado, no colapsable, con doble rótulo ("referencia histórica, no es el veredicto vigente" + "veredicto estadístico ≠ cumplimiento de límites" [inviolable]). Sin él, el PM no podría evaluar el diseño poblado de los veredictos (la ventana vigente es 20/250 → N/D por la regla de sub-ventana homogénea, demostrada honestamente).
3. **Cambio de supuesto efectivo en corte hábil**: el marcador compartido 03/01/2026 (sábado) se rotula "efectivo corte 05/01/2026" — auditable con cortes hábiles.
4. **Comportamiento del chip "Ventana: 1 cambio de supuesto"** (R-B4, declarado): visible en ok/loading/partial; en empty/error desaparece junto al dato (no hay historia que contar) — el badge de supuesto SÍ persiste en N/D (§6 intacto).
5. **KPI 5 Uso Límite con medida VaR fija** (55.8% vs $220MM): no sigue el selector global de otras secciones; el VaR base es la misma constante que el total de Métricas de Riesgo (cuadratura por construcción).

---

## 2026-08-21 — Bead librisk-7vy (F2.8 Prototipo — Factores de Riesgo)

**Decisiones y deferrals (X ronda 1: 14 ataques — 3 bloqueantes corregidos; R: PASS, 0 bloqueantes):**
1. **VaR forzado (X bloqueante)**: la sección calcula todo con la medida canónica VaR 99%·1a (`frAgg`), inmune al selector global de Métricas/Marginal; Uso Límite propio contra el límite del VaR (55.8% — cuadra con Backtesting).
2. **Subtítulo anti-Gauss (X bloqueante)**: en el cuerpo del panel TR (capturable) y como línea "Nota" del CSV — el §2 (nunca campana de Gauss para la distribución de valor) queda blindado también en el artefacto exportado.
3. **Fuente única del VaR (X bloqueante)**: KPI 1 = Total (Σ Euler) de la tabla = $122.79MM, idéntico a Métricas de Riesgo y a la base del 55.8% de Backtesting; sin constantes duplicadas.
4. **Rama "Atribución parcial — residual no atribuido" no demostrable en el mock** (los pesos Σ=1 garantizan atribución completa y `partial` vive en TR): implementada en código (`frLeyendaTL`) pero ningún estado del switcher la dispara. Para ratificación PM.
5. **Prob ≥1 default = 14.5%** — computada de las PD de la matriz de transición mock por posición (no cifra inventada); las Z de Merton derivan de la misma matriz (coherencia por construcción).
6. **Ramas de comparabilidad implementadas pero no ejercitadas** (chips categóricos KPI 2 → N/D; tarjeta completa KPI 4 → N/D): el corte anterior del mock comparte supuesto (cambio efectivo 05/01 < 28/01), como en el resto de secciones. Flag `D.FR.prevComparable`.
7. **Dependencia hacia Visión General (F2.7)**: la NavCard 6 (§11.3) debe espejar el KPI 2 de esta pantalla (Factor dominante + % Euler desde `D.FR`/`frAgg`) con la misma regla de comparabilidad categórica.
8. **Recomendación R aplicada**: etiquetas de banda del TR escalonadas (insideTop/insideBottom alternadas en bandas estrechas); capturas re-tomadas sin el harness de estado ocluyendo la tabla.

## 2026-08-21 — Bead librisk-p1d (F2.9 Prototipo — Sensibilidades)

**Decisiones y deferrals (X ronda 1: 12 ataques — 7 bloqueantes corregidos; R: PASS):**
1. **Flag único de comparabilidad (X-1)**: `sensComparable = D.FR.prevComparable && D.SENS.publishedUnderBadge` — derivado del badge entre cortes, con precedencia declarada (publishedUnderBadge domina). La columna Var del BR hereda el mismo flag (X-2) con tooltip N/D.
2. **Pies FX con alcance declarado (X-3)**: base/barridos del corte al mismo TC del as_of; la columna Var compara |ΔVaR máx| entre cortes, cada corte a su TC (incluye efecto FX) — las dos frases del spec F1.10 conviven con ámbitos separados, sin contradicción.
3. **Límite del TR fuera de escala (X-4 — desviación deliberada del spec "línea punteada")**: con límite $220MM a $81.25MM del máximo de la curva, la línea aplastaba los 3 puntos de ρ; se declara en negrita en el pie con la holgura mínima. Para ratificación PM.
4. **Tornado en eje VaR absoluto (X-5)** con línea central "VaR base $122.79MM" (ancla del badge, §2) y **segmentos por geometría con color por dirección del input (X-6)**: en μ recovery el input − SUBE el VaR y el color sigue siendo veraz; leyenda −/+ referida al valor del supuesto, declarado en el pie.
5. **Rama badge↔barridos demostrada (X-7)**: el estado "Error parcial" del prototipo ejercita publishedUnderBadge=false — banner con CTA "Ver el corte oficial en Métricas de Riesgo →", KPIs 2–4 y paneles a N/D, KPI 1 y Uso Límite sobreviven, badge intacto.
6. **KPI 4 renombrado** "Rango del barrido de ρ (15%→35%)" (X-9) con tooltip que cita el Efecto correlación de Factores (+$27.01MM incremental) para anclar la distinción. Para ratificación PM.
7. **KPI 3 siempre 0 en el mock (X-8, aceptado)**: ningún barrido cruza $220MM (holgura mínima 81MM); conteo neutro declarado ("el semáforo vive en Uso Límite") con remisión a curva/tabla. Fixture con cruce real diferido.
8. **Signo del barrido unilateral (X-12)**: +3.6% justificado en el pie del tornado ("la matriz Moody's del mock tiene PDs speculative-grade mayores") — convención del mock, la capa de datos gobierna.
9. **Empty vs desfase de badge (X-11, aceptado)**: empty reutiliza la caja global del molde ("dataset no listo"); el desfase tiene banner y copy propios — distinguibles. 
10. **R menores**: subtítulo literal "sobre VaR base" en Uso Límite corregido; evidencia de drill BR y panel de Filtros (Moneda deshabilitada) re-capturada; 2 cosméticos declarados sin corregir (etiqueta eje X del tornado parcialmente recortada por el pie; etiqueta "base" del TR pisa la línea en algunos anchos).
11. **CS01/spread duration**: fuera del mock v1 (extensión futura declarada en spec §13) — no aparece en la UI.
12. **Dependencia hacia Visión General (F2.7)**: la NavCard 7 (§11.3) debe espejar el KPI 2 de esta pantalla (Supuesto más influyente + ΔVaR máx desde `sensAgg`) con la regla de comparabilidad categórica ("anterior: N/D" bajo supuesto distinto).

## 2026-08-21 — Bead librisk-vyz (F2.7 Prototipo Visión General) — decisiones y deferrals

1. **Comparabilidad como condición de datos (X-2)**: la regla §11 "supuesto del corte anterior distinto ⇒ todos los Δ N/D" se evalúa desde `FR.prevComparable` (dato), no desde un estado de fallo; el estado "Error parcial" del switcher solo la simula rota. Portadores de la cascada: chip Δ% de la card VaR, Δ de la NavCard Portafolio, chip "vs corte anterior" de la NavCard Sensibilidades y panel Variación (state-box propio, no hueco vacío).
2. **Medida pinneada a VaR con señal (X-3)**: "VaR — 99% · 1 año" rotulado en card 4, fila 1 de la tabla de límites, subtítulos de Top Drivers/Variación y NavCards 3/6, con tooltip "medida fija — no sigue al selector de otras secciones" (patrón §14). Verificado con Playwright: dejar ES seleccionado en Métricas no altera el overview ni pierde la selección.
3. **CCC–D sin posiciones ≠ N/D**: la card de calificación muestra "— · Sin posiciones" (exposición nula real); N/D queda reservado a dato ausente. Tooltip lo declara.
4. **Fila "Mayor emisor (% del VM)" (X-6)**: rotulada como exposición con tooltip anti-granularidad §2; la fila de riesgo marginal lleva el tooltip de "por posición, no emisor-específico".
5. **Anti-duplicación §11.3 vs tabla de límites**: la NavCard Concentración repite el HHI que vive en la fila media — la tabla explícita del wireframe aprobado (§11.3) pinnea ambos, así que se sigue el mandato literal; la regla anti-duplicación se lee contra la fila 1. Anotado para ratificación PM.
6. **Terminología de semáforo**: el overview usa la terna canónica Ok/Advertencia/Incumplimiento; la tabla por-emisor de Concentración usa Ok/Alerta/Exceso (heredada de F2.2). Divergencia terminológica menor registrada para unificación futura — no se toca trabajo cerrado.
7. **R menores declarados sin corregir**: (a) el widget "Estado del prototipo" tapa parcialmente la NavCard Backtesting en capturas full-page (no es UI del producto); (b) icono del state-box de vacío sugiere carga (heredado del molde global F2.2 — cambiarlo tocaría todas las secciones); (c) cards 2–3 en vacío colapsan a un solo N/D (conforme al spec); (d) orden del sidebar difiere del de Mercado — fijado en Fase 1 aprobada (shell §2), no es hallazgo de este bead.

## 2026-08-21 — Bead librisk-ykp (F2.5 Prototipo — Escenarios)
**AX-DTR-D**: X 1 ronda (12 ataques: 5 bloqueantes, 5 menores, 2 obs — todos corregidos adoptando las fixes propuestas por el crítico, sin nueva libertad de diseño ⇒ sin re-ataque; el R independiente verificó las correcciones) → R **PASS** (3 hallazgos de evidencia, capturas completadas: esc-recovery.png, esc-empty.png).

**Decisiones y deferrals para el PM (gate de Fase 2):**
1. **Set de ρ NO editable en este mock** — desviación declarada del wireframe §9.3 ("preset editable"). Motivo: exige modelo de interpolación de factores; anclas para la implementación real documentadas (0.78@ρ0 · 0.885@15 · 1.0@25 · 1.13@35) + tie-break del ρ-ancla del límite (ante empate, el mayor = conservador).
2. **ES escala con ρ más rápido que el VaR** (factores propios 0.86/1.0/1.17): ES/VaR sube 1.40→1.45→1.50 — coherente con "ρ engorda la cola" y con el ES total de Métricas de Riesgo en ρ base.
3. **Familia Supuesto: reparto por posición = drift uniforme intra-rating, sin jitter** — G/P% idéntico entre emisores del mismo rating (demuestra §2 en pantalla); Driver principal = mayor exposición del rating más castigado (tooltip lo declara). Nota §9.5 con 2 variantes por familia.
4. **Alcance de downgrades sin "emisores seleccionados"** (solo Global/por rating) — simplificación del mock; el wireframe §9.3 lo contempla para la implementación real.
5. **Fallo del run** demostrado desde el switcher del prototipo (checkbox meta "Fallo del run"), no desde el riel — el riel queda superficie de producto pura.
6. **Estado "Error parcial"** en Escenarios degrada solo el histograma post-run: convención de demo del switcher sin semántica de producto (defensa plausible: la distribución completa es payload separado y pesado).
7. **KPI G/P en barrido con signo tipográfico atenuado** (no rojo pleno): la lectura principal del barrido es la franja VaR/ES (§9.7) — el rojo pleno queda para shocks de libro.
8. **Error/empty globales invalidan el run** (vuelta a pre-run): el run pertenecía a un corte que ya no está — evita "mentira por composición" (cifras de run + badge N/D).

## 2026-08-21 — Bead librisk-hzu (F2.6 Auto-validación completa + verificación Playwright)
**AX-DTR-D**: X 1 ronda — 12 ataques al spec de validación (3 BLOQUEANTES: oráculos ejecutables ausentes, exención del badge de Escenarios, test operativo de granularidad emisor; 7 MEDIOS: igualdad de coherencia transversal, consola acumulada en sesión, matriz completa por aserción vs muestreo PNG, checklist de migración del 05, A6 justificado por pantalla, universo 10×5 + ciclo §9.6, anti-Gauss a nivel dato; 2 BAJOS). Todos integrados salvo: anti-Gauss a nivel dato (parcial — verificado por subtítulos + inspección visual de capturas; los datos del histograma no son accesibles desde el DOM sin instrumentar el mock) y ciclo §9.6 completo re-asertado (solo post-run re-asertado en F2.6; obsoleto/fallo quedan en evidencia F2.5) — ambos declarados como desviación.
**Ejecución**: 146 aserciones DOM sobre matriz 10 pantallas × 5 estados (144 PASS, 2 artefactos de oráculo resueltos con evidencia); 0 errores de consola en toda la sesión; 24 capturas frescas f26-*.png; B1 JTBD en 1 clic (≤3 del brief).
**R (revisor independiente): PASS** — M-1 descartado (premisa errónea: atribuyó al bead una ronda de 15 ataques inexistente; la ronda fue de 12); M-2 corregido (aserción post-run de Escenarios + f26-esc-postrun.png; hallazgo del camino: post-run el badge cambia el rótulo "Supuesto:"→"Base:→Activo:" por diseño F2.5 — verificado como plantilla §9.2 correcta, no violación); M-3 corregido (tabla de mapeo de evidencia por pantalla); B-1 diferido (B4 sin tareas medibles por rol formalizadas — la fila B4 documenta el aterrizaje por rol; formalización de tareas si el PM lo pide); B-2 corregido (bloqueantes citados por número).
**Para el PM**: el consolidado de desviaciones 1–11 vive en 05-prototype-metadata.md; B4 flag (sin superficie de Administrador en el mock). El gate [GATE-PM] de Fase 2 es el siguiente bead — nada se auto-aprueba.

## 2026-08-21 — Ampliación PM: cumplimiento NIIF 9 (Deterioro/ECL)

Evaluación de cumplimiento solicitada al PM: el mock (Credit VaR económico) NO
cubre el marco NIIF 9 de deterioro. Se agrega el handoff vinculante
`06-handoff-ifrs9-ecl.md` y la sección 9 del sidebar **Deterioro (NIIF 9)** con
tabs Staging · ECL · Movimientos · Conciliación REA:
- `librisk-k9s` F1.14 staging + clasificación AC/FVOCI/FVTPL + SICR + expedient RD
- `librisk-1ob` F1.15 ECL (PD survival, EAD, LGD PIT, EIR original, ≥3 escenarios
  macro ponderados — promedio de ECLs, no ECL del promedio)
- `librisk-arr` F1.16 roll-forward + conciliación REA ("mayor de los dos") + FVOCI/ORI
- `librisk-nqj` F2.11 prototipo; `librisk-3vd` F2.12 re-validación
Todos bloquean el gate final `librisk-ufw`.

**Gap del Brain detectado** (pendiente de aprobación del PM para declararlo):
el Brain no tiene cobertura NIIF 9/ECL — `Capa2_RI_MetodologiaCredito.md` es solo
Credit VaR; Capa 4 cubre reportería SB/SIMV pero no deterioro ni REA vs ECL.

## 2026-09-02 — Bead librisk-k9s (F1.14 Wireframe spec — Deterioro NIIF 9: Staging + Clasificación contable)

**AX-DTR-D**: X 1 ronda — 2 FAIL (criterio SICR contradictorio badge/panel → fijado ≥3 notches activo + PD×2 declarada NO activa; TR-panel vs "molde íntegro" → desviación declarada con precedente §14) + 8 WARN, todos integrados (ponderaciones de escenarios diferidas a F1.15; backstop "(refutable)" en badge; columna Expedient en BR; mini-tabla de consecuencias por stage con base de interés bruto/neto; KPIs re-plantillados; sidebar 9 ítems con orden razonado; filtros Clasificación NIIF 9 + Stage; Δ provisión = impacto en deterioro, neutro). **R: PASS** — 0 ALTA; MEDIA #1 resuelto como deferral declarado (NavCard 9 → F1.15, cuando exista la cifra ancla Provisión ECL); BAJA #4 corregido (cita "§5.7" retirada — no respaldada por el 06); BAJA #5 corregido (regla de filtro Stage × FVTPL declarada); BAJA #2/#3 aceptados (simplificación de diagrama; narrativa secuencial de la línea 6).

**Decisiones para el PM**:
1. Clasificación contable NO es tab propio: panel BL de Staging + opción "Vista por: Clasificación NIIF 9" en la dona de Portafolio (§15.2, razonado).
2. Criterio SICR cuantitativo del mock = ≥3 notches desde el origen (06 §3 lo avala como el más operable); PD×2 visible como alternativa NO activa.
3. Ítem 9 del sidebar tras Backtesting (medición → validación → traducción contable); sin equivalente en Mercado.
4. Stages en paleta secuencial neutra — Stage 3 jamás rojo (semáforo solo límite).
5. Badge de supuesto extendido con segmento NIIF 9 solo en pantallas de Deterioro; escenarios macro se suman al badge en F1.15.

**Recordatorio de gap Brain** (ya registrado 2026-08-21, sin declarar): sin cobertura NIIF 9/ECL en el Brain; este bead lo re-confirma (retrieval 2026-09-02).

## 2026-09-02 — Bead librisk-1ob (F1.15 Wireframe spec — Deterioro NIIF 9: tab ECL)

- **Artefacto**: §15.3 en 03-wireframe-specs.md (tab ECL: escenarios macro ponderados como elemento central, KPI "Convexidad de escenarios" con ambos números, mecánica PD/EAD/LGD/EIR original auditable, tabla por posición con cuadre Σ=KPI 1) + badge seccional único de Deterioro completado con "3 escenarios (60/25/15)" (resuelve deferral WARN 3 de F1.14) + NavCard 9 en §11.3 (resuelve deferral R#1 de F1.14) + mermaid (nodo DTE expandido, 9 NavCards).
- **X ronda 1 — 6 FAIL + 6 WARN, todos integrados**: (1) comparabilidad extendida — ponderaciones/set de escenarios forman parte del supuesto activo; badge distinto → todos los Δ del tab N/D; (2) badge seccional único idéntico entre Staging y ECL; (3) guardarraíl anti-Gauss en curvas PD (render escalonado + subtítulo "no es la distribución de valor"); (4) KPI 2 con signo visible, neutro forzado, tooltip anti-malinterpretación; (5) footer de conciliación en BR + política de EIR proxy (jamás tasa de mercado); (6) TL declarado desviación del molde (precedente §14/§15 TR) con macro RD colapsable; (7) descomposición por escenario auditable (tooltip KPI 1 + columnas expandibles BR); (8) TR con apilado de exactamente 2 segmentos, toggle reemplaza no multiplica; (9) BL "vista pedagógica — no afecta KPIs"; (10) nota de frontera fija en el TL; (11) columna PD = "acumulada del horizonte, escenario base" con tooltip; (12) KPI 4 cobertura sobre costo amortizado, no VM.
- **R: PASS** (aceptación completa + invariantes 00 §2/§6/§10 + coherencia con §15.1/§9/§12/§13). Observación menor #1 corregida (inbound §15.3: NavCard 9 aterriza en Staging). Observación #2 sin acción (redacción ya hedged).
- **Decisiones para el PM (gate)**: valores del mock — probabilidades 60/25/15, variables macro ilustrativas, seniorities senior/subordinada; escenarios contables no editables en UI (gobernanza del tenant); política de EIR proxy pendiente de metodología real.
- **Pendiente**: F1.16 (Movimientos + Conciliación REA) — última pieza NIIF 9 antes de reabrir F2.

## 2026-09-02 — Bead librisk-arr (F1.16 — Deterioro NIIF 9: tabs Movimientos + Conciliación REA + FVOCI/ORI)

**X ronda 1 — 7 FAIL + 5 WARN, todos integrados**:
1. FAIL: BR de ambos tabs → jerárquicas rating→emisor→instrumento con agregados por nivel.
2. FAIL: badge seccional explícito e idéntico en ambos tabs (REA no agrega segmento).
3. FAIL: comparabilidad alineada con §15.3 — Δ de KPIs 2–4, BL y columna Δ del BR = N/D bajo divergencia de badge; el waterfall se renderiza como desviación declarada (roll-forward contable, ancla 06 §7) con bucket rotulado + ⚑.
4. FAIL: nota fija anti-suma-de-máximos en BR de conciliación; sin columna "gobierna" por instrumento.
5. FAIL: ámbito REA-sobre-FVOCI declarado (mock: AC+FVOCI por política del tenant, ⚑; norma SB del contrato de datos — gap ya registrado 2026-08-21).
6. FAIL: invariantes de cuadre obligatorias e incluidas en export (waterfall = KPI 2 = Σ BL = Σ Δ BR; bridge = KPI 4; Σ BR = KPIs 1/2).
7. FAIL: unidades rotuladas — sankey "VM (DOP MM)" vs waterfall "Provisión (DOP MM)" + nota "magnitudes distintas que no cuadran entre sí".
8. WARN: paleta secuencial neutra del sankey fijada en spec (Stage 3/Bajas jamás rojo).
9. WARN: sufijo "(VM, DOP)" en KPIs 3/4 de Movimientos.
10. WARN: precedente citado para el TR-panel de Conciliación (§14 TR, §15.1 TR).
11. WARN: selector de corte solo define comparación — KPI 1 pinneado jamás muta.
12. WARN: denominador del % de diferencia declarado (% sobre REA, subtítulo + tooltip).

**R — PASS**; 3 hallazgos menores corregidos: cita del tope de categorías §10→§4; "badge as_of" en nodo DTM del mermaid; separación explícita de los dos regímenes del waterfall (divergencia metodológica vs dato ausente).

**Decisiones del mock para ratificación del PM en el gate**: mapeo rating→categoría A-E y % REA por categoría son valores del mock (⚑, norma SB no está en el Brain — gap pendiente de aprobación); "mayor de los dos" evaluado a nivel cartera; ámbito REA = AC+FVOCI.

## 2026-09-02 — Bead librisk-nqj (F2.11 Prototipo Deterioro NIIF 9) — AX-DTR-D

**X (adversarial, 1 ronda, 7 FAIL + 5 WARN — todos integrados pre-implementación):**
1. FAIL Waterfall sin altas/bajas → buckets explícitos Altas/Bajas; la alta es pseudo-posición del corte actual en TODOS los tabs (Σ tabla = KPI 1 se preserva).
2. FAIL Filtros vs cifra pinneada → KPIs siempre globales; nota visible "Filtro activo — KPIs y cuadres sobre el universo completo"; footers declaran "Σ (sin filtro) = KPI".
3. FAIL Sin descuento EIR → EIR original mock por posición + DF=(1+EIR)^(−T/2); 2 posiciones con proxy documentada ⚑ (no "N/D" autocontradictorio).
4. FAIL Convexidad no garantizada → assert en código + Δ anotado entre ambas líneas; la convexidad del mock es +0.36% (pequeña y HONESTA: el ECL lo domina una posición en default, insensible a fPD) — ambas cifras y el Δ visibles, labels des-superpuestos.
5. FAIL Barras con signo → color neutro único; dirección por posición vs eje cero + etiqueta.
6. FAIL Partial contradice cuadres → régimen "cuadre SUSPENDIDO — badge distinto ⚑ (no es un descuadre)" en pantalla y CSV; ⚑ en bucket Cambio de medición.
7. FAIL PD12=0 → no aplica: FR.TRANS tiene columna D (PD 0.01%–22.73%).
8. WARN badge string vs comparabilidad → comparabilidad gobernada por estado (partial), no por igualdad de texto; un solo badge (mandato §15).
9. WARN FVOCI balance → VM siempre bruto; chip ORI + tooltips + fila fija de doble registro.
10. WARN plug del bridge → forward-looking y lifetime COMPUTADOS del dato; LGD/EIR fracciones mock ⚑; residual rotulado "base regulatoria (% fijo REA) — residual del mock ⚑" (es el driver económico real: % fijo REA ≫ pérdida esperada del modelo).
11. WARN simetría sin cura S3→S2 → nota fija en el sankey "cura S3→S2: sin casos en el corte — el staging es simétrico (06 §2)".
12. WARN interés sobre neto S3 → mini-tabla de consecuencias (TR Staging) + tooltip del chip S3.

**Decisiones declaradas:** convención notches del mock 1 letra = 3 notches (chip "escala del mock" + tooltip); "lifetime vs 12m" del bridge excluye Stage 3 (PD=1 en ambos horizontes); fila fija FVOCI al pie de la tabla de conciliación en vez de subtotal por clasificación (la jerarquía canónica rating→emisor→instrumento gana — desviación menor declarada); en Movimientos/Conciliación los filtros afectan la tabla BR (los paneles de cuadre son del universo completo por invariante); "vs corte a elegir" no interactivo (mock: solo corte anterior).

**R (revisor independiente): PASS.** Verificó pinneo $78.53MM en 4 tabs, cuadre waterfall 66.83 = KPI 2, bridge cierra con KPI 4 (−51.50), 5 estados, paleta neutra, filtros con KPIs inmutables. 3 menores no bloqueantes: (1) empty sin CTA (patrón del shell heredado — igual en todo el mock); (2) redondeo de etiquetas BL ±0.01 (el cuadre se cumple en el dato); (3) charts canvas sin capa accesible (observación para producción).

**Gap Brain (ya registrado 2026-08-21, sigue pendiente de PM):** norma REA SB (categorías A-E, %, mapeo de inversiones) sin cobertura — todos los valores REA del mock van ⚑.

## 2026-09-02 — Bead librisk-3vd (F2.12 Re-validación final incluye NIIF 9 + metadata) — AX-DTR-D

**X (adversarial, 1 ronda, 12 FAIL + 8 WARN — todos integrados al spec antes de ejecutar):** oráculos endurecidos: badge COMPLETO (no solo sufijo NIIF 9), pinneo 78.53 por selector de KPI, cuadres aritméticos con signo (+66.83 waterfall / −51.50 bridge, endpoints leídos de la opción ECharts), paleta anti-rojo vía opciones ECharts (canvas invisible al hex-scan DOM — limitación declarada y cubierta), PD uniforme por rating×base×T, provisión-sin-USD en headers, filtros que filtran de verdad (Stage=3: 9→4 filas + FVTPL fuera), régimen partial de Movimientos asertado, deep-link frío, CSVs descargados y asertados, controles nuevos F2.11, negativos con rutas enumeradas, y metadata con desviaciones NIIF 9 fusionadas al gate (12–19) + B4 re-mapeado sobre Deterioro.

**D:** `prototype-captures/f212-validate.mjs` → `f212-results.json`: **283 checks = 282 aserciones PASS + 1 exención declarada** (formato-MM Escenarios pre-run, re-asertada post-run), **0 errores de consola**, B1 = 1 clic. Capturas `f212-*` (4 tabs éxito, estados de Staging, partial de Movimientos, filtro Stage=3, Escenarios post-run, B1). Hallazgos de implementación resueltos durante el dev-loop: overlay del drawer interceptaba clics (cierre forzado); `page.goto` solo-hash es same-document (reset de filtros exigió `reload()` real); tablas de pantallas ocultas contaminaban los selectores (scope a `offsetParent !== null`); las "divergencias" iniciales de PD eran PD acumuladas a madurez efectiva — la clave correcta es rating×base×T (invariante se cumple: 0 conflictos); pseudo-posición de alta resuelta vía `IFRS.ALTA`.

**R: FAIL ronda 1 → PASS ronda 2.** R1: 3 ALTA (ok() incondicional en FVTPL; PD vacuo con 0 claves + cifra fabricada "28 claves" en metadata; "46→4" contradicho por el JSON) + 2 MEDIA (granularidad reclamada sin oráculo → declarada heredada de F2.6; tautologías por .catch) + 2 BAJA — todos corregidos con re-ejecución. R2: PASS; 2 residuales corregidos en el mismo bead (R2-1 cifra 19→20 claves; R2-2 toggle TL con existencia+efecto asertados, re-run 282/282).

**Estado del gate:** la sección "Re-validación final F2.12" de 05-prototype-metadata.md es la validación vigente: A1–A6 PASS, B1–B3 PASS, B4 flag PM, desviaciones 1–11 (F2.6) + 12–19 (NIIF 9) para ratificación. **Gap Brain NIIF 9/norma REA SB sigue registrado (2026-08-21) y pendiente de aprobación del PM — no declarado.**

## 2026-09-02 — Feedback PM (revisión del prototipo, gate final)

El mock está demasiado text-heavy: exceso de texto explicativo visible en las
gráficas. Corrección integral: patrón transversal InfoButton ⓘ — lo explicativo
se esconde detrás de "más información" por panel; visible solo título, ejes,
valores, badges y estados. Fuera de eso, el PM está conforme. → bead librisk-8yh (F2.13),
bloquea el gate final librisk-ufw.

## 2026-09-02 — F2.13 Corrección PM: reducción integral de densidad de texto (bead librisk-8yh)
- **Feedback PM (gate final)**: el mock es demasiado text-heavy; las gráficas cargan párrafos explicativos visibles.
- **Aplicado**: patrón transversal InfoButton ⓘ / InfoPopover en las 14 pantallas — todo pie de panel, leyenda metodológica, caveat y nota de granularidad movido detrás de UN ⓘ por panel (popover a 1 clic, portal al body, ARIA disclosure). Textos no eliminados: popover + líneas "Nota" en los exports CSV (ya presentes, verificado). Visible queda: títulos, ejes/series, valores, badges de estado, pills, banners de estado y la nota del empty-state del simulador (anti dead-end).
- **Decisiones**: (1) el PM sancionó explícitamente "1 clic" para los inviolables §2 (prorrateo/granularidad) — el ataque adversarial que exigía micro-copy visible queda overruled por instrucción PM; se conservan los chips cortos `prorr.` en tabla y KPI Top Driver. (2) CTA "Explorar → Escenarios" extraído a línea visible — jamás enterrado. (3) Banner de alcance de Deterioro (1 línea) se mantiene visible como excepción declarada.
- **Deferrals para PM**: (a) paridad del patrón ⓘ hacia la sección Mercado en producción — fuera del alcance del mock, decidir en handoff; (b) micro-textos de KPIs de Sensibilidades (no son gráficas) — candidatos opcionales al mismo patrón.
- **Evidencia**: prototype-captures/f2.13/ (before/after ×4 pantallas + popover abierto). Review independiente: PASS.
