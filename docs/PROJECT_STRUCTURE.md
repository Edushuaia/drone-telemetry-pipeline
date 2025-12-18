# 📁 Estructura del Proyecto: Pipeline Serverless de Telemetría de Drones

Este documento describe la organización profesional del proyecto, la función de cada carpeta y archivo principal, y los próximos pasos para el desarrollo y documentación.

---

## 🌳 Árbol de Directorios

drone-telemetry-pipeline/
├── .github/
│   └── workflows/
│       └── ci.yml                    # Pipeline CI/CD con GitHub Actions
├── config/
│   ├── bigquery_schema.json          # Esquema de tabla BigQuery (con GIS)
│   └── alert_rules.yaml              # Configuración de reglas de alertas (por crear)
├── docs/
│   ├── phases/                       # Documentación de cada fase del proyecto
│   │   ├── fase-1-infraestructura.md
│   │   ├── fase-2-simulador.md
│   │   ├── fase-3-pipeline.md
│   │   ├── fase-4-gis-alertas.md
│   │   ├── fase-5-optimizacion.md
│   │   ├── fase-6-looker.md
│   │   └── fase-7-testing.md
│   ├── guides/                       # Guías adicionales (deployment, troubleshooting)
│   ├── images/                       # Diagramas e imágenes
│   ├── index.md                      # Página principal de la documentación educativa
│   ├── ARQUITECTURA.md               # Arquitectura detallada
│   ├── DESARROLLO.md                 # Guía de desarrollo
│   ├── EVIDENCIAS.md                 # Evidencias del proyecto
│   ├── COMPARACION.md                # Comparación con proyecto base
│   └── PROJECT_STRUCTURE.md          # Este archivo
├── scripts/
│   ├── setup_gcp.sh                  # Script de setup de recursos GCP
│   ├── deploy_dataflow.sh            # Deploy del pipeline
│   ├── create_bigquery_table.sh      # Crear tabla en BigQuery
│   └── run_simulator.sh              # Ejecutar simulador
├── src/
│   ├── __init__.py
│   ├── simulator/
│   │   ├── __init__.py
│   │   ├── drone_simulator.py        # Simulador de drones
│   │   ├── trajectory_generator.py   # Generador de trayectorias
│   │   └── telemetry_message.py      # Modelo de mensaje
│   ├── pipeline/
│   │   ├── __init__.py
│   │   ├── dataflow_pipeline.py      # Pipeline principal de Dataflow
│   │   ├── transforms.py             # Transformaciones de Beam
│   │   ├── alert_detection.py        # Lógica de alertas
│   │   └── gis_functions.py          # Funciones geoespaciales
│   └── utils/
│       ├── __init__.py
│       ├── config.py                 # Carga de configuración
│       ├── logging_config.py         # Configuración de logging
│       └── validators.py             # Validaciones de datos
├── tests/
│   ├── __init__.py
│   ├── unit/
│   │   ├── __init__.py
│   │   ├── test_simulator.py
│   │   ├── test_transforms.py
│   │   ├── test_alert_detection.py
│   │   └── test_gis_functions.py
│   └── integration/
│       ├── __init__.py
│       └── test_pipeline.py
├── .env.example                      # Plantilla de variables de entorno
├── .gitignore                        # Archivos ignorados por Git
├── CONTRIBUTING.md                   # Guía de contribución
├── LICENSE                           # Licencia Apache 2.0
├── README.md                         # Documentación principal
├── requirements.txt                  # Dependencias Python
└── setup_project.sh                  # Script de setup inicial

