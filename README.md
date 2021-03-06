# VPC: Repositorio para las prácticas

---
## El Repositorio

<p align="justify"> 
En este repositorio encontrarás el resultado del trabajo para las prácticas de la asignatura de <b>Visión Por Computador (VPC)</b> del máster IARFID impartido en la Universidad Politécnica de Valencia. El trabajo ha sido realizado por el alumno <b>Luis Serrano Hernández</b>.
</p>

Dentro del repositorio podrás encontrar cada trabajo bajo la siguiente estructura de ficheros y archivos:

* TAREA
  * <i>accuracies.csv</i>
  * <i>models</i>
  * <i>jupyter_notebooks</i>
  * <i>training_graphs</i>

<p align="justify"> 
Antes de que detallemos su contenido y utilidad, debemos de tener en cuenta que hay uno de ellos para cada tarea. Además, hay que saber que cada trabajo se ha logrado llevar a cabo en base a la realizaciónn de varios intentos con diferentes configuraciones de los modelos. Cada uno de estos intentos se puede distinguir del resto por un identificador unitario.
</p>

### Accuracies

<p align="justify"> 
El archivo de nombre <i>accuracies.csv</i> es, como su nombre indica, un CSV con los valores de <i>accuracy</i> para las distintas pruebas realizadas en cada trabajo. No presentamos este archivo en primer lugar sin una buena razón; la columna de nombre <i>id</i> contiene los anteriormente mencionados identificadores únicos para cada configuración. Cafa fila de la tabla implícita en el documento relaciona las configuraciones con sus atributos y resultados. En todas ellas podemos encontrar información por el valor de <i>accuracy</i> en test de los distintos modelos, así como el número de parámetros del mismo lado. Adicionalmente, algunas configuraciones tienen también asociada una nota detallando algún dato de la implementación, o incluso el tiempo de ejecución aproximado que tomó cada epoch.
</p>

### Jupyter Notebooks

<p align="justify"> 
Directorio con los cuadernos Jupyter para cada configuración. Es fácil asociar a que modelo le corresponde cada uno, pues el nombre de los  cuadernos corresponde con el identificador presentado en la tabla. En estos cuadernos te puedes topar con el resultado de la última ejecución, pero sobretodo, el programa que crea los modelos que han dado los resultados expresados en la tabla. Téngase en cuenta que laos cuadernos han sido desarrolldos dentro de 
</p>

### Modelos

<p align="justify"> 
Un sencillo directorio con la descripción de los modelos para cada prueba. Se presenta en formato de texto plano y consiste en el resumen que ofrece <i>Keras</i> de los modelos cuando se le solicita con el método <i>sumary()</i>. Además, se separa una sección extra con más detalles sobre la implmentación que el resumen puede no haber ofrecido. Entre estos detalles, en ocasiones, hay una referencia a la posible inspiración del modelo. La forma de asociar cada modelo con su correspondiente descripción es la misma que en el caso de los cuadernos.
</p>

### Grafos de entrenamiento

<p align="justify"> 
Por últomo, el directorio con más interés gráfico <i>:)</i>. En él directorio, y bajo el mismo procedimiento que con los anteriores, podemos relacionar los modelos con la evolución de su entrenamiento y podemos hacerlo siguiendo el mismo concepto que en los casos anteriores: su identificador se corresponde con el nombre del archivo. Los gráficos son una buena forma de comprender de un vistazo la naturaleza del modelo. En estos aparecen enfrentadas la <i>accuracy</i> para validación y para entrenamiento época a época, lo que también sirve para determinar si se ha producido sobreentrenamiento.
</p>

---
## Los Tabajos

<p align="justify"> 
Esta sección tiene un aspecto que se asimila más al de una memoria, en contraposición a la anterior, que se limitaba a presentar los contenidos del repositorio. Aquí se va a presentar un pequeño resumen de los modelos empleados y un pequeño razonamiento de porque han sido escogidos, dados los objetivos. La estructura para todas las tareas es la misma: primeramente se presenta el problema en cuestión, junto a los objetivos; en segundo lugar se mostrará una tabla con los resultados obtenidos para la tarea; junto al identificador del modelo empleado aparecerá el resultado. Seguidamente se hanlará de las decisiones de diseño y se presentarán, en caso de haberlos, algunos datos de interés observados. Finalmente, se comentaran las conclusiones pertinentes.
</p>

