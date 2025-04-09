# Análise RFM para E-Commerce

## 📌 Visão Geral
Este projeto realiza uma análise RFM (Recência, Frequência e Valor Monetário) de clientes de um e-commerce internacional, utilizando dados de transações em 37 países. O objetivo é segmentar os clientes com base em seu comportamento de compra para auxiliar estratégias de marketing e vendas.

## 🔍 Base de Dados
A tabela utilizada contém informações detalhadas sobre transações de e-commerce:

| Coluna        | Descrição                                      | Tipo de Dados  |
|---------------|-----------------------------------------------|----------------|
| CustomerID    | Código único de identificação do cliente      | String         |
| Description   | Descrição detalhada do produto                | String         |
| InvoiceNo     | Código único da fatura/transação              | String         |
| StockCode     | Código de estoque do produto                  | String         |
| Quantity      | Quantidade de itens comprados                 | Inteiro        |
| InvoiceDate   | Data e hora da transação                      | DateTime       |
| UnitPrice     | Preço unitário do produto (em moeda local)    | Decimal        |
| Country       | País onde a transação foi realizada           | String         |

## 🛠️ Ferramentas Utilizadas
- **Linguagens**: Python (Pandas, NumPy), SQL
- **Visualização**: Python Graph Gallery, Matplotlib, Seaborn
- **Machine Learning**: SciKit Learn (para análise complementar)
- **Plataformas**: Google Colab, Excel
- **Versionamento**: GitHub

## 📊 Etapas do Projeto

### 1. Leitura e Inspeção dos dados
- Carregamento do dataset CSV
- Análise inicial da estrutura e qualidade dos dados

### 2. Tratamento de Valores Faltantes
- Identificação e tratamento de valores nulos no CustomerID
- Estratégia: Remoção de registros sem identificação de cliente

### 3. Limpeza de Dados
- Filtragem de preços unitários negativos ou zerados
- Correção de quantidades inválidas
- Exemplo de tratamento:
  ```python
  df = df[df['UnitPrice'] > 0]
  df = df[df['Quantity'] > 0]
  ```

### 4. Remoção de Duplicatas
- Identificação e eliminação de registros duplicados

### 5. Correção de Tipos de Dados
- Conversão de tipos (InvoiceDate para datetime, CustomerID para string)

### 6. Tratamento de Outliers
- Identificação estatística de outliers
- Limitação de faixas aceitáveis para quantidade e preço

### 7. Engenharia de Features
- Criação da coluna `TotalPrice` (Quantity * UnitPrice)
- Cálculo do ticket médio por transação

### 8. Análise Exploratória
- Visualizações chave:
  - Distribuição de compras por país
  - Sazonalidade das vendas
  - Distribuição de valores de transação
  - Relação entre frequência e valor gasto

![Distribuição de Compras por País](https://github.com/user-attachments/assets/a49e05e1-dec0-4ed8-8498-3ec9e9d46975)
![Sazonalidade das Vendas](https://github.com/user-attachments/assets/da0d01f9-d7d8-4784-9d18-6ebab596739c)
![Distribuição de Valores](https://github.com/user-attachments/assets/b2144c9a-dca7-4e4a-a936-3e5e3d40034f)
![Frequência vs Valor Gasto](https://github.com/user-attachments/assets/95aed3d7-60a6-4c40-927f-3951f32fc8fd)

### 9. Cálculo RFM
- **Recência (R)**: Dias desde a última compra
- **Frequência (F)**: Número de transações
- **Valor Monetário (M)**: Valor total gasto

```python
# Cálculo RFM
snapshot_date = df['InvoiceDate'].max() + timedelta(days=1)
rfm = df.groupby('CustomerID').agg({
    'InvoiceDate': lambda x: (snapshot_date - x.max()).days,
    'InvoiceNo': 'nunique',
    'TotalPrice': 'sum'
})
```

### 10. Segmentação de Clientes
- Classificação RFM usando quartis
- Criação de segmentos estratégicos:
  - Champions
  - Clientes em risco
  - Potenciais clientes fiéis
  - Novos clientes

## 📈 Próximos Passos
- Implementação de modelo preditivo para churn
- Análise de cohort para entender retenção de clientes
- Integração com dashboard Power BI/Tableau

## 🤝 Como Contribuir
1. Faça um fork do projeto
2. Crie sua branch (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## Contato ✉️

Se você tiver alguma dúvida ou sugestão, sinta-se à vontade para entrar em contato:

- **Email**: nantorres0@gmail.com
