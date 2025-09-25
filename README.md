# Modelo Preditivo para Sucesso de Startups

## Visão Geral

Este projeto desenvolve um modelo de machine learning para prever o sucesso de startups usando dados de financiamento, categoria de negócio, localização geográfica e marcos importantes. O modelo utiliza classificação binária para determinar se uma startup terá sucesso (labels = 1) ou não (labels = 0).

## Público-Alvo

- **Investidores**: Para auxiliar em decisões de investimento
- **Aceleradoras**: Para priorizar startups em processos de due diligence
- **Empreendedores**: Para entender fatores críticos de sucesso

## Estrutura do Projeto

```
modelo-preditivo-startups/
├── startup_success_model.ipynb    # Notebook principal com análise completa
├── train.csv                      # Dados de treinamento
├── test.csv                       # Dados de teste
├── sample_submission.csv          # Formato de submissão
├── submission.csv                 # Predições finais (gerado)
└── README.md                      # Documentação
```

## Metodologia

### 1. Análise Exploratória de Dados (EDA)

#### Distribuição da Variável Alvo

- Análise do balanceamento entre startups de sucesso e fracasso
- Identificação de possível desbalanceamento de classes
- Gráficos de barras e pizza para visualização da distribuição

#### Variáveis Numéricas

- **Funding Total USD**: Volume total de financiamento recebido
- **Relationships**: Número de relacionamentos da startup
- **Funding Rounds**: Quantidade de rounds de investimento
- **Milestones**: Marcos importantes alcançados
- **Age First/Last Funding**: Idade da empresa no primeiro/último financiamento

#### Variáveis Categóricas

- **Category Code**: Setor de atuação da startup
- **Localização**: Estados (CA, NY, MA, TX, outros)
- **Tipo de Investimento**: VC, Angel, Rounds A-D
- **Flags de Categoria**: Software, Web, Mobile, Enterprise, etc.

### 2. Análise de Correlação

**Matriz de Correlação**: Identificação de relações entre variáveis numéricas e a variável alvo, destacando:

- Variáveis com correlação positiva ao sucesso
- Variáveis com correlação negativa
- Multicolinearidade entre features

**Correlação com Sucesso**: Ranking das variáveis mais correlacionadas com o sucesso das startups.

### 3. Insights por Categoria

**Taxa de Sucesso por Setor**: Análise detalhada mostrando:

- Setores com maior taxa de sucesso
- Frequência de startups por categoria
- Identificação de nichos promissores

### 4. Pré-processamento

#### Tratamento de Valores Ausentes

- **Variáveis Numéricas**: Imputação pela mediana (robusta a outliers)
- **Variáveis Categóricas**: Imputação pela moda

#### Codificação e Normalização

- **One-Hot Encoding**: Para variáveis categóricas
- **StandardScaler**: Normalização de variáveis numéricas
- **Pipeline Unificado**: Garantia de reprodutibilidade

#### Tratamento de Desbalanceamento

- Uso de `class_weight='balanced'` nos modelos
- Foco em métricas apropriadas (Recall, F1-Score, ROC AUC)

### 5. Modelagem

#### Modelos Testados

1. **Regressão Logística**

   - Modelo linear interpretável
   - Baseline para comparação

2. **Random Forest**
   - Modelo ensemble robusto
   - Capacidade de capturar interações não-lineares

#### Otimização de Hiperparâmetros

- **RandomizedSearchCV**: Busca eficiente no espaço de hiperparâmetros
- **Validação Cruzada Estratificada**: 5-fold para avaliação robusta
- **Métrica de Otimização**: ROC AUC

#### Comparação de Modelos

Visualização comparativa entre modelo baseline e otimizado:

- Acurácia
- Precisão
- Recall
- F1-Score
- ROC AUC

### 6. Avaliação Final

#### Métricas de Desempenho

- **Acurácia**: Porcentagem de predições corretas
- **Precisão**: Proporção de verdadeiros positivos entre predições positivas
- **Recall (Sensibilidade)**: Proporção de sucessos corretamente identificados
- **F1-Score**: Média harmônica entre precisão e recall
- **ROC AUC**: Capacidade discriminativa do modelo

#### Matriz de Confusão

Análise detalhada dos tipos de erro:

- **Verdadeiros Negativos (TN)**: Fracassos corretamente identificados
- **Falsos Positivos (FP)**: Fracassos classificados como sucesso
- **Falsos Negativos (FN)**: Sucessos classificados como fracasso
- **Verdadeiros Positivos (TP)**: Sucessos corretamente identificados

#### Curva ROC

Visualização da capacidade discriminativa do modelo:

- Área sob a curva (AUC) como métrica de qualidade
- Identificação do threshold ótimo
- Comparação com classificador aleatório
- Interpretação dos resultados

#### Análise de Thresholds

Comparação de performance com diferentes pontos de corte:

- Threshold 0.3: Maior recall (identificar mais sucessos)
- Threshold 0.5: Balanceamento padrão
- Threshold 0.7: Maior precisão (mais conservador)

### 7. Importância das Features

#### Ranking de Importância

Identificação das variáveis mais relevantes para a predição:

- Features numéricas vs categóricas
- Top 15 variáveis mais importantes
- Interpretação dos resultados

## Principais Gráficos Gerados

