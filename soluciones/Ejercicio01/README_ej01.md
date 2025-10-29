## Solución al Ejercicio 01: Explorando Helm Charts en Artifact Hub

### Instrucciones

1. Accede al sitio web de [Artifact Hub](https://artifacthub.io/).
2. Busca un *Helm chart* de tu interés (por ejemplo, **nginx**, **postgresql**, **prometheus**, entre otros).
3. Responde las siguientes preguntas basándote en la información que encuentres en la página del *Helm chart* seleccionado.

---
## Resolución

## **Parte 1: Información Principal del Chart**

1. **Nombre del Chart y Mantenedor**  
   - ¿Cuál es el nombre del *chart* y quién es el mantenedor?

    He decidido usar el chart de Nginx cuyo mantenedor es Bitnami (https://artifacthub.io/packages/helm/bitnami/nginx).

2. **Descripción del Chart**  
   - ¿Cuál es la descripción general del *chart*? ¿Para qué sirve esta aplicación o servicio?

    La descripción general de este chart es una definición de Ngnix comentando que es de código abierto, un servidor web, pudiendo ser utilizado como proxy inverso, balanceador de carga y caché HTTP. También comenta su recomendación para sitios web con alta demanda por su capacidad.

3. **Versión del Chart**  
   - ¿Cuál es la versión más reciente del *chart* disponible?
   
   La versión mas reciente del chart es la 20.0.2

4. **Versiones de Aplicaciones Soportadas**  
   - ¿Qué versiones de la aplicación soporta este *chart* (es decir, la versión de la aplicación subyacente)?

    La versión de la aplicación subyacente es la 1.28.0.

---

## **Parte 2: Sección de Instalación**

5. **Comandos de Instalación**  
   - ¿Cuál es el comando principal para instalar este *chart* utilizando *Helm*?
    
    El comando es ``helm install my-release oci://REGISTRY_NAME/REPOSITORY_NAME/nginx`

6. **Repositorio del Chart**  
   - ¿En qué repositorio se encuentra alojado este *chart*? Proporciona la URL del repositorio.

    El repositorio se encuentra alojado en `https://github.com/bitnami/charts/tree/main/bitnami/nginx`

7. **Versión de Helm requerida**  
   - ¿Cuál es la versión mínima de *Helm* que se necesita para instalar este *chart*?
   
   La versión minima de Helm requerida es la 3.8.0+

---

## **Parte 3: Valores Predeterminados (Default Values)**

8. **Archivo de Valores Predeterminados**  
   - ¿Qué opciones de configuración aparecen en el archivo de valores predeterminados (`values.yaml`)? Menciona al menos 5 configuraciones importantes.

    Entre las opciones de configuración importantes se encuentran divididas en secciones por el propio archivo nos encontramos: los parámetros globales, la sección de parámetros comunes, de parámetros de NGINX (dividido en varios puntos como parámetros para los deployment o para custom), parámetros de exposición al tráfico o parámetros metrics.

    Dentro de estas secciones tenemos muchos tipos de configuraciones o valores a configurar como la imagen de Docker, el puerto de exposición, etc.

9. **Configuración de Recursos**  
   - ¿Qué valores predeterminados existen para la configuración de recursos (CPU, memoria, etc.)?

    En mi caso poseo de una variable llamada `resources` que contendrá los parámetros para aquellas configuraciones de recursos personalizadas. Sin embargo, existe otra variable denominada `resourcesPreset` que contiene los parámetros para la configuración predeterminada con el valor `nano`. Este valor siguiendo la ruta que nos aporta este archivo (https://github.com/bitnami/charts/blob/main/bitnami/common/templates/_resources.tpl#L15) nos muestra el conjunto de parámetros predeterminados para la configuración de recursos siendo:
    
    ```bash
    "nano" (dict 
      "requests" (dict "cpu" "100m" "memory" "128Mi" "ephemeral-storage" "50Mi")
      "limits" (dict "cpu" "150m" "memory" "192Mi" "ephemeral-storage" "2Gi")
   )
    ```

---

## **Parte 4: Plantillas (Templates)**

10. **Plantillas del Chart**  
    - ¿Cuántas plantillas (`templates`) tiene este *chart*? ¿Cuáles son los archivos de plantilla más relevantes?

    Nginx posee una cantidad de 16 plantillas. Entre los más importantes nos encontramos:
    - El Deployment que se encarga de definir cómo se despliegan y administran los pods de tu aplicación. Es un recurso central para aplicaciones escalables y resilientes.
    - El Service que define cómo se accede a tu aplicación. Es un recurso que permite a los usuarios acceder a tu aplicación desde fuera del cluster.
    - El Ingress proporciona el acceso externo a dichos servicios desde fuera del clúster, gestionando el enrutamiento del tráfico, el balanceo de carga, ...

    Aunque puede haber otros de relevancias, he querido mencionar los tres primeros que consideros más relevantes.

11. **Funcionalidad de Plantillas**  
    - Elige una plantilla del *chart* y describe su funcionalidad brevemente. ¿Qué parte del manifiesto de Kubernetes genera?

    He querido usar la plantilla `templates/deployment.yaml` como ejemplo. Esta plantilla se encarga de generar un recurso de tipo Deployment en el manifiesto de Kubernetes que implementa y configura un contendor Nginx mediante Helm. Entre las caracteristicas de esta plantilla se encuentran metadadatos, las especificaciones del propio deployment (replicas, estrategias de actualizaciones,...), la plantillas para crear los Pods(metadatos de estos, afinidades,tolerancias,...), la configuración del contenedor (con la imagen de Nginx y su política de pull, variables de entorno o configuraciones adicionales), configuración de los probes o de los volúmenes, etc.

    En general, esta plantilla nos sitúa en la configuración de un Deployment de Kubernete enfocado al servicio de Nginx. 

---

## **Parte 5: Esquema de Valores (Values Schema)**

12. **Validación de Esquema de Valores**  
    - ¿El *chart* tiene un esquema de valores (`values schema`) definido? Si es así, ¿qué propósito cumple y cómo ayuda a la validación de los valores proporcionados al instalar el *chart*?

    Nginx posee un esquema de valores ya definido y este nos permite estructurar y validar los valores que se proporcionan al instalar o actualizar el chart. Se encuentra en el archivo `values.schema.json`y al validar los valores proporcionados por el usuario se asegura de que cumplan con el esquema definido. Cuando queramos instalar o actualizar el chart, el esquema nos ayudará a asegurarnos de que los valores proporcionados por el usuario sean correctos ayudando a la instalación o actualización del chart, ya que en caso de no producirse no se podrá instalar o actualizar este.

13. **Campos Obligatorios del Esquema**  
    - ¿Cuáles son algunos de los campos obligatorios en el esquema de valores? Menciona al menos 3 y describe su propósito.

    El esquema de valores de Nginx no se encuentra ningún campo obligatorio. Sin embargo, si tuviéramos que elegir algunos de los campos relevantes, podríamos mencionar los siguientes:

    - replicaCount
    - service.type
    - ingress.enabled
    - image.repository

---

## **Parte 6: Preguntas de Personalización y Comparación**

14. **Personalización del Chart**  
    - Si quisieras personalizar la instalación del *chart* (por ejemplo, cambiar el puerto de la aplicación o modificar los recursos asignados), ¿qué pasos seguirías para hacerlo? ¿Qué archivos o secciones de la documentación consultarías?

    Para personalizar la instalación del chart, podemos seguir los siguientes pasos:
    - Primero, debemos revisar la documentación del chart para entender cómo se puede personalizar la instalación.
    - Luego, lo ideal sería crear un archivo `custom-values.yaml` personalizado con las configuraciones deseadas que modifiquen el comportamiento predeterminado del chart sin tener que modifcar el original.
    - Por ultimo, debemos instalar el chart con los nuevos valores modificados y observar los resultados.

    Si es verdad que desde la guía oficial de Helm (https://helm.sh/es/docs/intro/using_helm/) a la hora de personalizar un chart, en los ejemplos muestra la modificación de la configuración directamente en el `values.yaml` con comandos como:

    ```bash
    $ echo '{mariadb.auth.database: user0db, mariadb.auth.username: user0}' > values.yaml
    $ helm install -f values.yaml bitnami/wordpress --generate-name
    ``` 
    Para la consulta, lo más correcto de observar sería la documentación relativa al `values.yaml`, la documentación relativa al `values.schema.json`.



15. **Comparación entre Charts**  
    - Busca otro *chart* similar al que seleccionaste inicialmente. ¿Qué diferencias observas en términos de configuraciones predeterminadas, plantillas o valores entre ambos *charts*?

    Voy a comparar el Nginx de Bitnami y el Nginx de ingress-nginx. El primero está más relacionado a el despliegue de un servidor web con Nginx, mientras que el segundo actua como controlador de ingress. Algunos puntos de diferencia son:

    - Bitnami en su caracteristicas de ingress por defecto esta desactivado, mientras que ingress-nginx es literal un controlador propio. 
    - En resources, el ingress-nginx tiene por defecto ( cpu: 100m o memory: 90Mi), mientras que el de Bitnami esta vacía y usa nano por defecto.
    - Respecto a las plantillas (templates), Bitnami posee 16 plantillas, en tanto, el ingress-nginx posee 44 plantillas (diversos roles, configmap, services, etc).
    - Respecto a la validación de valores (values schema), el ingress-nginx posee un gran control de estas con validaciones concretas, siendo la de Bitnami más básica.


---

### Parte 7: Uso de Helm Template

16. **Generación de Manifiestos**  
   - Utiliza el comando `helm template <nombre-chart> [opciones]` para generar los manifiestos de Kubernetes sin instalarlos. Explica cómo puedes ver el archivo antes de lanzarlo.  

   Empezamos con la instalación de Helm descargando el binario y realizando el comportamiento que hicimos en kubernetes, es decir, crear una carpeta en disco C y crear una carpeta llamada `helm` dentro de ella. Luego, en el Path de las variables de entorno añadimos esta carpeta. Seguimos con usa serie de requisitos que son necesarios para el uso de este comando:

```bash
# Llevarnos el repositorio a nuestro repositorio local
helm repo add bitnami https://charts.bitnami.com/bitnami
# Obsevamos el manifiesto de la aplicación
helm template lcm-nginx bitnami/nginx --version 20.0.2
# Paso el manifiesto a un archivo propio
helm template lcm-nginx bitnami/nginx --version 20.0.2 > nginx-manifest.yaml
```
En el archivo `nginx-manifest.yaml` podemos ver el manifiesto de la aplicación, que es el archivo que se utiliza para crear la aplicación en el cluster de Kubernetes. También el mismo comando helm template nos permite ver el manifiesto de un chart en concreto antes de quererlo instalar.

![Captura sobre código](../../datos/Ejercicio01/comandos%20template.png)

![Captura sobre código](../../datos/Ejercicio01/a%20manifiesto.png)



