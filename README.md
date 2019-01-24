# Callbacks-hacia-plataformas

-	[Creación de Callbacks](#creación-de-callbacks)

-	[Callback hacia un correo](#callback-hacia-un-correo)
	
-	[Losant](#losant)

	-	[Webhook](#webhook)
	
	-	[Device](#device)
	
	-	[Workflow](#workflow)
	
	-	[Backend](#backend)

	-	[Dashboard Losant](#dashboard-losant)
		
-	[Microsoft Azure](#microsoft-azure)
	
	-	[Configuración del Callback](#configuración-del-callback)
		
	- 	[Stream Analytics Azure](#stream-analytics-azure)
		
	-	[Power BI](#power-bi)
	
-	[Amazon Web Services](#amazon-web-services)
	
	-	[Callback en AWS](#callback-aws)
	
	-	[Creación de una Tabla en DynamoDB](#creación-de-una-tabla-en-dynamodb)
	
-	[Ubidots](#ubidots)
	
	- 	[Callback hacia Ubidots](#callback-hacia-ubidots)

	-	[Visualización de la información en Ubidots](#visualización-de-la-información-en-ubidots)

	- 	[Dashboard Ubidots](#dashboard-ubidots)
		
-	[Thinger io](#thinger-io)

	- 	[Callback hacia Thinger io](#callback-hacia-thinger-io)
	
	-	[Dashboard Thinger io](#dashboard-thinger-io)
		

Creación de Callbacks
---------------------

A continuación se mostrará como realizar los Callbacks hacia diferentes plataformas, es decir, mandar la información hacia una plataforma específica para presentar la información enviada por el Devkit de manera mas intuitiva y facil de entender. Para entender mas sobre los callbacks ir al siguiente link: [Callback](https://github.com/Iotnet/Callback)

### Callback hacia un correo

El mas facil de los Callbacks es hacia un correo o conjunto de correos. Cada vez que llegue al backend un mensaje de nuestro dispositivo, se enviara un mensaje a los correos configurados. Para realizar el callback, damos click en el device type de nuestro dispositivo

![aws1](https://raw.githubusercontent.com/NXTIoT/NXTIoT_DEVKIT/master/images/aws1.png?raw=true)

en la columna del lado izquierdo damos click en "Callbacks"

![aws2](https://raw.githubusercontent.com/NXTIoT/NXTIoT_DEVKIT/master/images/aws2.png?raw=true)

enseguida, en la parte superior derecha, daremos click en "NEW" y de las diferentes opciones de callbacks, seleccionaremos "Custom Callback"

![call1](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/call1.png?raw=true)

Configuramos el callback de la siguiente manera

![call21](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/call21.png?raw=true)

Damos click en OK. Con eso nuestro Callback esta hecho. La proxima vez que mandemos un mensaje de nuestro devkit, nos llegara un correo con el "Subject" que nosotros elegimos asi como la informacion que recibimos.

### Losant

Para esta parte utilizaremos el ejemplo del sensor de temperatura anterior. 

Ahora que el backend está recibiendo los mensajes del Devkit, procederemos a visualizar los datos en [Losant](https://www.losant.com/), plataforma dedicada al internet de las cosas en donde se pueden visualizar y analizar datos provenientes de dispositivos IoT, además es facil de usar ya que se configura por medio de diagramas de flujo.

Comenzaremos por crear una cuenta gratuita. Ésta nos permite registrar hasta 100 dispositivos y enviar hasta 1M de payloads.
Una vez hecha la cuenta crearemos una nueva aplicación. 

![create](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/create.png?raw=true)

EL nombre de la aplicación puede ser cualquiera, pero de manera que sea facil de reconocer. 
Enseguida daremos click en 'Create Application'

![create2](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/create2.png?raw=true)

Dentro de nuestra aplicacíon configuraremos 3 cosas: 
<br />
1: Webhook - Url en donde se enviarán todos los datos desde el backend a la plataforma.
<br />
2: Device - Dispositivo en donde Losant guardará la informacion proveniente del Devkit para posteriormente mostrarla en un dashboard.
<br />
3: Workflow - Diagrama de flujo que se activará cada vez que haya un request por parte del backend de Sigfox.

### Webhook

Dentro de nuestra aplicación nos dirigimos a la pestaña 'Webhooks' y damos click.

![webhook](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/webhook.png?raw=true)

Damos click en 'Add Webhook' y aparecerá la siguiente ventana en donde configuraremos lo siguiente: 
 - El nombre de nuevo puede ser cualquiera y lo demás lo dejamos con la misma configuración
 
![webhook2](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/webhook2.png?raw=true)

Mas abajo marcamos la opción 'Wait for reply from workflow' y seguido damos click en 'Create Webhook"

![webhook4](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/webhook4.png?raw=true)

Notaremos que al momento de crearlo nos genera una URL: 

![webhook5](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/webhook5.png?raw=true)

Esta URL la copiaremos y guardaremos para usarla posteriormente para configurar el callback de Sigfox.

### Device

Ahora, configuraremos el device en donde Losant guardará los datos provenientes de Sigfox.
En nuestra pantalla principal de la aplicacion, daremos click en 'Devices', seguido daremos click en 'Create new device'

![createdev](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/createdev.png?raw=true)

Damos click en 'Create blank device'

![createdev1](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/createdev1.png?raw=true)

En el Device Name podemos poner el nombre que queramos pero de preferencia que indentifique a nuestro dispositivo
Marcamos la casilla 'Standalone' en el Device Type

![createdev2](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/createdev2.png?raw=true)

En la parte de atributos colocamos: 

![createdev3](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/createdev3.png?raw=true)

Debemos de tener en cuenta la información que estamos leyendo y enviando desde el dispositivo.
En este caso estamos enviando unicamente la temperatura del sensor por lo que el tipo de dato que recibira Losant será un número y el nombre de la variable puede ser cualquiera, pero una que identifique nuestra información.


### Workflow

Ahora es turno de configurar el diagrama de flujo para que una vez que Losant reciba la información sepa que hacer con ella.

En nuestro menú principal de la aplicación damos click en 'Workflows', seguido damos click en 'Create Workflow'

Le damos el nombre que nosotros queramos y opcionalmente podemos asignarle una descripción.
Seguido damos click en 'Create Workflow'

Notaremos que nos abrirá un espacio de trabajo donde podremos crear nuestro diagrama de flujo.

Del lado izquierdo nos muestra todos los nodos disponibles. Tales como 'Triggers', 'User Experience', 'Data', etc.

Debido a que nuestra información esta llegando por medio de un Webhook, el diagrama de flujo se activará cada que llegue información a ese Webhook que creamos.

Por lo tanto, en el lado izquierdo en la sección de 'Triggers' buscamos por el nodo 'Webhook'

![workflow](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/workflow.png?raw=true)

Lo arrastramos y pegamos a nuestro espacio de trabajo.

![workflow1](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/workflow1.png?raw=true)

Ahora, buscaremos el nodo 'Debug'. Este nodo nos sirve para observar que esta sucediendo en determinada parte del diagrama de flujo. Lo conectaremos debajo de nuestro 'Webhook' para poder observar que información llega.

![workflow2](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/workflow2.png?raw=true)

Ahora presionaremos en 'Deploy Workflow' para guardar nuestro diagrama de flujo y quede listo para recibir información.
Dejaremos esta parte pendiente para continuar configurando el backend en Sigfox.


### Backend 

Para esta parte es necesario haber registrado el dispositivo en el backend de Sigfox.
Daremos click en 'Device Type' y buscamos por nuestro dispositivo registrado

![backend1](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/backend1.png?raw=true)

Dentro de nuestro Device Type, del lado izquierdo en el menú buscamos la opción 'Callbacks' y damos click

![backend2](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/backend2.png?raw=true)

Los callbacks nos sirven para poder jalar nuestra información del backend Sigfox a nuestra webApp, plataforma, etc.
Para nuestro ejemplo haremos un callback a Losant

Dentro de la sección 'Callbacks' damos click en 'New', seguido daremos click en 'Custom Callback'

![callback](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/callback.png?raw=true)

En la ventana que nos aparece, configuraremos nuestro callback de la siguiente manera:

![callback1](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/callback1.png?raw=true)

-	Type : Data & Uplink
-	Channel: URL // 
- 	Custom Payload Config : Variables personalizadas, decodificación del mensaje hexadecimal
-	URL Pattern : URL a la que le enviaremos la información del dispositivo
-	Use HTTP method : POST	
-	Content type : Application/json


Así nuestro callback quedará listo para poder recibir la información en Losant.

Ahora conectado nuestro sensor de temperatura y el Devkit con el código cargado, procederemos a apretar el botón para enviar la información de temperatura a Losant.
Al hacer esto iremos al diagrama de flujo previamente creado y del lado derecho presionaremos en 'Debug' 

Ahí aparecera toda la información relacionada con el nodo 'Debug'. 

![callback2](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/callback2.png?raw=true)

Cada vez que presionamos el botón del Devkit, nos aparecera nueva información relacionada a Losant y al Devkit, en particular hay un Path dentro de ese formato Json que nos interesa el cual es : 'data.query.temp'

En la cual Losant esta recibiendo la informacion proveniente del Devkit y de Sigfox. 

Tal cual esta llegando la información no se esta guardando en ningun lado por lo tanto tenemos que guardar de alguna manera esa información y para ello haremos uso de nuestro 'device virtual' previamente creado.

En nuestro diagrama de flujo buscaremos por el nodo 'Device state' y lo agregaremos a nuestro diagrama de flujo de la siguiente manera.

![callback3](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/callback3.png?raw=true)

Justo entonces nos aparecera la configuración del nodo, el cual configuraremos de la siguiente manera:

-	Device : Marcamos la opción 'Select a specific device' y en la lista buscamos por nuestro device creado anteriormente

-	State : 
	-	Data Metod: Individual Fields 
	
![callback4](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/callback4.png?raw=true)
	
Dentro de esta parte veremos que ya esta preconfigurado nuestro campo Temperatura al cual le hace falta el valor asignado. Dentro de 'Value' colocaremos el Json path en donde llegaba la información de Sigfox de la siguiente manera:
						Value : {data.query.temp}

Finalmete damos click en 'Deploy Workflow'

De esta manera nuestra información proveniente de Sigfox quedará almacenada en nuestro Device para posteriormente mostrarla en el Dashboard de Losant.

### Dashboard Losant

Con la información ya almacenada en nuestro device en Losant. Podemos visualizarla en un Dashboard sencillo.

Para ello iremos a la parte superior y daremos click en 'Dashboards', seguido de 'Create Dashboard'.

Le daremos el nombre que queramos y damos click en 'Create Dashboard'.

Nos mostrará distintos wodgets que podemos elegir para mostrar la informacion en la forma que queramos. Para este ejemplo seleccionaremos 'Gauge' y damos click en 'Customize'

![dashboard](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/dashboard.png?raw=true)

Siguiendo la siguiente configuración, le damos el nombre que queramos y buscamos por nuestra aplicación anteriormente creada.

![dashboard1](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/dashboard1.png?raw=true)

En la parte de 'Block data', en Device buscaremos por el nuestro creado anteriormente
En Attribute seleccionamos Temperatura 
En Label podemos colocar las unidades de la informacion que estemos mostrando o simplemente a que se refiere ese Widget.

![dashboard2](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/dashboard2.png?raw=true)

### Microsoft Azure

En esta sección realizaremos un Callback hacia Microsoft Azure utilizando el ejemplo del sensor de temperatura, para mandar la información y desplegarla en un dashboard donde podamos observar una gráfica de la temperatura con respecto al tiempo. Lo que necesitamos es:
<br /> -Una cuenta en [Microsoft Azure](https://azure.microsoft.com/es-mx/) 
<br /> -Un correo no personal (academico o de trabajo) para crear una cuenta en [Power BI](https://powerbi.microsoft.com/es-es/)

Entramos en nuestra cuenta de Microsoft Azure y veremos el "Panel", donde se muestran los recursos que hagamos. En este caso está vacio porque no hemos creado ninguno.

![azure1](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure1.png?raw=true)

Ahora, crearemos un nuevo recurso con el que jalaremos los datos del backend hacia Azure. Damos click en Nuevo -> Internet de las cosas -> IoT Hub

![azure2](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure2.png?raw=true)

Asignamos un nombre a nuestro recurso y en "Grupo de recursos" seleccionamos "Crear Nuevo" y le damos un nombre. Todo lo demas se queda como aparece por default. Damos click en "Crear"

![azure3](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure3.png?raw=true)

Despues de unos minutos, en las notificaciones nos mostrará un mensaje de que la implementación fue creada con éxito. Damos click en "Ir al recurso"

![azure5](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure5.png?raw=true)

Enseguida nos mostrará la informacion de nuestro recurso creado.

![azure6](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure6.png?raw=true)

Para poder realizar el Callback, necesitaremos la clave de acceso hacia nuestro recurso. Nos vamos a 
<br /> Directivas de Acceso Compartido -> iothubowner -> Cadena de conexión (clave principal). Esta clave nos servira un poco mas adelante en la configuracion de nuestro callback en el backend

![azure7](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure7.png?raw=true)

### Configuración del Callback

Regresamos al backend de sigfox para crear el Callback. Nos vamos a nuestro dispositivo y damos click en el "Device Type"

![azure8](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure8.png?raw=true)

En el panel de la izquierda damos click en Callbacks -> New

![azure9](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure9.png?raw=true)

De los posibles Callbacks, seleccionamos "Microsoft Azure Iot hub"

![azure10](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure10.png?raw=true)

Ahora tendremos que configurar el Callback. 
<br /> - En "Custom Payload Config" escribimos "temp::float:32:little-endian"
<br /> - En "Connection string" pegamos la clave que copiamos de Azure.
<br /> - En "JSON body" pegamos el siguiente codigo

<br />{
<br /> "device" : "{device}",
<br /> "data" : "{data}",
<br /> "temperatura" : "{customData#temp}",
<br /> "time" : "{time}",
<br /> "snr" : "{snr}",
<br />"station" : "{station}",
<br /> "avgSignal" : "{avgSnr}",
<br /> "seqNumber" : "{seqNumber}"
<br />}

quedando como se muestra en la siguiente imagen

![azure11](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure11.png?raw=true)

Damos Click en "Ok" y con eso queda creado nuestro Callback. Ahora verificaremos que no exista ningun error. Damos click en "Associated devices"

![azure12](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure12.png?raw=true)

hacemos click en el ID de nuestro Devkit

![azure13](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure13.png?raw=true)

y en el panel izquierdo nos vamos a "Messages" para visualizar el estatus del Callback. Presionamos el boton de nuestro Devkit para mandar un mensaje. Si todo fue correctamente configurado la flecha en Callbacks ahora permanecerá en verde como se muestra en la imagen

![azure14](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure14.png?raw=true)

Con esto queda finalizada la parte en el backend.

### Stream Analytics Azure

Regresamos a Microsoft Azure y nos vamos a
<br /> Nuevo -> Internet de las Cosas -> Stream Analytics Job

![azure15](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure15.png?raw=true)

le asignamos un nombre y en "Grupo de recursos" seleccionamos "Usar existente" y nos aparecerá por default el recurso que creamos anteriormente y damos click en crear.

![azure16](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure16.png?raw=true)

Despues de un momento, en las notificaciones nos aparecerá que la implementacion fue correcta. Damos click en ir al recurso

![azure17](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure17.png?raw=true)

Ahora ya tenemos implementado nuestro recurso de Stream Analytics.

![azure18](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure18.png?raw=true)

Damos click en "Entradas" y configuramos el método por le cual entrarán los datos provenientes del backend hacia Azure. 
<br /> -Asignamos un alias a nuestra nueva entrada
<br /> -En "Tipo de origen" seleccionamos "Flujo de datos"
<br /> -En "Origen" seleccionamos "Centro de IoT" 
<br /> -En "Opción de importación" seleccionamos "Usar centro de IoT de la suscripción actual"
<br /> -En "Centro de IoT" seleccionamos nuestro recurso creado anteriormente, en este caso se llama "devkit-test"

Los demas campos los dejamos como aparecen por defecto, quedando como se muestra en las siguientes imagenes

![azure19](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure19.png?raw=true)

![azure20](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure20.png?raw=true)

Damos click en crear. Despues de unos momentos, en las notificaciones nos indicará que la prueba de conexión fue correcta.

![azure21](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure21.png?raw=true)

Regresamos a nuestro recurso de Stream Analytics. Ahora configuraremos la parte de salida de los datos. Damos click en "Salidas"

![azure22](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure22.png?raw=true)

Asignamos un "Alias" y en "Receptor" seleccionamos "Power BI". Para esta parte necesitaremos nuestra cuenta en Power BI. Damos click en "Autorizar" y nos pedira iniciar sesión en Power BI con nuestro correo institucional o de trabajo. 

![azure23](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure23.png?raw=true)

Una vez que iniciemos sesión, nos habilitará opciones para configurar y abajo aparecerá la cuenta con la que hemos iniciado sesión en Power BI. Seleccionamos "Mi area de trabajo" y asignamos nombres al "Conjunto de datos" y a la "Tabla" que nos creará. 

![azure24](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure24.png?raw=true)

Damos click en "Crear" y como en los anteriores recursos, en las notificaciones nos mostrará un mensaje de que fué creado con éxito. Ahora configuraremos las variables que mandaremos de nuestra "Entrada de datos" hacia la "Salida de datos". Nos dirigimos hacia "Consulta" 

![azure25](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure25.png?raw=true)

Copiamos y pegamos el siguiente código.
<br /> SELECT
<br />CAST(temperatura as float) as temp,
<br />System.Timestamp AS Timestamp
<br />INTO 
<br />[*El nombre de su salida*]
<br />FROM
<br />[*El nombre de su entrada*]

Con esto definimos que queremos enviar la variable *temperatura* como una nuava variable llamada *temp* y el tiempo hacia nuestra salida(Power BI) desde nuestro recurso de entrada. Y damos click en guardar. 

![azure26](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure26.png?raw=true)

ya que tenemos configurado la entrada y salida de datos, ya podemos empezar a enviar los datos de nuestro Devkit hacia Power BI y verlos en un dashboard. Damos click en "Iniciar"

![azure28](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure28.png?raw=true)

Nuevamente damos click en "Iniciar" y despues de unos segundos nos indicará en "Ejecución". 

![azure29](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure29.png?raw=true)

Presionamos el botón de nuestro Devkit para mandar mensajes.

### Power BI

Ahora abrimos nuestra cuenta en Power BI. Nos vamos a 
<br />Mi area de trabajo -> Conjunto de Datos

y veremos nuestra variable *Temp* que definimos cuando configuramos la salida hacia Power BI. Damos click en "Crear informe"

![azure27](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure27.png?raw=true)

Seleccionamos "Gráfico de lineas" y del lado derecho marcamos nuestras variables que queremos graficar, en este caso son *temp* y *timestamp*. Enseguida se graficarán los datos que enviamos desde que "Iniciamos" el recurso de Stream Analytics. Damos click en Guardar.

![azure30](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure30.png?raw=true)

Con eso ya tenemos nuestro dashboard donde se mostrá la grafica de la temperatura con respecto al tiempo. Tenemos que dar click en "Actualizar" para que la grafica muestre los datos mas recientes.

![azure31](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure31.png?raw=true)

Por último, para detener el envio de datos, regresamos a Azure y seleccionamos "Detener"

![azure32](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/azure32.png?raw=true)

### Amazon Web Services

Ahora es el turno de hacer la integración con la plataforma de Amazon Web Services (AWS). Se utilizará el ejemplo del sensor de temperatura, sin embargo puede utilizarse el ejemplo del sensor ultrasónico.

Creamos una cuenta en la plataforma de [Amazon](https://aws.amazon.com/es/)

Una vez creada la cuenta la dejamos abierta y accedemos al backend para visualizar nuestro dispositivo. Damos click en el "Device type"

![aws1](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws1.png?raw=true)

en la columna del lado izquierdo damos click en "Callbacks"

![aws2](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws2.png?raw=true)

enseguida, en la parte superior derecha, daremos click en "NEW" y de las diferentes opciones de callbacks, seleccionaremos "AWS IoT"

![aws3](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws3.png?raw=true)

ahora tendremos que configurar el callback hacia AWS. Tener en cuenta el "External ID", ya que lo necesitaremos mas adelante para configurar la parte de AWS. Hacemos click en "Launch Stack"

![aws4](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws4.png?raw=true)

a continuación nos abrirá una pagina donde configuraremos el STACK creado en AWS. En la esquina superior derecha seleccionaremos la region, en este caso se seleccionó "US East (N. Virginia)". En la parte de "Select template" dejamos todo como está y damos click en "Next"

![aws5](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws5.png?raw=true)

ahora tenemos que configurar "Specify Details", donde necesitaremos nuestro "Account number", el cual podemos obtener en la esquina superior derecha, en Support-> Support Center

![aws13](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/aws1010.png?raw=true)

Seleccionamos un nombre para nuestro Stack. Copiamos nuestro "Account number" y lo pegamos en "AWSAccountId" en la pagina de AWS. Ahora necesitaremos el External ID que nos proporciona sigfox en el backend. Regresamos al backend, lo copiamos y lo pegamos en "ExternalId". Dejamos la region como "us-east-1" y escribimos un "Topic name". Damos click en next

![aws7](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws7.png?raw=true)

En la parte de "Options", no modificamos nada y damos click en "Next". Finalmente en el "Review", seleccionamos "I acknowledge that AWS CloudFormation might create IAM resources" y seleccionamos "Create"

![aws8](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws8.png?raw=true)

Despues de unos minutos estara creado nuestro Stack. Con esto ya queda configurada la parte de AWS del Callback.

![aws9](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws9.png?raw=true)

Ahora falta terminar el Callback en el backend de Sigfox. Una vez que aparezca la leyenda "Create_complete", seleccionamos nuestro Stack y nos vamos a la pestaña "Outputs" y Copiamos el "ARNRole".

![aws10](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws10.png?raw=true)

### Callback AWS

Pegamos el "ARNRole" que obtuvimos de AWS. En "topic", escribimos el mismo que pusimos en nuestro Stack, escogemos la misma region (US East (N. Virginia)) y escribimos el siguiente json

<br />{
<br /> "device" : "{device}",
<br /> "data" : "{data}",
<br /> "time" : "{time}",
<br /> "snr" : "{snr}",
<br />"station" : "{station}",
<br /> "avgSnr" : "{avgSnr}",
<br /> "lat" : "{lat}",
<br /> "lng" : "{lng}",
<br /> "rssi" : "{rssi}",
<br /> "seqNumber" : "{seqNumber}"
<br />}

![aws11](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws11.png?raw=true)

y damos click en OK. Con esto ya tenemos creado nuestro Callback en el backend. Para verificar que no hay ningun problema con la configuración, mandamos un mensaje hacia sigfox y observamos el indicador del callback,que debe quedar de color verde, lo que indica que se realizó de manera exitosa

![aws12](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws12.png?raw=true)

### Creación de una Tabla en DynamoDB

Ahora que tenemos nuestro Stack creado, vamos a crear una tabla por medio de DynamoDB con los datos que mandamos por medio de nuestro dispositivo. Vamos a Services-> DynamoDB

![aws13](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws13.png?raw=true)

damos click en "Crear tabla"

![aws13](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/aws1001.png?raw=true)

Ahora tenemos que configurar nuestra tabla. Le asignamos un nombre, escribimos "deviceid" en Partition Key, seleccionamos "Añadir clave de ordenación" y escribimos "timestamp" y damos click a "Crear"

![aws14](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/aws1002.png?raw=true)

despues de unos minutos, se habrá creado nuestra tabla

![aws15](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws15.png?raw=true)

ahora debemos crear una regla que nos permita enviar enviar los datos recividos hacia nuestra tabla recien creada. Nos vamos a Services-> IoT Core

![aws16](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/aws1004.png?raw=true)

y seleccionamos "ACTUAR"

![aws17](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/aws1005.png?raw=true)

damos click en "Crear"

![aws17](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/aws1006.png?raw=true)

le asignamos el mismo nombre que nuestro Stack, y agregamos una pequeña descripcion (opcional)

![aws18](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/aws1007.png?raw=true)

en el campo "Instruccion de consulta de regla" escribimos SELECT * FROM 'sigfox' donde 'sigfox' es el mismo nombre del topic que pusimos en el callback. Despues tenemos que agregar la accion que queremos que se ejecute. Damos click en "Añadir acción"

![aws17](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/aws1008.png?raw=true)

y escogemos "DynamoDB"

![aws21](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws21.png?raw=true)

posteriormente, tenemos que configurar la acción de insertar los datos en DynamoDB. Seleccionamos nuestra tabla creada anteriormente y escribimos ${device} en "Hash key value", $ {timestamp()} en "Range key value" y "payload" en "Write message data to this column"

![aws22](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws22.png?raw=true)

Creamos un nuevo role dando click en "Create a new role"

![aws23](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws23.png?raw=true)

y le asignamos el nombre "dynamodbsigfox" y damos click en "Add action"

![aws24](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws24.png?raw=true)

finalmente damos click en "Crear una regla"

![aws17](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/aws1009.png?raw=true)

una vez creada, nos aparecera en nuestras reglas

![aws25](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws25.png?raw=true)

si le damos click nos mostrará las caracteristicas de la regla que hemos creado

![aws26](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws26.png?raw=true)

Finalmente, si nos regresamos a DynamoDB->Tables->sigfox->Items, podremos ver los mensajes que enviemos por medio de nuestro Devkit

![aws27](https://github.com/NXTIoT/NXTIoT_DEVKIT/blob/master/images/aws27.png?raw=true)

### Ubidots

Ahora toca la integración con la plataforma Ubidots. Al igual que en los ejemplos pasados, en este también se utilizará la práctica del sensor de temperatura. Lo primero que se debe hacer es crear una cuenta en el siguiente link [ubidots](https://app.ubidots.com/accounts/signup/).

Una vez creada la cuenta, nos aparecerá lo siguiente

![ubi1](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi1.png?raw=true)

Nos vamos a la esquina superior derecha y damos click en nuestro usuario para desplegar un menú, donde seleccionaremos “API CREDENTIALS”, para obtener un Token que nos permitirá crear el callback. 

![ubi2](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi2.png?raw=true)

Ahora, copiamos y guardamos el token ya que sera necesario posteriormente 

![ubi3](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi3.png?raw=true)

### Callback hacia Ubidots

Enseguida creamos el callback. Vamos al backend a nuestro dispositivo y damos click en el DEVICE TYPE.

![ubi4](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi4.png?raw=true)

nos desplegara la información sobre el DEVICE TYPE. Selecionaremos CALLBACKS en el panel izquierdo

![ubi5](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi5.png?raw=true)

y seleccionamos CUSTOM CALLBACK

![ubi6](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi6.png?raw=true)

configuramos el callback de acuerdo a la imagen de abajo y en “URL Pattern” escribimos las siguiente dirección 

http://things.ubidots.com/api/v1.6/devices/{device}/?token=YOUR_TOKEN

seguida del Token que copiamos enseguida de crear nuestra cuenta.

![ubi7](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi7.png?raw=true)

y damos click en OK para terminar el callback. Con esto queda creado el callback hacia Ubidots.

### Visualización de la información en Ubidots

Ahora que nuestro Callback esta creado, ya podemos mandar la información de la temperatura de nuestro Devkit hacia la plataforma. Presionamos el botón para mandar la información de la temperatura y en el backend podremos observar el estatus del callback, el cual debe quedar en color verde

![ubi8](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi8.png?raw=true)

si regresamos a Ubidots, veremos que aparece el ID de nuestro dispositivo

![ubi9](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi9.png?raw=true)

si damos click en el nos aparecerá la variable que enviamos, en este caso es la variable “temp”

![ubi10](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi10.png?raw=true)

finalmente, si damos click, podremos ver los datos en forma de gráfica, así como un historial de la información enviada.

![ubi11](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi11.png?raw=true)

![ubi12](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi12.png?raw=true)

### Dashboard Ubidots

Para crear el dashboard, en la parte superior, damos click en “DASHBOARD”

![ubi13](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi13.png?raw=true)

en la esquina superior derecha seleccionamos “Create Widget”

![ubi14](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi14.png?raw=true)

y tendremos que seleccionar de que tipo lo queremos. En este caso seleccionaremos una gráfica sencilla

![ubi15](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi15.png?raw=true)
 
seleccionamos nuestro dispositivo así como la variable de nuestro interés, que en este caso es “temp”. Finalmente damos click en “ADD VARIABLE”

![ubi16](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi16.png?raw=true)

y ahora nuestro dashboard tendrá la gráfica de la temperatura.

![ubi17](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi17.png?raw=true)

Para agregar más Widgets a nuestro dashboard se sigue el mismo procedimiento. 

Thinger io
----------

Thinger.io es una plataforma con librerías de código abierto que permite gestionar multitud de dispositivos a través de Internet. Es gratuita para makers con las siguientes limitaciones:

-	Permite conectar un máximo de 3 dispositivos.
-	No existe limitación en cuanto a los recursos de cada dispositivo, es decir el número de parámetros a medir por los sensores que tenga conectados (más allá de su propia capacidad) o el número de parámetros a enviar a los dispositivos desde la plataforma.
-	Los valores de los parámetros recibidos en la plataforma se pueden almacenar hasta en un máximo de 10 campos (Data Buckets) diferentes. Cada Data Bucket puede almacenar datos de múltiples sensores, con una frecuencia máxima de un minuto (un almacenamiento cada minuto). 
-	Los valores de los sensores se pueden visualizar hasta un máximo de 10 pantallas gráficas de visualización de datos (Dashboards).

Creamos una cuenta en [Thinger.io](https://thinger.io/). Una vez creada la cuenta, veremos la pantalla principal. 

![thin](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/tngr.png?raw=true)

Seleccionamos Device buckets->Add bucket

![thin](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/thin2.png?raw=true)

configuramos nuestro bucket. Escribimos un ID para identificarlo, un nombre y una descripción. Lo habilitamos y en Data Source seleccionamos "From Write Call". Click en Add bucket

![thin](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/thin3.png?raw=true)

Ahora necesitamos crer el token necesario para poder conectarnos con el backend. Seleccionamos "Access Tokens"

![thin](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/thin4.png?raw=true)

Escribimos un ID y un nombre para identificarlos y en la parte de "Tokens Permissions" damos click en +Add  

![thin](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/thin5.png?raw=true)

realizamos la siguiente configuración
-	Select Permission Type -> Bucket
-	Access -> Specific resource -> nuestro bucket creado (Devkit_NXTIoT)
-	Actions -> Select specific action -> WriteBucket

click en Add

![thin](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/thin6.png?raw=true)

ahora ya tenemos creado nuestro "Access token". Este Token lo necesitaremos para la configuracion en el backend

![thin](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/thin7.png?raw=true)

### Callback hacia Thinger io

Enseguida creamos el callback. Vamos al backend a nuestro dispositivo y damos click en el DEVICE TYPE.

![ubi4](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi4.png?raw=true)

nos desplegara la información sobre el DEVICE TYPE. Selecionaremos CALLBACKS en el panel izquierdo

![ubi5](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi5.png?raw=true)

y seleccionamos CUSTOM CALLBACK

![ubi6](https://github.com/Iotnet/IoTnet_DEVKIT/blob/master/images/ubi6.png?raw=true)

realizamos la siguiente configuracion
-	Type: DATA, UPLINK	Channel: URL
-	Custom payload config: Temp::float:32:little-endian
-	URL pattern: la url debe tener el siguiente formato https://api.thinger.io/v1/users/{user_id}/buckets/{bucket_id}/data
	-	{user_id} y {bucket_id} se deben cambiar de acuerdo a nuestra cuenta y a el Id de nuestro bucket. Para este ejemplo la URL quedo como https://api.thinger.io/v1/users/gpg117/buckets/Devkit_NXTIoT/data
-	Use HTTP Method: POST
-	Headers: En esta parte es donde necesitaremos pegar el Access token que creamos
	-	Authorization: Bearer "Your Token"
-	Content type: Application/json
-	Body:
		<br />{
		<br />	"device" : "´{device}",
		<br />	"snr" : {snr},
		<br />	"rssi" : {rssi},
		<br />	"station" : "{station}",
		<br />	"latitude" : "lat",
		<br />	"longitud" : "lng"
		<br />	"temperature" : {customData#Temp}
		<br />}
		
Damos click en "OK"

![thin](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/thin8.png?raw=true)

### Dashboard Thinger io

Una vez realizado el callback, presionamos el boton para enviar un mensaje. Si nos vamos a nuestro bucket creado, veremos los mensajes enviados con nuestro Devkit

![thin](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/thin9.png?raw=true)

Damos click en "Dashboards" en el panel izquierdo. Escribimos la informacion que nos pida y damos click en "Add dashboard"

![thin](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/thin10.png?raw=true)

habilitamos el switch de la derecha y seleccionamos "Add widget"

![thin](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/thin105.png?raw=true)

realizamos la configuracion y lo guardamos

![thin](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/thin11.png?raw=true)

y en nuestro dashboard veremos la grafica de la temperatura

![thin](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/thin12.png?raw=true)

podemos agregar mas widgets para visualizar mas informacion

![thin](https://github.com/NXTIoT/Callbacks-hacia-plataformas/blob/master/images/thin13.png?raw=true)

