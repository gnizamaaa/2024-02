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