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

# Reflexão: Do Pixel em C à Renderização Neural

Ao longo do semestre na disciplina de Computação Visual, a ideia de manter este blog veio quase como uma obrigação para compor nota, mas ao longo dele acabei podendo criar alguns posts que fogem de registros de aula dos quais achei mais interessantes. O espaço me forçou a sair da teoria pura e buscar conexões com códigos que eu já havia escrito no passado e com tecnologias que estavam acontecendo no mercado em tempo real.

---

Os principais pontos dessa jornada entre a teoria da sala de aula e os posts publicados aqui foram:

1. **A Base Matemática por Trás da Abstração:**
   - Quando revisitamos conceitos como matrizes de pixels (`RGBTRIPLE`), filtros espaciais e equalização de histograma, fica claro que qualquer processamento visual, por mais complexo que pareça, se resume a operações matemáticas sobre arrays de números.
   - Relembrar os algoritmos que implementei em C no início da graduação (como o Blur e o Edges do CC50), mesmo antes de conhecer a matéria de "computação visual", ajudou a visualizar na prática o cuidado necessário com o estado da memória e o porquê de conceitos como convolução e tratamento de bordas serem tão críticos.

2. **Mudança de Domínio e Eficiência Computacional:**
   - Um dos momentos mais interessantes da matéria foi sair do domínio espacial e enxergar a imagem no domínio da frequência através da Transformada de Fourier.
   - Entender a dualidade entre espaço e frequência mostra que muitos problemas computacionalmente caros (como aplicar máscaras gigantescas ou remover ruídos periódicos) se tornam simples multiplicações ponto a ponto quando mudamos a forma de representar o dado.

3. **Teoria Clássica vs. Mercado Atual (O Caso DLSS):**
   - Nos momentos em que precisei buscar temas fora do material padrão de aula para alimentar o blog, investigar o vazamento do DLSS 5 fez toda a matéria fazer mais sentido. Alguma coisa "bate diferente" quando você tropeça em um assunto e pensa "ah, eu vi isso na faculdade".
   - Contrastar a interpolação geométrica clássica (bilinear, vizinhos mais próximos) e os estágios tradicionais da pipeline gráfica (Vertex e Fragment Shaders) com a inferência por redes neurais evidenciou os trade-offs reais da computação moderna: o equilíbrio entre precisão matemática, alucinações de IA (como os artefatos bizarros em rostos que comentei no post) e o papel decisivo do hardware dedicado (como os Tensor Cores).

No fim das contas, mesmo que eu não siga especificamente para a área de computação gráfica, valeu a pena tirar um tempo para conectar esses pontos. Seja manipulando ponteiros em C, multiplicando matrizes na GPU ou rodando modelos de IA hoje em dia, entender o básico de como o dado é representado por baixo dos panos ajuda a não tratar tudo como uma 'caixa preta' mágica.