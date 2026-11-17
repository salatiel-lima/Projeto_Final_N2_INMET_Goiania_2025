# Projeto Final N2 — Big Data e Data Science

## Estimação da temperatura do ar em Goiânia utilizando Machine Learning

### 1. Apresentação do projeto

Este projeto foi desenvolvido para a disciplina de Big Data e Data Science, no curso de graduação em Inteligência Artificial da Faculdade FATESG.

O objetivo é aplicar técnicas de Machine Learning para estimar a temperatura do ar em Goiânia, utilizando dados meteorológicos públicos do Instituto Nacional de Meteorologia (INMET), referentes ao ano de 2025.

Foram implementados dois algoritmos de regressão, Random Forest Regressor e Gradient Boosting Regressor, para comparar seus desempenhos na estimação da temperatura do ar.

### 2. Fonte e descrição dos dados — R1

- **Fonte:** Instituto Nacional de Meteorologia (INMET).
- **Estação:** Goiânia — A002.
- **Período:** 01/01/2025 a 31/12/2025.
- **Frequência:** observações horárias.
- **Formato:** CSV.
- **Registros originais:** 8.760.
- **Colunas originais:** 19.
- **Registros utilizados na modelagem:** 6.058.

Fonte oficial: https://portal.inmet.gov.br/dadoshistoricos

O notebook contém a documentação das 19 colunas originais, incluindo as respectivas descrições e unidades de medida.

### 3. Tratamento e preparação dos dados

Os dados foram importados e analisados com a biblioteca Pandas.

As principais etapas realizadas foram:

1. Importação do arquivo CSV.
2. Exploração da estrutura e dos tipos de dados.
3. Identificação de valores ausentes.
4. Criação das variáveis HORA e MES.
5. Seleção das variáveis para a modelagem.
6. Exclusão dos registros incompletos nas variáveis selecionadas.
7. Separação dos dados em treinamento e teste.

Dos 8.760 registros originais, 2.702 foram excluídos da modelagem devido à presença de valores ausentes nas variáveis selecionadas, permanecendo 6.058 registros completos.

### 4. Variáveis utilizadas

**Variáveis explicativas (X):**

- Hora da observação.
- Mês da observação.
- Umidade relativa do ar (%).
- Temperatura do ponto de orvalho (°C).
- Pressão atmosférica ao nível da estação (mB).
- Velocidade horária do vento (m/s).

**Variável-alvo (y):**

- Temperatura do ar — bulbo seco, horária (°C).

### 5. Modelagem com Machine Learning — R3

Como a temperatura é uma variável numérica contínua, o problema foi tratado como uma tarefa de regressão.

Foram utilizados os algoritmos:

**Random Forest Regressor:** combina as estimativas de múltiplas árvores de decisão para produzir um valor numérico.

**Gradient Boosting Regressor:** constrói árvores sequencialmente, procurando reduzir os erros das estimativas anteriores.

Os modelos foram configurados com 100 estimadores e `random_state=42`.

Os dados foram divididos em 80% para treinamento (4.846 registros) e 20% para teste (1.212 registros).

Foram utilizadas duas estratégias de avaliação:

- Divisão aleatória.
- Divisão cronológica.

### 6. Métricas de avaliação

Foram utilizadas três métricas:

- **MAE:** erro absoluto médio, em graus Celsius.
- **RMSE:** raiz do erro quadrático médio, em graus Celsius.
- **R²:** coeficiente de determinação.

Valores menores de MAE e RMSE indicam melhor desempenho, enquanto valores de R² mais próximos de 1 indicam melhor ajuste em relação à referência baseada na média.

### 7. Resultados dos experimentos

| Algoritmo | Divisão | MAE (°C) | RMSE (°C) | R² |
|---|---|---:|---:|---:|
| Random Forest | Aleatória | 0,2729 | 0,5060 | 0,9889 |
| Gradient Boosting | Aleatória | 0,4783 | 0,6992 | 0,9788 |
| Random Forest | Cronológica | 1,0794 | 2,0747 | 0,8207 |
| Gradient Boosting | Cronológica | 1,2397 | 1,8603 | 0,8559 |

Na divisão aleatória, o Random Forest apresentou melhor desempenho nas três métricas.

Na divisão cronológica, o Random Forest apresentou menor MAE, enquanto o Gradient Boosting obteve menor RMSE e maior R².

A comparação demonstrou que a estratégia de divisão dos dados influencia a avaliação dos modelos.

### 8. Limitações

A temperatura do ponto de orvalho e a umidade relativa apresentam forte relação física com a temperatura do ar, podendo favorecer o desempenho dos modelos.

Além disso, as variáveis explicativas foram registradas no mesmo horário da temperatura-alvo. Portanto, o experimento realiza a estimação contemporânea da temperatura, e não a previsão de temperaturas futuras.

Outra limitação é a exclusão de aproximadamente 30,84% dos registros originais da modelagem, devido à presença de valores ausentes nas variáveis selecionadas.

### 9. Tecnologias utilizadas

- Python
- Google Colab
- Google Drive
- Pandas
- NumPy
- Matplotlib
- Scikit-learn

### 10. Arquivos do repositório

**Projeto_Final_N2_INMET_Goiania_2025.ipynb**

Notebook contendo a documentação, os códigos Python, o tratamento dos dados, os algoritmos de Machine Learning, as métricas, os gráficos e a análise dos resultados.

**INMET_CO_GO_A002_GOIANIA_01-01-2025_A_31-12-2025.csv**

Base de dados meteorológicos da estação Goiânia A002, referente ao ano de 2025.

**README.md**

Arquivo com a documentação geral do projeto, metodologia, resultados e instruções de execução.

### 11. Instruções para execução

1. Baixe o notebook e o CSV deste repositório.
2. Coloque os dois arquivos em uma pasta do seu Google Drive.
3. Abra o notebook no Google Colab.
4. Execute a célula de conexão com o Google Drive.
5. Execute a célula que procura o CSV no Google Drive.
6. Copie o caminho encontrado e atualize a variável `arquivo` na célula de importação.
7. Execute as demais células na sequência apresentada.

O caminho do CSV pode variar conforme a organização das pastas de cada usuário.

### 12. Conclusão

O projeto demonstrou a aplicação prática de técnicas de Machine Learning na análise de dados meteorológicos reais.

Os dois algoritmos apresentaram resultados satisfatórios, com diferenças de desempenho entre as estratégias de divisão aleatória e cronológica.

A comparação permitiu compreender a importância da preparação dos dados, da seleção das variáveis, da escolha dos algoritmos e da metodologia de avaliação para a interpretação dos resultados.

O experimento também evidenciou limitações relacionadas à dependência entre variáveis meteorológicas e à diferença entre estimação contemporânea e previsão futura.
