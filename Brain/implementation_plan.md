# "Sistema Nervoso" - Integração Frontend x Backend

Este plano descreve como vamos conectar o layout React atual com a API em Python recém-adicionada (FastAPI), dando vida ao upload de imagens e aos processamentos visuais (Threshold e Brightness/Contrast).

## Proposed Changes

Vamos elevar o estado da nossa aplicação para o componente pai e criar a camada de dados baseada em puro fetch API.

### 1. Camada de Serviço (API)
- **[NEW] `src/services/api.ts`**:
  - Função `processThreshold(file, threshold_value)` que criará um `FormData` contendo a imagem e parâmetros.
  - Função `processBrightnessContrast(file, brightness, contrast)` para a rota respectiva.
  - O retorno será interpretado como `Blob` e transformado em `URL.createObjectURL(blob)` para ser consumido nos componentes.

### 2. Gerenciamento de Estado (`MainLayout.tsx`)
- **[MODIFY] `src/components/layout/MainLayout.tsx`**:
  - Adicionaremos **React States**: `imageFile`, `originalImageUrl`, `processedImageUrl`, `activeTool` (threshold ou bc), `toolParams` (variáveis limiar, brilho, contraste).
  - Adicionaremos uma lógica local customizada de **Debounce** (via `useEffect` + `setTimeout`). Isso impedirá disparos desnecessários na porta :8000 se o usuário ficar puxando a barra repetidamente.

### 3. Componentes Visuais
- **[MODIFY] `src/components/layout/Sidebar.tsx`**:
  - O botão de 'Upload' funcionará como `trigger` para acionar via React `useRef` um input invisível `<input type="file" accept="image/*" />`.
  - Passagem da imagem ao componente pai.
- **[MODIFY] `src/components/workspace/CanvasArea.tsx`**:
  - Os quadros (`Original` e `Processed`) deixarão de ser estáticos e exibirão a tag `<img />` caso as URLs de imagem em estado existam, se não, exibirão os ícones atuais de Placeholder.
- **[MODIFY] `src/components/layout/Inspector.tsx`**:
  - Tornaremos os controles de sliders (range inputs) *Controlled Components*. 
  - Renderização condicional: se `activeTool` estiver em threshold, mostramos um Slider (0-255). Se estiver em brightness_contrast, mostramos dois: Brilho (-100 a +100) e Contraste (0.0 a 3.0), conectando os `onChange` via props.

## User Review Required

> [!IMPORTANT]
> Confirmar as escalas (mínimas/máximas) propostas para os ranges dos slides:
> - **Threshold**: de `0` até `255` (Padrão 128).
> - **Brilho**: de `-100` até `100` (Padrão 0).
> - **Contraste**: de `0.1` até `3.0` com variação minuciosa de `0.1` (Padrão 1.0).
> 
> Eles batem corretamente com o que os algoritmos `apply_threshold` e OpenCV em `apply_brightness_contrast` esperam no Backend em `point_operations.py`?

## Verification Plan
1. Após codificação, faremos upload de uma imagem simulada/real para o painel de original.
2. Com o FastAPI rodando em plano de fundo no terminal do usuário, eu verificarei se manipular sliders ativará o debouncer e preencherá o quadro direito (Processado) com resultados processados via chamadas transparentes.
