# **Ejercicio 06: Funciones en Helm**

### **Objetivo**

El objetivo de este ejercicio es aplicar funciones en un chart de Helm reutilizado, permitiendo la automatización en la generación de contraseñas y la manipulación de datos para mejorar la seguridad y la flexibilidad en la configuración de despliegues en Kubernetes.

---

### **¡Importante!**

Ten mucho cuidado con los valores sensibles que puedas exponer en tus soluciones. Recuerda que otros pueden acceder a los datos en tus entregables, lo que podría comprometer la seguridad de la información. ¡Siempre asegúrate de proteger tus datos y los de tus clientes!

---

### **Enunciado**

En este ejercicio, deberás reutilizar el chart de Helm anterior y aplicar funciones.

---

### **Requisitos del despliegue:**

1. Mediante el uso de funciones y sobre los manifiestos del ejercicio anterior, debes realizar lo siguiente:

- Las contraseñas se deben generar de forma randomizada (String de longitud 10, generado aleatoriamente).
- Aplicar `TRIM` a los nombres de usuario y donde creas que es necesario.
- Mediante función, hacer que el nombre de la base de datos se ingrese con mayúsculas.
- Si en el `value.yaml` no se ingresa el tag de Phpmyadmin, hacer que por defecto tome la version `latest`.

---

### **Entregables**

- **Capturas de pantalla** de todos los resultados obtenidos durante el despliegue (pods, servicios, acceso a la aplicación).
- Un archivo de texto con los **comandos ejecutados**.
- El **archivo values.yaml** que has creado para el despliegue.
- Los **archivos de manifiestos de Kubernetes** (`.yaml`), como los manifiestos de MySQL y phpMyAdmin.
- El **chart de Helm** empaquetado, con todos los recursos dentro de la carpeta `templates/`.