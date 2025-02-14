Muito mais prático e rápido enquanto de da muito controle e torna padrão
# Toolbar
Isso deve ser feito na Activity que hospeda os Fragments
Caso tenha o problema de aparecer duas toolbars (uma padrão do android que tem o nome do app), basta adicionar o trecho abaixo no theme.xml
```
	<item name="windowNoTitle">true</item>
```

Agora temos que conectar a toolbar com o activity
```
fun setToolbar() {
	val navHostFrag = supportFragmentManager.
					  findFragmentById(R.id.fragmentContainerView) as NavHostFragment
	val navController = navHostFrag.navController
	val appBarConfiguration = AppBarConfiguration(navController.graph)
	binding.toolbar.setupWithNavController(navController, appBarConfiguration)
}
```

Aqui, ela irá entender o grafo de navegação e colocará uma "setinha" para voltar na toolbar

Tem como definir um tema específico para a toolbar, caso seja desejado um estilo diferente
## Criando um menu
Use o resource manager para criar
Cada item do menu pode ter:
- Um id
- Título
- Ícone
- Tipo de ação
	- always, never, withText, ifRoom, collapseActionView
	O never fica sempre oculto num ..., always vai sempre mostrar, ifRoom verifica se tem espaço e, se não, deixa nos ...
E então podemos incluir essa toolbar em um container de UI
![[Pasted image 20250214160740.png]]

# Navigation Drawer
A gaveta que a gnt puxa do lado ou chama pelo icone de hambúrguer
No slide tá muito bem explicado, mas basicamente é uma view com a toolbar comprimida por um linear layout compat, uma FragmentContainerView e o NavigationView

# Bottom Navigation
Podemos reaproveitar um menu, como o da gaveta ou criar um próprio!
Bastou adicionar o navigation com isso
```
binding.bottomNavMenu.setupWithNavController(navController)
```