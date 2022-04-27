

La funcionalidad de EventBridge, es prácticamente la misma que CloudWatchEvents, pero con más funcionalidades. Además, AWS va a inicar una migración a este servicio. 

Entonces, dentro de la consola de EventBridge, Events, EventBuses, veremos que dentro de 'Default event bus', ya tenemos una cola de eventos, que podemos empezar a modificar y crear sobre el. Son los que se crean al crear la cuenta en AWS. 

Sin embargo, podemos crear nuestro event bus, entonces dentro de 'Custom Event bus', vamos a seleccinoar "Create Event BUS". 

## Creacion de event bus

Nombre: 

```
central-event-bus-v2
```

También, podemosincluso pbulcar los mensajes, y guardarlos indefinidamente, lo vamos a ahcer por lo que "Event archive"  lo vamos a posicionar como "Enabled". 

Archive name: 

```
central-event-bus-v2-archive
```

También seleccionaremos el "Schema discovery", por lo que automaticamente inferira el schema desde los eventos de esta cola de eventos. 

ATENCION! Si necesitamos ofrecer un "Cross-account access", tendremos quee ditar tambien el apartado de "Resource-based policy". 

Si no ten emos un resoruce-based policy, solo el dueño del bus podra enviar mensajes a ello. 

Creamos. 

## LO ponemos a funcionar. 


Para poder activar esto necesitamos desplegar un Rule, porlo que vamos allá.

### Creamos un rule

1. Define rule detail: 


Name: 

```
DemoRuleEVENTSBRIDGE
```

Event bus: seleccionamos el tipo de "Bus", seleccionaremos el "Default". 

Luego, podemos definir un Rule type:

A) Schedule: es deir, que el rule corra cada hora por ejemplo. 

B) Rule with an event pattern: es decir, que el rule, corre cada vez que p ase algo. Selccionamos

2. Build event pattern

Event source: 

Seleccionamos AWS, aunque se puede hacer desde otra manera. 


Sample event: 

Esto es una cosa nueva qu ehan sacado, es decir que podemos refereniar el sample event creando un patetrn, o usar el sample event ara testear si realmente el pattern funciona o no. Lo vamos a probar. 

Selccionamos: EC2. NO SELECCIONAMOS EL AUTO-SSCALING, sino que bajaos un poco y selccioanmos el 'EC2 INSTANCE STATE-CHANGE NOTIFICATION'. 

Esto nos genera el evento automatiamente. Es decir, nos genera un JSOn que se va a mandar como evento cada vez que por ejemplo, en este caso  haya un 'State change notification'. 

Tambien hay que tener en cuenta que podemos escoger un tipo de evento u otro. Este por ejemplo, el primero, va a mandar un aviso cada vez que este en 'Pending', pero vamos que si lo cambiamos a 'Sample-event 2', veremos que el 'state' de abajo cambia de 'pending', a 'runnig', por lo que mandara  el aviso cada vez que la instancia este en 'running'. 


Lo mismo, pero neustro objetivo recoger un evento cada vez que la instancia va al estado de 'Stopped', porlo que, vamos a tener que cambiar el Sample Event a dicho estado. 


Event pattern:  

Lo que vamos a ahcer, es crear ahora el event pattern ahora si que si: 

-Event source: EC2, 
-Event type: En neustro caso siguienod la linea nterior escogemos el 'EC2 INSTANCE STATE-CHANGE NOTIFICATION'. 

Specific state: stopped y terminated. 

Entonces, habiendo hecho lo de Sample event y Event pattern, podemos darle a la tecla de 'Test pattern' y nos verificara si loque hemos hecho en Event Pattern concuerda con lo de 'Sample event'




3. Select targets


Selccionarmeos a donde queremos que desencadene esto, nosotros elegiremos el SNS topic, (Si no tiees uno tiens la fomracion de como crearlo aqui: https://github.com/KAIET98/AWS-SNS-EMAILMESSAGING), y queremos mandar un mensaje a mi topic, cada vez que la instancia este termiando o parado. 

4. Configure tags

Next.

5. Review and create


Create. 



### Testeamos el invento: 

Si linkeamos el SNS con ese topic a nuestro email y luego, paramos una isntania nos tiene que aparecer un email en nuestra bandeja de entrada. 

