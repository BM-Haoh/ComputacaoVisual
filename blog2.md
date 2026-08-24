<style>
  body {
    background-color: #121212 !important;
    color: #e0e0e0 !important;
  }
  a {
    color: #bb86fc !important; /* Cor dos links */
  }
  code {
    background-color: #2d2d2d !important;
    color: #f1f1f1 !important;
  }
</style>

# Filtros de Imagem

Na nossa segunda aula vimos um pouco sobre como podemos representar imagens no computador, o que são pixels e os conceitos de RGB. Assistindo à aula, me lembrei de uma atividade que havia realizado no início do curso, entre o primeiro e o segundo semestre, relacionado à aplicação de filtros à imagens usando a linguagem C, com alguns algoritmos relacionados (Atividade proposta pelo curso CC50, de Harvard).

Decidi revisitar o minha [Solução](https://github.com/code50/154121560/blob/main/pset4/filter_more/helpers.c) para o problema, e compartilhar os algoritmos encontrados na época.

Obs: As imagens eram representadas por uma matriz de pixels com altura e largura, e os Pixels eram representados por uma estrutura `RGBTRIPLE`, que continha os campos `rgbtBlue` (Azul), `rgbtGreen` (Verde) e `rgbtRed` (Vermelho), em que cada um será um valor entre 0 e 255 representando a intensidade de cada cor.

Os filtros com que trabalhei na época foram 4:
1. GrayScale:
    - Converte a imagem para escalas de cinza (preto e branco).
    - Para cada pixel da matriz, tirar a média dos valores de Vermelho, Verde e Azul e substuir os valores originais das cores por essa média.
2. Reflect
    - Espelha a imagem horizontalmente (inverte esquerda e direita).
    - Trocamos os pixels da metade esquerda pelos pixels correspondentes na "mesma linha" na metade direita.
3. Edges
    - Destaca as bordas/contornos, deixando o fundo escuro.
    - Iteramos sobre cada pixel da imagem. Para cada pixel, calculamos a variação de cor na horizontal (representada por gx) e na vertical (gy) usando o próprio pixel + todos os pixels vizinhos para cada uma das cores RGB. Então combinamos essas variações (usando .sqrt(gx² + gy²)), limitamos o resultado a no máximo 255 e substituímos o valor das cores deste pixel pelo novo resultado obtido. É importante só fazer a substituição dos valores ao final, para não "envenenar" a informação das cores originais.
4. Blur
    - Aplica um desfoque (suavização) na imagem usando uma média de vizinhos.
    - Iteramos sobre cada pixel da imagem. Para cada pixel, tiramos a média do próprio pixel + todos os pixels vizinhos para cada uma das cores RGB (Vermelho tem uma média, Verde tem outra e Azul outra). Então, substituímos o valor das cores deste pixel pelo valor das médias correspondentes obtidas. Assim como no Edges, é importante só fazer a substituição dos valores ao final do processo.