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

# Resumão primeiro bimestre

Neste blog vou colocar todos os pontos que eu achei mais relevantes enquanto estudava para a prova:

## 1. Transformações de Intensidade (Ponto a Ponto)

As transformações de intensidade operam diretamente sobre os valores de pixéis de forma isolada, modificando o contraste e o brilho da imagem sem alterar a sua geometria espacial.

* **Transformações Lineares:** Ajustam o contraste e o brilho de forma proporcional.
* **Equação geral:** `s = c * r` (onde `r` é a entrada e `s` é a saída).
* **Expansão/Compressão:** Quando o fator de ajuste altera a inclinação, podemos expandir ou comprimir a faixa dinâmica da imagem.
* **Transformações Logarítmicas:** Úteis para expandir os valores de pixéis mais escuros em imagens com grande variação dinâmica (como imagens médicas ou astronómicas).
* **Equação logarítmica:** `s = c * log(1 + r)`.
* **Transformações de Potência (Correção Gama):** Essenciais para corrigir a forma como os dispositivos de exibição mostram a luminosidade.
* **Equação de potência:** `s = c * r^gama`. Se `gama < 1`, há uma expansão dos tons mais escuros (aumenta o contraste nas sombras); se `gama > 1`, o oposto ocorre.


## 2. Equalização de Histograma

O histograma de uma imagem representa a frequência estatística dos níveis de intensidade de cinzento. A **equalização** é uma técnica poderosa para redistribuir uniformemente esses valores, melhorando o contraste global da cena.

* **Probabilidade e Normalização:** Calculada dividindo a contagem de pixéis de um determinado nível pela quantidade total de pixéis (`M x N`).
* **Tabela de Conversão (LUT - Look-Up Table):** O processo mapeia os valores originais para novos níveis equalizados utilizando a função de distribuição acumulada, permitindo otimizar o uso dos tons disponíveis (por exemplo, expandindo de 8 tons para 16 ou mais).


## 3. Operações Geométricas e Interpolação

Quando precisamos de redimensionar, rotacionar ou transladar uma imagem, os pixéis resultantes podem cair em coordenadas não inteiras. É aí que entram os métodos de interpolação:

* **Interpolação Linear (LERP):** Estima valores entre dois pontos conhecidos (`V0` e `V1`) com base num fator de ponderação `alfa` (`0 <= alfa <= 1`): `V = (1 - alfa) * V0 + alfa * V1`.
* **Interpolação Bilinear:** Estende o conceito em duas dimensões (combinando 3 interpolações lineares entre os vizinhos) para estimar com suavidade o valor de pixéis em redimensionamentos.


## 4. Filtragem Espacial e Convolução

Saindo das operações pontuais, o processamento no **domínio espacial** utiliza a vizinhança dos pixéis através de máscaras ou núcleos (kernels).

* **Convolução vs. Correlação:** A correlação cruza a máscara diretamente sobre a imagem, enquanto a convolução exige a rotação prévia do kernel em 180 graus antes de realizar a soma dos produtos locais `f(x, y) * h(x, y)`.
* **Filtros de Média e Blur (Suavização):** Utilizados para reduzir ruídos e detalhes indesejados.
* **Matrizes de Suavização:** Exemplos clássicos incluem matrizes onde todos os pesos somados normalizam a saída (como máscaras de média 3 x 3), gerando um efeito de desfoque (blur).
* **Tratamento de Bordas:** Um desafio clássico na filtragem espacial ocorre nos limites da imagem (quando o kernel ultrapassa as dimensões da matriz). Estratégias comuns incluem replicar os pixéis de borda, ignorar ou preencher com zeros (zero padding).
