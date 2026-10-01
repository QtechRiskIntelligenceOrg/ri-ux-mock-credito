# UX/UI Plan — Sección Crédito (tracker interno)

Fase 1 (skill uxui-phase1-research-wireframes):
1. [x] F1.1 Brain context + brief estructurado (`01-structured-brief.md`, `brain-context-snapshot.md`) — bead librisk-gyz, AX-DTR-D completo (X: 2 FAIL corregidos; R: PASS)
2. [x] F1.2 User journey (`02-user-journey.md`) — bead librisk-xo9, AX-DTR-D completo (X: 2 rondas; R: PASS)
3. [x] F1.3 Wireframe specs + diagrama (`03-wireframe-specs.md`, `03-wireframe-diagram.mermaid`)
   - [x] F1.3a Shell: navegación + molde transversal — bead librisk-8ag, AX-DTR-D completo (X: 2 rondas, 2 FAIL corregidos; R: PASS)
   - [x] F1.4 Spec Portafolio (tabs Global · Concentración) — bead librisk-2v2, AX-DTR-D completo (X: 2 rondas, 2 FAIL corregidos; R: PASS)
   - [x] F1.5 Spec VaR/Riesgo (tabs Global · Por Calificación) — bead librisk-a66, AX-DTR-D completo (X: 1 ronda, 0 FAIL 8 WARN resueltos; R: PASS)
   - [x] F1.7 Spec Escenarios (tab Impacto en Riesgo, arquetipo simulador) — bead librisk-iq9, AX-DTR-D completo (X: 2 rondas, 2 FAIL corregidos; R: PASS)
   - [x] F1.6 Spec Marginal (tab Global, scatter iso-risk) — bead librisk-mvx, AX-DTR-D completo (X: 2 rondas, 4 FAIL corregidos; R: PASS)
   - [x] F1.8 CORRECCIÓN PM: Visión General activa como entrada default (§11 + shell §1/§2/§3 + mermaid) — bead librisk-dbv, AX-DTR-D completo (X: 2 rondas, 6 FAIL corregidos, 22/22 RESUELTO; R: FAIL→correcciones→PASS)
   - [x] F1.9 CORRECCIÓN PM: sección "Métricas de Riesgo" + tabs A la Fecha · Histórico (§8 rehecho; shell/journey/diagrama propagados) — bead librisk-08x, AX-DTR-D completo (X: 2 rondas, 7 FAIL + 11 WARN resueltos; R: FAIL→correcciones journey→PASS)
   - [x] F1.10 CORRECCIÓN PM: multi-moneda (revertir excepción 100% DOP) — bead librisk-eed, AX-DTR-D completo (X: 2 rondas, 17 ataques adoptados → PASS; R: PASS + 3 refinamientos menores aplicados)
4. [ ] [GATE-PM] Aprobación de Fase 1 (brief + journey + wireframes)

Fase 2 (skill uxui-phase2-prototype) — bloqueada por el gate:
5. [ ] Design System mapping (`04-design-system-mapping.md`)
6. [ ] Prototipo Val Town + auto-validación (`05-prototype-metadata.md`)
7. [ ] [GATE-PM] Aprobación del prototipo

## Bead librisk-6rq — F1.11 Wireframe spec Factores de Riesgo (2026-08-21)
1. [x] A — Brain re-fetch MetodologiaCredito + evidencia factores-mapa.png; spec en snapshot
2. [x] X — adversarial 2 rondas (4 FAIL + 8 WARN → 13/13 RESUELTO)
3. [x] D — §12 Factores de Riesgo + shell §2/§3/§4 + NavCard 6 §11.3 + screens + mermaid
4. [x] T — checklist 9/9 (aceptación bead, §2/§6/§10, F1.10, coherencia shell/mermaid)
5. [x] R — revisor independiente: PASS; 3 MEDIO corregidos, 2 BAJO diferidos (feedback-log)
6. [x] Doc — snapshot, feedback-log, status, uiux-plan
- [x] F1.12 (librisk-yct) — Wireframe spec Sensibilidades (activa): §13 + shell §2/§3 + NavCard 7 §11.3 + screens + mermaid; frontera Escenarios/Sensibilidades declarada; X 2 rondas + R PASS. 2026-08-21

