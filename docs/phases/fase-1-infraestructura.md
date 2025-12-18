# Fase 1: Infraestructura Base en GCP

## Objetivo

Provisionar todos los recursos necesarios en Google Cloud Platform para soportar el pipeline de telemetría de drones.

## Recursos a crear

- Proyecto GCP y billing
- Service Account con permisos mínimos
- Pub/Sub topic y subscription
- Dataset y tabla en BigQuery (con schema GIS)
- Bucket en Cloud Storage

## Pasos detallados

1. Crear proyecto y habilitar billing
2. Crear Service Account y asignar roles
3. Crear Pub/Sub topic y subscription
4. Crear dataset y tabla en BigQuery usando `config/bigquery_schema.json`
5. Crear bucket en Cloud Storage

## Comandos útiles

```bash
gcloud projects create ...
gcloud pubsub topics create ...
bq mk ...
gsutil mb ...
```

## Buenas prácticas

- Usa nombres descriptivos y consistentes
- Aplica principio de mínimo privilegio en IAM
- Documenta cada recurso creado

## Evidencias

### Agrega capturas de pantalla o logs de consola aquí

---
