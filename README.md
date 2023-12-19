# Cassificador de Posicionamento
Classificador automático de posicionamentos em comentários de texto sobre operações policiais

O BERT (_Bidirectional Encoder Representations from Transformers_) [Devlin et al. 2019] é um algoritmo de aprendizado profundo (do, inglês _Deep Learning_) desenvolvido pelo _Google_ para processamento de linguagem natural. BERT é um modelo pré-treinado com conteúdo do Wikipédia e o Book Corpus, ambos em língua inglesa, contendo 2.500 milhões e 800 milhões de palavras respectivamente. Um recurso importante do BERT é sua construção com representações contextuais de modelos pré-treinados, baseado na arquitetura de _transformers_.

Através desse recurso, comunidades de pesquisadores ou corporações podem treinar novos modelos adaptados a alguma linguagem no contexto local e distribuí-los como modelos pré-treinados BERT.

Neste trabalho utilizamos dois modelos pré-treinados que são o _Multilingual_ [Devlin et al. 2019] e o _BERTimbau_ [Souza et al. 2020].
O modelo _Multilingual_ é pré-treinado em 102 idiomas, e possui 12 camadas (blocos de _transformers_), 12 cabeçotes de atenção e 110 milhões de parâmetros.
No que lhe concerne, BERTimbau é pré-treinado na língua portuguesa do Brasil, e em nossas avaliações utilizamos a versão desse modelo com a maior quantidade de codificadores (_large_), contendo 24 camadas, 16 cabeçotes de atenção e 335 milhões de parâmetros.
Embora treinado para uma língua específica, BERTimbau já se mostrou eficiente em tarefas de processamento de linguagem natural que requerem reconhecimento de entidade nomeada, semelhança textual de sentença e reconhecimento de enlace textual [Souza et al. 2020].

[Mais detalhes](brasnam_marcos2022.pdf)


