# Handoff 2 — Implementación de IFRS 9 (Deterioro / ECL) para cartera de inversión

> **Propósito**: marco regulatorio-metodológico VINCULANTE para la sección
> **Deterioro (NIIF 9)** del mock de Crédito. Entregado por el PM 2026-08-21.
> Complementa (no sustituye) `00-handoff-metodologico.md`: el Credit VaR responde
> el riesgo económico; esta sección responde la provisión contable ECL.

## 1. Alcance: qué instrumentos entran

El modelo de deterioro aplica según la clasificación (test SPPI + modelo de negocio):
- **Costo amortizado (AC)**: aplica ECL completo, afecta P&L.
- **FVOCI**: aplica ECL, pero la provisión va contra ORI, no reduce el valor en
  balance (el activo sigue a fair value). El deterioro se reconoce en resultados
  y se compensa en ORI.
- **FVTPL**: NO aplica ECL — el riesgo de crédito ya está capturado en el fair value.

Para una cartera de inversión típica (bonos soberanos, corporativos, letras), lo
usual es AC o FVOCI, así que ECL sí aplica.

## 2. El modelo de tres stages

Eje: **SICR** (Significant Increase in Credit Risk) desde el reconocimiento inicial.

| Stage | Condición | ECL a reconocer | Ingreso por interés |
|---|---|---|---|
| 1 | Sin SICR (riesgo bajo o no deteriorado) | ECL a **12 meses** | Sobre valor bruto |
| 2 | SICR pero sin default | ECL **lifetime** | Sobre valor bruto |
| 3 | Deteriorado / default (impaired) | ECL **lifetime** | Sobre valor **neto** (bruto − provisión) |

Puntos finos:
- **Low credit risk expedient (5.5.10)**: instrumento con bajo riesgo a la fecha
  de reporte (típicamente investment grade) → puede asumirse sin SICR y quedarse
  en Stage 1. **Ojo RD**: el soberano dominicano es sub-investment grade
  (BB−/Ba3 aprox.) — el expedient NO es automático; exige juicio documentado o
  definición propia de "low credit risk".
- El movimiento entre stages es **simétrico** (Stage 2 → 1 si el riesgo mejora).

## 3. Definición de SICR — el punto más subjetivo

- **Cuantitativo (primario)**: PD lifetime a la fecha vs. PD lifetime esperada al
  origen para el plazo remanente — cambio RELATIVO, no PD absoluta. Umbrales:
  multiplicador de PD (se duplica) o cambio en bps ajustado por plazo.
  Alternativa práctica: deterioro de N notches de rating desde el origen.
- **Backstop obligatorio**: presunción refutable de 30 días de mora → SICR
  (en bonos bullet rara vez se activa antes del default).
- **Cualitativo**: watchlist, cambio de outlook, breach de covenants, deterioro
  sectorial/soberano.
- Para cartera de inversión con pocos emisores, el enfoque por rating/notch suele
  ser más operable que un modelo de PD relativa fino.

## 4. Cálculo del ECL — mecánica

ECL = valor presente de las pérdidas crediticias esperadas, ponderado por escenarios.

ECL = Σ_t [ PD_marginal(t) × EAD(t) × LGD(t) × DF(t) ]

- **PD marginal por período**: probabilidad de default en t condicional a
  sobrevivir hasta t; se construye desde curvas de PD acumulada (survival). 12m
  ECL usa solo el primer año; lifetime, toda la vida remanente.
- **EAD**: saldo esperado (amortized cost) en cada fecha futura, con devengados.
  Bullet ≈ estable; amortizable se proyecta.
- **LGD**: severidad, por colateral/seniority; **point-in-time y forward-looking**,
  no through-the-cycle.
- **DF**: descuento a la **EIR original** (tasa efectiva del reconocimiento
  inicial), NO a tasa de mercado actual — error frecuente.
- Forma simplificada (survival): S(t) y PD_marginal(t) = S(t−1) − S(t).

## 5. Forward-looking + escenarios macroeconómicos

- PD/LGD incorporan información prospectiva.
- **Mínimo 3 escenarios** (base, adverso, favorable) con probabilidades. ECL final
  = **promedio ponderado de los ECL de cada escenario — NO el ECL del escenario
  promedio** (la no linealidad importa).
- Overlays macro: PD/LGD ligadas a variables (PIB, desempleo, tasas, FX, commodities).
- **Para RD**: PIB, tipo de cambio DOP/USD (descalce), tasa de política BCRD, y
  para el soberano el acceso a mercados externos. Calibración difícil por escasez
  de defaults locales → proxies regionales / benchmarks de soberanos comparables.

## 6. Retos de implementación (dónde suele fallar)

- **Curvas de PD lifetime sin historia**: derivarlas de matrices de transición
  (elevar la matriz anual a la potencia t, cuidando la absorción del default).
- **Mapeo escala nacional → PD global**: la escala nacional comprime el riesgo
  relativo doméstico; usarla cruda infla la calidad crediticia.
- **LGD soberana local**: casi sin data; supuestos benchmark documentados.
- **EIR original**: almacenarla por instrumento desde el origen (legacy no la guarda).
- **Consistencia con normativa SB (REA)**: la entidad regulada corre AMBOS
  cálculos (provisión REA por categorías A-E y ECL NIIF 9) y explica la
  diferencia; NIIF prevalece para reporte financiero, el regulatorio exige el
  mínimo REA. Gestionar el "mayor de los dos" / conciliación es trabajo real.
- **FVOCI**: doble registro (fair value en balance, ECL en ORI).

## 7. Arquitectura de referencia (módulos)

1. **Motor de staging**: clasifica 1/2/3 según reglas SICR configurables.
2. **Librería de curvas de PD**: término, marginal, survival, por rating/emisor.
3. **Módulo LGD**: por seniority/colateral, con downturn adjustment.
4. **Proyección de EAD**: amortización + devengados.
5. **Overlay macro / escenarios**: liga PD/LGD a variables, pondera escenarios.
6. **Motor de descuento a EIR original**.
7. **Reporte**: ECL por stage, roll-forward de stages, conciliación REA, sensibilidades.
