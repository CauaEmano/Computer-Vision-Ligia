# Classificação de Pneumonia em Radiografias Torácicas 🫁

Este repositório contém a implementação completa do desafio de Visão Computacional para a classificação binária de radiografias de tórax (Normal vs. Pneumonia), desenvolvido como parte do processo seletivo da Ligia.

## 📁 Estrutura do Repositório

* `notebooks/ModeloCV.ipynb, EDA.ipynb, train.csv, trainEDA.csv`:
Notebook contendo EDA +  Notebook principal contendo todo o pipeline: Pré-processamento, Treinamento (com KerasTuner) e Inferência.
* `melhor_modelo.h5`: Arquivo serializado com os pesos do melhor modelo treinado (Época 16), salvo via callback `ModelCheckpoint`.
* `submissao_ligia.csv`: Arquivo de predições gerado para submissão na plataforma Kaggle.
* `requirements.txt`: Lista de dependências necessárias para reproduzir o ambiente.

## 🛠️ Tecnologias e Abordagem
* **Deep Learning:** Construção de uma CNN customizada do zero utilizando `TensorFlow/Keras`.
* **Otimização:** Busca de hiperparâmetros automatizada com `KerasTuner`.
* **Tratamento de Dados:** Uso de *Class Weights* para mitigação do desbalanceamento de classes e *Data Augmentation* conservador (preservando a lateralidade anatômica).
* **Interpretabilidade:** Geração de mapas de calor via *Grad-CAM* para validação clínica das predições.

## 🚀 Como Executar o Projeto

### 1. Preparação do Ambiente
Clone este repositório e instale as dependências:
```bash
git clone https://github.com/CauaEmano/Computer-Vision-Ligia
cd Computer-Vision-Ligia
pip install -r requirements.txt
```

### 2. Download dos Dados
Devido ao tamanho dos arquivos, as imagens originais não estão no repositório.
1. Faça o download do dataset na página da competição no kaggle.
2. Extraia as pastas train/ e test_images/ no diretório do projeto, mesmo nível do notebook.

### 3. Treinamento e inferência 
1. Abra o arquivo notebooks/ModeloCV.ipynb em um ambiente Jupyter.
2. Execute as células sequencialmente. O notebook está logicamente dividido em seções.
3. Para pular o treinamento e a otimização (que pode demorar) e ir direto para a inferência, você pode carregar diretamente o modelo salvo executando:

```bash
from tensorflow import keras
modelo = keras.models.load_model('melhor_modelo.h5')
```

### 4. Geração do Arquivo de Submissão (Kaggle)
A última célula do notebook contém o script exato de inferência. Ele lê as imagens da pasta ```test_images/```, extrai as probabilidades puras (```target```) usando o modelo otimizado, formata as strings de identificação (removendo o prefixo do caminho) e exporta o arquivo ```submissao_ligia.csv``` no formato exigido pela plataforma Kaggle.