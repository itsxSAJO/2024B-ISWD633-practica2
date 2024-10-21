# Redes
Las redes son un componente fundamental que permite la comunicación entre contenedores, así como la comunicación de los contenedores con el mundo exterior. 

![Imagen](img/redes.PNG)

- Bridge: Esta es la red por defecto en Docker. Permite la comunicación entre contenedores en el mismo host. Cada contenedor conectado a la red bridge tiene una IP propia en la subred de la red bridge.
    -  Brige por default: Cuando se ejecuta un contenedor, Docker crea automáticamente una red de tipo bridge por default. Esta red se utiliza para permitir la comunicación entre contenedores en el mismo host. Cada contenedor conectado a esta red obtiene su propia dirección IP en la subred de la red bridge.
    - Bridge creada por nosotros: Un usuario también puede crear sus propias redes de tipo bridge en Docker. Esto puede ser útil para organizar y segmentar los contenedores de una aplicación de manera más controlada. Al crear una red bridge personalizada, se puede especificar un rango de direcciones IP y otras configuraciones de red específicas. Los contenedores conectados a esta red utilizarán las direcciones IP de la subred definida por el usuario.
- Host: Con esta red, los contenedores comparten la red del host en lugar de tener su propia interfaz de red. Esto puede mejorar el rendimiento de red, pero los contenedores pueden entrar en conflicto con los puertos del host si intentan utilizar los mismos puertos.
- None: Con esta red, se deshabilita la configuración de red. Los contenedores que usan esta red tienen su propia red de bucle invertido y no pueden comunicarse con otros contenedores a menos que se conecten explícitamente a una red.

### Crear una red de tipo bridge

```
docker network create SAID -d bridge
```

![Imagen](img/4.1.png)

### Crear un contenedor vinculado a una red

```
docker run -d --name Red-P2 --network SAID  nginx:alpine
```
![Imagen](img/4.2.png)

### Para saber a qué red está conectado un contenedor

```
docker inspect Red-P2
```

![Imagen](img/4.3.png)

ó
```
docker network inspect SAID
```
![Imagen](img/4.4.png)

### Vincular contenedor a una red
```
docker network connect SAID Red-P2
```

el contenedor Red-P2 ya está conectado a la red SAID. No es necesario intentar conectarlo nuevamente, ya que Docker no permite duplicar conexiones a la misma red desde el mismo contenedor.

![Imagen](img/4.5.png)

### Para desvincular un contenedor de una red
```
docker network disconnect SAID Red-P2
```
![Imagen](img/4.6.png)

### Para listar las redes existentes
```
docker network ls
```
![Imagen](img/4.7.png)

### Crear los contenedores y las redes que se presentan en el esquema. Usar para todos los contenedores la imagen de nginx:alpine

![Imagen](img/esquema-ejercicio-redes.PNG)

# COLOCAR UNA CAPTURA DE LAS REDES EXISTENTES CREADAS
![Imagen](img/4.8.png)

# COLOCAR UNA(S) CAPTURAS(S) DE LOS CONTENEDORES CREADOS EN DONDE SE EVIDENCIE A QUÉ RED ESTÁN VINCULADOS

![Imagen](img/4.9.png)

### Para eliminar las redes creadas
```
docker network rm net-curso01
docker network rm net-curso02
```

