Estamos usando para mais coisas que apenas linguagem atualmente, como imagens e som, então esse nome fica desatualizado

Dada uma sequência de texto, qual é a probabilidade da sequência ocorrer
	O rato roeu -> sequência provável
	Roeu rato o -> Sequencia improvável

Sendo isso feito com sequências de tokens (entre letra, palavra e token; token é o que melhor performa)

A probabilidade pode ser decomposta usando chain rule of probability // product rule

Os auto-regressivos só conseguem ver uma janela, mesmo assim, com uma janela na casa de milhões de tokens conseguem ser superior a maioria dos humanos, já que cabe por exemplos 10 livros perfeitamente em contexto
## Aplicações
- Language Recognition -> vê qual lingaugem tem maior probabilidade daquela sequência de tokens
- Generative Model -> A partir de um início, qual token tem a maior probabilidade de completar a frase (testa qual token é o mais provável), ampliando e então pedindo o próximo token... Até ter o EOF
	- Pode também escolher nem sempre o mais provável por exemplo, ou fazer um leque de possibilidades (1 gerar 2, 2 gerar 4...), ou o mais comum, que é um ruído para nem sempre escolher o mais provável (Temperatura)

# Treinamento
Tem um conjunto de sentenças que é o conjunto de treinamento
Treinamos o modelo visando maximizar a probabilidade das sentenças
	Para datasets maiores, como as probabilidades serão baixas inicialmente, é mais adequado utilizar o log já que o produto das probabilidades de token, a probabilidade da sentença, tende a 0 muito rápido
Em cima dessa expressão é feita uma manipulação para que se busque minimizar a cross entropy entre a probabilidade da sentença e a média, a distribuição do modelo

## Avaliando os Character Language Models
Quanto que é o mínimo de bits necessários para se ter um modelo capaz de gerar uma sentença x
Os exemplos do slide ajudam no entendimento mas não valem ser escritos aqui
Se você precisa de mais de 1 bit para o modelo "fitar" o dado, ele não está bem "fitado", 
## Shannon Information
O quanto essa sentença seria surpresa, 1 seria algo como "Trump virou presidente de Brasil".
	O resultado dessa conta é uma estimativa de número de bits para o modelo conseguir gerar essa sequência dado uma distribuição já existente (sem essa surpresa)
![[Pasted image 20250206153942.png]]

## Cross Entropy
A surpresa ESPERADA do modelo sobre uma certa distribuição de dados
Atualmente utilizando uma simplificação da conta, já que é mais barata de computar e estaremos trabalhando com milhões de tokens para treinamento
![[Pasted image 20250206154259.png]]

## Para palavras
Utilizamos como media a **perplexity**, que é como se fosse o produto de todas as possibilidades de se gerar cada palavra da sentença
Perplexity mínima é 1!
Existe uma perplexidade característica do português, do inglês, do dataset. E um overfitting teria essa perplexibilidade
![[Pasted image 20250206155602.png]]
Um exemplo de perplexibilidade altissima é o exemplo 3

Shannon estimou que o texto em inglês fica entre 0.6 e 1.3 bits por caractere
	Tem como gerar texto em inglês com pouca complexidade
Word langauge models em 2017 tinham perplexibilidade na ordem de 60
	Com modelos de transformadores a ordem caiu para 10-20
	E modelos modernos caiu para a ordem de 2-3
É possível gerar texto de qualidade com modelos não muito complexos

Se um modelo aprender um mundo através de uma linguagem, se aparecer uma outra linguagem com o mesmo mundo não tem muito problema, é como se tivesse uma representação abstrata dentro do modelo
	A gramática não é um problema, é simples
# N-gram
Vê a probabilidade das sequências de tamanho n, quanto maior mais caro
N-gram de 3, a terceira palavra depende das 2 anteriores (history length)
![[Pasted image 20250206162541.png]]

History length é quantidade de palavras no passado que se leva em consideração para gerar a nova palavra
	History length vai ser sempre 1 menor
As dimensões vão aumentando e a memória necessária para representar cresce muito rápidamente
Até os anos 2000 se fazia assim 

As n-gram models are autoregressive models, sampling is easy
I We just need to iteratively draw tokens from $p(x_t |x_{t−n+1} , . . . , x_{t−1} )$ until we reach the end of sentence symbol \<EOS>

Não é viável utilizar n-grams para coisas como tradução por exemplo

# Word Representations
Local Discrete Word
	É um one-hot, assume a mesma distância entre todas as palavras, sem diferenciar as palavras. As palavras sendo apenas simbolos
	Não leva em conta as similaridades entre algumas palavras, no mundo, existem palavras que podem ser trocadas e mesmo assim a probabilidade da frase continuaria muito parecida

