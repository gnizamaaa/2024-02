# Definindo
Representa uma parte reutilizável da IU da aplicação
Ele tem o proprio layout, ciclo de vida e 
Difere da activity por não conseguir existir por conta própria, precisa de um host (geralmente uma activity)

# Porquê de existir?
A ideia era simplificar o desenvolvimento para ptablet e celular 
Uma subtela para podermos reutilizar as telas
![[Pasted image 20250207152355.png]]

Activity pode conter vários fragment
Um fragment só pode estar relacionado a uma Activity

Com uma única activity poder desenhar várias telas
Tem como trasitar informações entre fragmentos
Facilita também o uso de animações em transição de telas

# Teve resistência
**Principalmente por causa dos ciclos de vida!!**
2017 - Passou a recomendar a criação de aplicações Single Activityes
	Exemplo da Navigation Drawer
	Utilizou dos Fragments para facilitar a navegação (Passou a fazer mais sentido, muitos benefícios a mais)
	![[Pasted image 20250207153012.png]]

## Os ciclos de vida
Eles interagem entre si (essa imagem está desatualizada, mas é muito boa para ver a interação)
![[Pasted image 20250207153049.png]]

### Ciclo de vida do Fragment
No onCreate não conseguimos interagir com a VIew, mas sim no onViewCreated !!!!
O OnCreate fica para lógica de negócio, atualizaces e similares
	E para exibir, apenas no onViewCreated
![[Pasted image 20250207153216.png]]



# Criando Fragments
Cria um arquivo XML normal e extendendo a classe Fragment()
Então, para visualizar, criar uma Activity com um container, um "placeholder", chamado FragmentContainerView (aitigamente se utilizava FrameLayout)

E aí podemos criar o Fragment assim:
```
class MyFragment : Fragment() {
override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?,
savedInstanceState: Bundle?): View? {
super.onCreateView(inflater, container, savedInstanceState)
val fragView = inflater.inflate(R.layout.fragment_a, container, false)
return fragView
}
}
```

Se for esse onCreate básico, podemos simplesmente sobrecarregar como abaixo
![[Pasted image 20250207154031.png]]

### Embutindo na activity
E aí podemos deixar o fragment estático na Acitivity utilizando o código abaixo no código da nossa activity
![[Pasted image 20250207154215.png]]

Ou fazer dinâmico através da classe supportFragmentManager
![[Pasted image 20250207154325.png]]

E utilizando esse dinâmico, podemos fazer algo como abaixo, que já poupa a transição entre activity
![[Pasted image 20250207154454.png]]


# Transferência de dados entre Activity e Fragment
Vamos utilizar o bundle que funciona como um map

1. Primeiro, cria o bundle dentro da Activity e passa como argumento para o Fragment
2. Na sequência, recebe esse argumento dentro do método onCreate()

Exemplo no código da activity:
![[Pasted image 20250207154842.png]]

Para receber o dado no Fragment:
![[Pasted image 20250207155015.png]]
Reparemos de que temos que dar um get\<tipo>!!


## Para casos com muitos atributos, argumentos
Precisamos criar uma classe Produto que seja serializável (transformado em uma string estruturada)
```
import java.io.Serializable
data class Product(val id: Int, val name: String) : Serializable
```

Depois, iremos passar como um único argumento
![[Pasted image 20250207155344.png]]

E para receber esse objeto, iremos fazer:
![[Pasted image 20250207155424.png]]
OBS: Esse Log.i é muito bom para imprimir como um print() mas no log acessível na IDE, sem precisar imprimir na tela

# Utilizando ViewBinding em um Fragment
![[Pasted image 20250207155659.png]]

\_binding é um auxiliar e binding é esse auxiliar tratado para que caso utilize o binding antes da criação, gerar uma exceção
E na destruição é igualado a null para garantir a proteção em relação ao binding

Podemos utilizar o Binding sem fazer essa proteção, mas é algo não ideal, não recomendado pela documentação e ficará na mão do desenvolvedor para não dar problema e só chamar esse fragmento em momentos ideais