### CIFAR10

<p align="justify">
CIFAR10 es un pequeño subconjunto en proporcion a los 80 millones de pequeñas imágenes que el <i>Canadian Institute for Advanced Research</i> fue capaz de recopilar. Sus características principales son:
</p>
 
 * El subconjunto es de 60.000 imágenes
 * Cada imagen tiene forma de 32x32x3
 * Hay 50.000 muestras para entrenamiento
 * Hay 10.000 muestras para test
 * Hay 10 clases, con un reparto balanceado de 6.000 imágenes cada una.
 * Las clases son mutuamente excluyentes

Y los objetivos se plantearon como una tanda de propuestas sencillas, para <i>romper mano</i>:

 * Implementar redes <b>convolucionales</b> sencillas
 * Implementar modelos <b>VGG</b>
 * Implementar formas de <b>data augmentation</b>

y otra tanda, más elaborada:

* Implementar topologías </b>WideResNet</b>
* Implementar topologías </b>DenseNet</b>

Como ya se ha antticipado, primero presentamos los resultados y luego los discutimos. Para este caso, los modelos desarrollados dan estos resultados:

| ID                         | Accuracy | Error | Parámetros totales | Parámetros Entrenables | Tiempo / época (s) |
|----------------------------|----------|-------|--------------------|------------------------|--------------------|
| basic                      | 0.842    | 0,158 | 1840330            | 1838346                | 20                 |
| VGG11                      | 0.872    | 0,128 | 32221058           | 32215554               | 29                 |
| VGG16                      | 0.905    | 0,095 | 37721154           | 37712706               | 36                 |
| VGG11_DA                   | 0,787    | 0,213 | 32221058           | 32215554               | 30                 |
| VGG16_DA                   | 0,834    | 0,166 | 37721154           | 37712706               | 176                |
| VGG11_DA_b                 | 0.844    | 0,156 | 32221058           | 32215554               | 30                 |
| WideResNet_K8              | <b>0,9</b> | 0,03  | 23377900         | 23362922               | 176                |
| WideResNet_K4_NoPreTrained | 0,778    | 0,212 | 5860298            | 5853098                | 76                 |
| WideResNet_K8_NoPreTrained | 0.855    | 0,145 | 2337729            | 23362922               | 198                |
| DenseNet                   | 0.852    | 0,148 | 1084428            | 1065708                | 215                |
| DenseNet_Batch32           | 0.885    | 0,115 | 1084428            | 1065708                | 108                |

<p align="justify">
El primero objetivo fue hacer la implementación de redes convolucionales sencillas, el modelo en cuestión es el llamado <i>basic</i> y también incorpora un generador de imágenes sencillo para aportar algo de DA. El modelo es directamente el ofrecido en la práctica y obtiene el resultado expuesto, que podemos tomar como referencia. El siguiente paso fue implementar topologías VGG. En todo caso, salvo se diga lo contrarior, y esto vale para todo el texto, los modelos más avanzados están construidos sobre los anteriores, por lo que si alguna característica no se especifica, segurmaente la comparta con su predecesor; toda la información en los directorios <i>models</i>. Continuando con las redes VGG, suimplementación resultó sencilla y los resultadso acompañaron. Podemos observar un aumento proporcional en este caso con el aumento en la accuracy y el coste temporal por época, aunque este último dato se tiene solo como referencia, pues las máquinas de Google Colab no son todas igual de capaces.
</p>

