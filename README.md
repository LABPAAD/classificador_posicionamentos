# Cassificador de Posicionamento
Classificador automático de posicionamentos em comentários de texto sobre operações policiais

O BERT (_Bidirectional Encoder Representations from Transformers_) [Devlin et al. 2019] é um algoritmo de aprendizado profundo (do, inglês _Deep Learning_) desenvolvido pelo _Google_ para processamento de linguagem natural. BERT é um modelo pré-treinado com conteúdo do Wikipédia e o Book Corpus, ambos em língua inglesa, contendo 2.500 milhões e 800 milhões de palavras respectivamente. Um recurso importante do BERT é sua construção com representações contextuais de modelos pré-treinados, baseado na arquitetura de _transformers_.

Através desse recurso, comunidades de pesquisadores ou corporações podem treinar novos modelos adaptados a alguma linguagem no contexto local e distribuí-los como modelos pré-treinados BERT.

Neste trabalho utilizamos dois modelos pré-treinados que são o _Multilingual_ [Devlin et al. 2019] e o _BERTimbau_ [Souza et al. 2020].
O modelo _Multilingual_ é pré-treinado em 102 idiomas, e possui 12 camadas (blocos de _transformers_), 12 cabeçotes de atenção e 110 milhões de parâmetros.
No que lhe concerne, BERTimbau é pré-treinado na língua portuguesa do Brasil, e em nossas avaliações utilizamos a versão desse modelo com a maior quantidade de codificadores (_large_), contendo 24 camadas, 16 cabeçotes de atenção e 335 milhões de parâmetros.
Embora treinado para uma língua específica, BERTimbau já se mostrou eficiente em tarefas de processamento de linguagem natural que requerem reconhecimento de entidade nomeada, semelhança textual de sentença e reconhecimento de enlace textual [Souza et al. 2020].

[Mais detalhes](brasnam_marcos2022.pdf)

# Execução

### Passos para Executar o Treinamento do modelo BERT (RN_BERTimbay.py):

