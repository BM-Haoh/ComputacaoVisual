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

# Domínio da Frequência e Transformada de Fourier

Além do domínio espacial (em que manipulamos os pixels diretamente por suas coordenadas), podemos analisar e processar imagens no **domínio da frequência**. Através da Transformada de Fourier, decompomos a imagem em suas componentes de frequência (senos e cossenos), permitindo entender a taxa de variação das intensidades de brilho.

---

Obs: A Transformada de Fourier Bidimensional (DFT) é dada por `F(u,v) = sum(sum(f(r,c) * e^(-j2pi * (ur/M + vc/N))))`. O processo é **reversível**: a Transformada Inversa de Fourier (IFT) permite reconstruir a imagem espacial original sem perda de informação a partir do espectro.

Os conceitos centrais desse tema são:

1. **Centralização e Escala Logarítmica (Shift & Log):**
   - **Shift (Deslocamento):** Por padrão, a frequência zero (componente DC) fica no canto superior esquerdo. Aplicamos o shift para movê-la para o centro. No espectro centralizado, o centro contém as baixas frequências e as extremidades contêm as altas frequências.
   - **Escala Logarítmica:** Como a intensidade da frequência zero é ordens de grandeza maior que as demais, aplicamos `S = c * log(1 + |F(u,v)|)` para expandir o contraste e visualizar detalhes de alta frequência que ficariam invisíveis.

2. **Dualidade Espaço vs. Frequência:**
   - **Impulso no Espaço <-> Constante na Frequência:** Um pixel isolado com mudança abrupta (impulso) contém todas as frequências.
   - **Imagem Constante no Espaço <-> Impulso na Frequência:** Uma imagem uniforme possui apenas a frequência zero.
   - **Teorema da Convolução:** A convolução no domínio espacial equivale a uma simples multiplicação ponto a ponto no domínio da frequência (`f(x,y) * h(x,y) <=> F(u,v) . H(u,v)`). Filtros grandes costumam ser computacionalmente mais eficientes na frequência.
   - **Ortogonalidade:** As frequências no espectro são perpendiculares aos padrões espaciais (ex: bordas horizontais na imagem geram uma linha vertical no espectro).

3. **Tipos de Filtragem na Frequência:**
   - **Passa-Baixa (Low-Pass):** Mantém o centro e atenua as bordas do espectro. O resultado é um efeito de suavização/desfoque (blur), pois remove as altas frequências (variações abruptas).
   - **Passa-Alta (High-Pass):** Elimina a frequência zero e o centro, preservando as extremidades. O resultado é o destaque de bordas, contornos e ruídos.
   - **Filtro Rejeita-Faixa (Notch Filter):** Ruídos periódicos (como padrões repetitivos de grades) criam pontos brilhantes simétricos fora do centro. Zeramos esses pontos específicos no espectro e aplicamos a IFT para limpar a imagem.

4. **Amostragem e Aliasing:**
   - **Teorema de Nyquist:** A taxa de amostragem deve ser maior que o dobro da maior frequência da imagem (`f_amostragem > 2 * f_max`) para permitir a reconstrução perfeita.
   - **Aliasing:** Ocorre na subamostragem (quando a taxa fica abaixo de Nyquist). Frequências altas "se dobram" e simulam frequências baixas, gerando serrilhados e padrões Moiré.
   - **Anti-Aliasing:** Consiste em aplicar um filtro passa-baixa antes do redimensionamento/subamostragem para eliminar previamente as altas frequências problemáticas.
