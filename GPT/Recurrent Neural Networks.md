![[Pasted image 20250130151902.png]]
São redes que o neurônio pode receber como entrada a própria saída e/ou a saída de outro neurônio da mesma camada
	Sendo essa saída provinda do estado de tempo anterior, uma iteração anterior
Desenrolando isso ao longo do tempo, do index a rede vai se parecer como a abaixo, sendo os azuis saídas e verdes entradas
![[Pasted image 20250130152047.png]] ![[Pasted image 20250130152551.png]]

E considerando um período determinado de tempos, conseguimos fazer backpropagation para cada instante
	Observação importante é que as sinapses são iguais ao longo do tempo, o que muda é apenas a saída do próprio neurônio que entra. (Logo, fazer esse backpropagation para alterar essas sinapses é viável) ()-> Minha nota, não foi falado explicitamente em sala
As sinapses vão ser constantes no batch, vão ser ajustadas só quando terminar o index, o tempo

# Mapping -> Flexibilidade
Podemos ter diversos tipos de saída e entrada com esse tipo de rede
![[Pasted image 20250130153515.png]]

Assim conseguimos usar essa estrutura para várias finalidades como legendar uma imagem, reconhecer uma ação de um vídeo, tradução, conversão de voz em texto, tracking em vídeo

# Backpropagation
O que se faz para ajustar é acumular a mudança, igual faz com batch em uma rede de forward propagation
Aqui, os gradientes são calculados da direita p esquerda
Para treinar dois textos, tem que rodar um texto inteiro de cada vez
Não dá para rodar os estados em paralelo, é sequencial por natureza
![[Pasted image 20250130154126.png]]

## Truncated
Devido ao custo, o que é comum de se fazer é truncar a entrada, fazer mini-batches, divisão do batch inteiro

# Problemas com essa rede
Para utilizar tangente como função de ativação deveremos assumir a entrada entra -1 e 1, já que caso contrário, irá saturar. Isso faz com que a inicialização tenha que ser cuidadosa para evitar a saturação, já que a saída vai ser sempre somada, entrada para a próxima.
	Um valor minimamente diferente de 0 já pode causar a saturação
	Basicamente, o gradiente tem que ser praticamente 1 para não fazer tudo saturar, explodir a conta do gradiente. Isso porquê há uma parte em que fica $a^k$
Tem como contornar o estouro clippando os gradientes, mas para os gradientes sumindo (menor que 1) há a necessidade de uma mudança na arquitetura

## Gradient Clipping
Basicamente é a normalização do gradiente toda vez que passar de um certo valor
![[Pasted image 20250130160036.png]]
Sendo o hiperparâmetro T algo discutido em literatura, dependente de caso. Ponto de partida -> [1,10]

## Contornando o vanishing gradient
![[Pasted image 20250130160205.png]]

### UGRNN
É como se tivesse uma torneira que define o quanto o estado anterior vai influenciar a saída atual, controlada pela função sigmoide.
	Como sigmoide tem sempre saída entra 0 e 1, o valor puro vai ser multiplicado com o estado anterior e o inverso multiplicado com a tangente, depois soma os dois e será a saída
	Podemos pensar como se houvessem duas redes, em que uma controla a rede da outra. Se um subir o outro mata, assim não vai crescer absurdamente e os gradientes não irão explodir
### LSTM
Tem o gate de esquecimento, gate de entrada e gate de saída, nas outras o estado e saída estão juntas. A célula teria um estado interno (c), um valor computado, propagado e mantido apenas para o controle dos gates
![[Pasted image 20250130162847.png]]

A derivada fica sofisticada, ms tem termos para garantir que os gradientes não sumam ou explodam, mas com gradient clipping performa melhor ainda

![[Pasted image 20250130163317.png]]

# Character-level language models
Uma rede que recebe um caractere e prediz o próximo, com 1 hot vector

Uma rede com 3 camadas, 512 nós, todos caracteres e treinado com todas as obras de Shakespeare resultou em um gerador que faz pequenas frases com sentido, com erros de pontuação a partir de uma letra aleatória.
	Sendo esse resultado impressionante por ser uma rede tão simples
Conseguiu gerar LaTex compilável
