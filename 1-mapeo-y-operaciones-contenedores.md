# Mapeo de Puertos 
### Usando una forma más semántica cuando se especifican puertos

```
docker run -d --name Jenkins --publish published=8080,target=50000 jenkins/jenkins:alpine3.18-jdk11
```

![Imagen](img/mapeodepuertos1.png)


### Publicando todos los puertos
```
docker run -P -d --name Jenkins2 jenkins/jenkins:alpine3.18-jdk11 
```

-P: le indica a Docker que asigne automáticamente puertos aleatorios en tu host para todos los puertos expuestos por el contenedor.

**Recordar**
No puedes mapear puertos a un contenedor existente directamente después de su creación con Docker. El mapeo de puertos debe especificarse en el momento de crear y ejecutar el contenedor.

### Crear contenedor de Jenkins puertos contenedor: 8080 (interface web) y 50000 (comunicación entre nodos) imagen: jenkins/jenkins:alpine3.18-jdk11

# ACCESO http://localhost:8080

![Imagen](img/localHost8080.png)


### ¿Cómo obtener la contraseña solicitada?
Para obtener la contraseña solicitada es necesario ingresar al contenedor.

![Imagen](img/jenkins.PNG)

# Operaciones con contenedores

### Ejecutar un comando en un contenedor de Docker en ejecución
```
docker exec Jenkins ls -l
```

Este comando ejecuta ls -l dentro del contenedor llamado Jenkins, listando los archivos del directorio actual en el contenedor.

# COMPLETAR
### ¿Para qué se usa el comando ls?

El comando ls se utiliza para listar los archivos y directorios en el directorio actual o en un directorio específico que indiquemos. Es una de las herramientas más comunes para inspeccionar el contenido de un sistema de archivos.

### ¿Para qué sirve el argumento -l junto al comando ls?

El argumento -l muestra esa lista en un formato detallado, incluyendo información como los permisos, el propietario, el tamaño y la fecha de modificación de cada archivo o directorio.

### Usar el contenedor de jenkins creado previamente y ejecutar el comando ls con el argumento -l
# COMPLETAR

![Imagen](img/comandoEjecucion.png)

### Para ejecutar un shell interactivo en un contenedor de Docker especificado.
El comando **docker exec** te permite acceder a la sesión shell de un contenedor en ejecución, estarás dentro del contenedor y podrás ejecutar comandos como si estuvieras en una terminal normal. 
Para saber qué comando utilizar para abrir una terminal dentro de un contenedor, es útil conocer la imagen base del contenedor, ya que diferentes imágenes pueden usar diferentes shells o comandos para abrir una terminal. Puedes verificar la documentación de la imagen del contenedor en Docker Hub o en el repositorio de la imagen para obtener información específica sobre cómo abrir una terminal en esa imagen.
- Para imágenes basadas en Debian o Ubuntu, puedes probar con bash.
- Para imágenes basadas en Alpine Linux, puedes probar con sh.
![Imagen](img/jenkins-i.PNG)
```
docker exec -i <nombre contenedor> <programa o comando>
```
-i: mantiene abierta la entrada estándar (stdin) del contenedor. Esto significa que puedes enviar datos al proceso que se está ejecutando en el contenedor a través de la terminal local. *Sin embargo, esto no asigna un terminal al contenedor, por lo que no podrás ver la salida del proceso de forma interactiva.*

### Ejecutar una de las siguientes instrucciones
```
docker exec -i Jenkins /bin/bash 
```


ó
```
docker exec -i Jenkins bash 
```
![Imagen](img/binbash.png)

**Considerar**
- /bin/bash: Al especificar la ruta completa del shell, Docker buscará el ejecutable /bin/bash en el sistema de archivos del contenedor y lo ejecutará. Esto es útil cuando quieres asegurarte de que se está utilizando un shell específico que está ubicado en una ubicación conocida en el sistema de archivos del contenedor. 
- bash: Al especificar solo el nombre del shell, Docker buscará el comando bash en las rutas del sistema (por lo general, en las rutas definidas en la variable de entorno PATH) del contenedor y lo ejecutará. Esto asume que bash está disponible en alguna de las rutas del sistema definidas en el contenedor.

Ejecutar
```
echo "Hola mundo"
```

Ejecutar
```
whoami
```

**Si se visualiza el mensaje command not found, considerar**
El problema se debe a que no se ha asignado un terminal de salida al contenedor al ejecutar el comando. Cuando usas docker exec -i jenkins-server /bin/bash en Windows, el comando se ejecuta pero no hay un terminal asignado para mostrar la salida del comando ls.

Para solucionar el problema del carácter de fin de línea (\r), se debe usar una terminal interactiva con el comando docker exec -it Jenkins /bin/bash. Esto permite ejecutar comandos dentro del contenedor uno por uno.

![Imagen](img/comandosBashSolucion.png)


### Para ejecutar un shell interactivo bidireccional en un contenedor de Docker especificado.
Ejecutar un shell interactivo bidireccional en un contenedor de Docker significa abrir una sesión de shell en el contenedor que permite la interacción bidireccional entre la terminal local y el contenedor. Es decir, puedes enviar comandos desde tu terminal local al contenedor y recibir la salida de esos comandos de vuelta en tu terminal local, al igual que si estuvieras trabajando directamente en la terminal del contenedor.

![Imagen](img/jenkins-it.PNG)
```
docker exec -i -t Jenkins /bin/bash
```

Para que el comando se ejecute correctamente, los flags -i y -t deben estar separados por un espacio.

ó
```
docker exec -it Jenkins /bin/bash
```

![Imagen](img/comandosBashIT.png)

### Ahora puedes acceder al contenedor de jenkins y obtener la contraseña ubicada en /var/jenkins_home/secrets/initialAdminPassword

Para obtener la contraseña inicial de Jenkins, no se puede ejecutar el archivo directamente, porque no es un comando. En lugar de eso, se debe leer el contenido del archivo usando el comando: cat, este comando mostrará la contraseña en la terminal

![Imagen](img/comandoContrasena.png)

# COMPLETAR

### Colocar una captura de pantalla de la ventana que aparece después de colocar la contraseña.

**Para este punto no es necesario continuar con la instalación de Jenkins**

![Imagen](img/localHost8080contrasena.png)

### Para ver los logs de un contenedor

```
docker logs -n -t Jenkins
```
-t: para incluir la fecha y la hora

![Imagen](img/jenkinsLog.png)





