# 🏺 Rota do Arqueólogo

**Rota do Arqueólogo** é um web game educativo de quebra-cabeça e estratégia (Puzzle/Strategy). O jogador assume o papel de um arqueólogo explorando ruínas geradas proceduralmente, com o objetivo de coletar artefatos históricos preciosos enquanto lida com as restrições físicas de sua mochila.

O grande diferencial do jogo é o uso explícito e visual de **algoritmos clássicos da Ciência da Computação** para auxiliar o jogador nas tomadas de decisão.

## 🚀 Como Rodar o Jogo
O projeto foi construído puramente com HTML5, CSS3 e JavaScript (Vanilla), sem dependências externas.
1. Clone este repositório: `git clone https://github.com/seu-usuario/rota-do-arqueologo.git`
2. Navegue até a pasta do projeto.
3. Abra o arquivo `src/index.html` diretamente em qualquer navegador web moderno.

## 🎮 Mecânicas e Gênero
* **Gênero:** Puzzle / Estratégia / Pathfinding.
* **Movimentação:** Clique em qualquer bloco válido do grid para mover o personagem.
* **Coleta:** Chegue até um artefato para tentar colocá-lo na mochila.
* **Progressão:** Ao coletar os itens possíveis, avance para o próximo nível (que possui mapas maiores e mais densos).

## 🧠 Algoritmos Implementados
O jogo funciona como um laboratório interativo para três algoritmos fundamentais:
1. **BFS (Busca em Largura):** Calcula o caminho mais curto desviando de obstáculos na matriz do mapa.
2. **Knapsack 0/1 (Problema da Mochila):** Gerencia o inventário automaticamente usando Programação Dinâmica para maximizar o valor em pontos sem exceder os 15kg permitidos.
3. **TSP (Caixeiro Viajante):** Calcula a sequência de coleta mais eficiente. Utiliza o método exato de Held-Karp para poucos itens, e a heurística 2-opt para quantidades maiores, garantindo performance no navegador.