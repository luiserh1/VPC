# VPC: Repositorio para las prácticas

---
## El Repositorio

<p align="justify"> 
En este repositorio encontrarás el resultado del trabajo para las prácticas de la asignatura de **Visión Por Computador (VPC)** del máster IARFID impartido en la Universidad Politécnica de Valencia. El trabajo ha sido realizado por el alumno **Luis Serrano Hernández**.
</a>

Dentro del repositorio podrás encontrar cada trabajo bajo la siguiente estructura de ficheros y archivos:

* TAREA
  * *accuracies.csv*
  * *models*
  * *jupyter_notebooks*
  * *training_graphs*

<p align="justify"> 
Antes de que detallemos su contenido y utilidad, debemos de tener en cuenta que hay uno de ellos para cada tarea. Además, hay que saber que cada trabajo se ha logrado llevar a cabo en base a la realizaciónn de varios intentos con diferentes configuraciones de los modelos. Cada uno de estos intentos se puede distinguir del resto por un identificador unitario.
</a>

### Accuracies

<p align="justify"> 
El archivo de nombre *accuracies.csv* es, como su nombre indica, un CSV con los valores de *accuracy* para las distintas pruebas realizadas en cada trabajo. No presentamos este archivo en primer lugar sin una buena razón; la columna de nombre *id* contiene los anteriormente mencionados identificadores únicos para cada configuración. Cafa fila de la tabla implícita en el documento relaciona las configuraciones con sus atributos y resultados. En todas ellas podemos encontrar información por el valor de *accuracy* en test de los distintos modelos, así como el número de parámetros del mismo lado. Adicionalmente, algunas configuraciones tienen también asociada una nota detallando algún dato de la implementación, o incluso el tiempo de ejecución aproximado que tomó cada epoch.
</a>

### Jupyter Notebooks

<p align="justify"> 
Directorio con los cuadernos Jupyter para cada configuración. Es fácil asociar a que modelo le corresponde cada uno, pues el nombre de los  cuadernos corresponde con el identificador presentado en la tabla. En estos cuadernos te puedes topar con el resultado de la última ejecución, pero sobretodo, el programa que crea los modelos que han dado los resultados expresados en la tabla. Téngase en cuenta que laos cuadernos han sido desarrolldos dentro de 
</a>

### Modelos

<p align="justify"> 
Un sencillo directorio con la descripción de los modelos para cada prueba. Se presenta en formato de texto plano y consiste en el resumen que ofrece *Keras* de los modelos cuando se le solicita con el método *sumary()*. Además, se separa una sección extra con más detalles sobre la implmentación que el resumen puede no haber ofrecido. Entre estos detalles, en ocasiones, hay una referencia a la posible inspiración del modelo. La forma de asociar cada modelo con su correspondiente descripción es la misma que en el caso de los cuadernos.
</a>

### Grafos de entrenamiento

<p align="justify"> 
Por últomo, el directorio con más interés gráfico *:)*. En él directorio, y bajo el mismo procedimiento que con los anteriores, podemos relacionar los modelos con la evolución de su entrenamiento y podemos hacerlo siguiendo el mismo concepto que en los casos anteriores: su identificador se corresponde con el nombre del archivo. Los gráficos son una buena forma de comprender de un vistazo la naturaleza del modelo. En estos aparecen enfrentadas la *accuracy* para validación y para entrenamiento época a época, lo que también sirve para determinar si se ha producido sobreentrenamiento.
</a>

---
## Los Tabajos

<p align="justify"> 
Esta sección tiene un aspecto que se asimila más al de una memoria, en contraposición a la anterior, que se limitaba a presentar los contenidos del repositorio. Aquí se va a presentar un pequeño resumen de los modelos empleados y un pequeño razonamiento de porque han sido escogidos, dados los objetivos. La estructura para todas las tareas es la misma: primeramente se presenta el problema en cuestión, junto a los objetivos; en segundo lugar se mostrará una tabla con los resultados obtenidos para la tarea; junto al identificador del modelo empleado aparecerá el resultado. Seguidamente se hanlará de las decisiones de diseño y se presentarán, en caso de haberlos, algunos datos de interés observados. Finalmente, se comentaran las conclusiones pertinentes.
 
</a>

### CIFAR10