## Bead librisk-o07 — F1.13 Wireframe spec Backtesting (2026-08-21)
1. [x] A — Brain re-verificado (fetch nuevo `Capa2_RI_MetodologiaMercado.md` [guia] + regla de interfaz [inviolable]); evidencia: placeholder de Mercado, solo ruta
2. [x] X — 2 rondas (R1: 17 ataques, 2 VIOLACIONES; R2: 17/17 RESUELTO + N1–N6 incorporados)
3. [x] D — §14 + propagación (sidebar, tabs, NavCard 8, screens, mermaid)
4. [x] T — checklist aceptación bead + §2/§6/§10 + output contract skill
5. [x] R — PASS (1 MEDIO + 2 BAJO corregidos)
6. [x] Doc — status / feedback-log / snapshot / plan

- [x] F2.1 Design system mapping (04-design-system-mapping.md) — bead librisk-bql, 2026-08-21

## Bead librisk-zph (F2.2) — 2026-08-21
1. [x] A — Spec del prototipo (snapshot addendum; referencia visual: dataset context-mercado)
2. [x] X — Ataque adversarial (1 ronda, 19 hallazgos: 15 integrados, 1 rechazado con evidencia, deferrals registrados)
3. [x] D — Val Town joselier3/ri-credito-mock: shell + Portafolio Global/Concentración + 5 estados + filtro moneda + export CSV
4. [x] T — Verificación Playwright (11 capturas; 0 errores de consola; fixes: serie histórica, markline límite, ticks HHI)
5. [x] R — Revisor independiente: PASS (4 MEDIOS corregidos, 6 BAJOS: 3 corregidos, 3 diferidos)
6. [x] Doc — 05-prototype-metadata.md, status.md, feedback-log.md, prototype-captures/
- [x] F2.3 (librisk-qj3) — Prototipo Métricas de Riesgo: selector VaR·ES·Std funcional (datos, no layout), tabs A la Fecha + Histórico, 5 estados, drill-down con chip prorr., marcadores de cambio de supuesto, export por medida. AX-DTR-D: X 1 ronda (14 ataques) → R FAIL→PASS (2 rondas). Capturas en prototype-captures/mr-*.png.
- [x] F2.4 (librisk-hh0) — Prototipo Marginal: scatter iso-risk con hipérbola/cuadrantes/fallen angels, dona componental + diversificadoras, ranking divergente con signo, tabla 3 niveles rating→emisor→instrumento, KPIs §10.1, glosario ⓘ, selector de medida, export, 5 estados. Σ componental = total de Métricas (coherencia). AX-DTR-D: X 1 ronda (20 ataques) → R PASS (3 BAJO: 1 corregido, 2 declarados). Capturas f24-marginal-*.png.
- [x] F2.10 Backtesting — Resumen de Excepciones (bead librisk-6rn): pantalla desplegada, X 1 ronda, R PASS, capturas bt-*.png
- [x] F2.8 Factores de Riesgo — Mapa de Factores (bead librisk-7vy): pantalla desplegada (barras Euler + overlay incremental, Merton con selector 7 ratings, heatmap ρ uniforme, tabla factor→rating exportable), datos coherentes (VaR $122.79MM ≡ Métricas/Backtesting; PD y Z derivadas de una matriz de transición única), X 1 ronda (14 ataques, 3 bloqueantes corregidos) → R PASS, capturas fr-*.png
- [x] F2.9 Sensibilidades — Supuestos (bead librisk-p1d): tornado OAT+CRN en eje VaR absoluto (6 barras, dos neutros por dirección del input, unilateral fuente →Moody's), curva VaR vs ρ {15/25/35} con marcador base y límite declarado fuera de escala, Δ contribución Euler por rating con selector supuesto+extremo, tabla de barridos exportable con drill supuesto→rating; rama badge↔barridos demostrada como estado "Error parcial"; filtro Moneda deshabilitado. AX-DTR-D: X 1 ronda (12 ataques: 7 bloqueantes corregidos) → R PASS (5 menores: 3 corregidos con evidencia, 2 cosméticos declarados). Capturas sens-*.png
- [x] F2.7 Visión General — entrada default (bead librisk-vyz): pantalla overview §11 desplegada (4 cards resumen · tabla de límites 6 columnas + Top Drivers prorrateado + Variación divergente por rating · 8 NavCards navegables), medida pinneada a VaR 99%·1a sin contaminar el selector de otras secciones, 5 estados con "Error parcial" = comparabilidad de cortes rota. AX-DTR-D: X 1 ronda (12 ataques: 6 bloqueantes corregidos) → R PASS (2 menores + 2 cosméticos declarados). Capturas ov-*.png
- [x] F2.5 Escenarios — Impacto en Riesgo (bead librisk-ykp): arquetipo simulador desplegado (riel persistente Libro/Supuesto con Aplicar/Reiniciar y línea de consolidación TC; sidebar auto-colapsado; badge 6 plantillas §9.2; KPIs VM Pre/Post·G/P·Driver; divergentes P&L por rating; histograma multimodal anti-Gauss con minimapa + zoom + Comparar ρ; waterfall top-7+Otros; tabla rating→emisor→instrumento exportable con nota §9.5 por familia; franja VaR/ES por ρ con límite — **aceptación: barrido 15/25/35 comparativo presente**; ciclo §9.6 completo + fallo de run desde el switcher). Fuente única VaR $122.79MM ≡ Métricas/FR/SENS/BT. AX-DTR-D: X 1 ronda (12 ataques: 5 bloqueantes corregidos) → R PASS (3 huecos de evidencia completados). Capturas esc-*.png

## Bead librisk-hzu (F2.6) — 2026-08-21
1. [x] A — Spec de validación (corpus re-verificado 00dfc7c8353bacaf; re-fetch PlataformaUX + MetodologiaCredito sin cambios sustantivos; universo 10×5 + ciclo §9.6)
2. [x] X — 12 ataques (3 bloqueantes → oráculos DOM ejecutables; 2 deferrals declarados)
3. [x] D — Script f26-validate.mjs: 146 aserciones (144 PASS + 2 artefactos resueltos), 0 errores de consola, 24 capturas f26-*.png, B1 en 1 clic
4. [x] T — Grupo A (A1–A6) PASS, Grupo B B1–B3 PASS, B4 flag PM; invariantes §2/§6/§10 con oráculo
5. [x] R — PASS (M-2/M-3/B-2 corregidos; M-1 descartado con evidencia; B-1 diferido)
6. [x] Doc — 05-prototype-metadata.md consolidado (desviaciones 1–11 para el gate), feedback-log, status

## Bead librisk-k9s (F1.14 — Deterioro NIIF 9: Staging + Clasificación contable) — 2026-09-02
1. [x] A — Brain re-verificado (sin cobertura NIIF 9/ECL — gap ya registrado; fuente vinculante: 06-handoff-ifrs9-ecl.md §1–§3); spec en snapshot
2. [x] X — 1 ronda (2 FAIL + 8 WARN → 10/10 integrados; re-ataque delegado a R)
3. [x] D — §15 Deterioro (NIIF 9) tab Staging + §15.2 decisión clasificación contable + propagación (línea 6, sidebar 9 ítems, tabs §3, badge/filtros §4, dona §7.1, screens, mermaid DT/DTS)
4. [x] T — checklist 9/9 (aceptación bead + handoff 00 §2/§6/§10 + handoff 06 §1–§3 + propagaciones)
5. [x] R — PASS (0 ALTA; 1 MEDIA → deferral declarado NavCard 9 a F1.15; 2 BAJA corregidos, 2 aceptados)
6. [x] Doc — snapshot, feedback-log, status, uiux-plan

## Bead librisk-1ob (F1.15 — Deterioro NIIF 9: tab ECL) — 2026-09-02
1. [x] A — Spec en brain-context-snapshot (Brain re-verificado: sin cobertura NIIF 9; fuente 06 §4–§5)
2. [x] X — ataque adversarial: 6 FAIL + 6 WARN integrados (1 ronda)
3. [x] D — §15.3 + badge seccional + NavCard 9 §11.3 + mermaid
4. [x] T — checklist aceptación + invariantes 00 §2/§6/§10 (ver snapshot)
5. [x] R — revisor independiente: PASS (menor #1 corregida)
6. [x] Doc — status/feedback-log/plan

## Bead librisk-arr (F1.16 — Deterioro NIIF 9: Movimientos + Conciliación REA + FVOCI/ORI) — 2026-09-02
1. [x] A — Brain re-verificado (sin cobertura REA/ECL; fuente 06 §1/§6/§7); spec en brain-context-snapshot.md
2. [x] X — ataque adversarial: 7 FAIL + 5 WARN integrados
3. [x] D — §15.4 (Movimientos) + §15.5 (Conciliación REA) en 03-wireframe-specs.md; línea 6 Parte 12; mermaid DTM/DTR
4. [x] T — checklist en brain-context-snapshot.md (aceptación a/b/c + handoff 00 §2/§6/§10 + 06 + cuadres)
5. [x] R — PASS; 3 menores corregidos
6. [x] Doc — status, feedback-log, uiux-plan

## Bead librisk-nqj — F2.11 Prototipo Deterioro NIIF 9 (2026-09-02)
- [x] A: spec de implementación (brain-context-snapshot) sobre §15.1–15.5 + 06
- [x] X: 7 FAIL + 5 WARN integrados (1 ronda)
- [x] D: 4 tabs en el val (data.js IFRS + app.js módulo Deterioro + estilos); sidebar 9 ítems; NavCard 9; filtros; 4 exports CSV
- [x] T: Playwright chromium — 4 tabs × 5 estados, 0 errores consola; cuadres y pinneo verificados por DOM; capturas f211-*
- [x] R: PASS (3 menores documentados)
- [x] Doc: 05-prototype-metadata, feedback-log, status, uiux-plan

## Bead librisk-3vd — F2.12 Re-validación final (incluye NIIF 9) + metadata (2026-09-02)
1. [x] A: spec de oráculos (Brain re-consultado corpus 8b3bd636c070fe38; sondeo DOM vivo)
2. [x] X: 12 FAIL + 8 WARN integrados (1 ronda)
3. [x] D: f212-validate.mjs — 283 checks, 282 PASS + 1 skip, 0 console errors; capturas f212-*
4. [x] T: checklist aceptación bead + invariantes 00 §2/§6/§10 + contrato skill Fase 2
5. [x] R: FAIL→PASS (2 rondas; 3 ALTA + 2 MEDIA + 2 BAJA R1 y 2 residuales R2 corregidos)
6. [x] Doc: 05 (validación vigente, desviaciones 1–19), status, feedback-log

## Bead librisk-8yh — F2.13 Corrección PM densidad de texto (2026-09-02)
1. [x] A: inventario de texto explicativo + spec del patrón ⓘ (brain-context-snapshot)
2. [x] X: 5 BLOCKER + 9 MAJOR + 4 MINOR — integrados / 2 overruled por instrucción PM (1 ronda)
3. [x] D: applyInfoPattern() + CSS en el val (app.js/styles.css); chip prorr. en KPI; info-keep; extracción CTA
4. [x] T: Playwright — 14/14 pantallas 0 notas visibles, interacción completa del popover, 0 errores; capturas before/after
5. [x] R: PASS; hallazgo .mr-nota corregido y re-verificado
6. [x] Doc: 03-wireframe-specs (§4 patrón nuevo), 05-prototype-metadata, status, feedback-log
