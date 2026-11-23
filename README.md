# Classificação de acordes de guitarra

O arquivo de origem é o `chord-fingers.csv` original do [conjunto de dados Guitar Chords Finger Positions da UCI](https://archive.ics.uci.edu/dataset/575/guitar%2Bchords%2Bfinger%2Bpositions), armazenado sem alterações em `data/raw/chord-fingers.csv`.

Execute a análise com Python 3:

```sh
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/jupyter lab
```

Execute as células dos notebooks de cima para baixo, seguindo esta ordem:

1. [Análise exploratória](notebooks/eda.ipynb): estrutura do conjunto de dados, distribuições das 42 classes originais e das seis classes selecionadas, duplicatas, formato das posições dos dedos e ambiguidades.
2. [Investigação do pré-processamento](notebooks/preprocessing.ipynb): seleção das classes, remoção de duplicatas e os sete atributos preditores categóricos.
3. [Experimentos](notebooks/experiments.ipynb): codificação one-hot e comparação de Árvore de Decisão, KNN e Random Forest com cinco folds estratificados e semente 42.

As tabelas e os gráficos são apresentados diretamente nos notebooks. Sua execução não exporta arquivos auxiliares CSV, JSON ou de imagem.

O CSV original contém 2.632 registros (2.633 linhas incluindo o cabeçalho), embora a página da UCI informe 2.633 instâncias. As contagens deste projeto correspondem ao CSV baixado. Os rótulos exatos `maj` e `m` representam acordes maiores e menores; rótulos estendidos, como `maj7` e `m7`, são contabilizados separadamente.

## Investigação do pré-processamento das seis classes

Execute o [notebook de pré-processamento](notebooks/preprocessing.ipynb) pelo JupyterLab:

```sh
.venv/bin/jupyter lab
```

O notebook investiga o pré-processamento proposto inteiramente em memória. Ele filtra as seis classes, examina duplicatas exatas, divide `FINGER_POSITIONS` em seis colunas categóricas e analisa combinações ambíguas de raiz e posição dos dedos. Não exporta um conjunto de dados processado, não instancia pipelines de transformação nem treina classificadores. Sua conclusão registra as escolhas de pré-processamento a serem implementadas posteriormente no notebook completo de experimentação.
