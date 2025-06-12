import random
import time

# Tamanho do tabuleiro: 4x4 para o Puzzle 15
TAMANHO = 4

# Estado objetivo para o 15-Puzzle
OBJETIVO = (1, 2, 3, 4,
            5, 6, 7, 8,
            9, 10, 11, 12,
            13, 14, 15, 0)

# Gera os movimentos possíveis dinamicamente para um tabuleiro de tamanho TAMANHO x TAMANHO
def gerar_movimentos_possiveis(tamanho):
    movimentos = {}
    for i in range(tamanho * tamanho):
        vizinhos = []
        linha, col = divmod(i, tamanho)
        if linha > 0:
            vizinhos.append(i - tamanho)
        if linha < tamanho - 1:
            vizinhos.append(i + tamanho)
        if col > 0:
            vizinhos.append(i - 1)
        if col < tamanho - 1:
            vizinhos.append(i + 1)
        movimentos[i] = vizinhos
    return movimentos

MOVIMENTOS = gerar_movimentos_possiveis(TAMANHO)

# Troca o 0 (espaço vazio) com um vizinho
def mover(estado, origem, destino):
    estado = list(estado)
    estado[origem], estado[destino] = estado[destino], estado[origem]
    return tuple(estado)

# Heurística: soma das distâncias de Manhattan de cada peça até sua posição correta
def heuristica(estado):
    distancia = 0
    for i, val in enumerate(estado):
        if val == 0:
            continue
        pos_correta = OBJETIVO.index(val)
        linha_atual, col_atual = divmod(i, TAMANHO)
        linha_correta, col_correta = divmod(pos_correta, TAMANHO)
        distancia += abs(linha_atual - linha_correta) + abs(col_atual - col_correta)
    return distancia

# Gera os vizinhos do estado atual
def gerar_vizinhos(estado):
    vizinhos = []
    pos_vazio = estado.index(0)
    for destino in MOVIMENTOS[pos_vazio]:
        vizinhos.append(mover(estado, pos_vazio, destino))
    return vizinhos

# Gera um estado aleatório aplicando N movimentos a partir do objetivo
def gerar_estado_inicial(qtd_movimentos=100):
    estado = OBJETIVO
    for _ in range(qtd_movimentos):
        vizinhos = gerar_vizinhos(estado)
        estado = random.choice(vizinhos)
    return estado

# Algoritmo de Hill Climbing Estocástico
def hill_climbing_estocastico(estado_inicial, max_iteracoes=30000, prob_aceitar_pior=0.1):
    estado_atual = estado_inicial
    caminho = [estado_atual]
    heuristica_atual = heuristica(estado_atual)

    for _ in range(max_iteracoes):
        if estado_atual == OBJETIVO:
            break

        vizinhos = gerar_vizinhos(estado_atual)
        candidatos = []

        for v in vizinhos:
            h_v = heuristica(v)
            if h_v < heuristica_atual:
                candidatos.append(v)
            elif random.random() < prob_aceitar_pior:
                candidatos.append(v)

        if not candidatos:
            break

        estado_atual = random.choice(candidatos)
        heuristica_atual = heuristica(estado_atual)
        caminho.append(estado_atual)

        if estado_atual == OBJETIVO:
            break

    return caminho

# Imprime o tabuleiro formatado
def imprimir_estado(estado):
    for i in range(0, len(estado), TAMANHO):
        print(estado[i:i + TAMANHO])
    print()
while True:
    
    break
# Tenta encontrar a solução com reinícios aleatórios
def tentativa_com_reinicios(max_reinicios=10000, max_iteracoes=3000000):
    #estado_inicial = gerar_estado_inicial(qtd_movimentos=80)
    #erro
    # estado_inicial = (
    #   5, 12, 0, 1,
    #   3, 10, 15, 6,
    #   7, 13, 14, 2,
    #   8, 4, 11, 9
    # )
    estado_inicial = (
      5, 1, 2, 4,
      0, 6, 3, 8,
      9, 10, 7, 11,
      13, 14, 15, 12
    )

    print("\nEstado Inicial:")
    imprimir_estado(estado_inicial)
    for tentativa in range(max_reinicios):
        print(f"Tentativa {tentativa + 1}: Heurística inicial = {heuristica(estado_inicial)}")
        caminho = hill_climbing_estocastico(estado_inicial, max_iteracoes)
        if caminho[-1] == OBJETIVO:
            return caminho, tentativa + 1
    return None, max_reinicios

# Execução principal
if __name__ == "__main__":
    inicio = time.time()
    caminho, tentativas = tentativa_com_reinicios()

    fim = time.time()

    if caminho:
        print(f"\n✅ Solução encontrada em {len(caminho) - 1} passos, após {tentativas} tentativa(s):")
        for passo in caminho:
            imprimir_estado(passo)
    else:
        print(f"\n❌ Não foi possível encontrar uma solução após {tentativas} tentativa(s).")

    print(f"\nTempo total de execução: {fim - inicio:.2f} segundos\n")