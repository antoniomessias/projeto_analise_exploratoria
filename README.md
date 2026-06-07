# Desempenho Escolar de Estudantes — EDA e Modelagem de ML

**Disciplina:** CMPINAM – Introdução ao Aprendizado de Máquina  
**Instituição:** Instituto Federal de Educação, Ciência e Tecnologia — Câmpus Campinas  
**Professor:** Everton Meyer da Silva  

| Integrante | Matrícula |
|---|---|
| Antonio Messias | CP 3026451 |
| Alan Rocha | CP 3025039 |

---

## 📌 Problema Analisado

Este projeto analisa os **fatores associados ao desempenho escolar de estudantes do ensino secundário em Portugal**, com base em dados reais coletados em duas escolas durante o ano letivo de 2005–2006.

O objetivo é identificar quais variáveis — comportamentais, socioeconômicas e familiares — estão associadas às notas finais dos alunos nas disciplinas de **Matemática** e **Língua Portuguesa**, e construir modelos preditivos capazes de estimar a nota final (G3) de um estudante.

---

## 🗂️ Dataset Utilizado

**Nome:** Student Performance Dataset  
**Fonte:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/student+performance)  
**Referência:** P. Cortez e A. Silva. *Using Data Mining to Predict Secondary School Student Performance.* EUROSIS, 2008.

| Arquivo | Disciplina | Registros | Atributos |
|---|---|---|---|
| `student-mat.csv` | Matemática | 395 | 33 |
| `student-por.csv` | Língua Portuguesa | 649 | 33 |

Cada linha representa **um estudante** em uma disciplina. Os atributos cobrem dados demográficos, socioeconômicos, comportamentais e as notas dos três períodos (G1, G2, G3).

---

## 📁 Estrutura do Repositório

```
.
├── README.md
├── student-mat.csv                        # Dataset de Matemática
├── student-por.csv                        # Dataset de Português
└── student_performance_completo.ipynb     # Notebook unificado (Parte 1 + Parte 2)
```

---

## 🔍 Principais Achados da EDA (Parte 1)

1. **G1 e G2 são os melhores preditores de G3** — correlações de r ≈ 0.80–0.92, indicando que a trajetória ao longo do ano é altamente consistente.
2. **Reprovações anteriores** têm correlação negativa relevante com G3 (r ≈ −0.36 a −0.40), sendo um forte sinal de risco acadêmico.
3. **Aspiração ao ensino superior** está associada a notas 3–4 pontos maiores em Matemática e 2–3 em Português.
4. **Escolaridade dos pais** (especialmente da mãe) mostra tendência positiva com as notas dos filhos.
5. **Consumo de álcool** tem efeito negativo moderado no desempenho, sendo parte de um padrão comportamental mais amplo.
6. **Tempo de estudo** apresenta tendência positiva, mas com ruído — alunos com dificuldades tendem a estudar mais como compensação.
7. **Faltas** têm correlação fraca com G3 (r ≈ −0.03 a −0.09), não sendo um preditor isolado confiável.
8. **Estudantes urbanos** têm médias levemente superiores de forma consistente nos três períodos.
9. Em Matemática, o sexo masculino apresenta média ligeiramente maior; em Português, o feminino tem leve vantagem.
10. A distribuição de G3 em Matemática apresenta pico em zero (possíveis desistentes), enquanto em Português a distribuição é mais próxima da normal.

---

## 🤖 Metodologia de Modelagem (Parte 2)

### Tarefa
**Regressão:** Prever a nota final G3 com base em todas as features disponíveis (incluindo G1 e G2).

### Pré-processamento
- Remoção de registros com G3=0 (desistências): 357 registros em Matemática, 634 em Português
- One-Hot Encoding nas 17 variáveis categóricas (`drop_first=True` para evitar multicolinearidade)
- Divisão treino/teste (80/20) com `random_state=42` **antes** de qualquer transformação
- StandardScaler ajustado **apenas no treino**, aplicado no teste (prevenção de data leakage)

### Modelos Treinados
| Modelo | Justificativa |
|---|---|
| **Regressão Linear** | Baseline — modelo mais simples, relação linear |
| **Árvore de Decisão** | Modelo não-linear interpretável; contraste ao Random Forest |
| **Random Forest** | Ensemble robusto; reduz overfitting via bagging |
| **Gradient Boosting** | Ensemble sequencial; captura padrões residuais |

### Validação
- Métricas: RMSE, MAE, R², CV-R² (5-fold cross-validation no conjunto de treino)

---

## 📊 Principais Resultados (Parte 2)

### Matemática

| Modelo | RMSE | MAE | R² | CV-R² |
|---|---|---|---|---|
| **Random Forest** ✅ | **0.821** | **0.599** | **0.930** | 0.915 |
| Gradient Boosting | 0.910 | 0.679 | 0.914 | 0.919 |
| Regressão Linear | 0.900 | 0.675 | 0.916 | 0.923 |
| Árvore de Decisão | 1.124 | 0.847 | 0.869 | 0.853 |

### Português

| Modelo | RMSE | MAE | R² | CV-R² |
|---|---|---|---|---|
| **Regressão Linear** ✅ | **0.945** | **0.765** | **0.891** | 0.870 |
| Gradient Boosting | 1.010 | 0.766 | 0.876 | 0.861 |
| Random Forest | 1.025 | 0.766 | 0.872 | 0.869 |
| Árvore de Decisão | 1.950 | 1.205 | 0.536 | 0.764 |

> **Interpretação:** Os modelos erram em média menos de **1 ponto** na escala de 0–20. O Random Forest foi melhor em Matemática; a Regressão Linear foi competitiva em ambas, evidenciando que as relações são predominantemente lineares — puxadas pela dominância de G2 como preditor.

---

## ▶️ Como Executar o Notebook

### Pré-requisitos

- Python 3.8+
- Jupyter Notebook ou JupyterLab

### Instalação das dependências

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

### Execução

1. Clone o repositório:

```bash
git clone https://github.com/antoniomessias/projeto_analise_exploratoria.git
cd projeto_analise_exploratoria
```

2. Inicie o Jupyter:

```bash
jupyter notebook
```

3. Abra `student_performance_completo.ipynb` e execute **Run All** (`Kernel > Restart & Run All`).

> ⚠️ Os arquivos `student-mat.csv` e `student-por.csv` devem estar na **mesma pasta** do notebook.

---

## 📦 Sobre o Notebook

O notebook unificado `student_performance_completo.ipynb` cobre o pipeline completo:

| Seção | Conteúdo |
|---|---|
| 1 | Entendimento do Problema e Hipóteses |
| 2 | Descrição da Base de Dados |
| 3 | Importações e Carregamento |
| 4 | Limpeza e Preparação Inicial |
| 5 | EDA — 10 perguntas/hipóteses respondidas |
| 6 | Síntese Crítica da EDA |
| 7 | Definição do Objetivo Preditivo |
| 8–9 | Preparação dos Dados para ML |
| 10 | Treinamento dos 4 Modelos |
| 11 | Comparação Visual dos Modelos |
| 12 | Importância das Features |
| 13 | Análise de Resíduos |
| 14–15 | Interpretação dos Resultados e Conclusões |
