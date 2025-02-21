SnackBar - Toast 2.0, bonitinho que tem como dar dismiss deslizando o dedo em cima e com possível botão de ação dentro da mensagem

Alert Dialog - Uma caixa de diálogo que segue o padrão builder
![[Pasted image 20250221152601.png]] ![[Pasted image 20250221152622.png]]



Spinner - Menu com opções já definidas
Pode ser estático ou dinâmico (Em que as opções são definidas no código com alguma função)
![[Pasted image 20250221152825.png]]

Progress Bar
Pode ser contínua ou progressiva

![[Pasted image 20250221153150.png]]

Podemos, além de alterar manualmente, incrementar com o código
```
binding.progressBarBar.incrementProgressBy(10)
```

Tem como fazer blocos, views desaparecerem utilizando
```
binding.progressBarCircle.visibility = View.GONE
```

Checkbox e Switch
São praticamente a mesma coisa, mas o Switch é tão antigo que foi criado um SwitchCompat mais novo
![[Pasted image 20250221153701.png]]

Radio Button Group
Permite o usuário a escolher uma opção em um grupo
![[Pasted image 20250221153754.png]]

SeekBar
Barra em que você arrasta p escolher o valor, como o volume

DatePickerDialog
Abre o calendário para escolha de data
Se implementa dentro de um onclick ou algo assim
	É necessário usar um listener que observa se o valor mudou e depois chamar o método que abre esse diálogo
![[Pasted image 20250221154325.png]]

TimePickerDialog
Implementação muito parecida mas para seleção de horário
![[Pasted image 20250221154546.png]]

ScrollVIew
É uma viewGroup que permite fazer scroll em cima de um LinearLayout
Não deve ser usada para ListView e RecycleView, ela já implementa isso

![[Pasted image 20250221154736.png]]

Biblioteca MasckEditText
Muito útil para auxiliar o usuário a preencher um formulário, ele vai dinamicamente (ou n, flag maskStyle "completable") formatando a entrada do usuário
Muito bom para algo como um campo de CPF, que precisa dos pontos e traço sem o usuário digitar o . e -
Pode pegar o valor mascarado ou raw


Sensor
Existe um SensorManager que gerencia todos os sensores
Tem um get, se retornar nulo, não tem naquele aparelho
E então é necessário instanciar um Listener que irá ficar olhando atualizações dos valores
Para sensores como a digital, temos funções que medem a acurácia comparado com um padrão 
```
override fun onAccuracyChanged(p0: Sensor?, p1: Int) {
```

Os sensores também tem taxa de atualização, para não gastar bateria/performance atoa, temos 4 maneiras de obter
- SENSOR_DELAY_FASTEST: obtém os dados o mais rápido que puder
- ○ SENSOR_DELAY_GAME: obtém os dados em uma taxa factível para jogos
- ○ SENSOR_DELAY_UI: obtém os dados em uma taxa factível para UI
- ○ SENSOR_DELAY_NORMAL: obtém os dados em uma taxa factível para
- mudança de orientação de tela

Modificar o ícone do app
