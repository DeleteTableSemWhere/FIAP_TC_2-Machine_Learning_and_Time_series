# 📈 IBOVESPA Trend Predictor: Machine Learning Aplicado

Este projeto consiste em um pipeline completo de Ciência de Dados para prever a tendência diária (Alta ou Baixa) do índice **IBOVESPA** (^BVSP). Diferente de abordagens estáticas, este projeto consome dados em tempo real via API, processa indicadores técnicos e utiliza um **Ensemble de Modelos** para auxiliar na tomada de decisão financeira.

---

## 🚀 Principais Destaques

* **Automação Total (ETL):** Abandono de arquivos estáticos (`.xlsx`). O sistema baixa, limpa e padroniza dados diretamente do **Yahoo Finance** a cada execução.
* **Engenharia de Features Robusta:** Criação automática de indicadores técnicos (Médias Móveis, RSI, IFR) e variáveis de atraso (Lags) para capturar o "momentum" do mercado.
* **Prevenção de Data Leakage:** Implementação rigorosa de divisão temporal (Treino no passado, Teste no futuro) e remoção cirúrgica de variáveis "futuras" (como Máxima/Mínima do dia alvo).
* **Benchmark de Modelos:** Comparação automatizada entre 5 algoritmos: **Logistic Regression, Random Forest, SVM, XGBoost e Voting Classifier**.

---

## 🛠️ Arquitetura do Projeto

O projeto segue um pipeline linear e auditável:

### 1. Coleta de Dados (`Data Ingestion`)
* **Fonte:** API `yfinance`.
* **Tratamento:** Achatamento de cabeçalhos (MultiIndex), conversão de tipos (`float64`, `datetime`) e tradução de colunas para PT-BR.
* **Período:** Dados históricos de 2017 até o dia atual (D-0).

### 2. Engenharia de Atributos (`Feature Engineering`)
Transformamos preços brutos em inteligência de mercado:
* **Retornos:** Cálculo da variação percentual diária.
* **Tendência:** Médias Móveis Exponenciais (MME) de curto e longo prazo.
* **Alvo (Target):** Classificação binária (1 = Alta, 0 = Baixa/Estável).

### 3. Divisão de Dados (`Splitting`)
Utilizamos uma abordagem de **Série Temporal Estrita** (não aleatória) para simular o mundo real:
* **Treino:** Dados históricos passados.
* **Teste:** Janela temporal futura inédita para o modelo.
* *Blindagem:* Uso de `select_dtypes` para garantir que apenas dados numéricos entrem no modelo, prevenindo erros de tipagem e vazamento de datas.

### 4. Modelagem e Avaliação
Treinamento de múltiplos modelos e seleção baseada em métricas de negócio:
* **Acurácia:** Taxa global de acerto.
* **Precision:** Capacidade de não gerar falsos positivos (crucial para evitar prejuízo financeiro).
* **Matriz de Confusão:** Análise visual dos erros.

---

## 📦 Como Rodar o Projeto

### Pré-requisitos
* Python 3.8+
* Pip

### Instalação
1.  Clone o repositório:
    ```bash
    git clone [https://github.com/SEU-USUARIO/NOME-DO-REPO.git](https://github.com/SEU-USUARIO/NOME-DO-REPO.git)
    ```
2.  Instale as dependências:
    ```bash
    pip install -r requirements.txt
    ```

### Execução
Basta abrir o Jupyter Notebook e rodar todas as células. O pipeline irá:
1.  Baixar os dados mais recentes.
2.  Treinar os modelos.
3.  Exibir os gráficos de performance e a decisão final do dia.

---

## 📊 Resultados Alcançados

O modelo final selecionado (**Logistic Regression / Random Forest**) superou o benchmark aleatório (50%) e a média de mercado.

* **Acurácia em Teste:** ~62% (Consistente com dados reais e limpos).
* **Consistência:** O modelo demonstrou robustez ao migrar de dados estáticos para dados dinâmicos da API, mantendo a performance sem overfitting agressivo.

---

## 🛡️ Aviso Legal
Este projeto tem fins estritamente educacionais e acadêmicos. As previsões geradas pelo modelo **não constituem recomendação de investimento**. O mercado financeiro é volátil e envolve riscos.

---

## ✒️ Autor
Desenvolvido como parte do Tech Challenge (Fase 3) da Pós-Tech Data Analytics.
"""

