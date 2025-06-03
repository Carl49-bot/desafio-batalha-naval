# Desafio Batalha Naval
# 1 - Nivel Novato

#include <stdio.h>

// Tamanho fixo do tabuleiro
#define TAMANHO 10
#define TAMANHO_NAVIO 3

int main() {
    int tabuleiro[TAMANHO][TAMANHO] = {0}; // Inicializa todas as posições com 0 (água)

    // Coordenadas iniciais dos navios
    int linhaNavioVertical = 1, colunaNavioVertical = 2;
    int linhaNavioHorizontal = 5, colunaNavioHorizontal = 4;

    // Posiciona navio vertical
    for (int i = 0; i < TAMANHO_NAVIO; i++) {
        tabuleiro[linhaNavioVertical + i][colunaNavioVertical] = 3;
    }

    // Posiciona navio horizontal
    for (int i = 0; i < TAMANHO_NAVIO; i++) {
        tabuleiro[linhaNavioHorizontal][colunaNavioHorizontal + i] = 3;
    }

    // Exibe o tabuleiro
    printf("Tabuleiro - Nível Novato:\n");
    for (int i = 0; i < TAMANHO; i++) {
        for (int j = 0; j < TAMANHO; j++) {
            printf("%d ", tabuleiro[i][j]);
        }
        printf("\n");
    }

    return 0;
}

# 2 - Nivel Aventureiro

#include <stdio.h>

#define TAMANHO 10
#define TAMANHO_NAVIO 3

int main() {
    int tabuleiro[TAMANHO][TAMANHO] = {0};

    // Navio vertical
    int linhaV = 1, colunaV = 1;
    for (int i = 0; i < TAMANHO_NAVIO; i++) {
        tabuleiro[linhaV + i][colunaV] = 3;
    }

    // Navio horizontal
    int linhaH = 6, colunaH = 2;
    for (int i = 0; i < TAMANHO_NAVIO; i++) {
        tabuleiro[linhaH][colunaH + i] = 3;
    }

    // Navio diagonal principal (↘)
    int linhaD1 = 0, colunaD1 = 6;
    for (int i = 0; i < TAMANHO_NAVIO; i++) {
        tabuleiro[linhaD1 + i][colunaD1 + i] = 3;
    }

    // Navio diagonal secundária (↙)
    int linhaD2 = 2, colunaD2 = 7;
    for (int i = 0; i < TAMANHO_NAVIO; i++) {
        tabuleiro[linhaD2 + i][colunaD2 - i] = 3;
    }

    // Exibe o tabuleiro
    printf("Tabuleiro - Nível Aventureiro:\n");
    for (int i = 0; i < TAMANHO; i++) {
        for (int j = 0; j < TAMANHO; j++) {
            printf("%d ", tabuleiro[i][j]);
        }
        printf("\n");
    }

    return 0;
}

# 3 - Nivel Mestre 

#include <stdio.h>

#define TAMANHO 10
#define TAMANHO_HABILIDADE 5
#define NAVIO 3
#define AGUA 0
#define HABILIDADE 5

void aplicarHabilidade(int tabuleiro[TAMANHO][TAMANHO], int efeito[TAMANHO_HABILIDADE][TAMANHO_HABILIDADE], int centroLinha, int centroColuna) {
    int offset = TAMANHO_HABILIDADE / 2;

    for (int i = 0; i < TAMANHO_HABILIDADE; i++) {
        for (int j = 0; j < TAMANHO_HABILIDADE; j++) {
            int linha = centroLinha - offset + i;
            int coluna = centroColuna - offset + j;

            if (linha >= 0 && linha < TAMANHO && coluna >= 0 && coluna < TAMANHO) {
                if (efeito[i][j] == 1 && tabuleiro[linha][coluna] == AGUA) {
                    tabuleiro[linha][coluna] = HABILIDADE;
                }
            }
        }
    }
}

void construirCone(int matriz[TAMANHO_HABILIDADE][TAMANHO_HABILIDADE]) {
    for (int i = 0; i < TAMANHO_HABILIDADE; i++) {
        for (int j = 0; j < TAMANHO_HABILIDADE; j++) {
            if (j >= TAMANHO_HABILIDADE/2 - i && j <= TAMANHO_HABILIDADE/2 + i) {
                matriz[i][j] = 1;
            } else {
                matriz[i][j] = 0;
            }
        }
    }
}

void construirCruz(int matriz[TAMANHO_HABILIDADE][TAMANHO_HABILIDADE]) {
    for (int i = 0; i < TAMANHO_HABILIDADE; i++) {
        for (int j = 0; j < TAMANHO_HABILIDADE; j++) {
            if (i == TAMANHO_HABILIDADE/2 || j == TAMANHO_HABILIDADE/2) {
                matriz[i][j] = 1;
            } else {
                matriz[i][j] = 0;
            }
        }
    }
}

void construirOctaedro(int matriz[TAMANHO_HABILIDADE][TAMANHO_HABILIDADE]) {
    for (int i = 0; i < TAMANHO_HABILIDADE; i++) {
        for (int j = 0; j < TAMANHO_HABILIDADE; j++) {
            if (abs(i - TAMANHO_HABILIDADE/2) + abs(j - TAMANHO_HABILIDADE/2) <= TAMANHO_HABILIDADE/2) {
                matriz[i][j] = 1;
            } else {
                matriz[i][j] = 0;
            }
        }
    }
}

void exibirTabuleiro(int tabuleiro[TAMANHO][TAMANHO]) {
    for (int i = 0; i < TAMANHO; i++) {
        for (int j = 0; j < TAMANHO; j++) {
            printf("%d ", tabuleiro[i][j]);
        }
        printf("\n");
    }
}

int main() {
    int tabuleiro[TAMANHO][TAMANHO] = {0};

    // Posicionando navio para exemplo
    tabuleiro[2][2] = tabuleiro[2][3] = tabuleiro[2][4] = NAVIO;

    // Matrizes de habilidades
    int cone[TAMANHO_HABILIDADE][TAMANHO_HABILIDADE];
    int cruz[TAMANHO_HABILIDADE][TAMANHO_HABILIDADE];
    int octaedro[TAMANHO_HABILIDADE][TAMANHO_HABILIDADE];

    construirCone(cone);
    construirCruz(cruz);
    construirOctaedro(octaedro);

    // Aplicando habilidades em diferentes posições
    aplicarHabilidade(tabuleiro, cone, 5, 5);
    aplicarHabilidade(tabuleiro, cruz, 7, 2);
    aplicarHabilidade(tabuleiro, octaedro, 4, 7);

    // Exibe o tabuleiro final com habilidades
    printf("Tabuleiro - Nível Mestre (Habilidades):\n");
    exibirTabuleiro(tabuleiro);

    return 0;
}
