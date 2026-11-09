# 📈 Regressão Linear Simples — Previsão de Pontuação

Projeto de Machine Learning que usa **Regressão Linear Simples** para prever a **pontuação em um teste** a partir das **horas de estudo** de um aluno.

> 🚧 Projeto em desenvolvimento, parte dos meus estudos de Machine Learning.

## 🎯 Objetivo

Responder à pergunta: *quanto a quantidade de horas estudadas influencia a nota obtida?*
O modelo aprende a relação linear entre as duas variáveis:

```
pontuacao_teste = β0 + β1 · horas_estudo
```

## 📊 Dataset

Arquivo: [`datasets/pontuacao_teste.csv`](datasets/pontuacao_teste.csv) — 100 registros.

| Coluna            | Descrição                        |
|-------------------|----------------------------------|
| `horas_estudo`    | Horas dedicadas ao estudo (feature) |
| `pontuacao_teste` | Nota obtida no teste (alvo)      |

## 🧠 Etapas do projeto

- [ ] Análise exploratória dos dados (EDA)
- [ ] Análise de correlação
- [ ] Treinamento do modelo de Regressão Linear
- [ ] Avaliação (R², MAE, RMSE) e análise de resíduos
- [ ] Disponibilização do modelo via API (FastAPI)

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
