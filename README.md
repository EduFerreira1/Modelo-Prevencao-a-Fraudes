# Modelo de Prevenção a Fraudes em Cartões de Crédito com Machine Learning

<p align="center">
  <img src="/Images/fraud-case.png" width="500"/>
</p>

## Descrição do Projeto

Este projeto tem como objetivo construir, avaliar e comparar modelos de machine learning para **detecção automática de fraudes em transações de cartões de crédito em terminais físicos**. O foco é apoiar instituições financeiras na identificação rápida e precisa de operações fraudulentas, reduzindo perdas financeiras e minimizando impactos negativos para clientes e reputação das empresas.

## Motivação

O aumento no volume de transações eletrônicas em pontos de venda físicos elevou também a incidência de fraudes, como transações não autorizadas, uso indevido de dados de terceiros e ataques a terminais comprometidos. A prevenção eficiente desse tipo de fraude é crucial para garantir a confiança dos consumidores e evitar prejuízos significativos ao negócio.

## Estrutura do Projeto

<p align="center">
  <img src="/Images/crisp-dm.png" width="500"/>
</p>

O projeto segue as melhores práticas do framework **CRISP-DM**, com as seguintes etapas:

1. **Entendimento do Negócio**
   - Mapeamento dos desafios das fraudes em cartão (modalidades, impactos, necessidades do negócio).
   - Definição do problema, critérios de sucesso e stakeholders.

2. **Entendimento dos Dados**
   - Análise exploratória (EDA) dos dados transacionais: variáveis de cliente, terminal, valor, tempo, localização, etc.
   - Estudo das principais fontes e periodicidade das bases.
   - Testes de sanidade e análise de variáveis alvo (fraude vs. não fraude).

3. **Preparação dos Dados**
   - Ajuste de tipos, joins entre diferentes bases (cliente, terminal, transação).
   - Padronização de variáveis, criação de novas features (ex: médias e desvios por cliente ou terminal, contagem de transações por período, localização).
   - Tratamento de desbalanceamento: análise de técnicas como SMOTE, oversampling, target artificial.
   - Divisão em treino e teste, sempre respeitando o corte temporal (out-of-time split) para evitar vazamentos.

4. **Modelagem**
   - Treinamento de modelos de classificação como **Random Forest** e **XGBoost**, comparando com o modelo vigente.
   - Otimização de hiperparâmetros (grid/random search).
   - Avaliação por métricas técnicas e de negócio (ver abaixo).

5. **Avaliação**
   - Métricas técnicas: **Acurácia**, **ROC-AUC**, **Precision**, **Recall**, **F1-Score**, **KS**, **Gini**.
   - Avaliação do impacto operacional: taxas de aprovação, taxas de fraude, fraudes evitadas, transações impactadas (falsos positivos).
   - Simulação de cenários de política de aprovação, quantificando o trade-off entre reduzir fraude e impactar clientes legítimos.

6. **Implantação**
   - Orientação sobre como implementar o modelo em ambiente produtivo.
   - Recomendações para monitoramento contínuo, atualização de variáveis, revisão de políticas e acompanhamento das métricas de fraude e aprovação.

## Principais Desafios

- **Evento raro:** Proporção de transações fraudulentas extremamente baixa, exigindo cuidado extra em avaliação e balanceamento dos dados.
- **Falso positivo:** Impacto direto na experiência do cliente, exigindo simulação e análise de políticas para não rejeitar excessivamente transações legítimas.
- **Tempo de resposta:** Necessidade de decisão quase em tempo real.
- **Evolução dos golpes:** Novas modalidades surgem frequentemente, exigindo atualização contínua dos modelos e features.
- **Múltiplas fontes e tipos de dados:** Integração de informações comportamentais, de device, biometria, localização, entre outros.

## Principais Técnicas e Algoritmos Utilizados

- **Modelos:** Random Forest, XGBoost, (baseline: modelo vigente da empresa).
- **Técnicas de Data Prep:** Feature engineering, normalização, encoding de categóricas, criação de variáveis agregadas.
- **Tratamento de desbalanceamento:** Análise de uso de técnicas como SMOTE e target artificial.
- **Métricas:** KS, AUC-ROC, Precision, Recall, F1-Score, custo operacional (fraudes evitadas x transações impactadas).
- **Validação:** Out-of-time split para garantir robustez na generalização.

## Resultados

O desempenho dos modelos foi avaliado em diferentes cenários de política de aprovação. Destacam-se os seguintes resultados:

<p align="center">
  <img src="Images/results.png" alt="Resultados comparativos dos modelos" width="600">
</p>

#### Cenário 1 - Taxa de aprovação 99,50%  
- **Fraudes evitadas:**  
  - Random Forest: 89  
  - XGBoost: 91  
- **Transações impactadas (falsos positivos):**  
  - Random Forest: 200  
  - XGBoost: 198  

#### Cenário 2 - Taxa de aprovação 98,99%  
- **Fraudes evitadas:**  
  - Random Forest: 157  
  - XGBoost: 125  
- **Transações impactadas:**  
  - Random Forest: 429  
  - XGBoost: 429  

> Os modelos Random Forest e XGBoost superaram o modelo vigente em capacidade de evitar fraudes, mantendo uma taxa de aprovação próxima do desejado. O ajuste da política permite balancear o risco de fraude evitada com o impacto no cliente (transações legítimas bloqueadas).

## Discussão

- **Eficácia:** O uso de algoritmos de machine learning proporcionou ganhos claros em detecção de fraude, com redução da taxa de fraude e aumento do número de fraudes evitadas.
- **Trade-off negócio:** Existe uma relação direta entre aumentar a barreira contra fraudes e impactar clientes legítimos. O projeto quantifica esse trade-off, permitindo tomada de decisão orientada a dados.
- **Importância de métricas de negócio:** Métricas como fraudes evitadas e transações impactadas são tão importantes quanto as métricas técnicas (KS, ROC-AUC), pois conectam o resultado do modelo ao objetivo real da empresa.
- **Recomendações:**  
  - Monitoramento contínuo do modelo e das variáveis.
  - Atualização constante para novas modalidades de fraude.
  - Adoção de estratégias de segmentação e enriquecimento de dados (biometria, comportamento, device, etc).

## Próximos Passos

- Implantar o modelo em ambiente produtivo, com pipeline automatizado.
- Explorar integração de dados biométricos, comportamentais e de device.
- Implementar dashboards de monitoramento (fraudes evitadas, falsos positivos, taxas de aprovação).
- Realizar A/B tests para validar o ganho operacional frente ao modelo vigente.

## Contato

Para dúvidas, sugestões ou colaboração, entre em contato:
- [LinkedIn](https://www.linkedin.com/in/eduferreiraa)
- Email: contatoedu.fsg@gmail.com

---

> Este projeto segue as melhores práticas de ciência de dados aplicadas ao contexto real do varejo, sempre alinhando soluções técnicas com o impacto financeiro e estratégico para o negócio.

