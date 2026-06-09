# 🧠 Rota do Arqueólogo: Justificativas Algorítmicas

Este documento explica as decisões técnicas e matemáticas por trás dos algoritmos implementados no jogo. A escolha de cada estrutura foi baseada na necessidade de performance no navegador e na natureza do layout em grid 2D do mapa.

## 1. Movimentação e Pathfinding: Busca em Largura (BFS)
Para encontrar o caminho entre o jogador e um ponto clicado (ou o retorno à base), foi utilizado o **BFS (Breadth-First Search)**.
* **Justificativa:** O mapa do jogo é um grid não-ponderado (mover de um bloco para o vizinho tem sempre o mesmo custo = 1). Em grafos com arestas de peso uniforme, o BFS garante matematicamente encontrar o caminho mais curto.
* **Complexidade:** $O(V + E)$, onde $V$ são os tiles do chão e $E$ as transições entre eles. Algoritmos mais complexos como A* (A-Star) adicionariam um *overhead* desnecessário para o tamanho do nosso mapa.

## 2. Gestão de Inventário: Knapsack 0/1 (Programação Dinâmica)
Para automatizar a organização da mochila do arqueólogo, implementamos a solução do clássico **Problema da Mochila 0/1**.
* **Justificativa:** O jogador tem um limite de peso de 15 kg e cada artefato possui peso e valor (pontos). O objetivo é maximizar os pontos sem ultrapassar o peso. Como os artefatos não podem ser fracionados (ou leva inteiro ou não leva), a abordagem 0/1 é a ideal.
* **Complexidade:** Utilizamos Programação Dinâmica com uma tabela bidimensional de memorização, resultando em uma complexidade pseudo-polinomial $O(n \cdot W)$, onde $n$ é a quantidade de itens na mochila e $W$ é a capacidade de peso (15).

## 3. Rota de Coleta: Caixeiro Viajante (TSP)
Para traçar a "Rota Ótima" que visita todos os artefatos restantes, enfrentamos o desafio do **Traveling Salesperson Problem (TSP)**, que é um problema NP-Difícil. A solução escolhida foi uma abordagem híbrida:
* **Para instâncias pequenas ($n \le 12$ nós):** Utilizamos o algoritmo exato de **Held-Karp**.
  * **Por quê?** Ele usa bitmasking e programação dinâmica para garantir a rota absolutamente perfeita. A complexidade é $O(n^2 \cdot 2^n)$, mas com um $n$ pequeno, ele roda confortavelmente dentro dos 16ms de um *frame* no JavaScript sem congelar a tela.
* **Para instâncias maiores ($n > 12$ nós):** O jogo alterna automaticamente para a heurística de troca local **2-opt**, precedida por um *Nearest-Neighbor* (Vizinho Mais Próximo).
  * **Por quê?** Evita o congelamento da interface do usuário em mapas densos nos níveis avançados. A heurística de $O(n^2)$ garante um tempo de resposta imediato, gerando uma rota altamente otimizada, mesmo que não seja matematicamente a mais perfeita possível.