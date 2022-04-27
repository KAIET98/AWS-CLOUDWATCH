

Esto, es un tutorial para crear los eventos de CloudWatch. Para ello es necesario reealizar primero el tutorial de CloudWatchAalarms_SNS (https://github.com/KAIET98/AWS-CLOUDWATCH/blob/main/CloudWatchAlarms_SNS.md).

## Creamos un rule: 

1. Event source: vamos a escoger la modalidad de 'Event Pattern', Service Name: 
```
EC2
```

Event type: EC2 Instance State-change Notification. Es decir, vamos a medir un rule para cuando cambie de status el EC2. 

Specific state: "PENDING", es decir, cada vez que algun EC2 cambie al estado de Pending, nos saltara el rule. 


2. Target: 

Es decir, dodne va a desencadenar esta acción, en nuestor caso vamos a desencadenarlo en un email, entonces, nos interesa hacerlo por mediod del SNS Topic (si no tienes ninguno el tutorial para hacerlo: https://github.com/KAIET98/AWS-SNS-EMAILMESSAGING)


En cuanto al configure input, vamos a escoger el "Marched event" dicho de otra manera, el evento que nos crea en "Event source", se va a enviar por medio del mail. 

## Configurar los detalles

Nombre: 

```
DemoRule
```

Creamos.

## Lo probamos

Cogemos EC2, y lanzamos un t2.mico, y lo lanzamos. Estára 'initiated', entonces, saltara a 'pending', entonces, tras estar en pending a empezarlo, nos mandara un email, desde CloudWatchEvent, SNS. 