SQLite -> recomendado para coisas mais simples sem tanta concorrência e uma quantidade de dados menor que 10GB
Usamos a linguagem SQL
	SELECT \<colunas>
	FROM \<tabelas>
	WHERE \<condição>;

ROOM utiliza o SQLite como SGBD
Todas as queries são testadas em tempo de compilação
Arquitetura parecida com o retrofit, dividida em Entidade/Modelo, DAO (Data Acess Objects), contendo os métodos que mapeiam o acesso aos dados, e ROOM database

# Entidade
Aqui você vai mapear a relação entre objeto e tabela do SQL
Um exemplo básico seria
![[Pasted image 20250131155208.png]]

Para atributos que devem existir dentro da classe mas que seriam inúteis ou reduntantes no banco de dados, é utilizado o @ignore em cima do atributo
	Exemplo dado em sala: Dias para um produto vencer (sendo que no banco de dados já tem a data de fabricação e duração da validade)

# ROOM database
Exemplo básico, utilizando apenas uma classe (ProductModel), mas podemos colocar uma virgula e listar mais entidades
![[Pasted image 20250131160526.png]]

# DAO -> Crud
Vai ser uma interface que lista os métodos e as queries que o programa vai utilizar
Exemplo:
![[Pasted image 20250131160905.png]]

