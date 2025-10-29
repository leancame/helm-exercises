# **Ejercicio 04: Crear y Empaquetar Aplicaciones Complejas en Kubernetes Usando Helm**

### **Objetivo**

El objetivo de este ejercicio es aprender a crear manualmente los recursos de Kubernetes (como Deployments, Services, StatefulSets) y empaquetarlos en un chart de Helm propio. Con lo que conseguiremos desplegar aplicaciones complejas con persistencia de datos, secretos y ConfigMaps, gestionando configuraciones a través de un archivo `values.yaml`.

---

### **Enunciado**

En este ejercicio, deberás **crear manualmente** los manifiestos de Kubernetes necesarios para una aplicación compuesta por **MySQL** y **phpMyAdmin**. Posteriormente, empaquetarás estos manifiestos en un **chart de Helm propio** y desplegarás la aplicación en un clúster de Kubernetes utilizando este chart.

---

### **Requisitos del Despliegue:**

1. **Namespace:**
   - Todos los componentes deben ser desplegados en un namespace llamado `mysql-app`.

2. **Recursos de Kubernetes:**
   - Deberás crear los manifiestos de los siguientes recursos:
     - **MySQL**:
       - Utiliza la imagen oficial de MySQL, asegurándote de usar la versión adecuada.
       - No debe ser un deployment (¿Qué objeto sería el adecuado?)
       - Implementa un **volumen persistente** para la base de datos.
       - Configura los secretos necesarios (como las credenciales de acceso a la base de datos) usando un **Secret**.
     - **phpMyAdmin**:
       - Utiliza la imagen oficial de `phpmyadmin`.
       - Crea un **Deployment** para phpMyAdmin.
   - **Service**:
     - Crea los **Services** necesarios para exponer MySQL y phpMyAdmin.
     - Para MySQL, utiliza el puerto adecuado para la base de datos (3306).
     - Para phpMyAdmin, expón el servicio en un puerto configurable.
   - **ConfigMaps y Secretos**:
     - Crea los **ConfigMaps** y **Secretos** necesarios para la configuración de la aplicación (por ejemplo, las credenciales de MySQL).

3. **Empaquetar los Manifiestos en un Chart de Helm**:
   - Crea un **chart de Helm** desde cero, empaquetando todos los manifiestos que creaste.
   - Utiliza el comando `helm create <nombre-chart>` para generar la estructura básica de un chart.
   - Coloca tus manifiestos de Kubernetes en la carpeta correspondiente dentro del chart (`templates/`).
   - Asegúrate de que el chart esté correctamente estructurado y empaquetado.

4. **Archivo values.yaml**:
   - Crea un archivo `values.yaml` que incluya las configuraciones necesarias para los elementos a desplegar:
     - **Versiones de las imágenes** de MySQL y phpMyAdmin.
     - **Configuraciones de la Base de Datos** (credenciales, nombre de la base de datos, etc.).
     - **Capacidad de los volúmenes persistentes**.
     - **Configuraciones de phpMyAdmin**.
     - Las opciones que no deben ser modificadas no deben estar incluidas en el `values.yaml`.

---

### **Pasos del Despliegue:**

1. **Iniciar el Entorno:**
   - Asegúrate de que tu clúster de Kubernetes esté corriendo (puedes usar **Minikube** o cualquier otro clúster compatible con Kubernetes):
     ```bash
     minikube start
     ```

2. **Crear los Manifiestos:**
   - Crea los manifiestos de Kubernetes (Deployment, StatefulSet, Service, Secret, ConfigMap, etc.) para MySQL y phpMyAdmin. Los archivos deben estar en formato `.yaml`.

3. **Empaquetar los Manifiestos en un Chart de Helm:**
   - Usa el siguiente comando para crear la estructura básica de un chart de Helm:
     ```bash
     helm create mysql-app-chart
     ```
   - Coloca todos los manifiestos en la carpeta `templates/` del chart.
   - Modifica el archivo `Chart.yaml` para reflejar correctamente el nombre de tu chart y las versiones de los componentes.

4. **Crear el Archivo values.yaml:**
   - Configura el archivo `values.yaml` para gestionar las versiones de las imágenes, las credenciales, el tamaño de los volúmenes, y otras configuraciones necesarias.

5. **Instalar el Chart de Helm:**
   - Una vez que hayas empaquetado los manifiestos en el chart de Helm, instálalo en tu clúster utilizando:
     ```bash
     helm install <nombre-release> ./mysql-app-chart --namespace mysql-app --create-namespace
     ```

6. **Verificar el Despliegue:**
   - Comprueba que los pods y servicios están corriendo correctamente en el namespace `mysql-app`:
     ```bash
     kubectl get pods -n mysql-app
     kubectl get svc -n mysql-app
     ```

7. **Acceso a la Aplicación:**
   - Para acceder a phpMyAdmin, verifica los servicios expuestos:
     ```bash
     kubectl get svc -n mysql-app
     ```
   - Si estás usando **Minikube**, puedes acceder a los servicios utilizando:
     ```bash
     minikube service <nombre-release>-phpmyadmin -n mysql-app
     ```

---

### **Entregables**

- **Capturas de pantalla** de todos los resultados obtenidos durante el despliegue (pods, servicios, acceso a la aplicación).
- Un archivo de texto con los **comandos ejecutados**.
- El **archivo values.yaml** que has creado para el despliegue.
- Los **archivos de manifiestos de Kubernetes** (`.yaml`), como los manifiestos de MySQL y phpMyAdmin.
- El **chart de Helm** empaquetado, con todos los recursos dentro de la carpeta `templates/`.

