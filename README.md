# MONOGAME SNAKE - ANALYSIS (Ricardo Lopes: 22337)

### INTRODUÇÃO:
Este projeto consiste na análise de um jogo pré-programado através da framework Monogame. O jogo escolhido foi "Monogame Snake"; sendo este um simples clone do jogo clássico snake. A     velocidade do jogo aumenta conforme o jogador consome mais comida e as paredes da janela constituem um "Game Over".


### CONTROLS:
Movement: W, A, S, D


### ANÁLISE DOS FICHEIROS DO PROJETO:
- Os ficheiros encontrados na diretoria principal são ficheiros do github original e podem ser ignorados, com a exceção do ficheiro "monogame\_snake.sln", sendo este o ficheiro de solução do projeto.

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/bbeab16e-a819-45b7-a274-7139fb8b4c31)


- Dentro da diretoria podemos observar várias pastas e ficheiros. Das pastas a unica que nos é relevante para entender o funcionamento do jogo é a pasta "Content" que contém as imagens utilizadas para a elaboração do projeto.

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/a05b11ae-2c7c-4ccc-8c12-ec4019f919c1)


- O ficheiro "Content.mgcb" é o ficheiro que permite ao Monogame saber quais os "Assets" necessários para o funcionamento do jogo. Todos os ficheiros png e .spritefont são os nossos "Assets".

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/ddf84c86-56c7-4c4d-9e1c-61721e7f21f4)


- Os ficheiros portadores do source code deste projeto são os ficheiros "BallSpawner.cs" "Game1.cs" e "Snake.cs". Comecemos por analisár o ficheiro "BallSpawner.cs", responsável por criar a "comida" que a cobra deve comer.

## BallSpawner.cs
- Esta secção é responsável pela criação de variáveis a serem usadas para a criação e posicionamento da comida da cobra. Sendo a var "BallPosition" responsável por armazenar a localização da comida num espaço bidimensional; a "\_gridsize" por alocar localmente o tamanho predefinido de cada celula no ecrã (ou seja o número de passos que a cobra pode dar no ecrã), esta recebe o valor definido em "Game1.cs"; "\_rng" que recebe um valor que define uma "seed", usada para gerar um valor random; e finalmente a var "\_ballTexture" que armazena a textura da comida.

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/c819af63-5396-440c-852a-54d44b951262)


- Funções responsáveis por carregar a textura da comida e desenha-la no ecrã. São invocadas pelas funções com o mesmo nome no ficheiro principal do projeto ("Game1.cs"). A unica coisa de relevante nelas é a multiplicação da var "BallPosition" por um Vector2 de 20x20 e somado com um Vector2 de 47x47. A multiplicação serve com conversão, onde os valores no vetor estão delimitados pelo numero de "celulas" no background, ou seja estes valores estão numa escala de 0 a (MAX\_SIZE / 20), onde MAX\_SIZE é um Vector2 que representa as dimenções da janela (MAX\_SIZE é pseudo código); quanto á soma por um Vector2 de 47x47 a unica razão observável é para evitar que a comida spawne nos cantos do ecrã e spawnem mais perto do centro.

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/cb88190d-527b-43ea-965c-3e4ef996de88)


- Por fim temos a função responsável por gerar uma posição aleatória para a comida spawnar, não há muito a dizer considerando que usa uma função standard da Microsoft para gerar números Random, a função aceita um parametro e         gera um valor que seja >= 0 e < Int32.MaxValue (sendo este subsituido pelo valor que desejarmos se usarmos um parámetro).

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/2e4a5c3f-8637-46d7-93f7-8cba45424faf)


## Snake.cs
- Estrutura utilizada para gerir cada celula do corpo da cobra, armazenando a sua posição no espaço e a sua direção. A função BodyPart sendo responsável por dar "assign" às variáveis "Position" e "Direction".

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/3ec5ebca-3581-4f04-b34f-65c7f64eb896)


- Variáveis usadas na gestão e manipulação da cobra. MOVEMENT\_COUNTER é uma constante que determina a velocidade que é incrementada à cobra sempre que esta come um pedaço de comida; \_body é responsável por armazenar todas as instâncias da estrutura BodyPart que representam uma célula da cobra cada; "direction" que é responsável por armazenar a direção que a cobra se deslocava quando comeu um pedaço de comida (ou seja ao criar uma nova celula desta); \_headTexture/\_bodyTexture/\_tailTexture armazenam as texturas da cabeça do corpo e cauda respetivamente; \_gridSize é um tipo de dado chamado "combined data types" que armazena data types juntos, neste caso comporta-se como um array de size 2 e é responsável por armazenar a largura e altura da janela dividida por 20 tal como no ficheiro "BallSpwaner.cs"; \_snakeSpeed armazena a velocidade atual da cobra; \_movementCounter é responsável por determinar quando a cobra se deve mover, isto é, a variável armazena o tempo que a cobra deve se manter imóvel antes de se mover outra vez, quando esta chega a 0 sabe-se que é hora de se mover outra vez; por fim a variável \_lastKey armazena a ultima tecla pressionada, indicando a direção que a cobra se deve mover.

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/42916a4b-0b55-46d4-a2ca-982e5812f697)


