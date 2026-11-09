# 📈 Regressão Linear Simples — Previsão de Pontuação

Projeto de Machine Learning que usa **Regressão Linear Simples** para prever a **pontuação em um teste** a partir das **horas de estudo** de um aluno.

> 🚧 Projeto em desenvolvimento, parte dos meus estudos de Machine Learning.

## 💡 Contexto

Uma plataforma online de educação quer entender se **a quantidade de horas que os alunos passam estudando influencia a pontuação no teste final**.

Para responder isso, o projeto treina um algoritmo de **regressão linear simples** que prevê a pontuação do teste a partir das horas de estudo. O fluxo completo vai do carregamento dos dados até a disponibilização do modelo em uma **API** que outras aplicações podem consumir.

## 🎯 Objetivo

- Avaliar se existe relação entre horas de estudo e pontuação no teste final.
- Treinar e validar um modelo capaz de prever a pontuação de um aluno.
- Salvar o modelo treinado e expô-lo por meio de uma API.

## 📐 Como funciona a regressão linear simples

A regressão linear simples usa a **equação da reta** para prever uma variável dependente (`y`) a partir de uma variável independente (`x`):

```
pontuacao_teste = β0 + β1 · horas_estudo
```

- **β0 (intercepto):** ponto onde a reta cruza o eixo Y, ou seja, a pontuação prevista para 0 horas de estudo.
- **β1 (coeficiente):** inclinação da reta, que diz quantos pontos a nota aumenta a cada hora a mais de estudo.

O algoritmo busca a reta que **minimiza os erros** entre os valores reais e os previstos, usando o **método dos mínimos quadrados** (*Ordinary Least Squares*).

## 📊 Dataset

Arquivo: [`datasets/pontuacao_teste.csv`](datasets/pontuacao_teste.csv) — 100 registros.

| Coluna            | Descrição                        |
|-------------------|----------------------------------|
| `horas_estudo`    | Horas dedicadas ao estudo (feature) |
| `pontuacao_teste` | Nota obtida no teste (alvo)      |

## 🧠 Etapas do projeto

- [ ] Carregamento dos dados em um DataFrame do Pandas
- [ ] Análise exploratória dos dados (EDA) e correlação
- [ ] Treinamento do modelo de regressão linear
- [ ] Validação do modelo (R², MAE, RMSE e análise de resíduos)
- [ ] Salvamento do modelo treinado
- [ ] Criação da API com FastAPI para servir as previsões

## 🛠️ Tecnologias

Python · Pandas · Scikit-learn · SciPy · Statsmodels · Pingouin · Matplotlib · Seaborn · FastAPI · Uvicorn · Jupyter

## 🚀 Como executar

Pré-requisitos: Python e [pipenv](https://pipenv.pypa.io/).

```bash
git clone https://github.com/Manoelhns/regressao-linear-simples.git
cd regressao-linear-simples
pipenv install
```

Depois, abra o notebook `modelo_pontuacao.ipynb` no VS Code ou Jupyter e selecione o kernel do ambiente pipenv.

## 📁 Estrutura

```
.
├── datasets/
│   └── pontuacao_teste.csv
├── modelo_pontuacao.ipynb
├── Pipfile
├── Pipfile.lock
└── README.md
```

## 📄 Licença

Distribuído sob a licença MIT. Veja [LICENSE](LICENSE).