1. **Instalação de Bibliotecas:**
   Certifique-se de ter as bibliotecas necessárias instaladas. Você pode fazer isso executando o seguinte comando no terminal:

   ```bash
   pip install pandas tqdm seaborn matplotlib transformers torch scikit-learn

2. **Importação e Carregamento de Dados:**
O código começa importando bibliotecas necessárias e carregando um conjunto de dados a partir do arquivo 'dataset_atualizado_08022022.csv'. Certifique-se de que este arquivo está presente no mesmo diretório ou forneça o caminho correto. Pode ser encontrado em [Dataset](https://github.com/LABPAAD/dataset_posicionamento2022)

3. **Pré-processamento de Dados:**
Os rótulos na coluna 'rotulacao_manual' são ajustados para garantir que sejam valores 0, 1 e 2 (possivelmente negativo, neutro, positivo).
Duplicatas nos comentários são removidas e os dados são embaralhados.

4. **Tokenização:**
O código usa a biblioteca Transformers para tokenizar os comentários usando o modelo pré-treinado BERTimbau.
Divisão em Conjuntos de Treinamento e Teste:
Os dados são divididos em conjuntos de treinamento e teste usando a função train_test_split do scikit-learn.

6. **Definição do Modelo:**
Um modelo de classificação de sentimentos é definido usando a arquitetura BERTimbau. O modelo possui três classes (negativo, neutro, positivo).

7. **Treinamento do Modelo:**
O modelo é treinado em várias épocas usando o otimizador AdamW e a taxa de aprendizado é ajustada com um escalonador linear.

8. **Avaliação do Modelo:**
O desempenho do modelo é avaliado no conjunto de teste, e métricas como precisão, recall, F1-score e AUC-ROC são calculadas.

9. **Salvamento de Métricas:**
As métricas de desempenho do modelo são salvas em um arquivo CSV chamado 'metricas_rede_neural_BERTimbau_base.csv'.

10. **Conclusão:**
O código conclui exibindo um relatório de classificação e salva as métricas em um arquivo CSV.

11. **Observações:**
Certifique-se de ter espaço suficiente no seu dispositivo para armazenar o modelo treinado e os resultados.
Dependendo do tamanho do conjunto de dados e da complexidade do modelo, o treinamento pode levar algum tempo.
Lembre-se de ajustar caminhos de arquivos ou outras configurações conforme necessário, e execute o script em um ambiente Python com as bibliotecas instaladas.

### Passos para Executar o Treinamento do BERT (RN_Mutilingual.py):

1. **Bibliotecas Necessárias:**

Certifique-se de ter as bibliotecas necessárias instaladas. Utilize o seguinte comando no terminal para instalar:

```bash
pip install pandas tqdm seaborn matplotlib transformers torch scikit-learn
```
2. **Importação de Bibliotecas e Dados:**
Importa as bibliotecas necessárias, incluindo o PyTorch e o Transformers.
Carrega um conjunto de dados a partir do arquivo 'dataset_atualizado_08022022.csv'. Certifique-se de que o arquivo esteja no mesmo diretório ou forneça o caminho correto.

3. **Pré-processamento e Tokenização:**
Ajusta os rótulos e remove duplicatas nos comentários.
Utiliza o tokenizador BERT para preparar os dados para o treinamento.

4. **Divisão em Conjuntos de Treinamento e Teste:**
Divide os dados em conjuntos de treinamento e teste.
5. Definição do Modelo Multilingual:
Define uma arquitetura de rede neural para classificação de sentimentos usando o modelo pré-treinado BERT Multilingual.

6. **Treinamento do Modelo:**
Treina o modelo em várias épocas utilizando o otimizador AdamW e um escalonador linear.

7. **Avaliação do Modelo:**
Avalia o desempenho do modelo no conjunto de teste e calcula métricas como precisão, recall, F1-score e AUC-ROC.

8. **Salvamento de Métricas:**
Salva as métricas de desempenho do modelo em um arquivo CSV chamado 'metricas_rede_neural_Multilingual_base.csv'.

9. **Conclusão:**
Exibe um relatório de classificação e salva as métricas em um arquivo CSV.

10. **Observações:**
Ajuste as configurações, como caminhos de arquivos, conforme necessário.
Esteja ciente de que o treinamento pode demorar dependendo do tamanho do conjunto de dados e da complexidade do modelo.
Certifique-se de ter espaço suficiente no dispositivo para armazenar o modelo treinado e os resultados.
Execute o script em um ambiente Python com as bibliotecas instaladas para realizar o ajuste fino do modelo Multilingual.

### Passos para Executar os Classificadores(classificadores_BERTimbau.py e classificadores_multilingual.py)
1. **Instalação de Bibliotecas:**
Execute o seguinte comando no terminal para instalar as bibliotecas necessárias:

```bash
pip install -U sentence-transformers imbalanced-learn
```

2. **Importação de Bibliotecas e Dados:**
Importa as bibliotecas necessárias para classificadores SVM e RF.
Carrega o conjunto de dados do arquivo 'dataset_atualizado_08022022.csv'. Certifique-se de que o arquivo esteja no mesmo diretório ou forneça o caminho correto.

3.** Pré-processamento e Embedding:**
Realiza o pré-processamento nos comentários, removendo caracteres indesejados e convertendo para letras minúsculas.
Utiliza o modelo BERTimbau para gerar embeddings dos comentários.

4. **Random Forest (RF):**
Divide o conjunto de dados em treinamento e teste.
Treina um classificador Random Forest usando os embeddings.
Salva o modelo treinado e métricas de desempenho.

5. **Avaliação do Random Forest:**
Avalia o modelo RF no conjunto de teste.
Calcula métricas como precisão, recall, F1-score, AUC-ROC e gera uma matriz de confusão.

6. **SMOTE e Random Forest:**
Aplica a técnica SMOTE (Synthetic Minority Over-sampling Technique) para lidar com o desbalanceamento de classes.
Treina um novo modelo RF após a aplicação do SMOTE.
Salva o novo modelo e as métricas.

7. **SVM (Support Vector Machine):**
Treina um classificador SVM usando os embeddings.
Salva o modelo treinado e métricas de desempenho.
Avaliação do SVM:

Avalia o modelo SVM no conjunto de teste.
Calcula métricas como precisão, recall, F1-score, AUC-ROC e gera uma matriz de confusão.
8. **SMOTE e SVM:**
Aplica a técnica SMOTE para o SVM.
Treina um novo modelo SVM após a aplicação do SMOTE.
Salva o novo modelo e as métricas.

9. **Métricas Finais:**
Salva as métricas finais em um arquivo CSV chamado 'metricasBERTimbau0506.csv'.

10. **Observações:**

Certifique-se de ter os conjuntos de dados e os modelos treinados anteriormente para análise.
As métricas finais incluem precisão, recall, F1-score, AUC-ROC e informações detalhadas sobre a matriz de confusão para cada classe.
Realize os ajustes necessários nos caminhos de arquivos conforme a sua estrutura de diretórios.
Execute o script em um ambiente Python com as bibliotecas instaladas para realizar a classificação e avaliação.

