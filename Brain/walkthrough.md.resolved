# Conexão Frontend e Backend PDI

Implementei completamente a "espinha dorsal" e a "rede neural" da nossa aplicação! O frontend agora é capaz de conversar de verdade com os algoritmos poderosos de processamento que você escreveu no backend usando FastAPI e OpenCV.

## O Que Foi Feito:

1. **A Camada de Serviço (API):**
   - No `src/services/api.ts`, criamos a comunicação padronizada via Fetch. Quando acionada, ela encapsula as imagens (`File`) em `FormData`, junta os coeficientes dinâmicos como _Threshold Level_ ou _Brilho_, envia para o Python e transforma o binário mágico retornado do endpoint em um simples Endereço de Memória (Blob URL).

2. **Gerenciamento de Estado no Front:**
   - O coração do projeto foi alocado de forma sofisticada dentro de `MainLayout.tsx`. Ao invés de usar Contextos complexos, usamos *Lifted State* para que o App gerencie sozinho a "Foto Original" e a "Foto Final" e passe tudo para as pontas.
   - 🛡️ **O Debouncer Inteligente**: Implementei um timer que segura seus disparos ao Backend via Sliders. Então quando você desliza sem parar a barrinha "Contraste", o motor aguarda você aliviar o peso (cerca de 200 ms), poupando seu CPU no Python e dando aquela sensação real-time no Browser!

3. **Injeção Dinâmica em Componentes:**
   - **Upload Invisível**: Configurado um campo `#file` nativo oculto dentro da classe do botão da barra de ferramentas (na Sidebar) para capturar o seu arquivo e soltar a imagem crua no seu Canvas esquerdo automaticamente.
   - **Controles (Inputs controlados)**: As barrinhas do Painel Direito agora geram reatividade instantânea no Frontend em cima dos limites (`Min` `Max`) matematicamente compatíveis com OpenCV, já puxados da sua regra backend. Quando o motor esbarra, a requisição voa para o `localhost:8000`.

## É Hora do Show
Volte para o seu navegador em [http://localhost:5173](http://localhost:5173). As novidades visuais e lógicas já estão rodando nela:

1. Clique no Botão de Upload na esquerda (A Setinha para cima).
2. Carregue uma imagem clássica (Lenna.png, cameraman.png, etc).
3. Selecione o botão central de Brilho & Contraste, mexa os Sliders à direita e espie o resultado imediato chegar do Python! 🚀
