# Fase 4: GIS y Detección de Alertas

## Objetivo

Implementar lógica de alertas y análisis geoespacial sobre la telemetría de drones.

## Componentes clave

- Reglas de alertas (batería, zona, velocidad, etc.)
- Funciones GIS en BigQuery
- Escritura de alertas a Cloud Storage

## Pasos detallados

1. Definir reglas de alertas en `config/alert_rules.yaml`
2. Implementar lógica de alertas en el pipeline
3. Calcular distancias y zonas con funciones GIS
4. Escribir alertas a Cloud Storage

## Buenas prácticas

- Mantén reglas de alertas configurables
- Usa tipos GEOGRAPHY en BigQuery
- Documenta cada regla implementada

## Evidencias

_Agrega ejemplos de alertas generadas y queries GIS_

---
