## Solución del Ejercicio 05: Condiciones, bucles y operadores en Helm

### **Enunciado**

En este ejercicio, deberás reutilizar el chart de Helm que implementa MySQL, ahora aplicando condiciones y bucles.

### **Requisitos del despliegue:**

1. **Archivo `values.yaml`**: Debe incluir todas las configuraciones necesarias para:

    - Utilizar condiciones para elegir si se habilita el despliegue de phpMyAdmin. Es decir, permitir el despliegue de: 
        - mysql y phpmyadmin.
        - Solo mysql.

    - Definir variables de entorno en el `values.yaml` y utilizar bucles para iterar sobre ellas.

    - Usar operadores para asegurarse de que phpmyadmin se despliegue solo si se habilita tambien el despliegue de la base de datos.

---

## Resolución

En este ejercicio vamos a concretar los cambios con respecto a la solución del cuarto ejercicio. Nos centraremos en los cambios significativos que han hecho posible que se cumpla los requisitos dispuestos en este enunciado.

En primer lugar pasamos a utilizar condiciones que habiliten o inhabiliten el despliegue de phpMyAdmin y mysql. Con estes motivo, añadimos en el archivo `values.yaml` las siguientes líneas:

```yaml
mysql:
  enabled: true
phpmyadmin:
  enabled: true
```
Esto nos permite tener dos opciones de despliegue: mysql y phpmyadmin, o solo mysql. 

Para ello, en el archivo `templates/phpmyadmin-deployment.yaml` y `templates/phpmyadmin-service.yaml` debemos utilizar condiciones para que se despliegue o no phpmyadmin:

```yaml
{{- if and .Values.phpMyAdmin.enabled .Values.mysql.enabled }}
.....
{{- end }}
```
Con esta condición, se desplegará phpmyadmin solo si se habilita el despliegue de mysql. En caso de ser este último el que se inhabilite, phpmyadmin no se desplegará.

Además en el archivo `templates/mysql-statefulset.yaml` debemos utilizar condiciones para que se despliegue o no mysql:

```yaml
{{- if .Values.mysql.enabled }}
.....
{{- end }}
```
Con esta condición, se desplegará mysql solo si se habilita el despliegue de mysql.

Aquí aporto captura de pantalla de la inahibilitación de mysql solo y de phpmyadmin:

![Captura sobre código](../../datos/Ejercicio05/false%20mysql.png)

![Captura sobre código](../../datos/Ejercicio05/false%20mysql%202.png)

![Captura sobre código](../../datos/Ejercicio05/false%20phpadmin.png)


Para el caso de las variables de entorno, en el archivo `values.yaml` he creado el apartado `users` en mysql para poder configurar el usuario y la contraseña del root y del usuario de la base de datos:

```yaml
users:                         
    - name: "root"               
      isRoot: true               
    - name: "user"               
      isRoot: false
```

Y he creado un bucle en el archivo `templates/mysql-statefulset.yaml` para iterar sobre el array `users`:

```yaml
{{- range .Values.mysql.users }} # Iteración sobre la lista de usuarios definida en el archivo de valores
        - name: {{ if .isRoot }}MYSQL_ROOT_PASSWORD{{ else }}MYSQL_PASSWORD{{ end }} # Configura la contraseña de root o de usuario estándar
          valueFrom:
            secretKeyRef:
              name: mysql-secret       # Referencia al Secret donde están las contraseñas
              key: mysql-{{ .name }}-password # Clave específica en el Secret
        {{- if not .isRoot }}
        - name: MYSQL_USER             # Configura el usuario si no es root
          value: {{ .name }}
        {{- end }}
        {{- end }}
```
Con esto, se pueden configurar tanto el usuario como la contraseña del root y del usuario de la base de datos a través de variables de entorno con un bucle que recorre el array `users` observando si el usuario es root o no.

Tras la realización de ambos cambios, se puede proceder a actualizar el charm de Helm y a desplegar el despliegue con los nuevos cambios.

````bash
 helm upgrade mysql-app ./mysql-app-chart --namespace mysql-app
 minikube service phpmyadmin-service -n mysql-app
 ````

Con esto, se actualiza el despliegue de mysql-app y se accede a phpmyadmin.

![Captura sobre código](../../datos/Ejercicio05/ejecucion%201.png)