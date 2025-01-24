Underfitting: Um modelo muito simples para o problema e que erra por isso
Overfitting: Modelo muito treinado para o conjunto de treino e teste mas que tem pouca capacidade de generalização

Regularization: Forçar o modelo a trabalhar fora do ótimo (que resultaria em overfitting), é dar uma complexidade grande ao modelo mas limitando ele para que não use toda capacidade a fim de controlar a variância e buscando um bom fit

## Como restringir, como fazer a regularização
Mudar os coeficientes de parte da rede por parâmetros muito pequenos por exemplo

O normal é fazer uma mudança na loss, que se soma ao valor da loss original
$L̃(X , w) = L(X , w) + α R(w)$  aqui o alpha irá controlar a força desse regularizador
R deve levar os pesos para mais próximo de zero (menos certeza, menos influência)

A idéia é produzir a mesma entrada mas com pesos menores, que gera uma rede mais generalista
![[Pasted image 20241219160606.png]]

### L2 x L1
- L2 - Irá utilizar todas as informações providas para fazer as decisões (mas tenta levar as sinapses para 0)
- L1 - Irá focar toda a atenção em algumas poucas features (ele gosta de setar sinapses como 0, 0 mesmo)

# Early Stopping
O modleo passa por um momento que melhora tanto para o conjunto de teste quanto para o conjunto de validação, mas depois, começa a estabilizar o resultado para o validação (mas com erro sob o conjunto de validação subindo lentamente) enquanto o de treino continua a descer.
O ideal é você olhar o gráfico abaixo e quando o de validação começar a subir, parar de treinar

![[Pasted image 20241219163006.png]]

É comum identificar quantas épocas são necessárias e depois juntar o conjunto de vlaidação com o conjunto de treino e então treinar. Assim você garante que não irá ter overfitting enquanto consegue um conjunto de treino maior.
