<h1>🧩Solucionador do Quebra-Cabeça de 15</h1>
Este projeto implementa uma solução para o clássico jogo do Quebra-Cabeça de 15 (15-Puzzle) utilizando um algoritmo de Subida de Encosta Estocástica com reinícios aleatórios. O objetivo é organizar 15 peças numeradas em ordem crescente, deixando um espaço vazio.

<h2>✨ Funcionalidades</h2>
Implementação do 15-Puzzle: Lógica central do jogo para uma grade 4x4.
Geração Dinâmica de Movimentos: Determina eficientemente os movimentos possíveis para a peça vazia.
Heurística de Distância de Manhattan: Utiliza a distância de Manhattan para estimar o custo do estado atual até o estado objetivo, guiando a busca.
Subida de Encosta Estocástica (Stochastic Hill Climbing): Emprega um algoritmo de busca meta-heurístico que tenta encontrar a solução ótima movendo-se iterativamente em direção a estados melhores, com uma probabilidade de aceitar movimentos "piores" para escapar de ótimos locais.
Reinícios Aleatórios: Se o algoritmo ficar preso em um ótimo local, ele pode reiniciar a busca a partir de um novo estado inicial gerado aleatoriamente (embora atualmente um estado inicial fixo seja usado para demonstração).
Interface de Linha de Comando: Exibe o estado do quebra-cabeça e o progresso da busca diretamente no console.

<h2>🧠 Como Funciona</h2>
O projeto aborda o problema do quebra-cabeça de 15, que é conhecido por ser NP-difícil. O algoritmo de Subida de Encosta Estocástica é usado para navegar no espaço de busca:

Função Heurística: A função heuristica calcula a Distância de Manhattan para cada peça. Essa distância é a soma das distâncias horizontais e verticais de cada peça de sua posição correta no estado objetivo. Uma distância de Manhattan menor indica um estado mais próximo da solução.
Geração de Vizinhos: Para qualquer estado dado, gerar_vizinhos identifica todos os movimentos possíveis trocando a peça vazia (representada por 0) por uma posição adjacente.
Loop da Subida de Encosta Estocástica:
Começa a partir de um estado inicial.
Em cada iteração, explora os vizinhos do estado atual.
Prefere vizinhos com um valor heurístico menor (mais próximos do objetivo).
Crucialmente, possui uma prob_aceitar_pior (probabilidade de aceitar pior) que permite ocasionalmente mover-se para um estado com um valor heurístico maior. Isso ajuda o algoritmo a escapar de mínimos locais, onde todos os vizinhos diretos são piores que o estado atual, mas um ótimo global pode existir mais adiante.
A função tentativa_com_reinicios orquestra múltiplas tentativas a partir de um estado inicial (potencialmente) diferente se uma solução não for encontrada dentro de um certo número de iterações.

<h2>🚀 Primeiros Passos</h2>
Estas instruções permitirão que você obtenha uma cópia do projeto e o execute em sua máquina local.

Pré-requisitos
Você só precisa ter o Python 3.x instalado em seu sistema.

Executando o Solucionador
Salve o código: Salve o código Python fornecido em um arquivo chamado puzzle15_solver.py.

Abra seu terminal ou prompt de comando.

Navegue até o diretório onde você salvou o arquivo.

Execute o script:

Bash

python puzzle15_solver.py

O script começará a resolver o quebra-cabeça a partir de um estado inicial predefinido, mostrando o progresso e o caminho da solução final, se encontrada.

<h2>⚙️ Configuração</h2>
TAMANHO: Define o tamanho do tabuleiro (atualmente fixado em 4 para um quebra-cabeça 4x4).
OBJETIVO: Representa o estado objetivo do quebra-cabeça.
max_iteracoes: Número máximo de iterações para uma única tentativa de Subida de Encosta.
prob_aceitar_pior: Probabilidade (entre 0 e 1) de aceitar um movimento para um estado com um valor heurístico pior.
max_reinicios: Número máximo de reinícios aleatórios se uma solução não for encontrada.
A variável estado_inicial dentro de tentativa_com_reinicios está atualmente "hardcoded" para demonstração, mas você pode descomentar e usar gerar_estado_inicial(qtd_movimentos=80) para gerar um estado aleatório solucionável.
