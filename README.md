# **Aluno:** Ricardo Lopes (22337)

### **INTRODUÇÃO:**
  Este projeto consiste na análise de um jogo pré-programado através da framework Monogame. O jogo escolhido foi "Monogame Snake"; sendo este um simples clone do jogo clássico snake. A     velocidade do jogo aumenta conforme o jogador consome mais comida e as paredes da janela constituem um "Game Over".

### **CONTROLS:**
  Movement: W, A, S, D

### **ANÁLISE DOS FICHEIROS DO PROJETO:**
  - Os ficheiros encontrados na diretoria principal são ficheiros do github original e podem ser ignorados, com a exceção do ficheiro "monogame_snake.sln", sendo este o ficheiro de solução do projeto.
  
  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/bbeab16e-a819-45b7-a274-7139fb8b4c31)
  
  - Dentro da diretoria podemos observar várias pastas e ficheiros. Das pastas a unica que nos é relevante para entender o funcionamento do jogo é a pasta "Content" que contém as imagens utilizadas para a elaboração do projeto.
  
  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/a05b11ae-2c7c-4ccc-8c12-ec4019f919c1)
  
  - O ficheiro "Content.mgcb" é o ficheiro que permite ao Monogame saber quais os "Assets" necessários para o funcionamento do jogo. Todos os ficheiros png e .spritefont são os nossos "Assets".
  
  ![image](https://github.com/initializedentity/Monogame-Analysis/assets/167578514/ddf84c86-56c7-4c4d-9e1c-61721e7f21f4)
  
- Os ficheiros portadores do source code deste projeto são os ficheiros "BallSpawner.cs" "Game1.cs" e "Snake.cs". Comecemos por analisár o ficheiro 
