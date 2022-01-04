
Para poder obtener los datos que se mandan a través de Home Assistant, se necesitará crear un Event Hub Namespace dentro del Portal Azure. Para ello, primero se ha de crear un Resource Group que contenga dicho Event Hub.

![image](https://user-images.githubusercontent.com/95376526/148106624-c0d54373-c91f-4e28-9990-ea557ed22b12.png)

Se utilizará una suscripción, debido al servicio de pago, y se creará con un nombre especificado como Resource Group.

Seguidamente, se creará un Namespace, utilizando como Resource Group el que hemos creado anteriormente (en este caso, HomeAssistant), y se elegirá de nuevo la suscripción. Se le dará un nombre en Namespace, y se continuará con su creación.

![image](https://user-images.githubusercontent.com/95376526/148107040-a005bbe2-5cf0-4c9c-ab95-b30bae8679de.png)

Una vez lo tengamos generado, necesitaremos la Connection String para poder añadir a nuestro archimo configuration.yaml de HomeAssistant, y que genere la comunicación entre HomeAssistant y Azure.

Para la obtención, entraremos en el menú de All Resources, seleccionaremos el Event Hub que hemos generado, y en el nuevo menú izquierdo, seleccionaremos Shared Acces Policies, y a continuación, Add para generarla.

![image](https://user-images.githubusercontent.com/95376526/148107651-a01532f4-9784-462e-9922-cbfda71c888c.png)

Una vez se le de un nombre, añadiremos la Connection String a nuestro configuration.yaml de la siguiente manera: 

```
azure_event_hub:
  event_hub_instance_name: myeventhub
  event_hub_connection_string: Endpoint=xxxx
```
