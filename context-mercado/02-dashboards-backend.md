# Backend — risk-intelligence-dashboards (evidencia explore, 2026-08-20)

## Qué es

**Microservicio FastAPI (Python, puerto 8001)** que genera los dashboards como
JSON/opciones ECharts (**pyecharts**) consumidas por el front vía REST. El layout
de cada pantalla lo decide el BACKEND (`components[]` con `chart_type`); el front
solo posiciona con su mapa de grid.

- Entry: `main.py`; API: `src/api/routers/dashboard_endpoints.py` (`GET /dashboards/list`, `GET/POST /dashboards/{id}`, regeneración por componente).
- Registro: decorador `@register_dashboard(page_id, section, ...)` en `src/application/dashboard_management/dashboard_registry.py`.
- Generadores genéricos: `src/application/chart_generators/` (bar, pie, line, scatter, heatmap, waterfall, stacked_area, timeseries, cards, tables).
- Docs: `docs/prd/dashboards-prd.md`, `docs/prd/appendix-b-dashboard-api-contract.md`, `docs/COMPONENTES_DISPONIBLES.md`.

## Dashboards de mercado (`src/application/dashboards/`)

| Sección | page_id | Archivo | Contenido |
|---|---|---|---|
| general | `vista-general` | `vision_general/vision_general_dashboard.py` | Cards VaR/CVaR totales, card Backtesting, toggle VaR/CVaR/ES |
| var | `global`, `renta-fija`, `renta-variable` | `var/var_*.py` | VaR/CVaR con selector VaR↔CVaR |
| var | `marginal`, `tabla-marginal` | `var/var_marginal.py` | VaR marginal |
| var | `comparativa-metodologica` | `var/var_comparativa_metodologica.py` | comparación entre metodologías |
| sensibilidad | dv01/duración/convexidad | `sensibilidad/sensibilidad_*.py` | sensibilidades RF |
| factores-de-riesgo | contribución, fx, tasas, mapa | `factores_de_riesgo/factores_*.py` | contribución al VaR por factor |
| escenarios | impacto riesgo / P&L | `escenarios/escenarios_impacto_*.py` + `scenario_compute.py` | ΔVaR/ΔCVaR, `delta_gamma_impact` |
| portafolio | global, RF/RV, MTM, concentración | `portafolio/portafolio_*.py` | composición, MTM, concentración |

## Estado de CRÉDITO — clave para el mock

- **Nada implementado**, pero la arquitectura lo anticipa:
  - `src/application/dashboards/view_profiles/_profile.py:7` — el sistema de **view profiles** está diseñado explícitamente para **reutilizar secciones entre market ↔ credit** (solo cambia measure, ejes, columnas). Punto de extensión natural para CreditMetrics.
  - `portafolio/portafolio_tabla_renta_fija.py:709-820` y `..._renta_variable.py:726-776` — ya existe columna **"Calificación Crediticia"** en tablas de posiciones (solo visual).
  - No existe nada de CreditMetrics, migración, PD, matriz de transición.
- **Implicación para el mock:** el camino real de implementación será nuevos
  `ViewProfile`s de crédito + generadores genéricos existentes. El mock debe ser
  plausible bajo ese patrón backend-driven (chart_types del catálogo del front).

## Datos

- **Data Management Service** (`:8002`, httpx): fuente principal de datasets (`src/api/services/data_management_client.py`).
- **libriskanalytics** (git privada): analítica; seam único en `src/application/dashboards/engine_views.py` (fact frame → `PortfolioComposition` → `portfolio_analysis` → tidy frame; `marginal_risk.sensitivities.delta_gamma_impact`).
- Platform (`:8000`) auth; Redis cache de layouts. Contratos cross-repo: `docs/prd/appendix-a-cross-repo-contracts.md`.
