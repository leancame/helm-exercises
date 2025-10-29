# **Ejercicio 01: Explorando Helm Charts en Artifact Hub**

### Objetivo

Este ejercicio tiene como propósito de familiarizarnos con la lectura de la documentación de los *Helm charts* en Artifact Hub, tanto la parte principal como las secciones laterales (Install, Templates, Default Values, Values Schema).

### Instrucciones

1. Accede al sitio web de [Artifact Hub](https://artifacthub.io/).
2. Busca un *Helm chart* de tu interés (por ejemplo, **nginx**, **postgresql**, **prometheus**, entre otros).
3. Responde las siguientes preguntas basándote en la información que encuentres en la página del *Helm chart* seleccionado.

---

## **Parte 1: Información Principal del Chart**

1. **Nombre del Chart y Mantenedor**  
   - ¿Cuál es el nombre del *chart* y quién es el mantenedor?

2. **Descripción del Chart**  
   - ¿Cuál es la descripción general del *chart*? ¿Para qué sirve esta aplicación o servicio?

3. **Versión del Chart**  
   - ¿Cuál es la versión más reciente del *chart* disponible?

4. **Versiones de Aplicaciones Soportadas**  
   - ¿Qué versiones de la aplicación soporta este *chart* (es decir, la versión de la aplicación subyacente)?

---

## **Parte 2: Sección de Instalación**

5. **Comandos de Instalación**  
   - ¿Cuál es el comando principal para instalar este *chart* utilizando *Helm*?

6. **Repositorio del Chart**  
   - ¿En qué repositorio se encuentra alojado este *chart*? Proporciona la URL del repositorio.

7. **Versión de Helm requerida**  
   - ¿Cuál es la versión mínima de *Helm* que se necesita para instalar este *chart*?

---

## **Parte 3: Valores Predeterminados (Default Values)**

8. **Archivo de Valores Predeterminados**  
   - ¿Qué opciones de configuración aparecen en el archivo de valores predeterminados (`values.yaml`)? Menciona al menos 5 configuraciones importantes.

9. **Configuración de Recursos**  
   - ¿Qué valores predeterminados existen para la configuración de recursos (CPU, memoria, etc.)?

---

## **Parte 4: Plantillas (Templates)**

10. **Plantillas del Chart**  
    - ¿Cuántas plantillas (`templates`) tiene este *chart*? ¿Cuáles son los archivos de plantilla más relevantes?

11. **Funcionalidad de Plantillas**  
    - Elige una plantilla del *chart* y describe su funcionalidad brevemente. ¿Qué parte del manifiesto de Kubernetes genera?

---

## **Parte 5: Esquema de Valores (Values Schema)**

12. **Validación de Esquema de Valores**  
    - ¿El *chart* tiene un esquema de valores (`values schema`) definido? Si es así, ¿qué propósito cumple y cómo ayuda a la validación de los valores proporcionados al instalar el *chart*?

13. **Campos Obligatorios del Esquema**  
    - ¿Cuáles son algunos de los campos obligatorios en el esquema de valores? Menciona al menos 3 y describe su propósito.

---

## **Parte 6: Preguntas de Personalización y Comparación**

14. **Personalización del Chart**  
    - Si quisieras personalizar la instalación del *chart* (por ejemplo, cambiar el puerto de la aplicación o modificar los recursos asignados), ¿qué pasos seguirías para hacerlo? ¿Qué archivos o secciones de la documentación consultarías?

15. **Comparación entre Charts**  
    - Busca otro *chart* similar al que seleccionaste inicialmente. ¿Qué diferencias observas en términos de configuraciones predeterminadas, plantillas o valores entre ambos *charts*?

---

### Parte 7: Uso de Helm Template

16. **Generación de Manifiestos**  
   - Utiliza el comando `helm template <nombre-chart> [opciones]` para generar los manifiestos de Kubernetes sin instalarlos. Explica cómo puedes ver el archivo antes de lanzarlo.  


