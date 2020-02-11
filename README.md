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
* Security Definitions: por defecto, API Connect nos ha creado una API Key. Aquí también es dondese definen las políticas de seguridad.
* Security: indica qué definiciones de seguridad se van a aplicar por igual a todos los recursos del API
* Properties: por si queremos definir parámetros variables por entornos
* Paths: definición de los endpoints/recursos
* Parameters: definición de parámetros globales para usar en cualquier otra parte de la definición
* Definitions: definición de objetos para entrada y salida

-----

### Security Definitions

Por defecto se crea una API Key como parámetro de cabecera, se le puede cambiar el nombre en el campo **Name** pero nunca el **Parameter name**.

Además, le vamos a añadir una política de seguridad, pulsando el botón **+** y seleccionando la opción **OAuth**. Podemos configurarla como queramos pero el campo importante es el **Flow**, que en este caso usaremos la opción **Application**, que es lo equivalente a un **Client Credentials**. El campo **Token URL** es obligatorio pero podemos poner cualquier cosa.

Crearemos unos scopes, uno para el listado de cuentas **accounts_list.read** y otro para el detalle de cuenta **account_details.read**.

### Properties

Creamos una nueva propiedad llamada **target-url**, que será la URL que utilicemos para dar respuesta a la API, usaremos esta: https://cheredif-eval-test.apigee.net/

### Paths

Creamos 2 recursos, uno para mostrar un listado de cuentas **únicamente una /** y otro para mostrar el detalle de una cuenta **/{account_id}**. Nos quedamos con las operaciones GET, aunque dentro de cada recurso podemos definir varias operaciones con distinto verbo.

Dentro de cada operación tenemos que añadir tanto los parámetros de entrada como los de salida.

### Parameteres

Podemos definir parámetros de entrada que se van a repetir en la definición del API, para así solo definirlos una vez y luego referenciarlos.

Definimos la cabecera **Authorization** y la marcamos como obligatoria.

### Definitions

Aquí se definen los objetos JSON de entrada y salida.

Definimos los objetos necesarios para montar la siguiente estructura
```json
{
  "accountsList": [
    {
      "accountId": "1234567890",
      "alias": "MyAccount1",
      "mainBalance": {
        "amount": 10,
        "currency": "EUR"
      },
      "lastUpdateDate": "01/20/2020"
    }
  ]
}
```
