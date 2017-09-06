---
layout: post
title: Primeiros passos com Godot
published: true
---
Ao tentar aprender um pouco de desenvolvimento de jogos, me deparei com Godot, "uma Avançada engine de jogos open 
source, multiplataforma, 2D e 3D". O produto tem como filosofia, oferecer um grande número de ferramentas para que
o usuário possa focar em construir o game, sem "reinventar a roda".

## Buscando tutoriais:
Hoje parece ser unanimidade produzir tutoriais em forma de vídeo. Quando estou iniciando o aprendizado em alguma 
tecnologia/plataforma nova, sempre prefiro iniciar por tutoriais escritos, vídeos, para mim, tem um problema que não
consigo contornar, muitas vezes, os videos de iniciação são carregados de trechos extremamentes básicos entremeados
por informações importantes para quem é iniciante, então, muitas vezes somos obrigados a ver coisas entendiantes, ou 
arriscar avançar o video e perder informações importantes, por isso prefiro material escrito, geralmente procuro
tutorias na documentação do produto e acabo reproduzindo e/ou adpatando, como estou fazendo aqui.

## O "Arcabouço" de Godot
Uma interessante metáfora é criada na documentação da engine para explicar o recurso central de Godot que são os 
nodes, a metáfora faz alusão um chef de cozinha. Um chef cria receitas e essas são divididas em duas partes: A primeira
é o conjunto de ingredientes e a segunda engloba as instruções para o preparo, permitindo que qualquer pessoa possa
reproduzir a criação.

A criação de jogos em Godot, tem, de certa forma, grande semelhança, onde a engine pode ser comparada à cozinha. Nessa
cozinha os nodes são como um refrigerador cheio de ingredientes.

### Nodes
 Node é o elemento básico para a criação de um jogo. Node tem as seguintes características:
 
 * Tem um nome.
 * Tem propriedades editáveis.
 * Pode receber um callback para processos em cada frame.
 * Pode ser extendido.
 * Pode ser adicionado a outros nodes.
 
 A última, talvez seja a mais importante característica, nodes podem ter outros nodes 'filhos', quando arrajados dessa
 maneira, se torna arvores.
   
![nodes](/images/nodes_tree.png)
  
### Scenes
Uma scene (cena) é composta por um gupo de nodes (nós), organizados hierarquicamente em forma de árvore, e tem as 
seguintes propriedades:

* Um cena tem somente um único nó raiz.
* As cenas podem ser salvas e carregadas para um disco.
* Cenas podem ser instanciadas.
* Executar um game é executar uma cena.
* Podem haver várias cenas em um projeto.

O Editor de Godot é, basicamente, um editor de cenas que disponibilizar uma grande quantidade de ferramentas para 
edição de cenas 2D e 3D.


## Passeando no cirtuito de interlagos.
Para iniciar meus estudos com Godot, decidi não seguir os tutoriais e vídeos tradicionais que sempre consomem um bom 
tempo explicando o layout da interface, que, na minha opinião, é mais fácil aprender "tateando" o próprio produto ou, 
ainda mais eficiente, consultando a documentação. Dessa forma meu primeiro objetivo é criar um um path imitando o cirtuito
de interlagos e colocar a figura de um carro F1 'passeando' sobre ele.

Nesse primeiro post, vou fazer o mais básico possível, ou seja, adicionar apenas uma cena com um nó para 'traçar' o 
caminho e dois subnós, um para seguir o caminho traçado e outro para 'acomodar' o carro.

### Nodes utilizados:

#### Path2D:
Funciona como um nó container para um Curve2D que é uma classe que descreve uma curva Bezier no espaço 2D. É usado 
principalmente para prover forma a um Path2d.

#### PathFollow2D
Tem como nó 'pai', sempre um Path2D e retorna as coordenadas de um ponto dentro dele, dada a distancia a partir do 
primeiro vetor.

É util para fazer outros nodes seguirem um caminho, sem a necessidade de codificar o padrão do movimento. Para isso
os nodes precisam ser descendente do mesmo. Nodes descendente se moverão de acordo com o offset.

#### Sprite
Como "filho" de PathFollow2D, vamos colocar um node do tipo Sprite, nodes do tipo sprite no Godot, são o que podemos
chamar de "personagem", no caso será a figura de um carro F1


## Criando um novo projeto

Antes de iniciar vamos criar uma estrutura de pastas para o projeto, 

```bash
mkdir ~/interpath
mkdir ~/interpath/imagens
```

Ao iniciar Godot, a tela de gerenciamento de projetos será aberta:

![Project manager Godot](/images/project_manager_godot.png)

Vamos criar um novo projeto chamado Interpath

![Projeto interpath](/images/new-project-godot.png)


