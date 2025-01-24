Não pode ser 0 porquê a derivada de 0 será 0, mas então qual seria o ideal?

## Small Random Numbers
Uma abordagem seria decidir os pesos dos nós com uma distribuição gaussiana centralizada em 0 e com baixo desvio padrão
	Muitas sinapses ainda terão peso 0, mas com a grande quantidade de sinapses, basta algumas diverentes para 
	Entretanto, a cada camada vai piorando a situação, muitos neurônios terão apenas 0 recebendo e saindo, veja no gráfico abaixo
	![[Pasted image 20241219152936.png]]
Se na camada, uma saída é zero, não vai ter backpropagation, vai aprender muito lento ou não aprender

## Large Random Numbers
Inicializar com números que fiquem no limite de -1 e 1 também não é funcional, porquê todas as funções de ativação vão saturar e por isso, fazer o gradiente local ser zero

## Xavier Initialization ~~(macumba)~~
Obs: Não é boa para sigmoid, pesquisar uma melhor para ela quando precisar utilizar
### Para Tanh como função de ativação
Descobriram que se utilizar como desvio padrão $σ^2 = 1/Din$ em que Din é a dimensão da entrada para a camada, o que varia entre as camadas
Diferente dos outros casos, olha como fica a propagação nas camadas
![[Pasted image 20241219153523.png]]

### Para ReLU como função de ativação (He initialization)
A reLU não gera saídas negativas e isso faz com que, aos poucos, a saída fique prejudicada
Descobriram que para a ReLU o desvio padrão ideal deve ser dobrada, ou seja $σ^2 = 2/Din$ 

