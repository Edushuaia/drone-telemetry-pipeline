# 🚁 Pipeline Serverless de Telemetría de Drones - Proyecto Educativo

[![Shield-style badge displaying Google Cloud Platform branding with the text Google Cloud in white letters on a vibrant blue rectangular background, accompanied by the multicolored GCP hexagonal logo on the left side](https://img.shields.io/badge/Google%20Cloud-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white)](https://cloud.google.com/)
[![Apache Beam](https://img.shields.io/badge/Apache%20Beam-FF6F00?style=for-the-badge&logo=apache&logoColor=white)](https://beam.apache.org/)
[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![IoT](https://img.shields.io/badge/IoT-Real--Time-green?style=for-the-badge)](README.md)

## 🎓 Extensión del Pipeline Serverless: IoT Avanzado

Este proyecto es una **evolución natural** del [Pipeline Serverless de Streaming](https://github.com/Edushuaia/streaming-serverless-pipeline), aplicando la misma arquitectura a un caso de uso IoT más complejo: **telemetría de drones en tiempo real**.

### 🔗 Conexión con el Proyecto Base

| Aspecto | Proyecto Base (Transacciones) | Este Proyecto (Drones) |
| --------- | ------------------------------- | ------------------------ |
| **Arquitectura** | Pub/Sub → Dataflow → BigQuery | Pub/Sub → Dataflow → BigQuery + Cloud Storage |
| **Complejidad de Datos** | 4 campos simples | 15+ campos multi-sensor |
| **Volumen** | ~1.5 msg/seg | ~10 msg/seg (múltiples drones) |
| **Geoespacial** | ❌ No | ✅ Sí (GPS, rutas, zonas) |
| **Alertas** | ❌ No | ✅ Sí (batería, zona, velocidad) |
| **Visualización** | BigQuery console | Looker Studio + Mapas GIS |

## 📚 Contexto Educativo

Proyecto de investigación que explora cómo las arquitecturas serverless pueden aplicarse a **sistemas IoT complejos** con múltiples sensores, datos geoespaciales y requisitos de baja latencia para alertas críticas.

### 🔬 Motivación Científico-Tecnológica

Los drones modernos (investigación científica, monitoreo ambiental, agricultura de precisión) generan flujos continuos de telemetría desde múltiples sensores. Este proyecto explora:

- **Procesamiento multi-sensor**: GPS, IMU, batería, cámara
- **Análisis geoespacial en tiempo real**: Rutas, zonas de seguridad, puntos de interés
- **Detección de anomalías**: Batería crítica, pérdida de señal, zona restringida
- **Escalabilidad IoT**: De 1 drone a flotas de 100+

### 🎯 Desafío Investigado

**¿Cómo procesar telemetría de múltiples drones con latencia < 3 segundos, detectar situaciones críticas automáticamente, y visualizar trayectorias en tiempo real sin infraestructura dedicada?**

## 📋 Descripción

Pipeline de procesamiento de telemetría IoT en tiempo real que:

- ✅ **Ingiere datos de múltiples drones** simultáneamente
- ✅ **Procesa 15+ campos por mensaje** (GPS, batería, velocidad, altitud, etc.)
- ✅ **Detecta alertas críticas** (batería < 20%, zona restringida, velocidad excesiva)
- ✅ **Almacena telemetría histórica** en BigQuery con tipos geoespaciales (GEOGRAPHY)
- ✅ **Genera estadísticas por ventanas** de tiempo (60 segundos)
- ✅ **Visualiza rutas en mapas** interactivos con Looker Studio

**Capacidades Técnicas:**

- ✅ **Latencia ultra-baja** < 3 segundos end-to-end
- ✅ **Autoescalado** para flotas de 1 a 100+ drones
- ✅ **Procesamiento geoespacial** con BigQuery GIS
- ✅ **Sistema de alertas** basado en reglas configurables
- ✅ **Logging estructurado** por drone_id
- ✅ **Simulador realista** de trayectorias de vuelo

## 🏗️ Arquitectura

```text
┌──────────────┐      ┌──────────────┐      ┌──────────────┐      ┌────────────┐
│  Simulador   │─────▶│ Cloud Pub/Sub│─────▶│Cloud Dataflow│─────▶│  BigQuery  │
│  de Drones   │ JSON │  (telemetry) │Stream│ Apache Beam  │ Batch│  + GIS     │
│  (N drones)  │      │              │      │              │      │            │
└──────────────┘      └──────────────┘      └──────┬───────┘      └────────────┘
                                                     │
                                                     ├─ FixedWindow(60s)
                                                     ├─ Detección de Alertas
                                                     ├─ Agregación por drone_id
                                                     └─ Cálculo de Rutas
                                                     
                                            ┌────────┴────────┐
                                            │ Cloud Storage   │
                                            │ (alertas JSON)  │
                                            └─────────────────┘
```

### Componentes

| Servicio | Función | Novedad vs Proyecto Base |
| -------- | ------- | ------------------------ |
| **Cloud Pub/Sub** | Buffer de mensajes de telemetría | Topic con múltiples publishers (1 por drone) |
| **Cloud Dataflow** | Procesamiento y detección de alertas | Lógica geoespacial + reglas de alertas |
| **BigQuery** | Data Warehouse con columnas GEOGRAPHY | Tipos geoespaciales para coordenadas |
| **Cloud Storage** | Almacenamiento de alertas críticas | Nuevo: archivos JSON de alertas por timestamp |
| **Looker Studio** | Visualización de rutas en mapas | Nuevo: dashboards con mapas interactivos |

## 🛠️ Tecnologías

- **Google Cloud Platform (GCP)**
  - Cloud Pub/Sub
  - Cloud Dataflow
  - BigQuery (con BigQuery GIS)
  - Cloud Storage
  - Looker Studio
- **Apache Beam 2.x** (Python SDK)
- **Python 3.8+**
- **Shapely** para geometrías (puntos, polígonos)
- **JSON** para telemetría

## 📋 Datos de Telemetría

### Estructura del Mensaje

```json
{
  "drone_id": "DRONE_001",
  "timestamp": "2025-12-18T14:23:45.123Z",
  "latitude": 40.416775,
  "longitude": -3.703790,
  "altitude_m": 120.5,
  "speed_kmh": 35.2,
  "battery_percent": 67,
  "signal_strength": -45,
  "temperature_c": 28.3,
  "heading_degrees": 180,
  "vertical_speed_ms": 2.1,
  "flight_mode": "AUTO",
  "mission_id": "MISSION_2025_001",
  "operator_id": "OP_123",
  "camera_active": true,
  "payload_weight_kg": 2.5
}
```

### Campos Geoespaciales

- **latitude, longitude**: Coordenadas WGS84
- **altitude_m**: Altura sobre el nivel del mar
- **heading_degrees**: Rumbo (0-360°, 0=Norte)

## 🚀 Configuración Rápida

### 1. Clonar el repositorio

```bash
git clone https://github.com/tu-usuario/drone-telemetry-pipeline.git
cd drone-telemetry-pipeline
```

### 2. Instalar dependencias

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 3. Configurar variables de entorno

```bash
cp .env.example .env
nano .env  # Configurar PROJECT_ID, REGION, etc.
```

### 4. Crear infraestructura GCP

```bash
# Habilitar APIs
gcloud services enable dataflow.googleapis.com pubsub.googleapis.com bigquery.googleapis.com

# Crear Topic de Pub/Sub
gcloud pubsub topics create drone-telemetry

# Crear Dataset de BigQuery con soporte GIS
bq mk --dataset --location=US ${PROJECT_ID}:drone_warehouse
```

### 5. Ejecutar simulador de drones

```bash
python drone_simulator.py --num-drones 5 --duration 300
```

### 6. Desplegar pipeline a Dataflow

```bash
python dataflow_pipeline.py \
  --project=${PROJECT_ID} \
  --region=us-central1 \
  --runner=DataflowRunner \
  --temp_location=gs://${BUCKET}/temp/ \
  --staging_location=gs://${BUCKET}/staging/
```

## 📊 Casos de Uso

1. **Monitoreo de Flotas**: Control en tiempo real de múltiples drones
2. **Alertas de Seguridad**: Notificaciones automáticas por batería baja o zonas restringidas
3. **Análisis de Rutas**: Optimización de trayectorias de vuelo
4. **Mantenimiento Predictivo**: Detección de anomalías en temperatura o velocidad
5. **Investigación Científica**: Recolección de datos ambientales georeferenciados

## 🎓 Aprendizajes vs Proyecto Base

### Nuevos Conceptos Aplicados

- **BigQuery GIS**: Tipos GEOGRAPHY, funciones ST_GeogPoint, ST_Distance
- **Procesamiento Multi-Entidad**: Agregaciones por drone_id con GroupByKey
- **Detección de Anomalías**: Reglas de negocio en DoFn
- **Cloud Storage para Eventos**: Escritura de alertas en JSON
- **Windowing Avanzado**: Sesiones por drone + ventanas fijas
- **Enriquecimiento de Datos**: Cálculo de distancia recorrida, velocidad promedio

### Complejidad Incremental

| Métrica | Transacciones | Drones | Factor |
| ------- | ------------ | ------ | ------ |
| Campos por mensaje | 4 | 15 | 3.75x |
| Procesamiento geoespacial | No | Sí | ♾️ |
| Múltiples outputs | No | Sí (BQ + Storage) | 2x |
| Reglas de negocio | 0 | 5+ | ♾️ |
| Visualización | Básica | Mapas GIS | 🚀 |

## 📚 Documentación

- [Arquitectura Detallada](docs/ARQUITECTURA.md)
- [Guía de Desarrollo](docs/DESARROLLO.md)
- [Evidencias del Proyecto](docs/EVIDENCIAS.md)
- [Comparación con Proyecto Base](docs/COMPARACION.md)

## 🔗 Proyecto Base

Este proyecto extiende: [Pipeline Serverless de Streaming en GCP](https://github.com/Edushuaia/streaming-serverless-pipeline)

## 📧 Contacto

Eduardo Villena Lozano | [LinkedIn](https://linkedin.com/in/tu-perfil) | [GitHub](https://github.com/Edushuaia)

---

**🎓 Proyecto Educativo** | Apache License 2.0
