# API Connect
Registro en IBM Cloud: [IBM Cloud](https://www.ibm.com/es-es/cloud "IBM Cloud")

-----

Lo primero que necesitamos es crear una instancia de API Connect en nuestra cuenta de IBM Cloud.

En la página principal, pulsar el botón **Create resource** azul de arriba a la derecha, seleccionamos API Connect de la lista y pulsamos el botón **Create** azul de abajo a la derecha.

Una vez creado, podemos acceder al API Manager abriendo el menú de la izquierda y seleccionando la opcion **Resource List** y en la sección **Cloud Foundry services** lo encontraremos. Por defecto se nos abrirá el API Manager una vez creada la instancia.

-----

### Creación de un API

Al entrar a API Connect la primera vista es la del catálogo, debemos movernos a **Draft**, seleccionándolo en el menú de arriba a la izquierda **>>** y movernos a la sección de APIs.

Con el botón **Add +** podemos elegir una opción para crear una nueva API, las principales son:
* New API: abre el editor gráfico
* Import API from a file or URL: por si ya tenemos un yaml en local o en algún repositorio

Elegimos la primera opción y se nos abrirá una ventana donde deberemos rellenar los siguientes campos:
* Title: nombre del API que se expondrá hacia fuera
* Name: nombre interno del API, para uso de API Connect, **debe ser único**
* Base Path: base path del API
* Version: versión del API, **también única para un mismo Name interno**

En este caso vamos a crear la API Accounts y cuando rellenemos todos los campos pulsamos en el botón **Create API**.

-----

### Definición del API

La primera pestaña que se nos muestra es el editor gráfico, conforme vayamos rellenado campos y creando definiciones, se irá traduciendo a lenguaje swagger en la pestaña **Source**.

En el menú de la izquierda tenemos acceso directo a los principales objetos que se pueden definir en swagger. Los más importantes son:
* Info: solo faltaría por añadir la descripción del API
* Base Path: viene relleno con lo que indicamos al crear el API
* Security Definitions: por defecto, API Connect nos ha creado una API Key, podemos cambiarle el nombre en el campo **Name**. Aquí también es donde definiremos las políticas de seguridad.
  * fdas
