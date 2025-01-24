DOcumentação n eh boa, tem link no slide p

==**Lembre de colocar a permissão de permissão da internet no Manifest**==
Seguindo o modelo MVVN, se faz na camada de cliente
## Entidade x Serviço x Cliente
Mapeia o modelo de nefócios da aplicação - Uma classe chamada produto,
Serviço - Mapeia as URLs que serão feitas as requisiçÕes
Cliente - Mapeia as configurações, administra as requisições e header

Cliente guarda a instância do serviço, serviço faz as chamadas e mapeia as entidades, Entidade mapeia o objeto requisitado

## Outro import
converter-gson -> vai converter Json para objeto Java

## Mapear Entidade
Primeiro deve se criar a classe (Todos campos do JSON devem ter um "equivalente" na classe)
Importa a biblioteca de SerializedName (dentro do GSon)
ANota Usa as anotações para fazer o mapeamento do elemento do JSON com uma parte, uma característica do objeto java

Para cada entidade que iremos trabalhar deve ter uma classe

## Criando serviço
Cria uma classe com que vai mapear os endpoins
**Importe sempre as coisas do retrofit**, com atenção específica ao Call, que tem muito conflito de nome
Vai importar a entidade, os métodos vão trabalhar, retornar e ter entrada sendo essas entidades
Muito similar a entidade, mas vai ser uma interface com as funcionalidades desejadas que vão ser mapeadas utilizando @GET("\<endpoint>")
@FormUrlENcoded  indica que será um post com formado de form, atenção que será passado em JSON para a API

## Cliente
Se utiliza Singleton para poupar memória da aplicação!
Clriamos um cliente utilizando as classes OkHttpCliente
A configuração é feita utilizando os 
	Vai ser passado o que será repsonsável por fazer a concersão entre json e objeto
	Além da URL, 

### Como criar Singleton?
Envelopar tudo com um companion object -> Cria um bloco estático
Cria uma função privada que verifica se já foi inicializado, inicializa caso não tenha e retorna a instância caso contrário
E uma pública que retorna o cliente configurado
	Ou utilizando classe específica de Serviço
	Ou uma Generics que recebe qualquer tipo de serviço

# Problema: Requisições são assincronas
Para resolver isso, devemos utilizar o enqueue, que enfilera as requisições
