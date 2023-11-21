#include <stdio.h>
#include <stdlib.h>


int vazia(int i, int j, int L, int C, int **tabuleiro) {
  if (i < 0 || i >= L || j < 0 || j >= C) return 0; 
  if (tabuleiro[i][j] != 0) return 0; 
  return 1; 
}


int valida(int i, int j, int L, int C, int **tabuleiro) {
  if (!vazia(i, j, L, C, tabuleiro)) return 0; 
  
  if (tabuleiro[i-1][j] == 1 || tabuleiro[i+1][j] == 1 || tabuleiro[i][j-1] == 1 || tabuleiro[i][j+1] == 1) return 1;
  return 0; 
}


int conta(int L, int C, int **tabuleiro) {
  int i, j, total = 0;
  for (i = 0; i < L; i++) {
    for (j = 0; j < C; j++) {
      if (valida(i, j, L, C, tabuleiro)) total++; 
    }
  }
  return total;
}


int main() {
  int L, C, P, i, j, x, y, **tabuleiro;
  scanf("%d %d", &L, &C); 
  scanf("%d", &P); 
  
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
    scanf("%d %d", &x, &y); 
    tabuleiro[x-1][y-1] = 1; 
  }
  
  printf("%d\n", conta(L, C, tabuleiro));
  
  for (i = 0; i < L; i++) {
    free(tabuleiro[i]);
  }
  free(tabuleiro);
  return 0;
}
