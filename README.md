# Arquitetura PySpark

## Driver
- Coordena Jobs, cria o plano de execução e distribui tarefas para os executores via Task Scheduler.
- Monitora o progresso e coleta resultados.

## Executor
- Executa tarefas, armazena dados em cache, comunica progresso ao Driver.
- Possui tasks (unidades de processamento) e slots (threads disponíveis).

# Transformações Narrow vs Wide

## Narrow
- Operações locais sem dependência entre partições (ex.: map, filter).
- Mais rápidas e sem shuffling (processo de redistribuição de dados entre diferentes partições de um cluster distribuído).

## Wide
- Requerem embaralhamento de dados entre partições (ex.: reduceByKey, join).
- Mais lentas devido à redistribuição.

# Lazy Evaluation

- Transformações só são executadas quando uma ação (ex.: count(), show(), collect()) é chamada.
  
## Benefícios:
- Combina operações para eficiência.
- Evita cálculos desnecessários.

## Minimizando Shuffling:
- Prefira transformações locais como `combineByKey` em vez de `groupByKey`.
- Use `coalesce` para reduzir partições e `repartition` para redistribuir.

# Estruturas PySpark

## RDD
- Processamento baixo nível e mais flexível.

## DataFrame
- Estrutura tabular otimizada com Catalyst Optimizer.

## Dataset
- Extensão do DataFrame com segurança de tipos (principalmente em Scala/Java).

