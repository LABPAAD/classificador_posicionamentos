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

### Passos para Executar o Treinamento do BERT (RN_BERTimbay.py):

1. **Instalação de Bibliotecas:**
   Certifique-se de ter as bibliotecas necessárias instaladas. Você pode fazer isso executando o seguinte comando no terminal:

   ```bash
   pip install pandas tqdm seaborn matplotlib transformers torch scikit-learn

2. **Importação e Carregamento de Dados:**
O código começa importando bibliotecas necessárias e carregando um conjunto de dados a partir do arquivo 'dataset_atualizado_08022022.csv'. Certifique-se de que este arquivo está presente no mesmo diretório ou forneça o caminho correto.

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

**11. Observações:**
Certifique-se de ter espaço suficiente no seu dispositivo para armazenar o modelo treinado e os resultados.
Dependendo do tamanho do conjunto de dados e da complexidade do modelo, o treinamento pode levar algum tempo.
Lembre-se de ajustar caminhos de arquivos ou outras configurações conforme necessário, e execute o script em um ambiente Python com as bibliotecas instaladas.
