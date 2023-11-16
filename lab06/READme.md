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
CREATE INDEX FOR (d:Drug) ON (d.code)
CREATE INDEX FOR (p:Pathology) ON (p.code)
CREATE INDEX FOR ()-[t:Treats]-() ON (t.personId)
CREATE INDEX FOR ()-[s:SideEffect]-() ON (s.weight)
CREATE INDEX FOR (p:Person) ON (p.personId)

LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/drug-use.csv' AS line
MERGE (d:Drug {code: line.codedrug})
MERGE (p:Pathology {code: line.codepathology})
MERGE (d)-[t:Treats {personId: line.idperson}]-(p)

LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/sideeffect.csv' AS line
MERGE (p:Person {personId: line.idPerson})
MERGE (q:Pathology {code: line.codePathology})
MERGE (p)-[c:Colateral]->(q)

MATCH (p:Person)-[c:Colateral]-(d:Pathology)
MATCH ()-[t:Treats]-(q:Drug)
WHERE p.personId = t.personId
MERGE (q)-[s:SideEffect]->(d)
ON CREATE SET s.weight = 1
ON MATCH SET s.weight = s.weight + 1
~~~

## Exercício

Que tipo de análise interessante pode ser feita com esse grafo?

Proponha um tipo de análise e escreva uma sentença em Cypher que realize a análise.

### Resolução
~~~cypher
// primeiro vamos criar uma relação que nos dá a densidade das relações entre droga-trata-patologia, ou seja, quantas pessoas usaram tal droga para tratar uma patologia.

MATCH (d:Drug)-[t:Treats]-(p:Pathology)
MERGE (d)-[q:DensityTreats]-(p)
ON CREATE SET q.weight = 1
ON MATCH SET q.weight = q.weight + 1

// podemos estabelecer limiares para pegar remédios que são muito usados para tratar certas doenças, bem como para pegar efeitos colaterais que estão mais ligados à certos medicamentos. Assim, podemos descobrir os remédios mais usados para uma doença, e que estão associados poucos ou muitos efeitos colaterais

MATCH (p)-[r:DensityTreats]->(q)
WHERE r.weight > 15
MATCH (p)-[s:SideEffect]->(q)
WHERE s IS NULL OR s.weight < 15
RETURN p, q
~~~
