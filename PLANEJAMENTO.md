# 📊 Item 0: Planejamento e Agilidade (PMBOK & Ágil)

Este documento detalha o ciclo de vida do projeto de implementação da Plataforma de Dados para o cliente de E-commerce, unindo as áreas de conhecimento do PMBOK (Escopo, Cronograma, Riscos) com a execução ágil.

## 1. Escopo e Base de Dados (Item 1)
**Base Escolhida:** Amazon Product Metadata & Customer Reviews Dataset (Subconjunto de Eletrônicos/Acessórios).
**Justificativa:** Atende ao cenário de e-commerce e cumpre a exigência de possuir mais de 100.000 registros. Além disso, a base possui uma vasta quantidade de dados desestruturados em JSON (títulos e descrições longas de produtos), fornecendo o cenário ideal para o processamento de features via LLM e para a aplicação rigorosa de métricas de Data Quality.

## 2. Cronograma e Fluxo de Execução (Kanban/Checklist)

### 📌 Fase 1: Iniciação e Planejamento (Setup)
- [x] Kickoff e entendimento da arquitetura atual (AWS).
- [x] Definição e download do dataset Olist (>100k registros).
- [x] Criação do repositório padronizado no GitHub.

### ⚙️ Fase 2: Integração e Exploração (Engenharia)
- [ ] **(Item 2)** Conectar a base de dados Olist e realizar o carregamento para a Dadosfera.
- [ ] **(Item 3)** Organizar os dados nas zonas lógicas do Data Lake (Landing, Staging, Curated) e catalogar ativos.
- [ ] **(Item 4)** Desenvolver script no Colab utilizando `great-expectations` para auditoria de Data Quality.

### 🧠 Fase 3: Processamento com IA e Modelagem
- [ ] **(Item 5)** Utilizar LLM (OpenAI/GPT) para processar as descrições dos produtos e extrair novas *features* estruturadas.
- [ ] **(Item 6)** Criar a modelagem dimensional (Star Schema / Kimball) adequada para o negócio.
- [ ] **(Item 8)** Orquestrar o pipeline de dados utilizando o módulo de inteligência da plataforma.

### 📈 Fase 4: Análise e Geração de Valor (Analytics & Data Apps)
- [ ] **(Item 7)** Construir Dashboard no Metabase com análise de categorias e série temporal (mínimo de 5 visualizações).
- [ ] **(Item 9)** Desenvolver Data App interativo em Python utilizando Streamlit.
- [ ] **(Bônus)** Integrar IA Generativa (DALL-E) no Data App para geração visual de produtos.

### 🏁 Fase 5: Encerramento e Handover
- [ ] **(Item 10)** Gravação do pitch comercial e defesa técnica (Dadosfera vs. AWS).
- [ ] Documentação final do repositório em Markdown.

---

## 3. Análise de Riscos e Mitigação (Avançado)

| Risco Identificado | Impacto | Estratégia de Mitigação |
| :--- | :--- | :--- |
| **Timeout na API do LLM (Item 5)** | Alto (Gargalo no pipeline) | Processamento em *batches* (lotes) e implementação de rotinas de *retry* no script Python. |
| **Inconsistência nos Dados (Nulos)** | Médio (Viés na análise) | Utilização rigorosa da biblioteca `great-expectations` no Item 4 para barrar dados anômalos antes da camada Curated. |
| **Estouro de Memória no Streamlit** | Alto (Queda do App) | Otimização das queries em SQL para carregar apenas os dados agregados necessários para a visualização no Data App. |

## 4. Interdependências Críticas
* O **Item 5 (Processamento LLM)** depende diretamente da conclusão do **Item 4 (Data Quality)**, garantindo que o modelo de linguagem não consuma "lixo" (Garbage In, Garbage Out).
* O **Item 7 (Analisar - Metabase)** só pode ser iniciado após a consolidação do **Item 6 (Modelagem de Dados)**.
