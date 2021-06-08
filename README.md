# VPC: Repositorio para las prácticas

<p align="justify"> 
En este repositorio encontrarás el resultado del trabajo para las prácticas de la asignatura de **Visión Por Computador (VPC)** del máster IARFID impartido en la Universidad Politécnica de Valencia. El trabajo ha sido realizado por el alumno **Luis Serrano Hernández**.
</a>

Dentro del repositorio podrá encontrar cada trabajo bajo la siguiente estructura de ficheros y archivos:

* TAREA
  * *accuracies.csv*
  * *models*
  * *jupyter_notebooks*
  * *training_graphs*

<p align="justify"> 
Antes de que detallemos su contenido y utilidad, debemos de tener en cuenta que hay uno de ellos para cada tarea. Además, hay que saber que cada trabajo se ha logrado llevar a cabo en base a la realizaciónn de varios intentos con diferentes configuraciones de los modelos. Cada uno de estos intentos se puede distinguir del resto por un identificador unitario.
</a>

## Accuracies

<p align="justify"> 
El archivo de nombre *accuracies.csv* es, como su nombre indica, un CSV con los valores de *accuracy* para las distintas pruebas realizadas en cada trabajo. No presentamos este archivo en primer lugar sin una buena razón; la columna de nombre *id* contiene los anteriormente mencionados identificadores únicos para cada configuración. Cafa fila de la tabla implícita en el documento relaciona las configuraciones con sus atributos y resultados. En todas ellas podemos encontrar información por el valor de *accuracy* en test de los distintos modelos, así como el número de parámetros del mismo lado. Adicionalmente, algunas configuraciones tienen también asociada una nota detallando algún dato de la implementación, o incluso el tiempo de ejecución aproximado que tomó cada epoch.
</a>

## Jupyter Notebooks

<p align="justify"> 
Directorio con los cuadernos Jupyter para cada configuración. Es fácil asociar a que modelo le corresponde cada uno, pues el nombre de los  cuadernos corresponde con el identificador presentado en la tabla. En estos cuadernos te puedes topar con el resultado de la última ejecución, pero sobretodo, el programa que crea los modelos que han dado los resultados expresados en la tabla. Téngase en cuenta que laos cuadernos han sido desarrolldos dentro de 
</a>

## Modelos

<p align="justify"> 
Un sencillo directorio con la descripción de los modelos para cada prueba. Se presenta en formato de texto plano y consiste en el resumen que ofrece *Keras* de los modelos cuando se le solicita con el método *sumary()*. Además, se separa una sección extra con más detalles sobre la implmentación que el resumen puede no haber ofrecido. Entre estos detalles, en ocasiones, hay una referencia a la posible inspiración del modelo. La forma de asociar cada modelo con su correspondiente descripción es la misma que en el caso de los cuadernos.
</a>

## Grafos de entrenamiento

<p align="justify"> 
Por últomo, el directorio con más interés gráfico *:)*. En él directorio, y bajo el mismo procedimiento que con los anteriores, podemos relacionar los modelos con la evolución de su entrenamiento y podemos hacerlo siguiendo el mismo concepto que en los casos anteriores: su identificador se corresponde con el nombre del archivo. Los gráficos son una buena forma de comprender de un vistazo la naturaleza del modelo. En estos aparecen enfrentadas la *accuracy* para validación y para entrenamiento época a época, lo que también sirve para determinar si se ha producido sobreentrenamiento.
</a>

