# Comandos Avançados em Cypher

## Exercício

Faça a projeção em relação a Patologia, ou seja, conecte patologias que são tratadas pela mesma droga.

### Resolução
~~~cypher
MATCH (p1:Pathology)<-[a]-(d:Drug)-[b]->(p2:Pathology)
WHERE a.weight > 20 and b.weight > 20
MERGE (p1)-[r:Relates]-(p2)
ON CREATE SET r.weight=1
ON MATCH SET r.weight=r.weight+1
~~~

## Exercício

Construa um grafo ligando os medicamentos aos efeitos colaterais (com pesos associados) a partir dos registros das pessoas, ou seja, se uma pessoa usa um medicamento e ela teve um efeito colateral, o medicamento deve ser ligado ao efeito colateral.

### Resolução
~~~cypher
LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/drug-use.csv' AS line
MERGE (p:Person {code: line.idperson})
MERGE (d:Drug {code: line.codedrug})
MERGE (p)-[u:Uses {pathologyCode: line.codepathology}]->(d)

LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/sideeffect.csv' AS line
MERGE (p:Person {code: line.idPerson})
MERGE (q:Pathology {code: line.codePathology})
MERGE (p)-[c:Colateral]->(q)

CREATE INDEX FOR (p:Person) ON (p.code)
CREATE INDEX FOR (d:Drug) ON (d.code)
CREATE INDEX FOR (q:Pathology) ON (q.code)

MATCH (q:Pathology)<-[:Colateral]-(:Person)-[:Uses]->(d:Drug)
MERGE (d)-[c:Causes]->(q)
ON CREATE SET c.weight=1
ON MATCH SET c.weight=c.weight+1
~~~

## Exercício

Que tipo de análise interessante pode ser feita com esse grafo?

Proponha um tipo de análise e escreva uma sentença em Cypher que realize a análise.

### Resolução
~~~cypher
(escreva aqui a resolução em Cypher)
~~~
