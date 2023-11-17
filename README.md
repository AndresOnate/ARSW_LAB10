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

Realizamos una prueba y comprobamos que la función retorne el resultado esperado:

![image](https://github.com/AndresOnate/ARSW_LAB10/assets/63562181/09758d62-86ef-4b83-b99f-ff7ba2c854d7)


5. Modifique la coleción de POSTMAN con NEWMAN de tal forma que pueda enviar 10 peticiones concurrentes. Verifique los resultados y presente un informe.

Se crea la colección de POSTMAN para enviar las peticiones:

![image](https://github.com/AndresOnate/ARSW_LAB10/assets/63562181/91e3c452-5560-4ddc-b56d-fe266c188a93)

7. Cree una nueva Function que resuleva el problema de Fibonacci pero esta vez utilice un enfoque recursivo con memoization. Pruebe la función varias veces, después no haga nada por al menos 5 minutos. Pruebe la función de nuevo con los valores anteriores. ¿Cuál es el comportamiento?.

**Preguntas**

* ¿Qué es un Azure Function?
  Azure Functions es un servicio sin servidor de Microsoft Azure que permite a los desarrolladores escribir, desplegar y ejecutar funciones de manera rápida y eficiente. Elimina la necesidad de administrar la   
  infraestructura subyacente, escala automáticamente según la demanda y se integra de manera nativa con otros servicios de Azure. Puedes desarrollar funciones en varios lenguajes, desencadenarlas en respuesta a 
  eventos específicos, y solo pagar por el tiempo de ejecución efectivo, lo que lo hace ideal para cargas de trabajo intermitentes o con picos de demanda.
  
* ¿Qué es serverless?
  Serverless es un modelo de computación en la nube en el que los desarrolladores pueden construir, implementar y ejecutar aplicaciones sin tener que preocuparse directamente por la gestión de servidores 
  subyacentes. En un entorno serverless, la infraestructura es proporcionada y administrada por el proveedor de servicios en la nube, y los desarrolladores se centran únicamente en escribir el código para sus 
  funciones o servicios. El término "serverless" no significa que no haya servidores en absoluto, sino que los desarrolladores están liberados de la tarea de gestionar la infraestructura. Las funciones y 
  servicios se ejecutan en entornos efímeros y escalan automáticamente según la demanda. Esto permite un modelo de pago por uso, ya que solo se factura por el tiempo de ejecución real de las funciones.
  
* ¿Qué es el runtime y que implica seleccionarlo al momento de crear el Function App?

  El término runtime se refiere al periodo en el que un programa o aplicación está activo y en pleno funcionamiento. Durante este tiempo de ejecución, el programa se comunica con los componentes del sistema 
  operativo y del hardware para cumplir con las instrucciones que ha recibido. En Azure Functions, hay varias opciones de runtime, y la elección del runtime tiene implicaciones en términos de lenguajes de 
  programación compatibles y características disponibles. Algunos de los runtimes comunes incluyen: .NET, Node.js, Java, Python, etc.

  La elección del runtime afecta la disponibilidad de bibliotecas y características específicas del lenguaje, así como la forma en que se manejan ciertos aspectos, como las dependencias y las configuraciones. 
  Es importante seleccionar el runtime que mejor se alinee con tus preferencias y requisitos de desarrollo.Al crear un Function App en Azure, puedes especificar el runtime durante el proceso de configuración 
  inicial.
  
* ¿Por qué es necesario crear un Storage Account de la mano de un Function App?
  Azure Functions necesita una cuenta de Azure Storage para crear una instancia de la aplicación de funciones. La creación de un Azure Storage Account junto con un Azure Function App está relacionada con la 
  necesidad de gestionar y almacenar datos de forma persistente, así como facilitar la integración y el manejo de información entre los diferentes servicios de Azure. 
  
* ¿Cuáles son los tipos de planes para un Function App?, ¿En qué se diferencias?, mencione ventajas y desventajas de cada uno de ellos
  - Plan de consumo: Azure proporciona todos los recursos de cálculo necesarios. No tiene que preocuparse de la administración de recursos y solo paga por el tiempo que haya empleado en la ejecución del código.
  - Plan Premium: especifique un número de instancias activadas previamente que siempre están en línea y preparadas para responder de inmediato. Cuando se ejecuta la función, Azure proporciona todos los 
    recursos informáticos adicionales que sean necesarios. Se paga tanto por las instancias activadas previamente que se ejecutan de forma continua como por todas las instancias adicionales que se usen cuando 
    Azure reduce y escala horizontalmente la aplicación.
  - Plan de App Service: se ejecutan las funciones igual que aplicaciones web. Si ya usa App Service para las otras aplicaciones, las funciones pueden ejecutarse en el mismo plan sin costo adicional.

* ¿Por qué la memoization falla o no funciona de forma correcta?
  
* ¿Cómo funciona el sistema de facturación de las Function App?

  En el caso del Plan de Consumo, los usuarios pagan únicamente por el tiempo de ejecución de las funciones, basándose en el número de ejecuciones, tiempo de ejecución y memoria utilizada. Este plan es 
  óptimo para cargas de trabajo con fluctuaciones, ya que escala automáticamente y solo incurre en costos durante la ejecución de funciones.

  ![image](https://github.com/AndresOnate/ARSW_LAB10/assets/63562181/5bfbfc91-578f-4a2e-b300-17e7e675ac58)

  En el Plan Premium se fundamenta en el número de segundos de núcleo y memoria utilizados en instancias necesarias y precalentadas. Se mantiene al menos una instancia activa por plan para     
  garantizar un arranque rápido. Este plan proporciona precios más predecibles y mayor control sobre la escalabilidad y la latencia de arranque, siendo una opción ideal para aplicaciones con requisitos más     
  constantes.
  
  ![image](https://github.com/AndresOnate/ARSW_LAB10/assets/63562181/cbb2f5b0-1e8a-49e7-9721-0016c3f5a850)

  En el plan de App Service se establece una tarifa constante por las aplicaciones de funciones, equiparándolo a otros recursos de App Service como las aplicaciones web. Este plan ofrece 
  un mayor control sobre el entorno de ejecución y es adecuado para cargas de trabajo que requieren recursos dedicados y configuraciones específicas. La elección del plan depende de los requisitos particulares 
  de la aplicación y las preferencias en términos de escalabilidad y control.
  
* Informe

Para evaluar el rendimiento de la Azure Function App, ejecutamos peticiones concurrentes utilizando Newman, como se menciona en el enunciado del laboratorio, se realizarán 10 solicitudes concurrentes
:
```
newman run Newman.postman_collection.json & newman run Newman.postman_collection.json & newman run Newman.postman_collection.json & newman run Newman.postman_collection.json & newman run Newman.postman_collection.json & newman run Newman.postman_collection.json & newman run Newman.postman_collection.json & newman run Newman.postman_collection.json & newman run Newman.postman_collection.json & newman run Newman.postman_collection.json
```
Tras analizar los tiempos de respuesta, se observó que se encontraban en el rango de 23 a 24 segundos. Al revisar las estadísticas de rendimiento en el portal de Azure, se identificó un alto consumo de recursos,

![image](https://github.com/AndresOnate/ARSW_LAB10/assets/63562181/677239f3-05c4-4c46-bea4-17a44bc443bc)

Para obtener información más detallada, se realizó una prueba con 10 iteraciones. Los resultados mostraron un tiempo promedio de respuesta consistente con el rango encontrado durante las ejecuciones concurrentes, y todas las solicitudes se completaron con éxito.

![image](https://github.com/AndresOnate/ARSW_LAB10/assets/63562181/948ee6a1-040a-4e5b-8de7-b8e63502efba)

Este análisis sugiere que la Azure Function App puede estar experimentando una carga de trabajo intensiva, lo que contribuye a un alto consumo de recursos y, por ende, a tiempos de respuesta prolongados. Se recomienda optimizar la función.
