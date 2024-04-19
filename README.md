# MONOGAME SNAKE - ANALYSIS (Ricardo Lopes: 22337)

### INTRODUÇÃO:
  Este projeto consiste na análise de um jogo pré-programado através da framework Monogame. O jogo escolhido foi "Monogame Snake"; sendo este um simples clone do jogo clássico snake. A     velocidade do jogo aumenta conforme o jogador   consome mais comida e as paredes da janela constituem um "Game Over".


### CONTROLS:
  Movement: W, A, S, D


### ANÁLISE DOS FICHEIROS DO PROJETO:
  - Os ficheiros encontrados na diretoria principal são ficheiros do github original e podem ser ignorados, com a exceção do ficheiro "monogame_snake.sln", sendo este o ficheiro de solução do projeto.
  
  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/bbeab16e-a819-45b7-a274-7139fb8b4c31)

  
  - Dentro da diretoria podemos observar várias pastas e ficheiros. Das pastas a unica que nos é relevante para entender o funcionamento do jogo é a pasta "Content" que contém as imagens utilizadas para a elaboração do projeto.
  
  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/a05b11ae-2c7c-4ccc-8c12-ec4019f919c1)

  
  - O ficheiro "Content.mgcb" é o ficheiro que permite ao Monogame saber quais os "Assets" necessários para o funcionamento do jogo. Todos os ficheiros png e .spritefont são os nossos "Assets".
  
  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/ddf84c86-56c7-4c4d-9e1c-61721e7f21f4)

  
  - Os ficheiros portadores do source code deste projeto são os ficheiros "BallSpawner.cs" "Game1.cs" e "Snake.cs". Comecemos por analisár o ficheiro "BallSpawner.cs", responsável por criar a "comida" que a cobra deve comer.

    ## BallSpawner.cs
      | Esta secção é responsável pela criação de variáveis a serem usadas para a criação e posicionamento da comida da cobra. Sendo a var "BallPosition" responsável por armazenar a localização da comida num espaço bidimensional; a        "_gridsize" por alocar localmente o tamanho predefinido de cada celula no ecrã (ou seja o número de passos que a cobra pode dar no ecrã), esta recebe o valor definido em "Game1.cs"; "_rng" que recebe um valor que define uma          "seed", usada para gerar um valor random; e finalmente a var "_ballTexture" que armazena a textura da comida.
      
      ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/c819af63-5396-440c-852a-54d44b951262)


      | Funções responsáveis por carregar a textura da comida e desenha-la no ecrã. São invocadas pelas funções com o mesmo nome no ficheiro principal do projeto ("Game1.cs"). A unica coisa de relevante nelas é a multiplicação da          var "BallPosition" por um Vector2 de 20x20 e somado com um Vector2 de 47x47. A multiplicação serve com conversão, onde os valores no vetor estão delimitados pelo numero de "celulas" no background, ou seja estes valores estão         numa escala de 0 a (MAX_SIZE / 20), onde MAX_SIZE é um Vector2 que representa as dimenções da janela (MAX_SIZE é pseudo código); quanto á soma por um Vector2 de 47x47 a unica razão observável é para evitar que a comida spawne        nos cantos do ecrã e spawnem mais perto do centro.

      ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/cb88190d-527b-43ea-965c-3e4ef996de88)


      | Por fim temos a função responsável por gerar uma posição aleatória para a comida spawnar, não há muito a dizer considerando que usa uma função standard da Microsoft para gerar números Random, a função aceita um parametro e         gera um valor que seja >= 0 e < Int32.MaxValue (sendo este subsituido pelo valor que desejarmos se usarmos um parámetro).
      
      ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/2e4a5c3f-8637-46d7-93f7-8cba45424faf)


    ## Snake.cs
      | 
