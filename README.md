#include <stdio.h>
#include <stdlib.h>


int vazia(int i, int j, int L, int C, int **tabuleiro) {
  if (i < 0 || i >= L || j < 0 || j >= C) return 0; // Fora do tabuleiro
  if (tabuleiro[i][j] != 0) return 0; // Ocupada por uma peça
  return 1; // Vazia
}


int valida(int i, int j, int L, int C, int **tabuleiro) {
  if (!vazia(i, j, L, C, tabuleiro)) return 0; // Casa ocupada
  // Verifica se tem uma peça preta como vizinha
  if (tabuleiro[i-1][j] == 1 || tabuleiro[i+1][j] == 1 || tabuleiro[i][j-1] == 1 || tabuleiro[i][j+1] == 1) return 1;
  return 0; // Não tem peça preta como vizinha
}


int conta(int L, int C, int **tabuleiro) {
  int i, j, total = 0;
  for (i = 0; i < L; i++) {
    for (j = 0; j < C; j++) {
      if (valida(i, j, L, C, tabuleiro)) total++; // Casa válida para peça branca
    }
  }
  return total;
}


int main() {
  int L, C, P, i, j, x, y, **tabuleiro;
  scanf("%d %d", &L, &C); // Lê as dimensões do tabuleiro
  scanf("%d", &P); // Lê o número de peças pretas
  // Aloca memória para o tabuleiro
  tabuleiro = (int**) malloc(L * sizeof(int*));
  for (i = 0; i < L; i++) {
    tabuleiro[i] = (int*) malloc(C * sizeof(int));
  }
  
  for (i = 0; i < L; i++) {
    for (j = 0; j < C; j++) {
      tabuleiro[i][j] = 0;
    }
  }
  
  for (i = 0; i < P; i++) {
    scanf("%d %d", &x, &y); // Lê a posição da peça preta
    tabuleiro[x-1][y-1] = 1; // Coloca a peça preta na casa correspondente
  }
  // Imprime o número máximo de peças brancas que podem ser colocadas
  printf("%d\n", conta(L, C, tabuleiro));
  // Libera a memória do tabuleiro
  for (i = 0; i < L; i++) {
    free(tabuleiro[i]);
  }
  free(tabuleiro);
  return 0;
}