<p align="justify">
Los últimos resultados obtenidos daban la confianza para empezar a probar con distintas combinaciones del generador de imágenes. No obstante, los resultados no acompañaron la primera vez; bajo las configuraciones <i>VGG11_DA</i> y <i>VGG16_DA</i> se obtienen unos resultados considerablemente peores que en los casos en los que no se modifica el DA. Las cambios al respecto se habían hecho a imitación de la combinación que formó parte de la mejor solución a este problema, propuesto en otra asignatura del máster. Pero, contra todo pronóstico, esta configuracióin era un lastre para los resultados. Se entiende que la resolución de las imágenes no da mucho juego a ese respecto y sobretodo, aplicar el volteo vertical es una decisión terrible, pues como podemos ver en <i>VGG11_DA_b</i>, donde se desactivo, se logra una reducción del error superior al 5%. Reflexionando sobre ello, es cierto que quizá es poco común encontrar aviones del revés (no como los gatos), por lo que tiene sentido dejarlo así.
</p>

<p align="justify">
Llegados a este punto comienza la materia avanzada. Tenemos 3 configuraciones de <i>WideResNets</i> y 2 de DenseNet. Las fuentes para el desarrollo de las <i>WidwResNets</i> son dos, este post de <a href="https://www.kaggle.com/zjaume/resnet-cifar10"><i>Kaggle</i></a> para la versión con pesos iniciales automáticos y este <a href="https://github.com/keras-team/keras-contrib/blob/3fc5ef709e061416f4bc8a92ca3750c824b5d2b0/keras_contrib/applications/wide_resnet.py">repositorio</a> de <i>Kaggle</i> sobre las mismas. En cuanto a las <i>DenseNets</i>, ambas versiones implementadas son sin pesos aleatorios y la fuente es también un <a href="https://github.com/keras-team/keras-contrib/blob/3fc5ef709e061416f4bc8a92ca3750c824b5d2b0/keras_contrib/applications/densenet.py">repositorio</a> de <i>Keras</i>. Podemos ver que la <i>WideResenet</i> de <i>k=4</i> entrena aparentemenro mucho más rápido que la de <i>k=8</i>, pero el beneficio también es palpable. El gato al agua se lo lleva la red que partía con pesos ya preentrenados en la misma tarea, que consigue un arrollador 97% de <i>accuracy</i>. Las <i>DenseNet</i> no dan tanto para comentar en esta ocasión, salvo que han dado bastantes problemas para implementar y que finalmente, por el coste temporal, se ha descartado la idea de crear una de estas redes con los pesos preentrenados, a semejanza de la anterior expuesta. Viendo la tendencia, era una red de gran potencial.
</p>

<p align="justify"> 
En cuanto a las conclusiones, todos los modelos han tenido la misma base, como se ha comentado, pero se ha podido percibir que tal vez no era la mejor. Por un fallo de diseño inicial, el tamaño de <i>batch</i> se estableción a 100 y el número de épocas a 75. Lo que pudo pareceer una nimiedad al comienzo, haciendo el experimento de reducir el tamaño de lotes a 32 (<i>DenseNet</i> Vs <i>DenseNet_Batch32</i>), queda en evidencia. También era el mismo el planificador de enfriamiento del factor de aprendizaje y podemos apreciar en muchos gráficos que la tasa de validación varía demasiado de cara al final en demasiadas ocasiones. Finalmente, asumimos los fallos que han resultado evidentes, pero el resultado es altamente satisfactorio.
</p>

### LFW

<p align="justify">
*Labeled Faces in the Wild</i> es el nombre que recibe el conjunto de datos que recoge las caras de miles de individuos y les asigna una etiqueta de <i>género</i>. A destacar sobre el conjunto de datos:
</p>

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

* Definir un modelo que obteng amás de un <b>97%</b> de <i>accuracy</i>
* Definir un modelo que obteng amás de un <b>92%</b> de <i>accurac</i> con <b>menos de 100.000</b> parámetros

<p align="justify">
Las configuraciones para los modelos y sus respectivos resultados se presenatn en la tabla siguietne. Ahora se discutirán con más detalle, pero toda la información a su respecto puede obtenerse de los contenidos del directorio <i>gender</i> del repositorio.
</p>

