Prueba de concepto de cómo se puede trabajar con diferentes componentes de Onesait Platform:** DataFlow, Flow Engine, Entidades, APIs, etc**. para, de forma muy sencilla, generar expedientes bancarios para distintas entidades a partir de los datos obtenidos invocando un servicio REST.




Este demostrador está realizado con un enfoque** Low Code**, ya que todo se a creado a partir de diagramas, flujos, editores y formularios desde el Control Panel de la Plataforma. 

El flujo validará los datos entrantes de distintas formas, por ejemplo, validando algunos parámetros de cada registro contra entidades virtuales o comprobando si algún parámetro necesario no está relleno.

Tras realizar las validaciones, los registros validos serán redireccionados a los distintos subflujos de inserción en función de la entidad, para completar los datos para éstas, y para almacenar los registros en la entidad que corresponda, y los expedientes descartados se almacenan en una Entidad, con un campo error que indica porque no se han podido insertar.

Finalmente, los resultados del registro de expedientes pueden verse en un Dashboard que se carga accediendo a una aplicación web que la propia Plataforma sirve, para no tener que desarrollarla desde cero, teniendo únicamente que indicar los Dashboards a los que se tendrá acceso desde el menú de la aplicación web.

**configuración del bundle tras la instalación:**

	- proyecto web :fichero application-config.js aplicar el tipo de seguridad del entorno window.securityMode = "openid" 
	- cambiar host https://development.onesaitplatform.com por el del entorno en el que se instale 
	- cambiar apiToken 8f1fdc5ab7c64f75a1aea40ce401a7c6 por el del usuario en el que se instale

- flujos de datos:
	- mainflowingestdata:
		Nodo BankForm --> HTTP --> Resource URL : cambiar host https://development.onesaitplatform.com por el del entorno en el que se instale comprobar el X-OP-APIKey si conincide con el del usuario 
		Nodo OnesaitPlatform Lookup validar -->Connection-->Token comprobar si coincide el token con el del iotclient bank_cli
		Nodo OnesaitPlatform expedient_error -->Connection-->Token comprobar si coincide el token con el del iotclient bank_cli
	- client1Insert:
		Nodo Insertar Expediente en entidad -->Connection-->Token comprobar si coincide el token con el del iotclient bank_cli
	
- Entidades	
	insertar los datos del fichero adjunto en sus respectivas entidades		