# **Ejercicio 03: Desplegando Nginx en Kubernetes con Helm**

## Objetivo

El objetivo de este ejercicio es que los estudiantes aprendan a desplegar un chart de Helm utilizando un archivo `values.yaml`, facilitando configuraciones específicas y permitiendo un despliegue flexible para aplicaciones en Kubernetes.

## Enunciado

En este ejercicio, deberás desplegar el chart `bitnami/nginx`, configurando todos los elementos necesarios a través de un archivo `values.yaml`.

### Requisitos del despliegue:

1. **Descargar e instalar** el chart `bitnami/nginx` utilizando el comando que aparece en la documentación (en `artifacthub.io`).

1. **Crear un archivo `values.yaml`**: Debe incluir todas las configuraciones necesarias para el despliegue, tales como:
   - Usar la imagen por defecto, pero en su versión `1.26.1-debian-12-r0`.
   - Desplegar 3 réplicas.
   - La estrategia de actualización debe ser `Recreate`.
   - Desactivar `livenessProbe` y `readinessProbe`.
   - Cambiar el puerto HTTP del servicio al `8081`.
   - Habilitar la creación de un ingress, con el host en `prueba.nginx`.

1. **Actualizar** el chart desplegado, utilizando el fichero `value.yaml`.

1. **Verificar** que lo requerido en el value, fue desplegado con éxito.
## Entregables

- El archivo `values.yaml` creado para el despliegue.
- Un README explicando todo el proceso y adjuntando imágenes.
