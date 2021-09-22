# Aluno
*  `RA:232238 - Breno Nunes Tavares`

## Tarefa de Cypher sobre Marcadores e Taxonomia

## Tarefa 1

Escreva em Cypher uma consulta que retorne os marcadores da categoria `Serviços`, sem considerar as categorias subordinadas.

### Resolução

~~~cypher
MATCH (c:Categoria {id:"Serviços"})
MATCH (m:Marcador)
WHERE (m)-[:Pertence]->(c)
RETURN m
~~~

## Tarefa 2

Escreva em Cypher uma consulta que retorne os marcadores da categoria `Serviços`, considerando as categorias subordinadas.

### Resolução
~~~cypher
MATCH (m:Marcador)
MATCH (c:Categoria)-[:Superior*]->(p:Categoria)
WHERE p.id = "Serviços"
WITH COLLECT (c) + p AS all UNWIND all as p
MATCH (m)-[:Pertence]->(p)
RETURN m
~~~
