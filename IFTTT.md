# Configuración de IFTTT
Para la integración del servicio IFTTT en este trabajo, como primer paso se necesitará crear o disponer de una cuenta para poder crear nuestro Applets. 
Una vez se haya iniciado sesión, se procederá a crear el primer applet, que en este caso, detectara movimiento (o ausencia de movimiento) en nuestro multisensor, y lo escribirá en una spreadsheet de Google Drive. Para ello, apretaremos sobre el botón de crear. 
La parte del IF será nuestro desencadenante, el cual recibirá una petición web, y hará una acción, que definiremos en el Then.
En la parte de IF, escogeremos Webhooks. Una vez dentro de Webhooks, escogeremos “Receive a web request”, y le daremos un nombre, que en este caso será “evento movimiento”, como se muestra en la siguiente imagen. 

![image](https://user-images.githubusercontent.com/95376526/144298026-961710fc-8659-4e47-b8cb-e91afcfbde3c.png)

Ahora, en la parte del Then, escogeremos “Google Sheets”, y una vez dentro, escogeremos la opción de “New row added to spreadsheet”.
Dentro de las opciones, deberemos de elegir como se llamará el archivo, el formato de las líneas, y en que directorio de nuestro Google drive se guardará. En este caso, quedará de la siguiente forma:

![image](https://user-images.githubusercontent.com/95376526/144298046-d3271ad2-0c21-4669-b62c-a15d0c0c8612.png)

De esta forma, nuestro applet esta creado y a la espera de recibir una petición web, pero necesitamos nuestra API para poder ejecutar, que obtendremos del siguiente enlace:
https://ifttt.com/maker_webhooks/settings
Una vez dentro, la podremos encontrar en la URL

![image](https://user-images.githubusercontent.com/95376526/144298073-38b6023b-1700-4237-af52-a144e2a83aba.png)
 
Acto seguido, pasaremos a nuestro hub de HomeAssistant, e instalaremos el addon de IFTTT Webhook.

![image](https://user-images.githubusercontent.com/95376526/144298094-f5f41198-a363-4b12-aa1d-d47031a93c9f.png)

 
Una vez instalado, pasaremos a editar nuestro documento “configuration.yaml” (en este caso, a través del addon “File editor”, pero se puede editar extrayendo la tarjeta SD de nuestra raspberry y editando el archivo desde nuestro ordenador). En este documento, añadiremos las siguientes dos líneas de código, pero con la API que se haya obtenido anteriormente.
```
ifttt:
  key: cEpiZ2tc4e7i8Nkxxxxxxxx
```
Guardados los cambios, nos desplazaremos hacia el apartado de automatizaciones, añadiremos un desencadenante, el cual en este caso es la detección del movimiento a través del Multisensor 6 como muestra la siguiente imagen:

![image](https://user-images.githubusercontent.com/95376526/144298171-9f060364-15c6-4a55-b6e4-6c0c4897da68.png)

Y como acciones a realizar, editaremos directamente en YAML:

![image](https://user-images.githubusercontent.com/95376526/144298179-1838324e-37af-4bf6-9bda-69434115e68b.png)

Y añadiremos las siguientes líneas de código:
```
service: ifttt.trigger
data_template:
  event: evento_movimiento
  value1: movimiento detectado
```
De esta manera, cuando nuestro sensor de movimiento detecte movimiento, lo guardará en nuestro google sheets, añadiendo una línea con un registro de hora, y las dos variables que hemos determinado en IFTTT, como se puede observar en la siguiente foto: 

![image](https://user-images.githubusercontent.com/95376526/144298215-dce06b0c-8a00-4c2e-9cf3-ada274db2f61.png)

Para añadir una línea cuando deje de haber movimiento se aprovecha el mismo applet que hemos creado, pero se debe de crear una nueva automatización . 
En este caso el desencadenante será el dejar de detectar movimiento:

![image](https://user-images.githubusercontent.com/95376526/144298226-e1a9edc8-947b-4fe4-881f-63d2af7c9741.png)
 
Y en la acción se dejará el siguiente código para distinguirlo de la detección de movimiento:
```
service: ifttt.trigger
data_template:
  event: evento_movimiento
  value1: movimiento no detectado
```

De la misma forma que se ha creado una automatización con el sensor de movimiento, se ha creado dos automatizaciones diferentes para aprovechar que IFTTT da la posibilidad de crear 3 applets de forma gratiuita.
La primera de estas automatizaciones adicionales es la detección del estado de una puerta, abierta o cerrada, mediante el sensor "Door/Window Sensor 7", y el funcionamiento del mismo se comporta de la misma manera que el sensor anterior.
La segunda es un poco diferente, debido a que se utiliza como sensor un móvil con la aplicación de HomeAssistant instalada, y que como desencadenante, se usa la localización de mi dispositivo móvil dentro de un radio cercano de mi casa.
Al crear esta nueva automatización, el tipo de desencadenante deberá de ser "Dispositivo", y el desencadenante será este dispositivo en la zona, como se muestra en la siguiente imagen:

![image](https://user-images.githubusercontent.com/95376526/144475745-704c97cc-c484-48e2-acac-a7e71b2f9f09.png)

Como acciones, se añadirán dos. La primera, encender nuestro switch, dando electricidad (podemos imaginar que se trata de un switch que controla la calefacción) como se muestra a continuación:

![image](https://user-images.githubusercontent.com/95376526/144476041-d8c0267c-8060-48da-bc5b-1b0caedfd5bb.png)

Y se añadirá también un YAML como evento de zona, donde se guardará un registro de que estamos llegando a casa en nuestro Google Sheets. 
```
service: ifttt.trigger
data_template:
  event: evento_zona
  value1: llegando a casa
```