```
drone-telemetry-pipeline/
├── .github/
│   └── workflows/
│       └── ci.yml                    # Pipeline CI/CD con GitHub Actions
├── config/
│   ├── bigquery_schema.json          # Esquema de tabla BigQuery (con GIS)
│   └── alert_rules.yaml              # Configuración de reglas de alertas (por crear)
├── docs/
│   ├── phases/                       # Documentación de cada fase del proyecto
│   │   ├── fase-1-infraestructura.md
│   │   ├── fase-2-simulador.md
│   │   ├── fase-3-pipeline.md
│   │   ├── fase-4-gis-alertas.md
│   │   ├── fase-5-optimizacion.md
│   │   ├── fase-6-looker.md
│   │   └── fase-7-testing.md
│   ├── guides/                       # Guías adicionales (deployment, troubleshooting)
│   ├── images/                       # Diagramas e imágenes
│   ├── index.md                      # Página principal de la documentación educativa
│   ├── ARQUITECTURA.md               # Arquitectura detallada
│   ├── DESARROLLO.md                 # Guía de desarrollo
│   ├── EVIDENCIAS.md                 # Evidencias del proyecto
│   ├── COMPARACION.md                # Comparación con proyecto base
│   └── PROJECT_STRUCTURE.md          # Este archivo
├── scripts/
│   ├── setup_gcp.sh                  # Script de setup de recursos GCP
│   ├── deploy_dataflow.sh            # Deploy del pipeline
│   ├── create_bigquery_table.sh      # Crear tabla en BigQuery
│   └── run_simulator.sh              # Ejecutar simulador
├── src/
│   ├── __init__.py
│   ├── simulator/
│   │   ├── __init__.py
│   │   ├── drone_simulator.py        # Simulador de drones
│   │   ├── trajectory_generator.py   # Generador de trayectorias
│   │   └── telemetry_message.py      # Modelo de mensaje
│   ├── pipeline/
│   │   ├── __init__.py
│   │   ├── dataflow_pipeline.py      # Pipeline principal de Dataflow
│   │   ├── transforms.py             # Transformaciones de Beam
│   │   ├── alert_detection.py        # Lógica de alertas
│   │   └── gis_functions.py          # Funciones geoespaciales
│   └── utils/
│       ├── __init__.py
│       ├── config.py                 # Carga de configuración
│       ├── logging_config.py         # Configuración de logging
│       └── validators.py             # Validaciones de datos
├── tests/
│   ├── __init__.py
│   ├── unit/
│   │   ├── __init__.py
│   │   ├── test_simulator.py
│   │   ├── test_transforms.py
│   │   ├── test_alert_detection.py
│   │   └── test_gis_functions.py
│   └── integration/
│       ├── __init__.py
│       └── test_pipeline.py
├── .env.example                      # Plantilla de variables de entorno
├── .gitignore                        # Archivos ignorados por Git
├── CONTRIBUTING.md                   # Guía de contribución
├── LICENSE                           # Licencia Apache 2.0
├── README.md                         # Documentación principal
├── requirements.txt                  # Dependencias Python
└── setup_project.sh                  # Script de setup inicial
```

---

## 📂 Descripción de Carpetas y Archivos

### `.github/workflows/`

Automatización de CI/CD con GitHub Actions: testing, linting, build y cobertura.

### `config/`

Archivos de configuración para el pipeline:

- `bigquery_schema.json`: Esquema de la tabla de telemetría en BigQuery (incluye campos GEOGRAPHY).
- `alert_rules.yaml`: Reglas de alertas configurables (por crear).

### `docs/`

Documentación completa del proyecto:

- `phases/`: Una guía detallada para cada fase del desarrollo.
- `guides/`: Guías adicionales (deployment, troubleshooting, monitoring).
- `images/`: Diagramas de arquitectura, flujos y ejemplos.
- `index.md`: Página principal de la documentación educativa.
- Otros archivos: arquitectura, desarrollo, evidencias, comparación.

### `scripts/`

Automatización de tareas:

- `setup_gcp.sh`: Provisionar recursos en GCP.
- `deploy_dataflow.sh`: Desplegar el pipeline a Dataflow.
- `create_bigquery_table.sh`: Crear la tabla de telemetría.
- `run_simulator.sh`: Ejecutar el simulador de drones.

### `src/`

Código fuente del proyecto:

- `simulator/`: Simulador de drones, trayectorias y generación de mensajes.
- `pipeline/`: Pipeline de Dataflow, transformaciones, lógica de alertas y funciones GIS.
- `utils/`: Utilidades compartidas (configuración, logging, validaciones).

### `tests/`

Suite de tests:

- `unit/`: Tests unitarios de componentes individuales.
- `integration/`: Tests de integración end-to-end del pipeline.

### Archivos raíz

- `.env.example`: Plantilla de variables de entorno.
- `.gitignore`: Exclusiones para Git.
- `CONTRIBUTING.md`: Guía para contribuir.
- `LICENSE`: Licencia Apache 2.0.
- `README.md`: Documentación principal y resumen del proyecto.
- `requirements.txt`: Dependencias Python.
- `setup_project.sh`: Script para crear la estructura inicial del proyecto.

---

## 📝 Convenciones y Buenas Prácticas

- __Documentación__: Cada fase y componente debe estar documentado en `docs/`.
- __Variables de entorno__: Usar `.env` (basado en `.env.example`) para configuración sensible.
- __Testing__: Mantener cobertura >80% y ejecutar tests en cada push/PR.
- __CI/CD__: Automatización con GitHub Actions.
- __Licencia__: Apache 2.0 para todo el código y documentación.

---

## 🚦 Próximos Pasos

1. __Documentar cada fase__ en `docs/phases/` (infraestructura, simulador, pipeline, GIS, optimización, visualización, testing).
2. __Completar archivos de configuración** en `config/` (alert_rules.yaml, etc.).
3. __Desarrollar scripts de automatización__ en `scripts/`.
4. __Implementar y documentar el código fuente__ en `src/`.
5. __Mantener y ampliar la suite de tests__ en `tests/`.
6. __Actualizar la documentación__ en `README.md` y `docs/index.md` conforme avance el proyecto.

---

## 📚 Referencias

- [README.md](../README.md)
- [Google Professional Data Engineer Exam Guide](https://cloud.google.com/certification/data-engineer)
- [Pipeline Serverless de Streaming (proyecto base)](https://github.com/Edushuaia/streaming-serverless-pipeline)

---

__Actualizado:__ 18 de diciembre de 2025  
__Autor:__ Eduardo Villena Lozano
