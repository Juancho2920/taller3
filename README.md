## API Flask - Gestión de Productos

Este proyecto consiste en una API desarrollada en Flask que permite realizar las operaciones básicas de un catálogo de productos. La API cuenta con los métodos GET, POST, PUT y DELETE, los cuales permiten consultar, crear, modificar y eliminar productos.

## Requisitos previos

Antes de comenzar, es necesario tener instalados los siguientes programas:

Python. Se puede comprobar la instalación con python --version.
Git. Se puede verificar con git --version.
Postman, que se utilizará para realizar las pruebas de los diferentes endpoints.
Instructivo para ejecutar el proyecto
## 1. Clonar el repositorio

Primero se debe descargar el proyecto desde GitHub utilizando Git. Para esto, se ejecutan los siguientes comandos:

git clone https://github.com/MrHuesitozzz/api.git
cd api


El primer comando descarga el repositorio y el segundo permite ingresar a la carpeta del proyecto.

## 2. Crear el entorno virtual

Para trabajar con las dependencias del proyecto de manera independiente, se crea un entorno virtual con:

python -m venv .env


Esto genera una carpeta llamada .env, donde estarán los archivos relacionados con el entorno virtual.

## 3. Activar el entorno virtual

Si se está utilizando Windows PowerShell, el entorno virtual se puede activar con:

.\.env\Scripts\Activate.ps1


En caso de que aparezca un error relacionado con los permisos para ejecutar scripts, se puede ejecutar una sola vez:

Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser


Cuando el entorno virtual se encuentra correctamente activado, el nombre del entorno aparece al inicio de la consola. Por ejemplo:

(.env) PS C:\NTD\api>

## 4. Instalar las dependencias

Después de activar el entorno, se deben instalar las librerías necesarias para ejecutar el proyecto.

Si solamente se necesita Flask, se puede instalar con:

pip install flask


Si el proyecto ya cuenta con un archivo requirements.txt, es mejor instalar todas las dependencias desde ese archivo:

pip install -r requirements.txt

## 5. Ejecutar la aplicación

Para iniciar el servidor de Flask se utiliza:

python app.py


Si todo funciona correctamente, en la consola debería aparecer un mensaje similar a:

Running on http://127.0.0.1:5000


Esto significa que la API está ejecutándose de forma local. La terminal debe mantenerse abierta mientras se realizan las pruebas desde Postman.

[Pantallazo: terminal mostrando la aplicación de Flask ejecutándose](terminal.jpeg)

Pruebas de los endpoints con Postman

Para realizar las pruebas se utilizará como URL base:

http://127.0.0.1:5000


Importante: si Postman solicita seleccionar un agente para conectarse a 127.0.0.1, se debe seleccionar Desktop Agent. El Cloud Agent no puede acceder directamente al servidor que se está ejecutando de manera local.

## GET - Consultar todos los productos

Este endpoint permite obtener la lista completa de productos registrados.

Método: GET
URL: http://127.0.0.1:5000/api/productos
Body: No se necesita.

Si la petición se realiza correctamente, la API debe devolver un estado 200 OK junto con los productos en formato JSON.

[Pantallazo: petición y respuesta del GET de todos los productos](get.jpeg)

## GET - Consultar un producto por ID

También es posible consultar un producto específico utilizando su ID.

Método: GET
URL: http://127.0.0.1:5000/api/productos/1
Body: No se necesita.

En este caso, el número 1 corresponde al ID del producto que se quiere consultar.

Si el producto existe, se obtiene una respuesta 200 OK con sus datos. Si no se encuentra un producto con ese ID, la API debe responder con 404 Not Found.

## POST - Crear un nuevo producto

El método POST se utiliza para agregar un producto nuevo al catálogo.

Método: POST
URL: http://127.0.0.1:5000/api/productos
Body: raw → JSON

En Postman se debe enviar un JSON similar al siguiente:

{
    "nombre": "Monitor",
    "precio": 300
}


Al realizar correctamente la petición, la API debería responder con 201 Created y mostrar los datos del producto creado. El id se genera automáticamente.

[Pantallazo: petición y respuesta del POST](post.jpeg)

## PUT - Actualizar un producto

El método PUT permite modificar los datos de un producto que ya existe.

Método: PUT
URL: http://127.0.0.1:5000/api/productos/1
Body: raw → JSON

Por ejemplo, para cambiar el precio del producto con ID 1, se puede enviar:

{
    "precio": 999
}


El número 1 de la URL debe cambiarse por el ID del producto que se desea actualizar.

Si el producto existe, la respuesta será 200 OK con la información actualizada. Si el ID no existe, se obtiene un 404 Not Found.

[Pantallazo: petición y respuesta del PUT](put.jpeg)

## DELETE - Eliminar un producto

Finalmente, el método DELETE permite eliminar un producto del catálogo.

Método: DELETE
URL: http://127.0.0.1:5000/api/productos/1
Body: No se necesita.

Al igual que en el método PUT, el 1 debe reemplazarse por el ID del producto que se desea eliminar.

Si el producto existe, la API devuelve un 200 OK junto con un mensaje indicando que se realizó la eliminación. Si no existe, se devuelve un 404 Not Found.

[Pantallazo: petición y respuesta del DELETE](delete.jpeg)

## instalamos el gunicorn
usamos el comando pip install gunicorn
## creamos el archivo requirements
usamos el comando pip freeze > requirements.txt
## actualizamos el github
usamos el paso a paso del git 
git add .
git commit -m "Actualización"
git push
## Ingresamos a render
entramos a la pagina de render e iniciamos sesion con github 
creamos un new web service
conectamos con nuestro repositorio
en el Start Command ponemos gunicorn app:app
y le damos deploy web service
## creacion del web server 
si todo sale bien y lo hicimos de manera correcta 
se debería observar que:
El repositorio fue descargado.
Las dependencias fueron instaladas.
El build terminó correctamente.
La aplicación inició.
El servicio quedó disponible.
## Obtener la URL de la aplicación
Una vez finalizado correctamente el despliegue, Render proporciona una URL pública bajo el dominio:
https://nombre-del-servicio.onrender.com
Los Web Services de Render reciben automáticamente un subdominio onrender.com. También es posible configurar posteriormente un dominio propio.

## Verificar la aplicación
Abrir la URL proporcionada por Render:
https://nombre-del-servicio.onrender.com
y comprobar:
La página carga correctamente.
Los endpoints de la API responden.
El frontend puede comunicarse con el backend.
La conexión con la base de datos funciona.
Las variables de entorno están disponibles.
No aparecen errores en los logs.
Si se trata de una API, también se pueden probar endpoints como:
GET /api/health
en nuestro caso seria:
https://taller3-wfze.onrender.com/
y listo, compruebas ponindo lops ends del get, post, put and get y todo deberia funcionar correctamente
## Consideraciones finales
Los productos se almacenan directamente en una lista de Python, por lo que los datos se mantienen solamente mientras el servidor está ejecutándose.
Si se detiene y vuelve a iniciar la aplicación, los productos regresan a los valores iniciales definidos en el código.
Para las peticiones que envían información en el body, como POST y PUT, es necesario seleccionar en Postman Body → raw → JSON.
Al seleccionar JSON, Postman enviará automáticamente el encabezado Content-Type: application/json, que permite que Flask interprete correctamente la información recibida.


