# 🤖 Item 5: Processamento de Dados com GenAI e LLMs

Nesta etapa, o objetivo foi atuar na camada de processamento de dados desestruturados. No contexto de e-commerce, as descrições de produtos geralmente são longos blocos de texto (JSON/Textos de 3GB+) que escondem características vitais para análise e clusterização de produtos.

## 🛠️ Solução de Arquitetura Implementada

Utilizei a API da OpenAI via Google Colab para criar um pipeline de transformação (ETL Inteligente). 

- **Modelo Escolhido:** A arquitetura foi desenhada para utilizar modelos como o `gpt-4o-mini` ou `gpt-3.5-turbo`, que oferecem o melhor balanço entre velocidade, custo por token e capacidade de seguir esquemas estritos (JSON Output) para grandes volumes de dados.
- **Engenharia de Prompt:** O LLM foi instruído a atuar de forma determinística (`temperature=0.0`), extraindo variáveis específicas (como material, se é feito à mão e proteção RFID) e tipando os dados corretamente (booleanos, strings e arrays).

## 📸 Evidência da Extração (Print)

<img width="1600" height="719" alt="image" src="https://github.com/user-attachments/assets/604e6c52-d535-45d9-9b71-8cbbf4248d8d" />


🔗 **Link para o Google Colab com o script executável:** https://colab.research.google.com/drive/1MGM-9Tqm-07fV4alwCW2PO1nvUqYygpV#scrollTo=R33LYWATc2rw

Com essa transformação, o dado que antes era apenas texto passa a ser uma `feature` tabular, permitindo análises de correlação (ex: "Produtos 'Handmade' têm um LTV maior?") na próxima etapa de visualização.
