É como se pegasse a imagem 224x224x3(cores RGB) para 224x224x128(caracteristicas) e então depois vai diminuindo o "tamanho" da imagem, a dimensão de 224 enquanto aumenta a de "cores"
Assim você consegue fazer a máquina aprender a identificar características e poder por exemplo descartar a ultima camada que dá os labels e treinar de novo caso queira um classificador de imagens mas com fim diferente

### Notation
B: batch size
W: Width 
H: Height
C: Channel 
- Quantidades de neurônios p cada pixel, no caso seria a quantidade de cores (RGB)


## Totalmente conectada ou convolucionais
Uma camada totalmente conectada vai ter W × H × Cout × (W × H × Cin + 1) sinapses, o qu é muita coisa
Já uma convolucional vai ter Cout × (K × K × Cin + 1) sinapses
	Podemos fazer isso e conseguir tirar proveito das similaridades locais e ter uma boa otimização
	Cada neurônio vai ver apenas uma região da imagem, uma região com centro na "mesma posição" que iria estar na imagem
	Além disso, vai reutilizar, compartilhar, as sinapses entre os neurônios. É um kit p todos neurônios, isso é feito porquê mesmo assim se obtem um excelente desempenho enquanto otimiza significativamente 

Com um gráfico computacional da camada convolucional podemos entender melhor
![[Pasted image 20250123161020.png]]

## Notação de Einsten
- A[i, j] denotes one element of the matrix A
- A[i, J] denotes the i’th row of matrix A
- A[I, j] denotes the j’th column of matrix A
- A[I, J] denotes the full matrix A

## Camada convolucional na notação de Einstein

![[Pasted image 20250123155102.png]]



Sendo b - batch, x,y - localização espacial , $C_{in}$ e $C_{out}$ são os canais e g a função de ativação
$\Delta x$ e $\Delta y$ são os ranges de indices que vão ser utilizados  

### Exemplos de uso
E os kernels encontrados podem aplicar filtros na imagem, como uma suavização ou detecção de diferença de brilho

## Como lidar com a borda
Com essa técnica da convolução, vão ter neurônios que não vão ter todas as entradas, não vão ter "pixel vizinho".
Para resolver isso, se passa um valor neutro (0 se oscilar entre -1 e 1) 


# Downsampling
Redução da dimensão espacial da imagem
Aumenta o campo receptivo dos neurônios

## Pooling
Uma técnica muito utilizada é pegar o ponto mais ativo e seguir com o valor dele
Tipicamente iremos reduzir considerando que cada saida terá um quadrado de 2x2 
![[Pasted image 20250123161847.png]]


## Strided Convolution
É uma convolução que tem downsampling, que tem um pulo para fazer que a saída seja menor que a entrada
Imagine que isso será feito com a image, sendo o s o striding
Repare que dependendo do exemplo terão regiões que não serão vistas (as brancas)
![[Pasted image 20250123162336.png]]

# Para que fazemos isso?
Assim conseguimos aumentar o campo receptivo do neurônio sem ter que aumentar o kernel
![[Pasted image 20250123162246.png]]

## Upsampling
Muitas vezes é desejado q a saída tenha o mesmo tamanho da imagem, segmentar a imagem em classes por exemplo (recortar a img em diferentes classes)
![[Pasted image 20250123164100.png]]

É util fazer downsampling e depois upsampling para condensar as informações, "acumular elas para chegar a uma conclusão"
## Nearest neighbor
Repete o valor em todos os pixels

## Bed of Nails
Deixa um pixel (fixo, como o canto superior esquedo do quadrado) com o valor da entrada menor e preenche os outros com valores neutros

## Max Unpooling
Quando estava fazendo o downsampling, se guarda onde estava o pixel mais significante no quadrado e quando for fazer o upsampling, preenche apenas essa localização


# Dilated Convolution
Uma alternativa a fazer down e up sampling
Aqui, iremos pegar apenas um pixel de cada parte da imagem
Assim você consegue trabalhar com resolução maior e cobrir uma grande área sem utilizar pooling
![[Pasted image 20250123164813.png]]

# Inception
Resolve o problema do vanishing gradients tendo vários pontos de saída, que servem para o treinamento
Além disso, também fizeram módulos que usam mais de um filtro
![[Pasted image 20250123170420.png]]
# Resnet - skip connection
Para reoslver o problema dos vanishing gradients que acontece em redes mais profundas, eles arrumaram a solução de somar a entrada de duas camadas atrás com a que seria entrada da camada atual
![[Pasted image 20250123170252.png]]