<p align="justify">
CIFAR10 es un pequeño subconjunto en proporcion a los 80 millones de pequeñas imágenes que el *Canadian Institute for Advanced Research* fue capaz de recopilar. Sus características principales son:
</a>
 
 * El subconjunto es de 60.000 imágenes
 * Cada imagen tiene forma de 32x32x3
 * Hay 50.000 muestras para entrenamiento
 * Hay 10.000 muestras para test
 * Hay 10 clases, con un reparto balanceado de 6.000 imágenes cada una.
 * Las clases son mutuamente excluyentes

Y los objetivos se plantearon como una tanda de propuestas sencillas, para *romper mano*:

 * Implementar redes *convolucionales* sencillas
 * Implementar modelos *VGG*
 * Implementar formas de *data augmentation*

y otra tanda, más elaborada:

* Implementar topologías *WideResNet*
* Implementar topologías *DenseNet*

Como ya se ha antticipado, primero presentamos los resultados y luego los discutimos. Para este caso, los modelos desarrollados dan estos resultados:

| ID                         | Accuracy | Error | Parámetros totales | Parámetros Entrenables | Tiempo / época (s) |
|----------------------------|----------|-------|--------------------|------------------------|--------------------|
| basic                      | 0.842    | 0,158 | 1840330            | 1838346                | 20                 |
| VGG11                      | 0.872    | 0,128 | 32221058           | 32215554               | 29                 |
| VGG16                      | 0.905    | 0,095 | 37721154           | 37712706               | 36                 |
| VGG11_DA                   | 0,787    | 0,213 | 32221058           | 32215554               | 30                 |
| VGG16_DA                   | 0,834    | 0,166 | 37721154           | 37712706               | 176                |
| VGG11_DA_b                 | 0.844    | 0,156 | 32221058           | 32215554               | 30                 |
| WideResNet_K8              | **0,97** | 0,03  | 23377900           | 23362922               | 176                |
| WideResNet_K4_NoPreTrained | 0,778    | 0,212 | 5860298            | 5853098                | 76                 |
| WideResNet_K8_NoPreTrained | 0.855    | 0,145 | 2337729            | 23362922               | 198                |
| DenseNet                   | 0.852    | 0,148 | 1084428            | 1065708                | 215                |

<p align="justify">
El primero objetivo fue hacer la implementación de redes convolucionales sencillas, el modelo en cuestión es el llamado *basic* y también incorpora un generador de imágenes sencillo para aportar algo de DA. El modelo es directamente el ofrecido en la práctica y obtiene el resultado expuesto, que podemos tomar como referencia. El siguiente paso fue implementar topologías VGG. En todo caso, salvo se diga lo contrarior, y esto vale para todo el texto, los modelos más avanzados están construidos sobre los anteriores, por lo que si alguna característica no se especifica, segurmaente la comparta con su predecesor; toda la información en los directorios *models*. Continuando con las redes VGG, suimplementación resultó sencilla y los resultadso acompañaron. Podemos observar un aumento proporcional en este caso con el aumento en la accuracy y el coste temporal por época, aunque este último dato se tiene solo como referencia, pues las máquinas de Google Colab no son todas igual de capaces.
</a>

<p align="justify">
Los últimos resultados obtenidos daban la confianza para empezar a probar con distintas combinaciones del generador de imágenes. No obstante, los resultados no acompañaron la primera vez; bajo las configuraciones *VGG11_DA* y *VGG16_DA* se obtienen unos resultados considerablemente peores que en los casos en los que no se modifica el DA. Las cambios al respecto se habían hecho a imitación de la combinación que formó parte de la mejor solución a este problema, propuesto en otra asignatura del máster. Pero, contra todo pronóstico, esta configuracióin era un lastre para los resultados. Se entiende que la resolución de las imágenes no da mucho juego a ese respecto y sobretodo, aplicar el volteo vertical es una decisión terrible, pues como podemos ver en *VGG11_DA_b*, donde se desactivo, se logra una reducción del error superior al 5%. Reflexionando sobre ello, es cierto que quizá es poco común encontrar aviones del revés (no como los gatos), por lo que tiene sentido dejarlo así.
</a>

Llegados a este punto comienza la materia avanzada. Tenemos 3 configuraciones de *WideResNets* y 2 de DenseNet.

### LFW

*Labeled Faces in the Wild* es el nombre que recibe el conjunto de datos que recoge las caras de miles de individuos y les asigna una etiqueta de *género*. A destacar sobre el conjunto de datos:

