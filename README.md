# Análise Exploratória de Dados — Desempenho Escolar de Estudantes

**Disciplina:** CMPINAM – Introdução ao Aprendizado de Máquina  
**Instituição:** Instituto Federal de Educação, Ciência e Tecnologia — Câmpus Campinas  
**Professor:** Everton Meyer da Silva  

---

## 👥 Integrantes do Grupo

| Nome | Matrícula |
|------|-----------|
| [Nome do integrante 1] | [Matrícula] |
| [Nome do integrante 2] | [Matrícula] |

---

## 📌 Problema Analisado

Este projeto analisa os fatores associados ao **desempenho escolar de estudantes do ensino secundário em Portugal**, com base em dados reais coletados em duas escolas durante o ano letivo de 2005–2006.

O objetivo é identificar quais variáveis — comportamentais, socioeconômicas e familiares — estão associadas às notas finais dos alunos nas disciplinas de **Matemática** e **Língua Portuguesa**, gerando insights que possam orientar intervenções pedagógicas e políticas educacionais.

---

## 🗂️ Dataset Utilizado

**Nome:** Student Performance Dataset  
**Fonte:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/student+performance)  
**Referência:** P. Cortez e A. Silva. *Using Data Mining to Predict Secondary School Student Performance.* EUROSIS, 2008.

| Arquivo | Disciplina | Nº de registros | Nº de atributos |
|---------|------------|-----------------|-----------------|
| `student-mat.csv` | Matemática | 395 | 33 |
| `student-por.csv` | Língua Portuguesa | 649 | 33 |

Cada linha representa **um estudante** em uma disciplina. Os atributos cobrem dados demográficos, socioeconômicos, comportamentais e notas dos três períodos (G1, G2, G3).

---

## 🔍 Principais Achados da EDA

1. **G1 e G2 são os melhores preditores de G3** — correlações de r ≈ 0.80–0.92, indicando que a trajetória ao longo do ano é altamente consistente.
2. **Reprovações anteriores** têm correlação negativa relevante com G3 (r ≈ −0.36 a −0.40), sendo um forte sinal de risco acadêmico.
3. **Aspiração ao ensino superior** está associada a notas 3–4 pontos maiores em Matemática e 2–3 em Português.
4. **Escolaridade dos pais** (especialmente da mãe) mostra tendência positiva com as notas dos filhos — alinhado à literatura de capital cultural familiar.
5. **Consumo de álcool** tem efeito negativo moderado no desempenho, sendo parte de um padrão comportamental mais amplo (mais saídas, menos estudo).
6. **Tempo de estudo** apresenta tendência positiva, mas com ruído — alunos com dificuldades tendem a estudar mais de forma compensatória.
7. **Faltas** têm correlação fraca com G3 (r ≈ −0.03 a −0.09), não sendo um preditor isolado confiável.
8. **Estudantes urbanos** têm médias levemente superiores de forma consistente nos três períodos.
9. Em Matemática, o sexo masculino apresenta média ligeiramente maior; em Português, o feminino tem leve vantagem.
10. A distribuição de G3 em Matemática apresenta pico em zero (possíveis desistentes), enquanto em Português a distribuição é mais próxima da normal.

---

## 📁 Estrutura do Repositório

```
.
├── README.md
├── student-mat.csv          # Dataset de Matemática
├── student-por.csv          # Dataset de Português
├── EDA_student_performance.ipynb   # Notebook da Parte 1 (EDA)
└── (em breve) Modelagem_student_performance.ipynb  # Notebook da Parte 2
```

---

## ▶️ Como Executar o Notebook

### Pré-requisitos

- Python 3.8+
- Jupyter Notebook ou JupyterLab

### Instalação das dependências

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### Execução

1. Clone o repositório:
   ```bash
   git clone https://github.com/[usuario]/[repositorio].git
   cd [repositorio]
   ```

2. Inicie o Jupyter:
   ```bash
   jupyter notebook
   ```

3. Abra o arquivo `EDA_student_performance.ipynb` e execute **Run All** (`Kernel > Restart & Run All`).

> ⚠️ Os arquivos `student-mat.csv` e `student-por.csv` devem estar na **mesma pasta** do notebook.

---

## 📦 Parte 2 — Modelagem e Avaliação (em desenvolvimento)

A Parte 2 incluirá pré-processamento avançado, treinamento de modelos de ML (baseline + pelo menos 3 técnicas), validação cruzada e análise crítica dos resultados. Será adicionada a este repositório até **junho de 2026**.