| ID                         | Accuracy | Error | Parámetros totales | Parámetros Entrenables |
|----------------------------|----------|-------|--------------------|------------------------|
| a1                         | 94,67    | 5,33  | 11551426           | 11543298               |
| a2                         | <b>97,09</b>| 2,91  | 11551426           | 11543298               |
| b1                         | 85,57    | 14,43 | 89810              | 89506                  |
| b2                         | 87,12    | 12,88 | 98194              | 97810                  |
| b3                         | 85,35    | 14,65 | 98194              | 97810                  |
| b4                         | 86,67    | 13,33 | 98194              | 97810                  |
| StartingCNN                | 0.955    | 0,045 | 1342690            | 1340898                |
| StartingCNN_64x64I         | 0.955    | 0,045 | 687330             | 685338                 |
| StartingCNN_32x32I         | 0.945    | 0,055 | 294114             | 292322                 |
| StartingCNN_16x16I         | 0.902    | 0,098 | 195810             | 194018                 |
| StartingCNN_32x32_b        | <b>0.927</b>| 0,073 | 75122              | 74226                  |

<p align="justify">
Las configuraciones que tienen un identificador que comienza por <i>a</i> o por <i>b</i> son simples intentos de fuerza bruta de superar las marcas. Con <i>a</i> y un total de 11551426 ya se logra supera el primer objetivo. Cuando comienza por <i>a</i> y <i>b</i> pertecenecen al primer y segundo objetivo, respectivamente. Cuando se ha mencionado fuerza bruta se hacía referencia a tomar el modelo <i>basic</i> usado en la tarea anterior y añadirle capas y profundidad manualmente hasta alcanzar el objetivo. Aún así, observese que el número de parámetros entrenables entre los dos modelos del primer objetivo no varía, es en la modificacióin de otros hiperparámetros que se logra. El segundo objetivo se intentó lograr capando por distintas partes <i>a2</i>, siendo <i>b2</i> la mejor aproximación, pero lejos de ser un buen objetivo.
</p>

<p align="justify">
Es entonces cuando el recomendado <a href="https://www.researchgate.net/figure/Distribution-of-the-LFW-database-images-over-the-ethnicity-in-the-individual-folds_fig5_228888218">paper</a> entra en escena. <i>StartingCNN</i> está hecho a semejanza de lo que los autores describen como su punto de partida de cara a encontrar la red minimalista óptima para el reconocimiento basado en rostros. No obstance, cadece del apoyo por preproceso que podía tener la original, pues las imágenes no se recentran hacia la faz. Aún así, el resultado es estupendo; con 10 veces menos parámetros, se obtiene un error similar a <i>a2</i>, el mejor resultado hasta ahora. Posteriormente, se procede a reducir el tamaño de las imagenes de entrada; esto reduce considerablemente el número de parámetros y podemos observar que hasta un tamaño de entrada de 32x32 no se aprecian grandes pérdidas, mientras se ha partido el número de parámetros entre 4. Además de reducir el tamaño de entrada, se había adaptado la red a una similar a la propuesta <i>I</i> de los autores del paper, siendo finalmente bastanet adaptada. Una vez decidido el tamaño de entrada ideal, se redujo a la mitad el ancho de las capas convolucionales y el número de neuronas en la capa densa. El resultado, el segundo objetivo cumplido con menos del 75% de parámetros permitidos requerido.
</p>

<p align="justify">
Las conclusiones aquí son más positivas, tal vez sea por la experiencia ganada, pero en el desarrollo de esta tarea se ha seguido una metodología firme y certera. Los resutados avalan el esfuerzo. Es sorprendente ver que se pueden obtener grandes resultados con redes realmente pequeñas. También que, si bien la mayoría de los parámetros suelen residir en la parte densa, si se marca un bajo objetivo de estos, es necesario atacar la parte convolucional.
</p>


## Otros

Con solo estas dos tareas queda lejos la puntación máxima. Reiterando, de nuevo, el trabajo realizado es satisfactorio, pero el resquemor de no haber llegado a más está presente. No considero, en esta ocasión, haberme organizado mal, pero sí que no he sido capaz de estar en todo lo que se me exigía. Aún con todo, ha sido un placer y yo me marcho a seguir trabajando en más asuntos.
