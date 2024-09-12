# Previsão de Churn em Clientes de Telecom

## Introdução
<p>O churn (cancelamento de serviço) é um dos maiores desafios para empresas de telecomunicações. A capacidade de prever quais clientes têm maior probabilidade de cancelar seus serviços pode ajudar a direcionar estratégias de retenção e personalizar intervenções preventivas.

Neste projeto, utilizamos dados de uma empresa de telecomunicações fictícia para prever o churn de clientes. O objetivo é criar um modelo de machine learning eficaz para prever quais clientes provavelmente cancelarão seus serviços no futuro, permitindo ações estratégicas de retenção.</p>

## Dataset
O dataset utilizado é um conjunto de dados do Kaggle (https://www.kaggle.com/code/psugunnasil/961701-workshop-on-telco-dataset)

## Atributos do Dataset

Churn: Indica se o cliente cancelou o serviço.
Demográficos: Gênero, idade, parceiros, dependentes.
Serviços Assinados: Internet, múltiplas linhas, segurança online, backup online, proteção de dispositivo, suporte técnico, streaming de TV/filmes
Informações da Conta: Duração de contrato, forma de pagamento, cobrança sem papel, taxas mensais e totais.

## Objetivo
Criar um modelo preditivo de churn usando Random Forest. Avaliar a performance do modelo e compará-lo com outras técnicas de machine learning, como XGBoost e LightGBM, para selecionar o melhor modelo baseado em métricas como Acurácia, F1-score, Recall e AUC-ROC.

## Análise Exploratória dos Dados (EDA)
Durante a análise exploratória, foram feitas as seguintes observações:

* Distribuição de Churn: O dataset apresenta um leve desbalanceamento, com a maioria dos clientes não cancelando o serviço.
* Correlação entre variáveis: Variáveis como duração de contrato e método de pagamento têm alta correlação com churn.
* Falta de dados: A coluna TotalCharges apresentou valores nulos, que foram tratados preenchendo com a mediana.

## Principais Insights:
Clientes com contratos mensais têm maior probabilidade de churn, em comparação com clientes que possuem contratos de um ou dois anos.
Formas de pagamento eletrônicas (ex.: cheque eletrônico) estão mais associadas ao churn do que métodos automáticos como transferência bancária.

## Pré-processamento dos Dados
### Limpeza e Tratamento dos Dados

* Conversão de colunas numéricas: A coluna TotalCharges foi convertida para valores numéricos e preenchida com a mediana em valores ausentes.
* Codificação de variáveis categóricas: Aplicamos o One-Hot Encoding para transformar as variáveis categóricas em dados numéricos.
* Divisão de treino e teste: Os dados foram divididos em 80% para treino e 20% para teste.

## 1. Random Forest (Modelo Final)
O Random Forest foi selecionado como o modelo final após a comparação com outros modelos. Ele demonstrou um excelente equilíbrio entre acurácia e AUC-ROC.

* Ajuste de hiperparâmetros: Utilizamos GridSearchCV para ajustar o número de estimadores e a profundidade máxima das árvores.
* Ajuste de pesos de classes: Como o dataset era levemente desbalanceado, aplicamos class_weight='balanced' para dar mais importância à classe minoritária.

## 2. XGBoost
Outro modelo testado foi o XGBoost, que mostrou bons resultados, mas foi superado pelo Random Forest nas métricas de AUC-ROC e F1-score. A inclusão de técnicas de undersampling ajudou, mas o modelo ainda apresentou uma leve perda de precisão em comparação ao Random Forest.

## Comparação de Desempenho
Modelo  | Acurácia	| F1-Score	| AUC-ROC
--------|-----------|-----------|---------
Random Forest (Pesos) |	79.2% |	0.76	| 0.84
XGBoost (Sem Undersampling) |	76.5% |	0.74	| 0.81
XGBoost (Undersampling) |	73.3%	 |0.72	| 0.80


O Random Forest com ajuste de pesos foi o modelo de melhor desempenho, apresentando o maior valor de AUC-ROC e uma alta acurácia e F1-score, o que indica um bom equilíbrio entre a identificação de clientes churn e não churn.

## Importância das Variáveis
O Random Forest também nos permite identificar as variáveis mais importantes no modelo:

* Duração do Contrato: Clientes com contratos mais curtos tendem a cancelar com mais frequência.
* Forma de Pagamento: Métodos eletrônicos, como cheque eletrônico, foram fortemente associados ao churn.
* Custo Mensal: Clientes com cobranças mais altas mensalmente mostraram maior tendência a cancelar.

## Conclusão
O modelo de Random Forest ajustado com pesos foi o mais eficaz para prever o churn de clientes, superando outras abordagens como XGBoost. Este modelo apresentou a melhor combinação de acurácia e AUC-ROC, o que o torna ideal para ser usado em um sistema de previsão de churn em uma empresa de telecomunicações.

## Autor:
Luiz Gustavo <br>
Conecte-se comigo no [Linkedin](https://www.linkedin.com/in/gustavoalmeidas/)
