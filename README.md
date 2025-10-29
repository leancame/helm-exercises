## Ejercicios de Helm para iniciarse en el Mundo de DevOps

¡Bienvenido/a a los ejercicios básicos de Helm para iniciarse en el mundo de DevOps!

Este repositorio contiene una serie de ejercicios diseñados para ayudarte a familiarizarte con los conceptos básicos de Helm. 
Los ejercicios están diseñados para ser completados en un entorno local o en un clúster de Kubernetes, y cubren temas relevantes como son la gestión y creación de charts de Helm.

## Objetivos

El propósito principal de estos ejercicios es proporcionarte una introducción práctica a los conceptos clave de Helm que son esenciales para cualquier persona interesada en trabajar en el área de DevOps. Al completar estos ejercicios, esperamos que adquieras experiencia práctica con:

- Uso de repositorios.
- Despliegue de charts con archivo de valores
- Gestión de releases.
- Creación de charts. Uso de templates y archivo de valores.
- Uso de condiciones, bucles y operaciones.
- Uso de funciones.

## Estructura del Repositorio

Este repositorio está organizado de la siguiente manera:


- El directorio `enunciados/` contiene los ejercicios propuestos en este repositorio. Cada archivo proporciona una descripción detallada de los objetivos del ejercicio, así como instrucciones paso a paso sobre lo que se espera que completes.
- El archivo `ASSIGMENT.md` proporciona instrucciones sobre cómo enviar tus soluciones una vez que completes los ejercicios.
- El directorio `soluciones/` será el lugar donde almacenar las soluciones a los ejercicios.
- El directorio `auxiliar/` (opcional) contiene los archivos necesarios para completar los ejercicios. Puedes incluir scripts, archivos de configuración, archivos de texto para edición, etc.
- El directorio `datos/` (opcional) contiene conjuntos de datos u otros archivos de entrada que pueden ser necesarios para los ejercicios.
- El archivo `CONTRIBUTING.md` proporciona instrucciones sobre cómo contribuir al repositorio.

## Estructura del directorio `soluciones/`
Las soluciones a los ejercicios deben respetar la siguiente estructura *mínima* para lograr una correcta entrega de todos los elementos y facilitar las correcciones a los tutores. Los ejercicios que no respeten esta estructura *mínima*, serán considerados como `no entregados`. Si considera que debe agregar algún fichero o directorio a la estructura, puede hacerlo, siempre que la original esté presente.
```
Ejercicio01
    └── README_ej01.md
Ejercicio02
    └── README_ej02.md
Ejercicio03
    ├── README_ej03.md
    └── values.yaml
Ejercicio04
    ├── README_ej04.md
    ├── values.yaml
    └── <nombre-del-chart>
        └── ... archivos del chart ...
Ejercicio05
    ├── README_ej05.md
    ├── values.yaml
    └── <nombre-del-chart>
        └── ... archivos del chart ...
Ejercicio06
    ├── README_ej06.md
    ├── values.yaml
    └── <nombre-del-chart>
        └── ... archivos del chart ...
Ejercicio07
    ├── README_ej07.md
    └── <chart-empaquetado>.tgz
```

## Contribución

¡Tus contribuciones son bienvenidas! Si tienes ideas para nuevos ejercicios o mejoras para los existentes, no dudes en abrir un issue o abrir un pull request.