### 1. Distribuição da Variável Alvo

- **Gráfico de Barras**: Contagem de sucessos vs fracassos
- **Gráfico de Pizza**: Proporção percentual
- **Análise de Balanceamento**: Classificação como balanceado/desbalanceado

### 2. Distribuições por Classe

- **Histogramas Sobrepostos**: Comparação de distribuições entre sucessos e fracassos
- **Estatísticas Descritivas**: Média, mediana e desvio padrão por classe

### 3. Matriz de Correlação

- **Heatmap**: Correlações entre todas as variáveis numéricas
- **Gráfico de Barras**: Correlações específicas com a variável alvo

### 4. Análise Categórica

- **Taxa de Sucesso por Categoria**: Gráfico horizontal ordenado
- **Frequência por Categoria**: Volume de startups por setor
- **Distribuições**: Gráficos de barras para variáveis categóricas principais

### 5. Comparação de Modelos

- **Gráfico de Barras Agrupadas**: Comparação de métricas entre modelos
- **Barras de Erro**: Desvio padrão das métricas em validação cruzada

### 6. Distribuição de Predições

- **Histograma de Probabilidades**: Distribuição das probabilidades preditas
- **Gráfico de Barras**: Contagem de predições finais (sucesso/fracasso)

### 7. Importância das Features

- **Gráfico Horizontal**: Top 15 features mais importantes
- **Valores Quantitativos**: Importância relativa de cada variável

### 8. Matriz de Confusão

- **Heatmap com Anotações**: Valores absolutos e percentuais
- **Análise Visual**: Identificação de padrões de erro

### 9. Curva ROC

- **Curva ROC Completa**: Taxa de verdadeiros vs falsos positivos
- **Ponto Ótimo**: Threshold que maximiza a performance
- **Área Sombreada**: Representação visual do AUC
- **Linha de Referência**: Comparação com classificador aleatório

### 10. Análise de Thresholds

- **Gráficos de Linha**: Performance vs threshold para cada métrica
- **Análise Comparativa**: Visualização do trade-off precisão-recall

## Resultados Obtidos

### Performance do Modelo Final

O modelo Random Forest otimizado apresentou:

- **ROC AUC**: [Valor específico será exibido na execução]
- **F1-Score**: [Valor específico será exibido na execução]
- **Recall**: [Valor específico será exibido na execução]
- **Precisão**: [Valor específico será exibido na execução]

### Insights de Negócio

#### Fatores Críticos de Sucesso

1. **Volume de Financiamento**: Startups com maior financiamento têm maior probabilidade de sucesso
2. **Categoria de Negócio**: Alguns setores apresentam taxas de sucesso significativamente maiores
3. **Estágio de Investimento**: Presença de rounds específicos indica maturidade
4. **Rede de Relacionamentos**: Número de relacionamentos correlaciona com sucesso

#### Recomendações para Investidores

1. **Priorização**: Usar o modelo para ranquear oportunidades de investimento
2. **Due Diligence**: Focar em startups com alta probabilidade predita
3. **Diversificação**: Considerar diferentes categorias com base nas taxas de sucesso
4. **Threshold**: Ajustar ponto de corte conforme estratégia de risco

## Tecnologias Utilizadas

- **Python 3.x**
- **Pandas**: Manipulação de dados
- **NumPy**: Operações numéricas
- **Scikit-learn**: Machine learning
- **Matplotlib**: Visualizações estáticas
- **Seaborn**: Visualizações estatísticas

## Como Executar

1. **Instalar Dependências**:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```

2. **Executar Notebook**:

```bash
jupyter notebook startup_success_model.ipynb
```

3. **Arquivos Necessários**:

   - `train.csv`: Dados de treinamento
   - `test.csv`: Dados de teste
   - `sample_submission.csv`: Formato de submissão

4. **Saída**:
   - `submission.csv`: Predições para o conjunto de teste

## Limitações e Considerações

### Limitações do Modelo

- **Dados Históricos**: Baseado em padrões passados que podem não se repetir
- **Fatores Externos**: Não considera mudanças econômicas ou de mercado
- **Qualidade dos Dados**: Dependente da completude e precisão dos dados de entrada

### Recomendações de Uso

- **Recalibração Periódica**: Retreinar com novos dados regularmente
- **Combinação com Expertise**: Usar como ferramenta de apoio, não substituição
- **Monitoramento**: Acompanhar performance em produção

## Próximos Passos

### Melhorias Técnicas

1. **Ensemble Methods**: Combinar múltiplos algoritmos
2. **Feature Engineering**: Criar novas variáveis derivadas
3. **Hyperparameter Tuning**: Otimização mais extensiva
4. **Cross-validation**: Técnicas mais robustas de validação

### Melhorias de Dados

1. **Dados Temporais**: Incluir séries temporais de crescimento
2. **Dados Externos**: Incorporar indicadores econômicos
3. **Dados Textuais**: Analisar descrições das startups
4. **Dados de Mercado**: Incluir informações de concorrência

### Implementação

1. **API REST**: Criar serviço para predições em tempo real
2. **Dashboard**: Interface para visualização e análise
3. **Pipeline Automatizado**: Retreinamento automático
4. **Monitoramento**: Alertas para degradação do modelo

---

<div align="center">
    <p>Feito com 🩷 por Rayssa</p>
