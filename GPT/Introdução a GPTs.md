Arquitetura pensada em fazer uma tradução, converter uma sequência em outra sequência
Na época usavam redes de tradução q passam por um codificador e um decodificador (meio q passando a uma linguagem intermediária), mas que se baseavam em redes neurais recorrentes ou convolucionais complexas, e em 2017 testaram um básico e único mecanismo de atenção.

# A arquitetura de transformers
Dos dois lados temos embedding, que tokenizam (quebram a palavra em origem e flexão por exemplo, sem inteligência artificial per si) a linguagem e positional encoding para representar a ordem. 
Cada token vira um vetor que só um é hot (1) entre todas as possibilidades (possíveis tokens), a partir disso, cria-se o embedding, um vetor de números de ponto flutuante de baixa magnitude que comprime para em torno de 3k possibilidades atualmente.
	Esses embeddings são obtidos com o processo de treinamento da rede inteira, esses embeddings vão representar o token de forma muito coerente. O processo de treinamento "espalha" as palavras no espaço possível, concentrando em "ilhas"
	E de forma muito curiosa, se pegar a palavra "rei", subtrair "homem" e adicionar "mulher" obteríamos "rainha".

A entrada passa por um bloco de atenção e um de feed forward, que pode se repetir essa sequência repetidamente e no fim passar para o processo de saída, que passa novamente por um bloco de atenção, feed forward, linear, softmax e então é retornado para uma sequência de tokens. Sendo possível também encadear decoders, mas todos recebem também direto do decoder, além da entrada do decoder anterior.

O mecanismo de atenção eh uma junção de contas em cima de matriz, cujas entradas são query, key e value, obtidas multiplicando o embedding por matrizes (obtidas por aprendizado de máquina). A estrutura está melhor detalhada na imagem do paper.
	Isso é feito múltiplas vezes, multi-head, cada uma focada em uma parte e então combinamos eles em um só

## E o GPT
Percebemos que para a maioria dos problemas, basta ter o decoder, não precisa do encoder no início.
E além disso, pré treinamos ela, na arquitetura vai se "compactando o conhecimento". 
	Esse treinamento é feito colocando na entrada o texto (tokenizado, passado por one off, embedding, sequênciado...) o máximo que couber. E então treina, dado uma palavra, qual será a próxima palavra. Até dada a entrada, conseguir produzir a saída.
	Podemos treinar também múltiplas de uma vez, várias entradas e várias saídas de uma vez, paralelo.
Acredita-se que com esse pré treinamento, é criada uma ideia do significado da palavra, com base no conhecimento anterior.
Repare que, pela camada de softmax, temos uma possibilidade para cada palavra, para cada token da saída tem um vetor de possibilidades para cada possível token.

Depois do pré treino, ela consegue completar o texto com o conhecimento, mas em cima disso deve ser feito o ajuste fino para por exemplo responder perguntas, para chatbot (como o chatgpt).

# Porquê não foi feito antes
Pq não tinha o mecanismo de atenção, capacidade de considerar todos os tokens anteriores, de forma ponderada, com várias cabeças de ponderação, para se criar a próxima palavra

E também nos faltava, por um tempo anterior, a ideia de modelos auto-regressivos, que você pega a saída e coloca na entrada novamente para produzir uma nova saída. Essa arquitetura traz restrições e que põem em desvantagem (naturalmente) quando consideradas a outras redes, mas não temos formas melhores de treinar essas outras redes, como as recursivas, recorrentes.
	Com o treinamento de chatbot, consegue=se obter um comportamento muito mais geral, já que no prompt enviado, se contem instruções

# Linguagens, programas e interpretadores - uma viagem
Dentre as linguagens, acredita-se que a matemática seria a mais poderosa e por exemplo a física, uma receita de bolo, um programa (informação) e quem executa esse programa é o interpretador, "dá vida" ao programa
GPT é um meta-interpretador nessa ideia, sendo o interpretador o computador

Hoje entendemos a linguagem a ponde compreender e manipular images, sons e outras modalidades de dados

