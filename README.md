### Escuela Colombiana de Ingeniería
### Arquitecturas de Software - ARSW

## Escalamiento en Azure con Maquinas Virtuales, Sacale Sets y Service Plans

### Dependencias
* Cree una cuenta gratuita dentro de Azure. Para hacerlo puede guiarse de esta [documentación](https://azure.microsoft.com/es-es/free/students/). Al hacerlo usted contará con $100 USD para gastar durante 12 meses.
Antes de iniciar con el laboratorio, revise la siguiente documentación sobre las [Azure Functions](https://www.c-sharpcorner.com/article/an-overview-of-azure-functions/)

### Parte 0 - Entendiendo el escenario de calidad

Adjunto a este laboratorio usted podrá encontrar una aplicación totalmente desarrollada que tiene como objetivo calcular el enésimo valor de la secuencia de Fibonnaci.

**Escalabilidad**
Cuando un conjunto de usuarios consulta un enésimo número (superior a 1000000) de la secuencia de Fibonacci de forma concurrente y el sistema se encuentra bajo condiciones normales de operación, todas las peticiones deben ser respondidas y el consumo de CPU del sistema no puede superar el 70%.

### Escalabilidad Serverless (Functions)

1. Cree una Function App tal cual como se muestra en las  imagenes.

![](images/part3/part3-function-config.png)

![](images/part3/part3-function-configii.png)

2. Instale la extensión de **Azure Functions** para Visual Studio Code.

![](images/part3/part3-install-extension.png)

3. Despliegue la Function de Fibonacci a Azure usando Visual Studio Code. La primera vez que lo haga se le va a pedir autenticarse, siga las instrucciones.

![](images/part3/part3-deploy-function-1.png)

![](images/part3/part3-deploy-function-2.png)

4. Dirijase al portal de Azure y pruebe la function.

![](images/part3/part3-test-function.png)

5. Modifique la coleción de POSTMAN con NEWMAN de tal forma que pueda enviar 10 peticiones concurrentes. Verifique los resultados y presente un informe. \
   **Comando:** newman run Test.postman_collection.json -n 10 \
   ![image](https://github.com/Tianrojas/Lab10-ARSW_LOAD-BALANCING_AZURE_II/assets/62759668/86a6d460-6058-4da2-8576-aff9b4a5e6a4) 

7. Cree una nueva Function que resuleva el problema de Fibonacci pero esta vez utilice un enfoque recursivo con memoization. Pruebe la función varias veces, después no haga nada por al menos 5 minutos. Pruebe la función de nuevo con los valores anteriores. ¿Cuál es el comportamiento?. \
   ![image](https://github.com/Tianrojas/Lab10-ARSW_LOAD-BALANCING_AZURE_II/assets/62759668/ba4f3eab-3412-40c1-ac6e-c7c42da6ff5b)

**Preguntas**

1. **¿Qué es un Azure Function?**
   Un Azure Function es un servicio de cómputo sin servidor en Microsoft Azure que permite ejecutar código en respuesta a eventos sin necesidad de aprovisionar o administrar servidores de manera explícita. Permite la ejecución de funciones individuales de forma escalable y automática.

2. **¿Qué es serverless?**
   Serverless es un modelo de computación en la nube donde el proveedor de servicios gestiona automáticamente la infraestructura, permitiendo a los desarrolladores centrarse en escribir código y crear aplicaciones sin preocuparse por la administración de servidores subyacentes.

3. **¿Qué es el runtime y qué implica seleccionarlo al momento de crear el Function App?**
   El runtime es el entorno de ejecución donde se ejecutarán las funciones. Al seleccionar el runtime al crear un Function App, se elige el lenguaje de programación y las bibliotecas compatibles. Esto afecta la forma en que se desarrollan las funciones y qué características específicas del lenguaje están disponibles.

4. **¿Por qué es necesario crear un Storage Account de la mano de un Function App?**
   Un Storage Account es necesario para almacenar la configuración, registros y otros datos utilizados por el Function App. Además, se utiliza para almacenar información de estado, especialmente en situaciones donde las funciones se escalan horizontalmente, permitiendo compartir datos entre instancias de funciones.

5. **¿Cuáles son los tipos de planes para un Function App? ¿En qué se diferencian? Mencione ventajas y desventajas de cada uno de ellos.**
   Hay tres tipos de planes para un Function App: Consumption Plan, Premium Plan y Dedicated (App Service) Plan.
   - **Consumption Plan:** Se factura según el consumo de recursos y es adecuado para cargas de trabajo intermitentes y ligeras. Escala automáticamente según la demanda.
   - **Premium Plan:** Ofrece ventajas como ejecución más rápida y escalado automático, pero se paga una tarifa fija por la capacidad reservada.
   - **Dedicated (App Service) Plan:** Proporciona control total sobre el entorno, pero requiere la gestión manual del escalado y tiene un costo fijo asociado.

6. **¿Por qué la memoization falla o no funciona de forma correcta?**
   La memoization puede fallar si la función depende de datos mutables o si la entrada de la función no cumple con los requisitos de inmutabilidad. También puede haber problemas si no se gestiona adecuadamente la expiración de la memoria caché.

7. **¿Cómo funciona el sistema de facturación de las Function App?**
   El sistema de facturación de las Function App se basa en el consumo de recursos, como el tiempo de CPU y el consumo de memoria, así como en el número de ejecuciones. En el plan de Consumo, solo se paga por los recursos utilizados durante la ejecución de las funciones, lo que hace que sea un modelo rentable para cargas de trabajo variables y ligeras. En otros planes, se paga una tarifa fija, independientemente del consumo exacto.

* Informe
