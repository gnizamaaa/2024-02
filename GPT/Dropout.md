É o processo de durante o treinamento, setar algumas sinapses ou neurîonios para não serem alteradas, com uma dada probabilidade, e aí funciona como uma masca binária sobre um vetor de bits que liga e desliga parte da rede
Exemplo, cada sinapse ter a probabilidade de 0.5 de ficar congelado por um batch, ou seja, que não vai ser alterado no back-propagation e não vai ser utilizado para o forward (mas tomando cuidado para multiplicar as entradas pelo inverso da taxa de dropout, ou seja, a taxa de quantos neurônios de uma camada estão ativos da sua entrada)

Cria um ensamble on the fly porquê algumas estruturas surgem e seguirão durante o treinamento

Força o modelo a aprender de forma redundante, ter uma representação redundante
Diminui a capacidade do modelo, porquê sempre vai estar usando metade por exemplo