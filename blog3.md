<style>
  body {
    background-color: #121212 !important;
    color: #e0e0e0 !important;
  }
  a {
    color: #bb86fc !important;
  }
  code {
    background-color: #2d2d2d !important;
    color: #f1f1f1 !important;
  }
</style>

# Equalização de Histograma

Técnica do domínio espacial utilizada para melhorar o contraste global de imagens digitais. O objetivo principal é redistribuir os níveis de intensidade de brilho para cobrir uniformemente todo o intervalo dinâmico disponível [0, L-1].

Muito aplicada em imagens de **raio-X e exames médicos** (para destacar estruturas com pouca diferença de contraste), **imagens de satélite** e **sistemas de visão noturna**.

Obs: O histograma discreto `h(r_k) = n_k` indica a quantidade de pixels com intensidade `r_k`. Na equalização, calculamos um novo valor `s_k` para cada pixel usando a Função de Distribuição Acumulada (CDF), dada por: `s_k = round((L - 1) * sum(p(r_j)))` onde `p(r_k) = n_k / (M * N)`.

Etapas do processo de computação:

1. **Histograma Original:**
   - Mapear a quantidade de pixels `n_k` para cada nível de intensidade `r_k` (de 0 a 255 em 8 bits).

2. **Probabilidade Normalizada:**
   - Calcular a probabilidade de cada tom ocorrer: `p(r_k) = n_k / (M * N)` (onde `M * N` é o total de pixels).

3. **Soma Acumulada (CDF):**
   - Realizar a soma acumulada das probabilidades do nível 0 até k. A curva resultante varia de 0 a 1.

4. **Mapeamento e Substituição:**
   - Multiplicar o valor acumulado por `L - 1` (255) e arredondar para o inteiro mais próximo.
   - Substituir os pixels originais `r_k` pelos novos valores `s_k`.
