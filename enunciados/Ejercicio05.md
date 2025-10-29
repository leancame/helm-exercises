# **Ejercicio 05: Condiciones, bucles y operadores en Helm**

### **Objetivo**

El objetivo de este ejercicio es que los estudiantes aprendan a utilizar estructuras de control como condiciones y bucles en un archivo values.yaml de un chart de Helm. A través de la configuración de un despliegue complejo, los alumnos podrán aplicar sus conocimientos sobre la parametrización de aplicaciones en Kubernetes, permitiendo la personalización de variables de entorno y configuraciones de servicios.

---

### **¡Importante!**

Ten mucho cuidado con los valores sensibles que puedas exponer en tus soluciones. Recuerda que otros pueden acceder a los datos en tus entregables, lo que podría comprometer la seguridad de la información. ¡Siempre asegúrate de proteger tus datos y los de tus clientes!

---

### **Enunciado**

En este ejercicio, deberás reutilizar el chart de Helm que implementa MySQL, ahora aplicando condiciones y bucles.

---

### **Requisitos del despliegue:**

1. **Archivo `values.yaml`**: Debe incluir todas las configuraciones necesarias para:

    - Utilizar condiciones para elegir si se habilita el despliegue de phpMyAdmin. Es decir, permitir el despliegue de: 
        - mysql y phpmyadmin.
        - Solo mysql.

    - Definir variables de entorno en el `values.yaml` y utilizar bucles para iterar sobre ellas.

    - Usar operadores para asegurarse de que phpmyadmin se despliegue solo si se habilita tambien el despliegue de la base de datos.

---

### **Entregables**

- **Capturas de pantalla** de todos los resultados obtenidos durante el despliegue (pods, servicios, acceso a la aplicación).
- Un archivo de texto con los **comandos ejecutados**.
- El **archivo values.yaml** que has creado para el despliegue.
- Los **archivos de manifiestos de Kubernetes** (`.yaml`), como los manifiestos de MySQL y phpMyAdmin.
- El **chart de Helm** empaquetado, con todos los recursos dentro de la carpeta `templates/`.