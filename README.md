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

As tabelas e os gráficos são apresentados diretamente nos notebooks.

O CSV original contém 2.632 registros (2.633 linhas incluindo o cabeçalho), embora a página da UCI informe 2.633 instâncias. As contagens deste projeto correspondem ao CSV baixado. Os rótulos exatos `maj` e `m` representam acordes maiores e menores; rótulos estendidos, como `maj7` e `m7`, são contabilizados separadamente.

## Investigação do pré-processamento das seis classes

Execute o [notebook de pré-processamento](notebooks/preprocessing.ipynb) pelo JupyterLab:

```sh
.venv/bin/jupyter lab
```

O notebook filtra as seis classes, remove duplicatas exatas, divide `FINGER_POSITIONS` em seis colunas categóricas e analisa combinações ambíguas de raiz e posição dos dedos. Sua conclusão registra as escolhas de pré-processamento adotadas nos experimentos.

O CSV `data/processed/chords_six_classes.csv` é gerado para consultas futuras e não é utilizado na experimentação. Para reproduzir o procedimento dos testes, o notebook de experimentação lê o CSV original em `data/raw/chord-fingers.csv`, refaz o pré-processamento e ajusta a codificação one-hot apenas com os dados de treino de cada fold.

A seção final do notebook de experimentação treina os três pipelines com as 959 instâncias, salva os modelos em `models/` e mostra como carregar um deles e prever a classe a partir de `CHORD_ROOT` e `STRING_1` a `STRING_6`. Os arquivos salvos foram gerados com scikit-learn 1.9.1 e joblib 1.6.0. Use essas versões para carregá-los.
