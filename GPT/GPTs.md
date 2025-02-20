# GPT 1 - Improving Language Understanding by Generative Pre-Training
Antigamente faziam vários modelos, um para cada tarefa

Agora se faz um único modelo para uma ampla gama de tarefas e depois fine-tuning para cada tarefa (e no GPT 1 também um ajuste arquitetural), mas sempre com um "engenho geral" muito poderoso.
1. Primeiro, usamos um objetivo de modelagem de linguagem nos dados não rotulados para aprender os parâmetros (sinapses) iniciais de um modelo de rede neural.
2. Posteriormente, adaptamos (fine-tuning) esses parâmetros (sinapses) a uma tarefa alvo usando o objetivo supervisionado correspondente.

Aqui surge a ideia de se utilizar apenas o decoder do Transformer, que demonstrou um forte desempenho em várias tarefas
Na entrada colocamos as tarefas descritas no prompt

## Arquitetura do GPT 1
![[Pasted image 20250220152252.png]]

Pré treina com muito texto fazendo apenas a tarefa de predizer a próxima palavra, depois "joga fora" a camada de saída e coloca uma nova estrutura adequada para a sua tarefa e faz um treinamento pequeno SUPERVISIONADO depois (fine-tuning).
	Inclusive essa estrutura consegue ser mais eficiente e com custo menor
A carga grande ficava só no pré treino e um treino depois com 1000 exemplos já conseguia executar bem a tarefa

### Tokenização
Utilizou o algoritmo de BPE (Byte pair encoding)
Você pega um para que acontece mais frequentemente e troca por um byte que não é usado, e guarda esse byte numa tabela e o que significa.
Então vai repetindo isso recursivamente, podendo inclusive fazer byte de "par de byte" 

E essa tabela no final terão os tokens

# GPT 2
Agora sem fazer o aprendizado supervisionado no fine-tuning
Utilizaram um conjunto de dados muito maior chamado WebText
	Testaram com o GPT 1 nesse conjunto de dados mas não performou tão bem
	Com muitos exemplos diferentes
Capacidade de fazer zero-shot task transfer, uma tarefa que nunca havia sido dado treinamento específico para a tarefa ou exemplos no contexto
Esses achados sugerem um caminho promissor para a construção de sistemas de processamento de linguagem que aprendem a realizar tarefas _from their naturally occurring demonstrations_
Aumentou o contexto de 512 para 1024 e batch de 512 exemplos

# GPT 3
A rede aprende com alguns poucos exemplos
	Basta explicar a tarefa para que a rede aprenda a executar a função desejada, realizar uma nova tarefa de linguagem com apenas alguns exemplos ou a partir de instruções simples
As vezes alcançando competitividade com abordagens anteriores de ajuste fino no estado da arte
GPT-3 pode gerar amostras de artigos de notícias que avaliadores humanos têm dificuldade em distinguir de artigos escritos por humanos