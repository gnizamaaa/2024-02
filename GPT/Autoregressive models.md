Para produzir o estado 3, uso o 1 e 2. Para produzir o 4, uso 3 e 2.
	Sempre usando dois(quantidade arbitrária) estados anteriores

![[Pasted image 20250130171020.png]]
Aqui, difernete da recorrente, não é um conhecimento infinito para trás, é limitado a uma quantidade fixa

A rede autoregressiva é bem mais facil de treinar por ser feedforward, não tem que fazer backpropagation pelo tempo

## Multi-Layer
Podemos ter várias camadas no caminho, que pode atuar como uma convolução temporal, um neurônio próximo da saída pode ver quase a entrada inteira, quase como a soma dos kernels na convolução
![[Pasted image 20250130171550.png]]

## WaveNet
Combina convoluções dilatadas (não pega neurônios seguidos, pega espaçados) com residual e algumas conexões puladas

# Possibilidades
Por ser feedforward, podemos usar muitas "tecnicas", orelha de morcego, como dropout, weightNorm, convolução, padding...

# O que foi descoberto
Não se precisa ter contexto ilimitado (como o das redes recorrentes) para se ter bons resultados
A vantagem de memória infinita, na prática, não faz tanta diferença
	Bastava uma sequencia de tamanho 13 ou 25 para competir com as RRN da época
	Conquistou a comunidade, quando chegou transformer (que segue esse princípio), conquistou completamente