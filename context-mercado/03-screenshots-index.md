# Índice de screenshots — Mercado (stack local, 2026-08-20, viewport 1600px, full-page)

Login: app local `http://localhost:3000`. Datos reales (dataset `calc-submit
1782766289`, as_of 30/01/2026). El nav superior muestra los módulos **Mercado ·
Liquidez · Crédito · Operacional** — Crédito aparece DESHABILITADO: ahí vivirá
esta sección.

| Captura | Ruta | Qué observar para Crédito |
|---|---|---|
| `vision-general.png` | `/dashboard/mercado/vision-general` | resumen ejecutivo: fila de KPIs + tabla + charts + fila de 5 card_small |
| `var-global.png` | `/var-y-es/global` | **el molde de referencia**: columna izquierda de 5 KPI cards (VaR Global $139.30MM, % VM, vs corte anterior, Top Driver, Uso Límite N/D), área apilada temporal, dona componental, barras de cambio, tabla de descomposición DOP/USD; tabs pill; badge "Datos 30/01/2026"; selector dataset; Filtros |
| `var-renta-fija.png` | `/var-y-es/renta-fija` | misma plantilla recortada a una clase; pie + stacked area |
| `var-marginal.png` | `/var-y-es/marginal` | equivalente Mercado de la sección Marginal de Crédito |
| `portafolio-global.png` | `/portafolio/global` | composición y concentración (equivalente de Portafolio Crédito) |
| `portafolio-concentracion.png` | `/portafolio/concentracion-prudencial` | heatmap/pyramid/scatter de concentración |
| `factores-mapa.png` | `/factores-de-riesgo/mapa-de-factores` | mapa de factores (equivalente futuro: migración/default/correlación/recovery/spread) |
| `sensibilidades-duracion.png` | `/sensibilidades/renta-fija-duracion` | patrón de sensibilidades (futuro: tornado de supuestos) |
| `escenarios-impacto-riesgo.png` | `/escenarios/impacto-en-riesgo` | panel de configuración de shock + comparación base/shock |
| `backtesting-excepciones.png` | `/backtesting/resumen-excepciones` | excepciones + semáforo |

Rutas completas de la sección (39): ver `../../mercado_routes.txt`.
