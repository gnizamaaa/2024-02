# Aprendizado supervisionado - Classificação

## Esquema

**x -> $f_w$ -> y**

## Termos
Aprendizado: Estimar os parâmetros w a partir das amostras, da informação de treinamento disponível
Inferência: Fazer novas predições, obter o $y=f_w(x)$

# Problemas
Regressão é quando queremos um número na saída, não uma categoria. Uma estimativa de número real
Classificação é quando temos categorias, podendo ser binária ou um número limitado e determinado de categorias (Será o foco)


# Classificação binária
## Como avaliar?
Para identificar um bom parâmetro w, precisamos de um critério, uma forma de julgar se o classificador, com esse parâmetro está bom
Utilizamos a loss, a perda
	Mais especificamente, utilizaremos iremos utilizar uma fórmula que faça a possibilidade do modelo, já treinado, dizer a resposta correta dado os pesos e entradas, chamada Maximum Likelihood Estimator
	![[Pasted image 20241121153703.png]]
		Pega cada exemplo, passa pelo modelo, vê a perda e vai somando e então vai testando w's a fim de tornar a expressão máxima de acerto

Perceba que nos restou definir $P_{model}$ que é a probabilidade de a saída estar correta, para essa função, utilizamos a função da distribuição de Bernoulli , que está presente abaixo
Com ela, é possível determinarmos a probabilidade de uma saída do classificador estar correta.
		![[Pasted image 20241121154433.png]]
Mas, isso faz com que a saída precise ser entre 0 e 1 para a conta funcionar corretamente, ou seja, torna necessário que seja um modelo probabilístico
	Inclusive, pode ser testado que ele dá 1 quando ŷ e y são iguais (1 ou 0 sendo mais fáceis de calcular) e 0 quando estão em opostos (um sendo 0 e outro 1)

Um modelo que não esteja performando bem, resultará em valores negativos de módulo alto; e um que esteja bom resultará em módulos próximos de 0, sempre negativos também
	O uso do log em cima da probabilidade é justificado exatamente para manter a monotonia (manter o mesmo sinal, indo para o mesmo lado) e não irá explodir

Juntando a expressão por completo e manipulando os logaritmos e sinal (argmin é mais fácil de se encontrar do que o mínimo, porquê há um limite que é o log ser próximo de zero quando estiver correto) podemos obter a expressão abaixo
![[Pasted image 20241121160223.png]]

Uma propriedade interessante dessa Binary Cross Entropy Loss é que podemos definir o comportamento dela através de duas funções simples para os valores de 0 e 1 (os extremos)
![[Pasted image 20241121160556.png]]

Podemos chegar a uma equação//modelagem equivalente ao utilizar KL-Divergence, apesar de partir de pontos iniciais bem diferentes (um computacional, outro matemático)
	A divergência KL mede a concordância entre duas distribuições
## Como definir $F_w$?
O requerimento, como vimos anteriormente, é ter o domínio de saída entre 0 e 1
Podemos pensar na função mais simples
$$f_w(x)=\sigma(w^Tx)$$
Sendo F_w a saída, x a entrada, w um vetor (ou matriz, a depender da entrada) de pesos e a função $\sigma$ a função sigmoide $\sigma(x) = 1/(1+e^{-x})$ 
Essa função é interessante porquê x pode ir ao infinito, que continuará limitada entre 0 e 1

## Como encontrar os parâmetros?
Podemos utilizar várias técnicas mas a "mãe" é o gradiente descendente
### Gradiente descendente
O gradiente é a tangente da curva da loss, então dada uma variação de w, o quanto varia a loss
	Para simplificar o cálculo, podemos definir o gradiente como: $$∇w L(ŷi , yi ) = (ŷi − yi )xi$$
Sabendo do gradiente, podemos "caminhar" na direção que faz o gradiente descer, para isso temos o algoritmo:
1. Pick step size η and tolerance $\epsilon$
2. Initialize w⁰
3. Repeat until $||v|| < \epsilon$
	1. $v = ∇w L(ŷ, y)$
	2. $w^{t+1} = wt − ηv$

Temos diversas variações para esse algoritmo, mas sempre pulando, saltando para uma posição melhor

Tem um algoritmo novo também, chamado ADAM mas não foi muito explicado


# Grafos computacionais
Como representar coisas mais complexas, não lineares, a partir do que vimos acima?

Ideia base é decompor a computação complexa em uma sequência de atomos mais simples
Calcular a saída é seguir para frente na rede
Os gradientes podem ser calculados usando passos para trás, fazendo o caminho contrário
Podemos fazer redes que são eficientes em progredir/propagar para frente e para trás

Assim a representação daquele exemplo simples de $y = w_0 + w_1x$, temos o grafo abaixo:![[Pasted image 20241121171718.png]]

E podemos simplificar esse grafo juntando os W's para um vetor W, ou até mesmo dar mais entradas a um nó
![[Pasted image 20241121172057.png]] ![[Pasted image 20241121172224.png]]

Também podemos compor um grafo com múltiplas sigmoides e/ou múltiplas camadas
![[Pasted image 20241121172501.png]]