- Função que cria a cobra no seu estádo inicial, a variável gridsize é inicializada neste momento para todo o Snake.cs, a direção inicial é definida como 1, onde os valores correspondentes às direções são (0 - Cima, 1 - Direita, 2 - Baixo, 3 - Esquerda), a lista que contém a cobra é inicializada com uma cabeça, uma celula de corpo e uma cauda, a velocidade é definida como 31 e o counter de movimento é incializado.

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/57c2f183-a657-49be-ac15-18098d072603)


- Função igual à encontrada no ficheiro "BallSpawner.cs".

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/c23e044b-3c16-4e7c-8ba1-ada08eed3f80)


- Função responsável por gerir o movimento da cobra, nesta secção ela vai buscar a tecla que está atualmente a ser premida e guarda a tecla a ser premida como a ultima tecla premida.

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/57b23b25-ed90-4075-a3a9-7051ac457ed2)


- Esta secção é responsável por determinar se o tempo "idle" da cobra terminou, e se terminou para que direção (atribuindo o valor da direção correspondente à cabeça da cobra, a qual é sempre o primeiro elemento da lista).

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/12e671bc-224b-470d-9f17-ee267da1150e)


- Esta secção é responsável por efetuar o movimento da cobra, onde cada parte do corpo incluindo a cabeça e cauda são movidas para sua nova posição, esta é obtida através da soma do valor de retorno da função GetMovement que devolver um vetor. Caso esteja-se a mover a cabeça e esta tiver uma posição abaixo de 0 ou acima do limite da grelha causa um fim de jogo. Caso contrário altera as direções dos elementos do corpo, primeiro armazena a direção da célula atual para usar como referência para a próxima (efetivamente fazendo cada célula seguir a cabeça), de seguida altera a direção da célula para a da anterior (ou cabeça se for a primeira célula do corpo) e muda o valor da direção atual para o valor antigo da célula que acabamos de alterar, para repetir o ciclo para as outras células.

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/adaacc78-c9d4-4211-bd78-b9d81542fbf2)


- Se a algum ponto ouver uma célula que não seja a cabeça com a mesma posição da cabeça, então o jogo termina (a cabeça esbarrou contra o corpo).

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/f91934f5-5f0f-40f0-a783-66311f89c2ff)


- Se a cabeça está na mesma posição que a comida (cobra comeu comida) então gera-se uma nova cabeça e diminui-se a variável \_snakeSpeed, que por mais que contra intuitivo pareça, aumenta a velocidade da cobra, pois faz com que o tempo entre movimentos seja menor (o qual é obtivo através da multiplicação da velocidade da cobra pela constante MOVEMENT\_COUNTER), a velocidade desta nunca é menor que 0.18359375 (estes valores de velocidade são pelo meu entender usados arbitráriamente, tendo sendo definidos pelo gosto do programador originais). A cauda é armazenada numa váriável à parte e a sua versão na lista é transformada numa celula do corpo, por fim a cauda é adicionada de volta com um offset para estár atrás da célula que ocupa a posição antiga da cauda.


  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/e3b4f032-725f-4a0c-940b-abd10babf5ac)


- Esta função é uma simples função que desenha os elementos da cobra, sendo o primeiro if responsável pela cabeça, o segundo pela cauda e o else pelas células do corpo da cobra.

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/060cea25-a936-4e92-840e-0f2dbb83d51d)


- Função responsável pelos vetores utilizados nos cálculos de movimento e offset

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/a3f9672c-c1e5-45e4-9d09-c09d1df1ce1d)


## Game1.cs

- Váriáveis usadas nesta secção do código, onde GameOver é usada para determinar o estado do jogo; \_graphics e \_spriteBatch são variáveis usadas para interagir com a framework Monogame; \_gridTexture é a textura do background; \_snake é uma instância da classe Snake que gere a cobra (Snake.cs); \_ball é usada para gerir a comida; _font para gerir a font usada no jogo; e _gameOverTextures para gerir a Game Over screen.

  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/4b4ab45b-ace5-4b81-80c0-c5536a757967)

- Funções responsáveis pela inicialização do jogo. Game1() não apresenta nada de relevante para além do standard. LoardContent() apenas carrega as texturas para as variáveis correspondentes, a unica de relevância é a GameOver var que cria 
