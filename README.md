# sparkLogNasa

Cache
-------------
O comando cache persiste (armazena) em memória (default – MEMORY_ONLY) o conjuntos de dados na primeira vez que foram processados, permitindo que sejam reutilizados em outras aç?es com uma rapidez 10x mais rápidos.


MapReduce x Spark
------------------
MapReduce é mais lento que o Spark na inicializaç?o das tarefas de operaç?es de leitura de entrada e fase de map.
O Spark utiliza RDD, com o uso de cache em memória e reutilizaç?o dos dados nas fases do processamento.
O Spark executa processamento em memória - sem utilizaç?o de escrita e leitura em disco rígido como no MapReduce.


SparkContext
---------------
É o principal componente do ambiente de execuç?o do Spark. O SparkContext configura serviços internos e estabelece uma conex?o com um ambiente de execuç?o do Spark. Possui métodos e funç?es para processamento de dados, criaç?o de RDD's, processamento paralelo e outros serviços Spark.



Explique com suas palavras o que é Resilient Distributed Datasets (RDD). 
------------------------------------------------------------------------
É a tecnologia que tem o conceito de processamento distribuído e paralelo em cluster, com alta velocidade de processamento e tolerancia a falhas.


GroupByKey é menos eficiente que reduceByKey em grandes dataset. Por quê? 
-------------------------------------------------------------------------

O reduceByKey trabalha com funç?o de chave única, combinando e reduzindo dados para cada chave. Sendo assim minimizando os dados trafegados em rede e tendo uma eficiencia melhor.

O groupByKey trabalha com chave e lista de valores, gerando troca de dados em excesso podendo gerar algumas falhas, como memória insuficiente ou disco cheio.



Explique o que o código Scala abaixo faz. 
-----------------------------------------

```
// Abre o arquivo no caminho informado no método textFile do SparkContext
val textFile = sc.textFile("hdfs://...")

//  Cria uma única lista com todas as palavras encontradas no texto
val counts = textFile.flatMap(line => line.split(" ")) // quebra linha por " " 
	.map(word => (word, 1)) // Avalia uma funç?o sobre cada elemento na lista
	.reduceByKey(_ + _) // processa o conteúdo do arquivo em memória

// Salva a lista em arquivo particionado, ex.: part-0000, PART-00001, ...
counts.saveAsTextFile("hdfs://...") 
```


Referências
----------------------

http://spark.apache.org/docs/latest/rdd-programming-guide.html#rdd-persistence

http://spark.apache.org/docs/2.2.2/api/java/org/apache/spark/SparkContext.html

https://spark.apache.org/docs/latest/rdd-programming-guide.html#overview

https://www.infoq.com/br/articles/mapreduce-vs-spark

https://data-flair.training/blogs/learn-apache-spark-sparkcontext/

http://etlcode.com/index.php/blog/info/Bigdata/Apache-Spark-Difference-between-reduceByKey-groupByKey-and-combineByKey
