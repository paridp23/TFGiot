# Configuración de DuckDNS
Una vez instalado HomeAssistant, el acceso al dashboard, tanto mediante la aplicación como por navegador, solo está disponible a través de la red local, debido a que se accede a la IP y puerto dentro de nuestra red local.  Para poder acceder al dashboard desde fuera de nuestra red local, se necesitará usar un DNS, que traducirá un nombre de domino a la IP pública de nuestro sistema. En este caso, se utilizará el complemento DuckDNS.
Primero de todo, se accederá y se instalará el complemento DuckDNS a través de la página de complementos de HomeAssistant, en la pestaña “Supervisor”. 

![image](https://user-images.githubusercontent.com/95376526/144292178-ae6964fb-f723-49a0-9653-7d60de8ab210.png)

Una vez quede instalado, se accederá a la página del servicio web de DuckDNS, donde se creará una cuenta, y una vez creada, se procederá a crear un nombre de dominio a nuestra elección. En este caso, el dominio utilizado será http://homeassistanttfgiot.duckdns.org/, como se muestra en la siguiente imagen.

![image](https://user-images.githubusercontent.com/95376526/144292202-d4a345ad-d3ba-49f4-89ce-8c9b228894ef.png)

Cuando tengamos el domino creado, se volverá al complemento de duckdns que hemos instalado en HomeAssistant, y en la pestaña configuración, rellenaremos con los datos que nos ha facilitado la página los campos de “token” y “domains”, de la siguiente forma:
```
lets_encrypt:
  accept_terms: true
  certfile: fullchain.pem
  keyfile: privkey.pem
  algo: secp384r1
token: 3b52cd8b-927d-4f11-a3bb-a2dce57e4bbe
domains:
  - http://homeassistanttfgiot.duckdns.org
aliases: []
seconds: 300
```
El último paso será realizar el mapeado de puertos. Esta configuración cambia en función del tipo de router y de la compañía telefónica que se tenga en cada caso. Deberemos de acceder a los ajustes del router, a través de 192.168.1.1, y añadir las siguientes reglas:

![image](https://user-images.githubusercontent.com/95376526/144292408-c7780a34-ab57-4487-9097-5c72d1114c1e.png)

Una vez estos pasos sean ejecutados, podemos acceder a HomeAssistant a través de la dirección de dominio que hemos creado anteriormente, tanto a través de un navegador web, como a través de la aplicación, donde en este caso se deberá de especificar dicha dirección de dominio. 

![image](https://user-images.githubusercontent.com/95376526/144292711-3e99f15f-6a06-4819-b370-e5b4944d89f9.png)
