# sparkLogNasa

Cache
-------------
O comando cache persiste (armazena) em mem�ria (default � MEMORY_ONLY) o conjuntos de dados na primeira vez que foram processados, permitindo que sejam reutilizados em outras a�?es com uma rapidez 10x mais r�pidos.


MapReduce x Spark
------------------
MapReduce � mais lento que o Spark na inicializa�?o das tarefas de opera�?es de leitura de entrada e fase de map.
O Spark utiliza RDD, com o uso de cache em mem�ria e reutiliza�?o dos dados nas fases do processamento.
O Spark executa processamento em mem�ria - sem utiliza�?o de escrita e leitura em disco r�gido como no MapReduce.


SparkContext
---------------
� o principal componente do ambiente de execu�?o do Spark. O SparkContext configura servi�os internos e estabelece uma conex?o com um ambiente de execu�?o do Spark. Possui m�todos e fun�?es para processamento de dados, cria�?o de RDD's, processamento paralelo e outros servi�os Spark.



Explique com suas palavras o que � Resilient Distributed Datasets (RDD). 
------------------------------------------------------------------------
� a tecnologia que tem o conceito de processamento distribu�do e paralelo em cluster, com alta velocidade de processamento e tolerancia a falhas.


GroupByKey � menos eficiente que reduceByKey em grandes dataset. Por qu�? 
-------------------------------------------------------------------------

O reduceByKey trabalha com fun�?o de chave �nica, combinando e reduzindo dados para cada chave. Sendo assim minimizando os dados trafegados em rede e tendo uma eficiencia melhor.

O groupByKey trabalha com chave e lista de valores, gerando troca de dados em excesso podendo gerar algumas falhas, como mem�ria insuficiente ou disco cheio.



Explique o que o c�digo Scala abaixo faz. 
-----------------------------------------

```
// Abre o arquivo no caminho informado no m�todo textFile do SparkContext
val textFile = sc.textFile("hdfs://...")

//  Cria uma �nica lista com todas as palavras encontradas no texto
val counts = textFile.flatMap(line => line.split(" ")) // quebra linha por " " 
	.map(word => (word, 1)) // Avalia uma fun�?o sobre cada elemento na lista
	.reduceByKey(_ + _) // processa o conte�do do arquivo em mem�ria

// Salva a lista em arquivo particionado, ex.: part-0000, PART-00001, ...
counts.saveAsTextFile("hdfs://...") 
```


Refer�ncias
----------------------

http://spark.apache.org/docs/latest/rdd-programming-guide.html#rdd-persistence

http://spark.apache.org/docs/2.2.2/api/java/org/apache/spark/SparkContext.html

https://spark.apache.org/docs/latest/rdd-programming-guide.html#overview

https://www.infoq.com/br/articles/mapreduce-vs-spark

https://data-flair.training/blogs/learn-apache-spark-sparkcontext/

http://etlcode.com/index.php/blog/info/Bigdata/Apache-Spark-Difference-between-reduceByKey-groupByKey-and-combineByKey
