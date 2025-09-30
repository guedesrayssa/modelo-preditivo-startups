<div align="center">
    <img src="assets/unicorn-predictor-logo.png" alt="Unicorn Predictor Logo" width="200"/>
</div>
<div align="center">
<h1> Unicorn Predictor</h1>
</div>
<div align="center">

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+code&weight=300&size=18&pause=1000&color=E05A80&width=435&lines=Transformando+dados+em+vis%C3%A3o+de+futuro!)](https://git.io/typing-svg)

</div>

# Introdução

&ensp;No mundo das startups, poucas atingem o status lendário de unicórnios, empresas avaliadas em mais de um bilhão de dólares. Elas são raras, brilhantes e altamente desejadas pelos investidores.

&ensp;O projeto Unicorn Predictor nasce exatamente dessa ambição: usar inteligência artificial e dados para prever quais startups têm o potencial de alcançar esse patamar de sucesso. O nome reflete não apenas a exclusividade do objetivo, mas também a magia da inovação transformada em ciência de predição.

&ensp;Em um ecossistema onde apenas 1% das startups conseguem atingir uma avaliação de unicórnio, cada decisão de investimento carrega enormes riscos e recompensas. Este projeto representa uma tentativa de trazer metodologia científica para um campo tradicionalmente dominado por intuição e sorte, oferecendo aos investidores uma ferramenta baseada em dados históricos, padrões de crescimento e indicadores de sucesso comprovados.

## Visão Geral

Este projeto desenvolve um **modelo de machine learning** avançado para prever o sucesso de startups através de técnicas sofisticadas de ciência de dados. O modelo utiliza classificação binária para determinar se uma startup terá sucesso (labels = 1) ou não (labels = 0), implementando um pipeline completo que inclui engenharia de features, otimização de hiperparâmetros e tratamento de classes desbalanceadas.

### Objetivo do Projeto

Desenvolver um modelo preditivo capaz de identificar startups com maior probabilidade de sucesso com base em características empresariais, métricas financeiras e indicadores de performance, alcançando alta precisão através de técnicas avançadas de machine learning.

## Público-Alvo

- **Investidores**: Auxiliar em decisões de investimento baseadas em dados objetivos
- **Aceleradoras**: Priorizar startups em processos de seleção e due diligence
- **Venture Capital**: Otimizar estratégias de investimento e análise de risco
- **Empreendedores**: Compreender fatores críticos de sucesso para benchmarking

## Estrutura do Projeto

```
modelo-preditivo-startups/
├── startup_success_model.ipynb     # Notebook completo com análise e modelagem
├── train.csv                       # Dados de treinamento (646 samples)
├── test.csv                        # Dados de teste (277 samples)
├── sample_submission.csv           # Formato de submissão
├── submission.csv                  # Predições do modelo base
├── submission_optimized.csv        # Predições do pipeline otimizado
├── submission_ultra_precision.csv  # Predições do modelo ultra-preciso
├── assets/                         # Recursos visuais
│   └── unicorn-predictor-logo.png
└── README.md                       # Documentação do projeto
```

## Metodologia e Pipeline de Desenvolvimento

### 1. Carregamento e Exploração Inicial dos Dados

#### Estrutura dos Datasets

- **Dataset de Treino**: 646 amostras com 70 features + target
- **Dataset de Teste**: 277 amostras com 70 features
- **Variáveis**: Mix de numéricas, categóricas e binárias

#### Análise de Dados Ausentes

- Identificação de valores faltantes em colunas relacionadas a datas
- Estratégia de preenchimento com zero (ausência indica evento não ocorrido)
- Colunas tratadas: `age_first_funding_year`, `age_last_funding_year`, `age_first_milestone_year`, `age_last_milestone_year`

### 2. Pré-processamento e Transformação

#### Encoding de Variáveis Categóricas

- **OneHotEncoding** para `category_code` (setor de atuação)
- Tratamento adequado de categorias desconhecidas no teste
- Criação de múltiplas variáveis binárias por categoria

#### Engenharia de Features

Criação de 6 novas features derivadas:

- **funding_per_round**: Eficiência financeira por rodada
- **log_funding_total**: Normalização de distribuição assimétrica
- **log_relationships**: Transformação logarítmica de conexões
- **has_funding**: Indicador binário de presença de financiamento
- **has_milestone**: Indicador binário de marcos alcançados
- **milestone_ratio**: Eficiência na conquista de marcos ao longo do tempo

### 3. Análise Exploratória de Dados

#### Distribuição da Variável Target

- **Taxa de sucesso geral**: Análise do balanceamento entre classes
- **Visualizações**: Gráficos de barras e distribuições por resultado
- **Impacto no modelo**: Identificação de possível desbalanceamento

#### Análise de Correlação

- **Matriz de correlação** com foco na variável target
- **Identificação das variáveis mais correlacionadas** com sucesso
- **Mapa de calor** para visualização de relações lineares
- **Ranking de importância** baseado em correlação

#### Validação de Hipóteses de Negócio

Teste estatístico de 3 hipóteses fundamentais:

**Hipótese 1: Financiamento e Sucesso**

- Startups com mais rodadas de financiamento têm maior probabilidade de sucesso
- **Status**: CONFIRMADA através de análise comparativa

**Hipótese 2: Marcos e Performance**

- Empresas com maior número de marcos demonstram tendência superior ao sucesso
- **Status**: CONFIRMADA através de análise estatística

**Hipótese 3: Vantagem Geográfica da Califórnia**

- Localização na Califórnia representa vantagem competitiva
- **Status**: CONFIRMADA - taxa de sucesso superior aos outros estados

### 4. Seleção e Curadoria de Features

#### Critérios de Seleção

- Análise de correlação com variável target
- Validação através das hipóteses de negócio confirmadas
- Importância prática para o domínio de startups

#### Features Selecionadas

7 variáveis principais escolhidas:

- `funding_rounds` (confirmada pela Hipótese 1)
- `milestones` (confirmada pela Hipótese 2)
- `is_CA` (confirmada pela Hipótese 3)
- `funding_total_usd` (alta correlação)
- `relationships` (rede de conexões)
- `avg_participants` (envolvimento em eventos)
- `has_milestone` (feature engineered)

### 5. Desenvolvimento do Modelo Preditivo

#### Comparação de Algoritmos

Avaliação de 5 algoritmos através de validação cruzada estratificada:

1. **Logistic Regression**: Modelo linear interpretável com class balancing
2. **Decision Tree**: Modelo de árvore para captura de padrões não-lineares
3. **Random Forest**: Ensemble robusto com múltiplas árvores
4. **Gradient Boosting**: Algoritmo de boosting sequencial (VENCEDOR)
5. **KNN**: Algoritmo baseado em vizinhos próximos

#### Modelo Selecionado: Gradient Boosting Classifier

- **Melhor performance** na comparação inicial
- **Capacidade de capturar interações complexas** entre variáveis
- **Robustez a outliers** e overfitting

#### Treinamento e Avaliação Inicial

- Divisão estratificada: 80% treino, 20% validação
- **Acurácia base**: 77.69%
- Métricas detalhadas: Precisão, Recall, F1-Score, AUC-ROC

### 6. Otimização de Hiperparâmetros

#### Grid Search para Otimização Automática

- **Parâmetros otimizados**: `n_estimators`, `learning_rate`, `max_depth`, `subsample`
- **Método**: GridSearchCV com validação cruzada 5-fold
- **Métrica de otimização**: Accuracy
- **Total de combinações testadas**: 54

#### Resultados da Otimização

- **Melhores parâmetros**: `learning_rate=0.1`, `max_depth=3`, `n_estimators=100`, `subsample=0.8`
- **Melhor acurácia CV**: 79.87%
- **Melhoria**: +2.18 pontos percentuais sobre o modelo base

### 7. Pipeline Avançado de Otimização

#### Estratégias Avançadas Implementadas

1. **Features de Interação Polinomiais**

   - Criação de 6 novas features através de interações entre variáveis importantes
   - Foco nas 4 variáveis mais correlacionadas: `funding_rounds`, `milestones`, `relationships`, `funding_total_usd`

2. **Seleção Automática com RFECV**

   - Seleção de 41 features de 76 disponíveis
   - Critério: ROC-AUC com validação cruzada
   - Eliminação recursiva para identificar subset ótimo

3. **Tratamento de Classes Desbalanceadas**

   - Sample weights balanceados aplicados
   - Classe 0 (fracasso): peso 1.42
   - Classe 1 (sucesso): peso 0.77

4. **Grid Search Expandido Focado em Precisão**
   - 324 combinações testadas com métrica de precisão
   - Hiperparâmetros expandidos: `min_samples_leaf`, `subsample` refinado

#### Modelo Ultra-Preciso

Pipeline especializado para **maximizar precisão**:

- **Técnica**: Threshold optimization (0.865)
- **Objetivo**: Minimizar falsos positivos para investidores conservadores
- **Resultado**: 83.95% de precisão (máxima alcançada)

### 8. Análise de Importância das Features

#### Features Mais Importantes (Pipeline Avançado)

1. **age_last_milestone_year** (24.54%) - Tempo desde último marco
2. **relationships × funding_total_usd** (12.00%) - Interação rede-capital
3. **age_first_funding_year** (8.23%) - Maturidade no primeiro investimento
4. **milestones × funding_total_usd** (7.97%) - Interação marcos-capital
5. **milestones × relationships** (4.81%) - Interação marcos-rede

#### Validação da Engenharia de Features

- **Features de interação** aparecem entre as mais importantes
- **Confirma estratégia** de criação de variáveis derivadas
- **Justifica complexidade** do pipeline avançado

## Visualizações e Análises Geradas

### 1. Análise Exploratória

- **Distribuição da variável target**: Gráficos de barras com análise de balanceamento
- **Estatísticas descritivas**: Tabelas resumo das variáveis numéricas
- **Matriz de correlação**: Heatmap focado na correlação com target

### 2. Validação de Hipóteses

- **Boxplots comparativos**: Funding rounds, marcos e localização por classe
- **Análises estatísticas**: Médias, diferenças e confirmação de hipóteses
- **Gráficos de barras**: Taxa de sucesso por categoria

### 3. Seleção de Features

- **Matriz de correlação das features selecionadas**: Heatmap detalhado
- **Ranking de correlações**: Lista ordenada por importância

### 4. Performance dos Modelos

- **Comparação de algoritmos**: Accuracy ± desvio padrão
- **Métricas detalhadas**: Precisão, Recall, F1-Score, AUC-ROC
- **Matriz de confusão**: Análise visual dos tipos de erro

### 5. Pipeline Avançado

- **Evolução da performance**: Gráficos comparativos entre modelos
- **Curva ROC**: Capacidade discriminativa do modelo otimizado
- **Distribuição de probabilidades**: Histogramas por classe
- **Importância das features**: Top 15 variáveis mais relevantes
- **Curva Precision-Recall**: Análise do trade-off

### 6. Análise Final

- **Threshold optimization**: Gráficos de otimização do ponto de corte
- **Comparação de modelos**: Evolução básico → avançado → ultra-preciso
- **Predições finais**: Distribuição dos resultados no conjunto de teste

## Resultados Finais Alcançados

### Performance dos Modelos Desenvolvidos

#### 1. Modelo Base (Gradient Boosting)

- **Acurácia**: 77.69%
- **Objetivo**: Estabelecer baseline sólido
- **Arquivo**: `submission.csv`

#### 2. Pipeline Otimizado

- **Acurácia**: 80.00%
- **Precisão**: 80.68%
- **AUC-ROC**: 83.05%
- **Melhoria**: +2.31 pontos percentuais
- **Arquivo**: `submission_optimized.csv`

#### 3. Modelo Ultra-Preciso

- **Precisão**: 83.95% (MÁXIMA ALCANÇADA)
- **Acurácia**: 77.69%
- **F1-Score**: 82.42%
- **AUC-ROC**: 83.46%
- **Threshold otimizado**: 0.865
- **Arquivo**: `submission_ultra_precision.csv`

### Evolução da Performance

| Modelo        | Acurácia | Precisão   | Técnicas Aplicadas                            |
| ------------- | -------- | ---------- | --------------------------------------------- |
| Básico        | 77.69%   | 79.00%     | Grid Search padrão                            |
| Avançado      | 80.00%   | 80.68%     | Features polinomiais + RFECV + Sample weights |
| Ultra-Preciso | 77.69%   | **83.95%** | Threshold optimization + Calibração           |

### Insights de Negócio Obtidos

#### Fatores Críticos de Sucesso Identificados

1. **Tempo de Maturação**: `age_last_milestone_year` é o fator mais importante (24.54%)
2. **Sinergia Capital-Rede**: Interação entre `relationships` e `funding_total_usd` (12.00%)
3. **Maturidade no Investimento**: `age_first_funding_year` influencia significativamente (8.23%)
4. **Eficiência em Marcos**: Interação entre `milestones` e capital/rede é crucial
5. **Vantagem Geográfica**: Califórnia confirma vantagem estatisticamente significativa

#### Hipóteses Validadas

- ✅ **Financiamento**: Mais rodadas = maior probabilidade de sucesso
- ✅ **Marcos**: Mais milestones = melhor performance
- ✅ **Localização**: Califórnia tem vantagem competitiva real

#### Recomendações Estratégicas

**Para Investidores:**

- Usar **modelo ultra-preciso** para minimizar falsos positivos
- Focar em startups com **interações sinérgicas** (capital + rede + marcos)
- Considerar **timing de maturação** antes do investimento

**Para Startups:**

- Investir em **construção de rede de relacionamentos**
- Estabelecer **marcos mensuráveis** e comunicá-los
- Considerar **localização estratégica** em ecossistemas maduros

**Para Aceleradoras:**

- Usar **pipeline otimizado** para seleção balanceada
- Focar desenvolvimento em **áreas de alta importância**
- Implementar **métricas de acompanhamento** baseadas no modelo

## Tecnologias e Bibliotecas Utilizadas

### Core Technologies

- **Python 3.13**: Linguagem principal
- **Jupyter Notebook**: Ambiente de desenvolvimento interativo

### Manipulação e Análise de Dados

- **Pandas**: Manipulação de DataFrames e análise exploratória
- **NumPy**: Operações numéricas e arrays multidimensionais

### Machine Learning

- **Scikit-learn**: Framework principal para ML
  - `GradientBoostingClassifier`: Algoritmo principal
  - `OneHotEncoder`: Encoding de variáveis categóricas
  - `PolynomialFeatures`: Criação de features de interação
  - `RFECV`: Seleção automática de features
  - `GridSearchCV`: Otimização de hiperparâmetros
  - `train_test_split`: Divisão de dados
  - Métricas: `accuracy_score`, `precision_score`, `roc_auc_score`, etc.

### Visualização

- **Matplotlib**: Gráficos básicos e personalização avançada
- **Seaborn**: Visualizações estatísticas e heatmaps elegantes

### Tratamento de Dados

- **Warnings**: Supressão de avisos para limpeza de output
- **Class balancing**: Sample weights para tratamento de desbalanceamento

## Como Executar o Projeto

### 1. Pré-requisitos

```bash
# Instalar dependências principais
pip install pandas numpy scikit-learn matplotlib seaborn

# Ou usar o arquivo requirements (se disponível)
pip install -r requirements.txt
```

### 2. Estrutura de Execução

```bash
# Clonar o repositório
git clone https://github.com/guedesrayssa/modelo-preditivo-startups.git
cd modelo-preditivo-startups

# Iniciar Jupyter Notebook
jupyter notebook startup_success_model.ipynb
```

### 3. Arquivos de Entrada Necessários

- ✅ `train.csv`: Dataset de treinamento (646 amostras)
- ✅ `test.csv`: Dataset de teste (277 amostras)
- ✅ `sample_submission.csv`: Formato esperado de submissão

### 4. Arquivos de Saída Gerados

- 📄 `submission.csv`: Predições do modelo base
- 📄 `submission_optimized.csv`: Predições do pipeline otimizado
- 📄 `submission_ultra_precision.csv`: Predições do modelo ultra-preciso

### 5. Execução Sequencial Recomendada

1. **Seções 1-3**: Carregamento, pré-processamento e EDA
2. **Seções 4-6**: Seleção de features e modelagem básica
3. **Seção 7**: Otimização de hiperparâmetros
4. **Seções 8-9**: Pipeline avançado (opcional, para máxima performance)
5. **Seção 10**: Análise final e conclusões

### 6. Tempo Estimado de Execução

- **Execução completa**: ~15-20 minutos
- **Pipeline básico (até seção 7)**: ~5-8 minutos
- **Pipeline avançado (seções 8-9)**: ~10-12 minutos adicionais

## Limitações e Considerações Importantes

### Limitações do Modelo

#### Limitações dos Dados

- **Snapshot temporal**: Dados representam um momento específico, não evolução temporal
- **Viés de sobrevivência**: Apenas startups que chegaram a certo estágio estão representadas
- **Missing features**: Fatores importantes como qualidade da equipe, timing de mercado não estão capturados
- **Tamanho da amostra**: 646 amostras podem limitar generalização para nichos específicos

#### Limitações Metodológicas

- **Correlação vs Causalidade**: Modelo identifica padrões, não necessariamente causas
- **Estabilidade temporal**: Padrões podem mudar com evolução do ecossistema de startups
- **Threshold sensitivity**: Performance varia significativamente com ponto de corte escolhido
- **Feature interactions**: Interações complexas podem não estar totalmente capturadas

### Considerações de Uso Prático

#### Para Investidores

- **Ferramenta de apoio**: Usar para screening inicial, não decisão final
- **Combine com due diligence**: Análise humana permanece essencial
- **Monitore false positives**: Especialmente importante em modelo ultra-preciso
- **Considere contexto macro**: Condições econômicas afetam todas as startups

#### Para Desenvolvedores

- **Retreinamento regular**: Novos dados podem mudar padrões importantes
- **Validação contínua**: Monitor drift de performance em produção
- **A/B testing**: Comparar predições com resultados reais
- **Feature engineering**: Explorar novas variáveis conforme disponibilidade

## Próximos Passos e Roadmap

### Melhorias Técnicas Imediatas

#### Modelos Avançados

1. **XGBoost/LightGBM**: Testar algoritmos de gradient boosting mais modernos
2. **Neural Networks**: Implementar redes neurais para capturar padrões complexos
3. **Ensemble Stacking**: Combinar múltiplos modelos via meta-learning
4. **AutoML**: Usar ferramentas como AutoSklearn para otimização automática

#### Feature Engineering Avançada

1. **Séries temporais**: Incluir padrões de crescimento ao longo do tempo
2. **Network features**: Analisar grafo de relacionamentos entre startups/investidores
3. **NLP features**: Extrair informações de descrições textuais das startups
4. **Market features**: Incluir dados de concorrência e tamanho de mercado

### Expansão de Dados

#### Fontes Externas

1. **Dados econômicos**: PIB, taxa de juros, índices de mercado
2. **Dados setoriais**: Crescimento por indústria, regulamentações
3. **Dados geográficos**: Detalhamento de ecossistemas regionais
4. **Social media**: Sentiment analysis de menções às startups

#### Enriquecimento Temporal

1. **Tracking longitudinal**: Acompanhar startups ao longo do tempo
2. **Early indicators**: Identificar sinais precoces de sucesso/fracasso
3. **Milestone progression**: Modelar sequência temporal de marcos
4. **Funding patterns**: Analisar padrões de investimento ao longo do tempo

### Implementação em Produção

#### Infraestrutura

1. **API REST**: Endpoint para predições em tempo real
2. **Dashboard interativo**: Interface web para análise e visualização
3. **Data pipeline**: ETL automatizado para novos dados
4. **Model monitoring**: Alertas para drift e degradação de performance

#### Integração

1. **CRM integration**: Conectar com ferramentas de investidores
2. **Batch processing**: Processamento de lotes de startups
3. **Real-time scoring**: Avaliação instantânea de novas oportunidades
4. **Reporting automation**: Relatórios automáticos de performance

### Pesquisa e Desenvolvimento

#### Explainabilidade

1. **SHAP values**: Explicações individuais por predição
2. **LIME integration**: Explicações locais interpretáveis
3. **Feature attribution**: Contribuição de cada variável por caso
4. **Bias detection**: Identificação de vieses sistemáticos

#### Validação Avançada

1. **Time series split**: Validação respeitando ordem temporal
2. **Stratified sampling**: Validação por segmentos específicos
3. **Adversarial testing**: Teste de robustez contra ruído
4. **Fairness metrics**: Avaliação de equidade entre diferentes grupos

## Conclusões e Resultados Finais

### Principais Conquistas

1. **Modelo Base Sólido**: Gradient Boosting com 77.69% de acurácia
2. **Pipeline Otimizado**: Melhoria para 80.00% através de técnicas avançadas
3. **Modelo Ultra-Preciso**: 83.95% de precisão para uso conservador
4. **Validação Científica**: Confirmação de 3 hipóteses de negócio importantes
5. **Engenharia de Features**: 6 novas variáveis derivadas com impacto comprovado

### Impacto Prático

O modelo desenvolvido oferece uma **ferramenta baseada em dados** para o ecossistema de startups, permitindo:

- **Decisões mais informadas** por parte de investidores
- **Identificação objetiva** de fatores críticos de sucesso
- **Redução de riscos** através de screening quantitativo
- **Benchmarking** para startups em desenvolvimento

### Aplicação Recomendada

- **Investidores conservadores**: Usar modelo ultra-preciso (83.95% precisão)
- **Análise balanceada**: Usar pipeline otimizado (80.00% acurácia)
- **Screening inicial**: Usar modelo base para análise rápida
- **Pesquisa acadêmica**: Framework completo para estudos futuros

---

<div align="center">
    <p><strong>Modelo Preditivo de Startups</strong></p>
    <p>Transformando dados em insights para o ecossistema de inovação</p>
    <p>Desenvolvido por <strong>Rayssa Guedes</strong></p>
</div>
