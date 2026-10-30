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

# Introdução aos Shaders e Pipeline Gráfica

Os **shaders** são procedimentos personalizados de tonalização e iluminação escritos em linguagens apropriadas (Shading Languages) que especificam como os vértices e pixels de uma cena são calculados diretamente na GPU. Por serem arquivos de texto leves com instruções diretas para o processador gráfico, o tempo de carregamento pesado em aplicações 3D não vem deles, mas sim da transferência de modelos, cenas e texturas do armazenamento para a VRAM.

---

Obs: O pipeline gráfico evoluiu de um modelo de **Pipeline Fixa** (onde o desenvolvedor só alterava flags de estado no hardware, como no Nintendo Wii) para a **Pipeline Programável**, permitindo injetar algoritmos customizados para controle total da geometria, iluminação e aspectos visuais dos pixels.

Os pontos centrais sobre a arquitetura, comunicação e funcionamento dos shaders são:

1. **Arquitetura de Comunicação e APIs Gráficas:**
   - A comunicação segue o fluxo: `Aplicação (CPU) -> API Gráfica -> Driver do S.O. -> GPU (Hardware)`.
   - **APIs Padrão:** Direct3D/DirectX (Microsoft), OpenGL/Vulkan (Khronos Group, sendo o Vulkan focado em baixo nível derivado do Mantle), Metal (Apple) e WebGL (navegadores).
   - **Compute Shader (GPGPU):** Estágio desvinculado do fluxo visual tradicional, focado exclusivamente no processamento matemático paralelo de uso geral na GPU (como simulações físicas e multiplicação de matrizes).

2. **Estágios Principais da Pipeline Programável:**
   - Para renderizar qualquer elemento em tela, são necessários no mínimo dois shaders: **Vertex Shader** e **Fragment/Pixel Shader**.
   - **Vertex Shader (Programável):** Primeiro estágio obrigatório. Processa vértices individualmente e converte posições do espaço local para o espaço de tela via matriz MVP (`Vtela = Mprojeção * Mvisão * Mmodelo * Vlocal`).
   - **Tessellation Shader (Opcional):** Subdivide primitivas em tempo real para ajustar dinamicamente o nível de detalhe (LOD) com base na distância da câmera.
   - **Geometry Shader (Opcional):** Gera ou destrói primitivas geométricas diretamente na GPU (pode ser custoso).
   - **Fragment / Pixel Shader (Programável):** Atua sobre os fragmentos após a rasterização para calcular cor final, iluminação, texturas, transparências e pós-processamento no framebuffer.

3. **Modificadores e Tipos de Dados Básicos (GLSL):**
   - **in / out:** Definem dados que entram e saem do estágio da pipeline.
   - **uniform:** Variáveis globais enviadas da CPU para a GPU que permanecem constantes
