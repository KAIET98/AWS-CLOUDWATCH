

Lo que vamos a hacer en este tutorial es ver si en los logs de un EC2 existe algún tipo de error. 

El EC2, se crea por medio del tutorial de ECS/ECR: https://github.com/KAIET98/AWS-ECR-ECS

Es decir, dentro de access logs, tendremos que mirar dentro del LogStream, dicho de otra manera, si hay algun 400. 


## Cramos el metric filter

### Create metric filter

1. Define Pattern

Filter pattern: 

```
400
```

2. Test Pattern

Podemos obtener datos de test, o obtener datos reales sde los logs, nosotros escogeremos la segunda opción.

Además le daremos a "Test pattern", paraobtener un resultado.

3. Next. 

4. Assign metric

En el nombre le ponemos

```
MetricFilter400Code
```

Metric Details:

En el Metric namespace ponemos: 

```
MetricFilters
```
En el metric name: 

```
MyDemoFilter
```

En el metric value: 

```
1
```

Default value: valor si no ocurre ninguna incidencia

```
0
```


### Ver el efecto

Si vamos a las metricas, veremos que no hay nada, normal, porque lo que acabamos de crear NO TIENE CARACTER RETROACTIVO. 


Dicho eto, vamos a desplegar la máquina otra vez y accederemos a ella para obtener logs.

Entonces, tal cual hemos accedido a ello, supuestamente generara, metricas. 

### Creación de Alarmas

Igual queremos estar atentos a lo que ocurra con ese Metric, por lo que dentro, de esa métrica le damos a 'Create Alarm'. 

Creando eso, podemos hacer alguna automatización.

Seleccionamos nuestra alarma, y en Condiciones, podemos bien crear un threshodl estático, con un valor que le damos nosotros, o uno para deterctar anomalias. 

Nosotros vamos a establecer, un threshold de: 50; si supera es que algo va muy mal con mi server.

Siguiente, vamos a levantar un trigger, es decir, esto tiene que desencadenar en algo. 

Tutorial de como crear un SNS: https://github.com/KAIET98/AWS-SNS-EMAILMESSAGING

Seleccionamos la modalidad "In alarm", por lo que mandaremos la informacion a una SNS existente, y tras seleccionarlo, le ponemos un nombre a la alarma: 

```
DemoMetricFilterAlarm
```

Y listo.