Distributed Word Representations - Embedding
	Mapeia aquele vetor one-hot com dimensões altissimas para um de dimensão menor mas de valores flutuantes, distribuindo os pesos, as distâncias, onde importa
	São capazes de ver similaridade entre as palavras
	Permite a generalização entre as sentenças
![[Pasted image 20250206164855.png]]
Fazendo a mão perde para quando fazemos por aprendizado de máquina

# Neural Probabilistic Language Model

Na entrada da rede tem os one-hots vectors de algumas palavras (as anteriores), com uma matriz, que seria a que gera o  embedding, inicializada aleatoriamente
Daí a rede pode mudar esses valores da matriz compartilhada e então se passa p uma camada de tanh e depois uma de softmax para gerar a saída das probabilidades

O resultado foi muito melhor do que o n-grams mas era muito mais caro de treinar
A rede neural consegue tirar proveito de mais palavras, não tem a limitação de n da anterior

## Skip-grams
Para facilitar o treinamento, poderia se usar para predição entre duas palavras
	O importante, os embeddings, conseguia ser treinado assim com menos iterações
	Treino eficiente com muito dado
	Ex: O [palavra a ser predita] roeu 
## Word Vector Arithmetics
Propriedade interessante que surgiu com o uso de rede neural
Aqui, podemos ver contas em cima dos embeddings como
Windows - Microsoft + Gooogle -> Gera um embedding muito próximo de Android

# Neural Machine Translation
## Sequence to Sequence Learning
O primeiro Google tradutor utilizava essa arquitetura
O intuito é de que teria um vetor que expressaria o pensamento, o conceitual
![[Pasted image 20250206171044.png]]

A decodificação era feita tal que:
Baseada no thought vector e um token, qual a próxima palavra, dado o estado do decoder e o token anterior, qual a próxima palavra...
	A sentença fica armazenada como um estado no conjunto de neurônios

### Escolhendo os Tokens//Sentenças
Não adianta utilizar **Greedy**, guloso, Algorithm. Simplesmente porquê p(Apples are good) > p(Those apples are good)
	Assim o modelo fica burro
Para melhorar isso utilizamos **Beam Search**, a cada etapa, mantém uma lista dos melhores tokens e retorna esses tokens (separadamente) para a rede
![[Pasted image 20250206171616.png]]

O que se utiliza atualmente é temperatura, uma roleta que utiliza as probabilidades de cada token como entrada e um hiper-parâmetro de temperatura para quanto será "aleatorizado"

# Transformer
Não é recorrente
Ele trata todos os tokens em paralelo (Não sequencialmente como na [[Recurrent Neural Networks]])
Baseado na atenção, presta atenção em todos os tokens para trás ao mesmo tempo
	Só é possível pelos avanços de memória
Aprende muito rápido, vários tokens de uma vez só, a sentença inteira

## A arquitetura

![[Pasted image 20250206172300.png]]

Apenas as camadas de entrada e saída são diferentes, depois são apenas dois "tipos" de camadas, encoder e decoder.
	Atualmente é comum ter algo como 100 camadas de encoder

A parte de estado e "thought vector" é muito similar ao Long Term Short Memory
Sendo o thought vector, que fica fixo, a saída do encoder. E os tokens vão entrando na segunda entrada do decoder

O transformer tem um tamanho definido de entrada!!!
## Entendendo
T é quantos tokens/palavras podem ter de entrada
	Entradas menores são preenchidas com um token de "not a token"
O transformer tem um tamanho definido de entrada!!!
	Atualmente é de 128k (contexto do gpt) de embeddings que tem 8k de valores flutuantes
Esse 128k*8k é passado de camada em camada

Diferente das RNNs, que usavam da mesma arquitetura para utilizar os pesos como status e ir gerando a prox palavra
Aqui não faz isso, coloca uma camada depois da outra 

### Self-attention
Todo token tira proveito de todos tokens anteriores, e em alguns casos 
	Os tokens da própria camada presta atenção nos tokens da camada
Não se computa essa camada de atenção só uma vez
	Vai calcular mutiplas vezes, ter multiple heads
	Isso vai gerar um tensor de pesos de atenção

> [!NOTE]
> Self-attention then constructs a tensor A[k, t1 , t2 ] – the strength of the attention
> weight from t1 to t2 for head k
> In the paper, an embedding dimension of DJ = 512 is chosen per token
> The authors use K = 8 heads and a dimension of DQ = DK = DV = 64 for the
> query, key and value embeddings that are used for each token (can be different)

![[Pasted image 20250206174259.png]]
O softmax é a atenção
Para cada token eu preciso computar a atenção com todos os outros tokens
A ultima linha é a parte de Feed Forward