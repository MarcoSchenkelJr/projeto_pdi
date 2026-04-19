# 🎨 PDI Studio

Um sistema interativo completo para **Processamento Digital de Imagens (PDI)**, desenvolvido com foco acadêmico e didático. O projeto une a performance matricial do OpenCV no backend com uma interface rica, reativa e moderna construída em React.

## 🚀 O Projeto

Este software foi desenvolvido como projeto de conclusão/avaliação da disciplina de Processamento Digital de Imagens. O grande diferencial do PDI Studio é o seu **Exportador Acadêmico**: além de processar as imagens em tempo real na tela, o sistema permite baixar um `.zip` contendo a imagem original, o resultado e um arquivo `algoritmo_utilizado.py`, que explica a fundamentação teórica e demonstra a implementação matemática do algoritmo em **Python Puro** (usando laços de repetição e matrizes, sem caixas-pretas).

## 🛠️ Funcionalidades Implementadas

* **Operações Pontuais:** Conversão para Tons de Cinza (Grayscale), Limiarização (Threshold), Controle de Brilho e Contraste.
* **Filtros Espaciais:** Suavização por Média (Blur), Filtro de Mediana, Passa-Baixa (Gaussiano) e Passa-Alta (Detecção de Bordas via Máscaras de Sobel).
* **Transformações Geométricas:** Translação nos eixos X e Y, Rotação (em graus), Escala (Zoom in/out) e Espelhamento (Horizontal e Vertical).
* **Morfologia Matemática:** Erosão e Dilatação com controle dinâmico do tamanho do Elemento Estruturante (*Kernel Size*) e Iterações.

## 🏗️ Arquitetura de Microsserviços

O projeto foi construído separando completamente a camada visual do motor de processamento:

* **Frontend (O Rosto):** Construído com React, TypeScript, Vite, TailwindCSS e ícones Lucide. Gerencia o estado da imagem e a interface responsiva.
* **Backend (O Cérebro):** Construído com Python e FastAPI. Utiliza a biblioteca `opencv-python-headless` para processamento rápido de matrizes no servidor, recebendo e devolvendo arrays de bytes em milissegundos.

## ⚙️ Como executar localmente

Certifique-se de ter o Node.js e o Python 3 instalados na sua máquina.

**1. Rodando o Backend (Terminal 1):**
```bash
cd backend
python -m venv venv
source venv/bin/activate  # (No Windows: venv\Scripts\activate)
pip install -r requirements.txt
uvicorn main:app --reload

**2. Rodando o Frontend (Terminal 2):**

cd frontend
npm install
npm run dev
