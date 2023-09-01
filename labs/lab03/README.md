Aluno(_ra_, nome)  
Restaurante(_id_restaurante_, nome, endereco)  
Cardapio(_id_cardapio_, id_restaurante, data, refeicao)  
id_restaurante: chave estrangeira para Restaurante

Porção(_id_porção_, nome_no_cardapio, tipo_de_porção, quantidade_produzida, quantidade_consumida)  
CardapioOferece(_id_porção_, _id_cardapio_)  
_id_porção_: Chave estrangeira para Porção  
_id_cardapio_: Chave estrangeira para Cardápio  

Ingrediente(_id_ingrediente_, nome, unidade_de_referencia)  
IngredientePorção(_id_ingrediente_porção, id_ingrediente, quantidade)  
id_ingrediente: Chave estrangeira para __Ingrediente__  

IngredienteIngrediente(_id_ingrediente_principal_, id_ingrediente_secundario, proporção_ingrediente_secundario)  
id_ingrediente_principal: Chave estrangeira para __Ingrediente__  
id_ingrediente_secundario: Chave estrangeira para __Ingrediente__  

Nutriente(_id_nutriente_, nome)
NutrienteIngrediente(_id_nutriente_, _id_ingrediente_, proporcao_nutriente_ingrediente)  
_id_nutriente_: Chave estrangeira para __Ingrediente__
_id_ingrediente_

Consumo(_id_consumo_, id_porcao, ra_aluno, data, refeicao_do_dia)
ra_aluno: chave estrangeira para Aluno
id_porcao: chave estrangeira para Porção

