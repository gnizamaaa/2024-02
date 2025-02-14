Dependencias:
```
dependencies {
(...)
implementation 'androidx.navigation:navigation-fragment-ktx:2.5.3'
implementation 'androidx.navigation:navigation-ui-ktx:2.5.3'
}
```
# Componentes
- Grafo de navegação (ou navigation graph)
- Hospedeiro de navegação (NavHost)
- Controlador de navegação (NavController)

Pode ter mais de um navigation controller, mas só é justificável//útil quando o app é muito grande
# Passo a passo
1. Crie o XML
2. Adicionar os destinos, as views navegáveis, através do **navigation editor**
	1. Tem como alterar o home no menu da direita
	2. Para adicionar conexões, ações, basta clicar e arrastar um p cima do outro
3. Tem que incluir o hospedeiro de navegação dentro da activity!
4. No onviewCreated, crie um Listener, um botão ou algo assim, que chame o findNavController().navigate()
	![[Pasted image 20250214153903.png]]


# Safe Args
Plugin para transmissão de dados de navegação com segurança
Ele gera classes simples para navegação tipada para acesso a qualquer argumento associado

Passar um argumento para transmitir para o destino
	É possível deixar ele inferir o tipo, mas sempre que souber, especifique o tipo do argumento
	Se não definir um valor default, é obrigatório a tela anterior passar um argumento, se não irá crashar o app
	Pega os argumentos para os valores dos parâmetros na mesma ordem que deginiu os parâmetros no xml

Pela interface (a mesma da navegação) é bem mais fácil de criar e organizar esses argumentos

Para passar o parâmtero, fica assim no código
```
override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
	super.onViewCreated(view, savedInstanceState)
	
	binding.textFragmentA.setOnClickListener({
		val action = AFragmentDirections.actionAFragmentToBFragment("Monitor TV", 1000f)
		findNavController().navigate(action)
	})
}
```

**Podemos passar uma classe que criamos também!!!**
