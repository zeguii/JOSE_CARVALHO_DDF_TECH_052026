# 🛡️ Item 4: Data Quality (Qualidade de Dados)

Após a integração inicial dos dados do e-commerce (Amazon Dataset), foi identificada a necessidade de auditar inconsistências e dados faltantes (missing values) para garantir a integridade dos modelos de Inteligência Artificial posteriores e a experiência de compra dos clientes.

Conforme as melhores práticas, optei pela implementação da biblioteca `great-expectations` rodando via Google Colab.

## 🛠️ Abordagem de Melhoria de Qualidade

1. **Mapeamento de Regras de Negócio (Expectations):**
   - **Completude:** As colunas `product_id`, `title` e `description` foram marcadas com a regra `expect_column_values_to_not_be_null`. Textos nulos impossibilitam a extração de features via LLM.
   - **Consistência Numérica:** A coluna `price` recebeu a regra `expect_column_values_to_be_between` (mínimo de 0.01), evitando faturamentos irreais ou negativos.
   - **Unicidade:** A coluna `product_id` foi testada com `expect_column_values_to_be_unique` para evitar duplicidade no catálogo.

2. **Implementação e Relatório:**
   O script processou o dataset e gerou um log de validação isolando as anomalias, como pode ser visto na evidência abaixo.

🔗 **Link para o Google Colab com o código fonte:** [COLE O LINK DO SEU COLAB AQUI]

## 📸 Evidência da Auditoria (Print)

<img width="1600" height="716" alt="image" src="https://github.com/user-attachments/assets/a4700fca-968e-4b37-abba-3413fb967d81" />


## 💡 Bônus: Common Data Model (CDM)
Para padronizar os dados utilizados, foi definido o seguinte Common Data Model focado no contexto do cliente de varejo:
- `id_produto` (String/UUID)
- `nm_titulo_produto` (String)
- `ds_produto` (Text)
- `vl_preco_venda` (Float)
- `dt_inclusao` (Timestamp)
