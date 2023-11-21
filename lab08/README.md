# Equipe `LAMEV`

# Subgrupo `A`
* `Artur De Miranda Rodrigues` - `224538`
* `Eliel Oliveira da Silva` - `221437`

## Modelo Lógico do Banco de Dados de Grafos

## Perguntas de Pesquisa/Análise Combinadas e Respectivas Análises

Vamos propor uma rede de ingredientes, onde cada aresta representa que os dois ingredientes estão na mesma receita. Cada aresta tem um peso que corresponde à quantas receitas aqueles dois ingredientes aparecem juntos.

### Pergunta/Análise 1
> * Quais os ingredientes que, se removidos, teriam um maior impacto na integridade da dieta dos norte-americanos?
>   * Podemos, por meio da análise do degree centrality de cada nó inserido na rede, encontrar os ingredientes mais importantes para a dieta dos norte-americanos. Um alto degree-centrality e um alto peso em cada uma das arestas, que ligam o nó analisado a outros nós, indicam que esse ingrediente está muito presente em diferentes receitas e muitas vezes acompanhado de outros ingredientes.

### Pergunta/Análise 2
> * Com base nas conexões, como podemos visualizar grupos de ingredientes que compõem certos tipos de receitas?
>   * É possível determinar comunidades de ingredientes, com base nos ingredientes  que estão mais fortemente conectados entre si, de acordo com algum parâmetro de peso mínimo das arestas estabelecido. Por exemplo, ovo, farinha e açúcar estão fortemente ligados entre si, e poderiam ser classificados como ingredientes de confeitaria. Pode haver intersecção entre as comunidades, visto que o ovo é um ingrediente tanto de doces quanto de salgados. Portanto, uma análise interessante seria fazer uma seleção dos ingredientes que estão fortemente conectados com um dado conjunto de ingredientes previamente selecionados.

### Pergunta/Análise 3
> * Suponha que você tenha uma lista de ingredientes, e queira compor uma nova receita. Quais ingredientes você provavelmente acrescentará à essa lista?
>   * Podemos, com base nas conexões já estabelecidas, prever outros ingredientes que provavelmente tem haver com os ingredientes. Assim, seria possível montar uma receita parecida com as receitas de nossa base.
