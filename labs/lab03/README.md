Aluno(_ra_, nome)
Restaurante(_id_restaurante, nome, endereço)
Cardapio(_id_cardapio_, _id_restaurante, data, refeicao)
 ---- relacao
CardapioPorção(_id_
Porção(_id_porção_, nome_no_cardapio, tipo_de_porção, quantidade_produzida, quantidade_consumida)
Ingrediente(_id_ingrediente_, nome, unidade_de_medida, quantidade)
Nutriente(_id_nutriente_, nome)

Consumo(_id_consumo_, _id_porcao_, _id_aluno_, data, refeicao_do_dia)
---- relacao