* Contiene 13233 imágenes
* En las que aparecen 5749 personas
* Y un total de 1680 personas aparecen en más de una foto
* Está desbalanceado respecto a la realidad humana. <a href="https://www.researchgate.net/figure/Distribution-of-the-LFW-database-images-over-the-ethnicity-in-the-individual-folds_fig5_228888218">Fuente</a> de las imágenes

<div class="row">
  <div class="column">
    <img src="https://user-images.githubusercontent.com/54946908/121286669-766cbf80-c8e0-11eb-8dba-3d8d3ac06d7a.png" width=50% alt="Gender distribution" align="center">
  </div>
  <div class="column">
    <img src="https://user-images.githubusercontent.com/54946908/121286673-77055600-c8e0-11eb-921b-9fa95100e6c0.png" width=50% alt="Etnithity distribution" align="center">
  </div>
</div>

Los objetivos con respecto a este conjunto de datos se presentan de forma concisa, pero no por ello son más sencillos. Estos son:

* Definir un modelo que obteng amás de un **97%** de *accuracy*
* Definir un modelo que obteng amás de un **92%** de *accuracy* con **menos de 100.000** parámetros

Las configuraciones para los modelos y sus respectivos resultados se presenatn en la tabla siguietne. Ahora se discutirán con más detalle, pero toda la información a su respecto puede obtenerse de los contenidos del directorio *gender* del repositorio.

| ID                         | Accuracy | Error | Parámetros totales | Parámetros Entrenables |
|----------------------------|----------|-------|--------------------|------------------------|
| a1                         | 94,67    | 5,33  | 11551426           | 11543298               |
| a2                         | **97,09**| 2,91  | 11551426           | 11543298               |
| b1                         | 85,57    | 14,43 | 89810              | 89506                  |
| b2                         | 87,12    | 12,88 | 98194              | 97810                  |
| b3                         | 85,35    | 14,65 | 98194              | 97810                  |
| b4                         | 86,67    | 13,33 | 98194              | 97810                  |
| StartingCNN                | 0.955    | 0,045 | 1342690            | 1340898                |
| StartingCNN_64x64I         | 0.955    | 0,045 | 687330             | 685338                 |
| StartingCNN_32x32I         | 0.945    | 0,055 | 294114             | 292322                 |
| StartingCNN_16x16I         | 0.902    | 0,098 | 195810             | 194018                 |
| StartingCNN_32x32_b        | **0.927**| 0,073 | 75122              | 74226                  |

<p align="justify">
Las configuraciones que tienen un identificador que comienza por *a* o por *b* son simples intentos de fuerza bruta de superar las marcas. Con *a2* y un total de 11551426 ya se logra supera el primer objetivo. Cuando comienza por *a* y *b* pertecenecen al primer y segundo objetivo, respectivamente. Cuando se ha mencionado fuerza bruta se hacía referencia a tomar el modelo *basic* usado en la tarea anterior y añadirle capas y profundidad manualmente hasta alcanzar el objetivo. Aún así, observese que el número de parámetros entrenables entre los dos modelos del primer objetivo no varía, es en la modificacióin de otros hiperparámetros que se logra. El segundo objetivo se intentó lograr capando por distintas partes *a2*, siendo *b2* la mejor aproximación, pero lejos de ser un buen objetivo.
</a>

<p align="justify">
Es entonces cuando el recomendado <a href="https://www.researchgate.net/figure/Distribution-of-the-LFW-database-images-over-the-ethnicity-in-the-individual-folds_fig5_228888218">paper</a> entra en escena. *StartingCNN* está hecho a semejanza de lo que los autores describen como su punto de partida de cara a encontrar la red minimalista óptima para el reconocimiento basado en rostros. No obstance, cadece del apoyo por preproceso que podía tener la original, pues las imágenes no se recentran hacia la faz. Aún así, el resultado es estupendo; con 10 veces menos parámetros, se obtiene un error similar a *a2*, el mejor resultado hasta ahora. Posteriormente, se procede a reducir el tamaño de las imagenes de entrada; esto reduce considerablemente el número de parámetros y podemos observar que hasta un tamaño de entrada de 32x32 no se aprecian grandes pérdidas, mientras se ha partido el número de parámetros entre 4. Además de reducir el tamaño de entrada, se había adaptado la red a una similar a la propuesta *I* de los autores del paper, siendo finalmente bastanet adaptada. Una vez decidido el tamaño de entrada ideal, se redujo a la mitad el ancho de las capas convolucionales y el número de neuronas en la capa densa. El resultado, el segundo objetivo cumplido con menos del 75% de parámetros permitidos requerido.
</a>
