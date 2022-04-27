# AWS-CLOUDWATCH
Este repositorio consta en la creación de una métric amuy simple por medio del CLI de AWS. Es decir, como resutlado obtendremos una métrica, creada por nosotros además de las que nos ofrece CloudWatch.


# Tutorial -documentación

Vamos a seguir al documentación oficial de Cloudwatch, especialmente sobre su call: PUT-METRIC-DATA, que se encuentra en la siguiente dirección: https://docs.aws.amazon.com/cli/latest/reference/cloudwatch/put-metric-data.html

# Pasos: 

Vamos a replicar el ejemplo que aparece en la documentación, nada nuevo. Entonces:

1. Abrimos el Shell de AWS como hemos hecho en otros tutoriales: 

```
aws cloudwatch put-metric-data --metric-name Buffers --namespace MyNameSpace --unit Bytes --value 231434333 --dimensions InstanceID=1-23456789,InstanceType=m1.small
```

Lanzaremo ese mismo comando sobre el CLI de AWS, donde indicaremos el valor de nuestra métrica, el tipo de instancia y el identificador. 

2. Abrimos cloudwatch: 

Nos posicionamos en métricas, y veremos que efectivamente, en All en la región especificada, tendremos un grupo de recursos, es decir de métricas nuestras donde aparecera, uno con un nombre que nos sonará. Entonces, si clickamos ahí, nos posicionaremos en la métrica que acabamos cde crear. En las gráficas no vamos a ver casi nada, porque acabamos de crear el invento, pero en sí; está ahí. 

:)
