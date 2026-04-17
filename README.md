Detecção de Fraude em Cartões de Crédito: Otimização de F1-Score
Descrição do Projeto
Este repositório contém um pipeline de Machine Learning desenvolvido para a detecção de fraudes em transações de cartão de crédito. O foco central do projeto é a maximização da métrica F1-Score, lidando com o extremo desbalanceamento de classes inerente a bases de dados de fraude. O fluxo de trabalho implementa otimizações específicas de hiperparâmetros, ajuste de limiares de decisão (threshold tuning) e técnicas de sobreamostragem (oversampling).

Otimizações Implementadas
Otimização de Hiperparâmetros: Ajuste de regularização (C=0.1) e tolerância para o modelo LinearSVC, com max_iter=5000 para garantir convergência.

Correção e Aplicação de SMOTE: Implementação da técnica Synthetic Minority Over-sampling Technique (SMOTE) para tratamento do desbalanceamento de classes, com correção de parâmetros obsoletos (remoção de n_jobs).

Threshold Tuning: Algoritmo adaptado para buscar o limiar de decisão ótimo que maximiza o F1-Score, utilizando precision_recall_curve.

Eficiência de Memória: Otimização na ingestão dos dados (creditcard.csv), forçando a tipagem das variáveis independentes (V1-V28, Time, Amount) para float32 e a variável alvo (Class) para int8.

Balanceamento de Pesos: Utilização do parâmetro class_weight='balanced' nativo dos modelos para penalização proporcional de erros na classe minoritária.

Arquitetura do Pipeline
O fluxo de execução é dividido em quatro etapas progressivas para isolar e avaliar o ganho de performance de cada técnica:

Etapa 1: Baseline com Dados Brutos - Treinamento e avaliação inicial dos modelos com configurações focadas em F1-Score, sem transformações nos dados.

Etapa 2: Normalização - Aplicação de StandardScaler para padronização das escalas das variáveis independentes, visando melhoria em modelos sensíveis à distância (como SVM).

Etapa 3: Redução de Dimensionalidade (PCA) - Aplicação de Análise de Componentes Principais (PCA) retendo 95% da variância explicada para ganho de eficiência computacional.

Etapa 4: Balanceamento com SMOTE - Geração de amostras sintéticas da classe minoritária (fraude) sobre os dados reduzidos por PCA, objetivando a elevação primária da métrica de Recall sem degradação severa da Precision.

Modelos Avaliados
Regressão Logística (LogisticRegression)

Support Vector Machine (LinearSVC)

Árvore de Decisão (DecisionTreeClassifier)

Naive Bayes (GaussianNB)

Requisitos do Sistema e Dependências
O código foi desenvolvido em Python 3. As bibliotecas primárias requeridas incluem:

pandas

numpy

scikit-learn

imbalanced-learn

matplotlib

seaborn

tqdm

Instruções de Execução
O dataset original não está incluído no código fonte devido ao seu tamanho. É necessário realizar o download do arquivo creditcard.csv no repositório do Kaggle.

O arquivo .csv deve ser posicionado no mesmo diretório de execução do notebook.

A execução das células gerará os relatórios de classificação, métricas isoladas por etapa e as visualizações comparativas finais.