Apos o projeto criado, o próximo passo é abri-lo. Isto abrirá o editor godot, abaixo a apresentação do editor logo 
após aberto:

![Projeto interpath](/images/editor-godot.png)

Ao abrir um projeto a engine já dispnibiliza uma cena "em branco", em um projeto do tipo 3D.
Vamos alterar o tipo de projeto para 2D, para isto é só pressionar o botão 2D na barra ao alto, acima da apresentação
da cena (marcado em amarelo na figura abaixo)

![Projeto interpath](/images/editor-godot-2.png)

Em seguida vamos criar um node so tipo Path2D, para isso basta clicar no botão onde aparece um sinal de + no painel ao alto
no lado direito, depois, na janela de dialgo que aparece, digitamos path2 no campo de busca e escolhemos Path2D, destaques
marcados de amarelo na figura:

![Projeto interpath](/images/criando-node-2.png)


Agora, para criar um caminho para nosso sprit principal, vamos 
[baixar essa imagem](http://s.glbimg.com/es/ge/f/original/2011/10/10/11_gp_brasil.png) que represente o circuito de 
interlagos e 'cola-la' no node criado (Path2D) como se fosse um script, servirá como guia para traçarmos o caminho.

A imagem foi recortada e colocada na pasta imagens do projeto, a partir disso arrastada para cima do node Path2D, 
o nome do node é o prróprio nome da imagem do cirtuito (interlagos), vamos manter. destaques na figura abaixo.

![Projeto interpath](/images/criando-path-1.png)


Em seguida esticamos a figura do circuito para que fique assim:

![Projeto interpath](/images/mapa-esticado.png)

Agora criaremos um nó filho de Path2D do tipo Patfollow2D e mudamos o nome para Follow1

![Projeto interpath](/images/criando-path2.png)

O próximo passo é selecionar Path2D e criar o caminho sobre o mapa utilizando o conjunto de 5 botões para manipulação
de pontos, com esses botoes podemos adicionar, selecionar, excluir e manipular posicoes e inclinações dos pontos, 
usamos essencialmente 2 botões, o de incluir e o de excluir pontos, para ter curvas mais suaves, aumentamos o numeros
de pontos nos trechos onde as curvas são mais acentuadas. Não utilizamos, nesse passo, o botão para fechamento da curva.
O ultimo ponto deve ficar próximo do primeiro, sem toca-lo.


![Projeto interpath](/images/criando-path3.png)

Em seguida psicionamos o cursor no nome do node sprite do traçado do circuito (interlagos) e o excluimos com a tecla
delete para, sem a figura, fica mais fácil perceber caso tenhamos cometido algum erro e colocado pontos a mais, 
nesse caso é só usar os botões para manipulação dos pontos e fazer os ajustes finais.
Após a retirada da imagem e dos ajustes finais a cena deve ficar mais ou menos assim:

![Projeto interpath](/images/criando-path4.png)

O próximo passo é clicar no botão "close curve", para o circuito ser fechado. Agora é uma boa hora para salvar a 
cena, menu no extremo esquerdo superior "scene/save as"

Agora vamos adicionar nosso personagem principal, um node do tipo sprit, o sprit utilizado aqui é uma figura de 
[Opengameart.org](https://opengameart.org/), como a figura já foi copiada para a pastas de imagens, agora basta
arrasta-la para dentro do retangulo que representa o node Follow1, este retangulo aparece quando selecionamos 
o node (painel do lado direito)

Selecionando o node

![Projeto interpath](/images/selecionando-node.png)
 
Após seleciona-lo, o retangulo que o representa deverá aparecer no ponto em que se iniciou o circuito, então é só 
arrastar a figura que queremos para representar o sprit, para dentro dele.

![Projeto interpath](/images/criando-sprite1.png) 


Agora, é necessário definir a rotação do sprit, pode-se atribuir atravésa da propriedade rot da paleta Node2D (painel
a direita), ou clicando em "rotate mode", na barra de botões e encontrar a rotação manualmente. 

![Projeto interpath](/images/tela-final-rot.png) 


### Scripting:
Para fazermos o sprite se mover é necessário um pequeno script:


```bash
extends Path2D
onready var follow = get_node("Follow1")
var speed=100

func _ready():
	set_process(true)
	
func _process(delta):
	follow.set_offset(follow.get_offset() + speed * delta)
```

Para adicioná-lo, é só selecionar o node Path2D e clicar no botão localizado no extremo superior direito do painel 
de nodes.

![Projeto interpath](/images/script1.png) 


### Resultado final

<iframe width="720" height="391" src="https://www.youtube.com/embed/-N1O3KrkSGA" frameborder="0" allowfullscreen></iframe>