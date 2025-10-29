## Solución al Ejercicio 2 - Desplegar el chart de Nginx utilizando Helm

### **Enunciado y Resolución**

En este ejercicio, vamos a trabajar con el *chart* de **Nginx** y aprenderemos a gestionar aplicaciones en Kubernetes utilizando Helm. Sigue los pasos a continuación:

---

## **Parte 1: Desplegar el chart de Nginx utilizando Helm**

1. **Inicia tu entorno de Kubernetes con Minikube**
   - Asegúrate de que Minikube está funcionando. Si no está corriendo, inicia Minikube:
     ```bash
     minikube start
     ```
   - Verifica que tu *cluster* esté activo y funcionando:
     ```bash
     kubectl get nodes
     ```
      ![Captura sobre código](../../datos/Ejercicio02/parte%201.png)

2. **Agrega el repositorio oficial de charts de Bitnami (si no lo tienes agregado)**
   - Para utilizar el *chart* de **Nginx**, debes agregar el repositorio de **Bitnami** a Helm (si no lo has hecho previamente):
     ```bash
     helm repo add bitnami https://charts.bitnami.com/bitnami
     ```
      ![Captura sobre código](../../datos/Ejercicio02/parte%202.png)

3. **Actualiza los repositorios de Helm**
   - Asegúrate de tener las versiones más recientes de los *charts* disponibles:
     ```bash
     helm repo update
     ```
      ![Captura sobre código](../../datos/Ejercicio02/parte%203.png)

4. **Desplegar el chart de Nginx**
   - Despliega **Nginx** en tu *cluster* de Kubernetes utilizando el *chart* de **Bitnami**. Para esto, ejecuta el siguiente comando, donde `<nombre-release>` es el nombre que le darás a la instalación (por ejemplo, `nginx-release`):
     ```bash
     helm install <nombre-release> bitnami/nginx
     helm install lcm-nginx bitnami/nginx
     ```
      ![Captura sobre código](../../datos/Ejercicio02/parte%204.png)

5. **Verificar la instalación**
   - Una vez que se haya completado la instalación, verifica que todo esté corriendo correctamente:
     ```bash
     kubectl get pods
     ```
      ![Captura sobre código](../../datos/Ejercicio02/parte%205.png)

6. **Acceso a la aplicación**
   - Para obtener información sobre cómo acceder a Nginx, puedes ejecutar el siguiente comando:
     ```bash
     helm status <nombre-release>
     helm status lcm-nginx
     ```
   - Esto te proporcionará información sobre cómo acceder a la aplicación desde un navegador web. Si usas Minikube, puede que necesites ejecutar:
     ```bash
     minikube service <nombre-release>-nginx
     minikube service lcm-nginx
     ```
   - Esto abrirá el servicio en tu navegador y te permitirá ver la aplicación en ejecución.
    ![Captura sobre código](../../datos/Ejercicio02/parte%206.png)
    ![Captura sobre código](../../datos/Ejercicio02/parte%207.png)

---

## **Parte 2: Gestionar releases y explorar comandos de Helm**

1. **Verificar el estado de tu release**  
   Una vez que hayas desplegado Nginx, utiliza los siguientes comandos para explorar y gestionar tu *release*:
   
   - **Listar las releases instaladas:**
     ```bash
     helm list
     ```
     ![Captura sobre código](../../datos/Ejercicio02/parte%202%20punto%201.png)

   - **Ver el estado de tu release:**
     ```bash
     helm status <nombre-release>
     helm status lcm-nginx
     ```
     ![Captura sobre código](../../datos/Ejercicio02/parte%202%20punto%202.png)

   - **Ver el manifiesto generado por Helm:**
     ```bash
     helm get manifest <nombre-release>
     helm get manifest lcm-nginx
     ```
      ![Captura sobre código](../../datos/Ejercicio02/parte%202%20punto%203.1.png)
      ![Captura sobre código](../../datos/Ejercicio02/parte%202%20punto%203.2.png)
      ![Captura sobre código](../../datos/Ejercicio02/parte%202%20punto%203.3.png)
      ![Captura sobre código](../../datos/Ejercicio02/parte%202%20punto%203.4.png)

   - **Ver las notas de instalación:**
     ```bash
     helm get notes <nombre-release>
     helm get notes lcm-nginx
     ```
      ![Captura sobre código](../../datos/Ejercicio02/parte%202%20punto%204.png)

   > **Pregunta**: Cuéntanos con tus palabras qué información brinda cada uno de estos comandos.

    El primer comando nos muestras todas los releases que tenemos instalados en nuestro cluster que sería como las aplicaciones de Helm desplegado de algún chart. El segundo comando nos muestra el estado de nuestro release concreto, si esta activo, con cual version de helm, etc. El tercer comando nos muestra el manifiesto generado por helm. El cuarto nos muestra las notas del propio char tras su despliegue. 
   
---

## **Parte 3: Realizar cambios en la configuración del chart (Upgrade)**

2. **Realiza un upgrade del chart**
   - Cambia el tipo de servicio a **NodePort** y selecciona un puerto de tu elección para exponer el servicio:
     ```bash
     helm upgrade <nombre-release> bitnami/nginx --set service.type=NodePort --set service.nodePorts.http=<puerto-elegido>
     
     helm upgrade lcm-nginx bitnami/nginx --set service.type=NodePort --set service.nodePorts.http=30080
     ```
   - Verifica que los cambios se han aplicado correctamente:
     ```bash
     helm get values <nombre-release>
     helm get values lcm-nginx
     ```
      ![Captura sobre código](../../datos/Ejercicio02/parte%203%20punto%201.png)
      ![Captura sobre código](../../datos/Ejercicio02/parte%203%20punto%202.png)

---

## **Parte 4: Gestionar el historial de releases**

3. **Revisar el historial de versiones del release**
   - Utiliza el siguiente comando para ver el historial de versiones del *release*:
     ```bash
     helm history <nombre-release>
     helm history lcm-nginx
     ```
      ![Captura sobre código](../../datos/Ejercicio02/parte%204%20parte%201.png)
  

4. **Realizar un rollback**
   - Realiza un *rollback* a la versión anterior utilizando el comando correspondiente:
     ```bash
     helm rollback <nombre-release> <número-de-versión-anterior>
     helm rollback lcm-nginx 1
     ```
   - Revisa nuevamente el historial:
     ```bash
     helm history <nombre-release>
     helm history lcm-nginx
     ```
      ![Captura sobre código](../../datos/Ejercicio02/parte%204%20parte%202.png)

   > **Pregunta**: ¿Qué ocurrió tras realizar el rollback?  

   El rollback nos devuelve a la version anterior de nuestro release volviendo a la version 1. En el historial podemos ver que el release ha sido actualizado a la version 2 y luego volvimos a la version 1.

---

## **Parte 5: Eliminar el release**

5. **Elimina el release**
   - Utiliza el siguiente comando para eliminar el *release* de tu clúster:
     ```bash
     helm uninstall <nombre-release>
     helm uninstall lcm-nginx
     ```
      ![Captura sobre código](../../datos/Ejercicio02/Punto%205%20entero.png)



