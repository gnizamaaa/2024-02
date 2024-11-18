1943 - Primeiros estudos com a estrutura do neurônio
	Descoberta de que toda a comunicação e ideia é feita através de pulsos, e o resultado neural é fruto de uma computação neural
	
1945 - Primeiro principio de programa armazenado "First Draft of a Report on the EDVAC" - Von Neumann
	Ideia de juntar o programa e os dados, uma parte da memória para a instrução

1950 - Computing Machinery and Intelligence - Alan Turing - Primeira ideia de inteligência, problema da inteligência em máquinas e o "Teste de Turing"
	1955 - Cunho do termo IA - McCarthy
	 
1958 - O teste principal sendo feito (consideravam o de Turing absurdo) uma IA q identifique o padrão no xadrez

1959 - McCarthy, Minsky criaram o lab e Rosenblatt - Introdução do Perceptron, um modelo de rede neural simplificado
	Entrada-> Multiplica por números -> Função de soma -> Função de ativação (limiar simples)
	E para alterar essas sinapses de acordo com a saída, considerar esse erro para mudar os pesos com base no algoritmo (que foi o que gerou as limitações depois expostas), um algoritmo de aprendizado
	1969 - Mostrou limitações nesse algoritmo, não conseguir fazer um ou exclusivo 
		Só conseguia separar de forma linear (mas podia separar em planos de qualquer dimensão), trabalhava fazendo um plano (uma reta) em um hiperplano
			Inicio da descrença em IA - Inverno na IA

1964 - Sistema ELIZA - Primeiro software, baseado em regras, para manter diálogos inteligentes, o primeiro chatterbot//chatbot

1975 - Holland - Algoritmo Genético - Conseguimos superar a barreira do linear

1979 - Visão artificial, um robô capaz de cruzar de forma autônoma uma sala cheia de obstávulos em 5h

1982 - Hinton: Descrição do Backpropagation; Hopfield: "Neural networks and physical systems with emergent collective computational abilities"
	A ideia de medir uma propriedade da rede, a loss e como fazer para minimizar essa perda

Algoritmo de backpropagation - Consegue resolver o problema da espiral
	Inicio do verão da IA

### Random thought - Conexionistas x Simbólico
Conexionistas - Ideia de que a inteligência surge da junção de estruturas simples (como os neurônios que vimos até aqui)
	Só tem poder quando em grupos muito grandes

Simbólicos - Manipula os símbolos e através de um algoritmo conseguir adquirir a inteligência
	O linguajar de xadrez é muito simbólico, jogadas que tem nomes
	Tabela verdade é totalmente simbólica, computador é totalmente simbólico
	Muito bom em sistemas especialistas, avanço grande com as linguagens de programação
		Por meio de regras, produzir uma resposta; PROLOG vem daí 
	Muito caro de treinar e manter - Tudo é feito a partir do trabalho dos especialistas, pouco escalável
		Levou ao segundo inverno (já que foi o escolhido na época contra os neurônios)
		1997 - Máquina ganhou do Kasparov (jogou xadrez e ganhou do melhor jogador do mundo)

2000 - Muitos investimentos pela DAPA (desafio de 142 milhas autônomas), Google e mundial para carros autônomos; Causando muitos avanços em robótica probabilística
	2009 - UFES começou o projeto de carros autônomos e tirando proveito da quantidade de sinalizações e afins para ter um protótipo que ande em rua

LCAD - Ideia de implementar uma rede neural similar a região do cérebro que processa espaço, para criar uma imagem estéreo, um 3D com duas câmeras
	Foi usado para, com um número de fotos, estimular o volume de uma pilha de minério por exemplo

2008 - UFES desenvolve o modelo mais avançado de reconhecimento de faces do mundo
	Com uma imagem, conseguir reconhecer a mesma pessoa em várias posições e expressões
	De forma muito boa e rápida (redes neurais sem peso)

2005 - Hinton e colegas criam a área de Deep Learning
	Antes não se conseguia treinar redes neurais com mais de 3 camadas, e agora conseguimos treinar redes mais profundas
	1989 - Ideia de rede convolucional (LeCun) - Um neurônio só vê parte da entrada, na matemática é similar a uma convolução e tem desempenho muito satisfatório mas era difícil de treinar (muita conexão a ser "pesada"); É uma ideia inclusive muito biologicamente plausível 

2006 - NVIDIA lança a Geforce 8800
	Diferente da CPU, que tem apenas uma pequena parte destinada a parte de conta (ALU), GPU tem a maior parte destinada a fazer conta, com pouco controle e pouca memória interna
		É algo muito mais focado, de uso específico de computação gráfica
	E o treino é muito similar a uma multiplicação de matrizes, assim como os jogos, os gráficos

1997 - Long Short-term memory, a ideia de colocar neurônios para controlar os pesos

2011 - IBM lança um Question Answering System, apesar de não neural, probabilístico com determinístico

Culture Series, Iain M.Banks