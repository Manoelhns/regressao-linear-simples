# 📈 Regressão Linear Simples — Previsão de Pontuação

Projeto de Machine Learning que usa **Regressão Linear Simples** para prever a **pontuação em um teste** a partir das **horas de estudo** de um aluno. O projeto cobre o ciclo completo: análise exploratória, treinamento, validação estatística do modelo e disponibilização das previsões por meio de uma **API REST com FastAPI**.

## 💡 Contexto

Uma plataforma online de educação quer entender se **a quantidade de horas que os alunos passam estudando influencia a pontuação no teste final**.

Para responder isso, o projeto treina um algoritmo de **regressão linear simples** que prevê a pontuação do teste a partir das horas de estudo. Depois de validado, o modelo é salvo e servido em uma **API** que outras aplicações podem consumir.

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

Arquivo: [`datasets/pontuacao_teste.csv`](datasets/pontuacao_teste.csv) — 101 registros, sem valores ausentes.

| Coluna            | Descrição                           | Faixa de valores |
|-------------------|-------------------------------------|------------------|
| `horas_estudo`    | Horas dedicadas ao estudo (feature) | 1,1 a 46,9 horas |
| `pontuacao_teste` | Nota obtida no teste (alvo)         | 30 a 800 pontos  |

## 🧠 Etapas do projeto

- [x] Carregamento dos dados em um DataFrame do Pandas
- [x] Análise exploratória dos dados (EDA) e correlação
- [x] Treinamento do modelo de regressão linear
- [x] Validação do modelo (R², MAE, MSE, RMSE)
- [x] Análise de resíduos (linearidade, homocedasticidade e normalidade)
- [x] Salvamento do modelo treinado (`joblib`)
- [x] Criação da API com FastAPI para servir as previsões

### 1. Análise exploratória (EDA)

- Estatísticas descritivas com `describe()`.
- Gráfico de dispersão entre horas de estudo e pontuação.
- Boxplots para identificar outliers.
- Correlação de **Pearson** e **Spearman** (heatmaps).
- Histogramas para ver a distribuição de cada variável.

### 2. Treinamento

Os dados foram divididos em **70% para treino e 30% para teste** (`train_test_split`, `random_state=50`), e o modelo `LinearRegression` do scikit-learn foi treinado com o conjunto de treino.

**Equação da reta encontrada:**

```
pontuacao_teste = 15,64 × horas_estudo + 8,48
```

Ou seja, **cada hora a mais de estudo soma cerca de 15,6 pontos** à pontuação prevista.

### 3. Validação com métricas (conjunto de teste)

| Métrica | Valor  | Interpretação |
|---------|--------|---------------|
| **R²**   | 0,983  | As horas de estudo explicam **98,3%** da variação da pontuação |
| **MAE**  | 22,96  | Em média, o modelo erra a nota em **~23 pontos** |
| **MSE**  | 767,00 | Erro quadrático médio (penaliza erros grandes; usado para comparar modelos) |
| **RMSE** | 27,69  | Erro típico de **~28 pontos**, na mesma unidade da nota |

Numa escala de 30 a 800 pontos (média de 455), o erro médio é de cerca de **5% da nota média**. Como o RMSE ficou próximo do MAE, os erros são homogêneos, sem previsões muito discrepantes.

### 4. Análise de resíduos

Os resíduos (`real − previsto`) foram analisados para verificar as premissas da regressão linear:

- **Normalidade:** o QQ plot mostra os resíduos dentro do intervalo de confiança de 95% (R² = 0,959), e o teste de **Shapiro-Wilk** retornou **p-valor = 0,157 (> 0,05)**. Não há evidência contra a normalidade dos resíduos. ✅
- **Homocedasticidade:** o gráfico de resíduos vs. previstos não mostra formato de funil, ou seja, a variância dos erros é parecida em toda a faixa de previsões. ✅
- **Linearidade:** os resíduos padronizados ficam praticamente entre −2 e +2, mas formam um **padrão curvo**. O modelo subestima as notas nos extremos e superestima na faixa intermediária, o que indica que a relação é **levemente não linear**. ⚠️

### 5. Uso do modelo

Exemplos de previsões feitas no notebook:

- Um aluno que estuda **30,4 horas** tem pontuação prevista de **~484 pontos**.
- Para atingir **600 pontos**, o modelo indica cerca de **37,8 horas** de estudo (isolando `x` na equação da reta).

O modelo treinado foi salvo em [`modelo_regressao_linear.pkl`](modelo_regressao_linear.pkl) com `joblib`.

## ✅ Conclusão

Existe uma **relação positiva e muito forte** entre horas de estudo e pontuação no teste final: quanto mais o aluno estuda, maior tende a ser a nota. O modelo de regressão linear simples explica 98% da variação das notas, com erro típico de ~28 pontos, e já pode ser usado pela plataforma por meio da API.

> Uma correlação forte não prova causa e efeito sozinha, mas, neste contexto, é um bom indicativo de que incentivar mais horas de estudo tende a elevar o desempenho dos alunos.

## 🔮 Próximos passos

- Testar uma **regressão polinomial** (incluindo `horas_estudo²`) para capturar a curvatura vista na análise de resíduos e comparar as métricas com o modelo atual.
- Usar **validação cruzada** (*cross-validation*) para uma estimativa de erro mais robusta.
- Adicionar validação de entrada na API (por exemplo, impedir horas negativas).

## 🛠️ Tecnologias

| Finalidade | Bibliotecas |
|---|---|
| Manipulação de dados | Pandas, NumPy |
| Visualização | Matplotlib, Seaborn |
| Modelagem | Scikit-learn |
| Estatística | SciPy, Statsmodels, Pingouin |
| API | FastAPI, Uvicorn, Pydantic |
| Persistência do modelo | Joblib |
| Ambiente | Jupyter, Pipenv |

## 🚀 Como executar

Pré-requisitos: Python 3.13 e [pipenv](https://pipenv.pypa.io/).

```bash
git clone https://github.com/Manoelhns/regressao-linear-simples.git
cd regressao-linear-simples
pipenv install
```

### Notebook

Abra o [`modelo_pontuacao.ipynb`](modelo_pontuacao.ipynb) no VS Code ou no Jupyter e selecione o kernel do ambiente pipenv.

### API

Suba o servidor:

```bash
pipenv run uvicorn api_modelo_regressao_linear:app --reload
```

A API fica disponível em `http://127.0.0.1:8000`, com documentação interativa (Swagger) em **http://127.0.0.1:8000/docs**, onde dá para testar o endpoint direto pelo navegador.

**Endpoint:** `POST /predict`

Requisição:

```json
{
  "horas_estudo": 30.4
}
```

Resposta:

```json
{
  "pontuacao_teste": [484]
}
```

Exemplo com `curl`:

```bash
curl -X POST http://127.0.0.1:8000/predict \
  -H "Content-Type: application/json" \
  -d '{"horas_estudo": 30.4}'
```

## 📁 Estrutura

```
.
├── datasets/
│   └── pontuacao_teste.csv          # dados de horas de estudo x pontuação
├── modelo_pontuacao.ipynb           # EDA, treino, validação e análise de resíduos
├── modelo_regressao_linear.pkl      # modelo treinado
├── api_modelo_regressao_linear.py   # API FastAPI que serve as previsões
├── Pipfile
├── Pipfile.lock
├── LICENSE
└── README.md
```

## 📄 Licença

Distribuído sob a licença MIT. Veja [LICENSE](LICENSE).
