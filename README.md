# Cassificador de Posicionamento
Classificador automático de posicionamentos em comentários de texto sobre operações policiais


O BERT (_Bidirectional Encoder Representations from Transformers_) [Devlin et al. 2019] é um algoritmo de aprendizado profundo (do, inglês _Deep Learning_) desenvolvido pelo _Google_ para processamento de linguagem natural. BERT é um modelo pré-treinado com conteúdo do Wikipédia e o Book Corpus, ambos em língua inglesa, contendo 2.500 milhões e 800 milhões de palavras respectivamente. Um recurso importante do BERT é sua construção com representações contextuais de modelos pré-treinados, baseado na arquitetura de _transformers_.

Através desse recurso, comunidades de pesquisadores ou corporações podem treinar novos modelos adaptados a alguma linguagem no contexto local e distribuí-los como modelos pré-treinados BERT.

Neste trabalho utilizamos dois modelos pré-treinados que são o _Multilingual_ [Devlin et al. 2019] e o _BERTimbau_ [Souza et al. 2020].
O modelo _Multilingual_ é pré-treinado em 102 idiomas, e possui 12 camadas (blocos de _transformers_), 12 cabeçotes de atenção e 110 milhões de parâmetros.
No que lhe concerne, BERTimbau é pré-treinado na língua portuguesa do Brasil, e em nossas avaliações utilizamos a versão desse modelo com a maior quantidade de codificadores (_large_), contendo 24 camadas, 16 cabeçotes de atenção e 335 milhões de parâmetros.
Embora treinado para uma língua específica, BERTimbau já se mostrou eficiente em tarefas de processamento de linguagem natural que requerem reconhecimento de entidade nomeada, semelhança textual de sentença e reconhecimento de enlace textual [Souza et al. 2020].

> Matriz de embeddings

Utilizamos matrizes de _word embeddings_ extraídas do BERT para treinar classificadores supervisionados na inferência de posicionamento de _tweets_. Em suma, _Word Embedding_ é uma forma de representar palavras através de números para processamento de linguagem natural. Essa representação é normalmente na forma de um vetor de valores reais, que representa o significado das palavras conforme o contexto e o significado da sentença, i.e., o _tweet_ em que a palavra está inserida. Para gerar essa representação, utilizamos os modelos pré-treinados acima descritos. O BERTimbau _large_ gera um vetor de tamanho 1024 para cada sentença, ao passo que o Multilingual gera um vetor de tamanho 768. Ao fim temos uma matriz de word embeddings em que cada linha representa um _tweet_ e cada coluna representa uma característica do _tweet_. 

> Classificadores

A matriz de _words embeddings_ foi utilizada como as características de um conjunto de _tweets_ rotulados para treinar dois classificadores populares que são _Random Forest_ (RF) e _Support Vector Machine_ (SVM) [Mahesh 2020].
RF combina um conjunto de preditores de árvores de modo que cada árvore depende dos valores de um vetor aleatório da amostragem com a mesma distribuição. 
SVR busca predizer um valor real após traçar duas retas paralelas, chamadas limites. O modelo ainda traça uma reta linear entre as duas outras retas retas de modo a ajustar seus valores.

> Rede Neural

Além dos modelos de classificação acima, avaliamos outra abordagem baseada em ajustes finos diretamente sob os modelos BERT.
Especificamente, adicionamos uma nova camada de neurônios aos modelos BERT pré-treinados e a treinamos para nossa tarefa de classificação com os _tweets_ rotulados. Esse ajuste tem a vantagem de acrescentar novas informações aos modelos, que já codificam muitas informações sobre a língua em que foram pré-treinados. Dessa forma pode-se obter melhores resultados para inferência de posicionamentos com menor quantidade de dados rotulados para treinamento, apesar do tempo e complexidade para construção de mais uma camada na rede neural do BERT.

> Configurações, Treinamento e Métricas de avaliação

Como ambiente de experimentação utilizamos uma máquina virtual da AWS do tipo G4dn que são instâncias que usam GPUs otimizadas para aprendizagem profunda. Logo, ajustamos os modelos pré-treinados BERTimbau e Multilingual com 10 épocas e otimizador Adam com os respectivos _learning rate_ e _batch size_ de cada modelo. 

Para a avaliação da rede neural ajustada, consideramos 80\% dos _tweets_ rotulados para treino e 20\% para teste, treinamos esse modelo em cada época, e ao fim de cada época avaliamos o seu desempenho. Para a abordagem com os classificadores, geramos a matriz de _word embedding_ com os modelos BERT pré-treinados, em seguida dividimos a matriz em treino e teste com 80\% e 20\% dos _tweets_ respectivamente, e treinamos os classificadores sem e com balanceamento de classes utilizando a técnica _smote_ [Mahesh 2020].

Avaliamos os modelos com o conjunto de teste utilizando cinco métricas, que são acurácia, precisão, revocação, f1-score e f1-macro, para cada classe (Desaprova, Aprova, Neutro).
A acurácia indica o percentual de _tweets_ corretamente classificados, isto é, a soma acertos de todas as classes dividido pelo número total de _tweets_ classificados. Já a precisão é calculada para cada classe individualmente e evidencia o percentual de _tweets_ corretamente classificados para aquela classe. A revocação é calculada justamente pelo total de _tweets_ corretamente classificados para uma classe sobre o total de _tweets_ dessa classe. F1-score é a média harmônica entre precisão e revocação para cada classe, ao passo que o F1-macro é a média do F1-score considerando todas as classes.

