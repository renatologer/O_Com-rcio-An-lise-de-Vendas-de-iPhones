# 📱 O Comércio — Análise de Vendas de iPhones

Notebook Databricks para exploração e análise do dataset de vendas de iPhones (`O_Phone_sales_dataset.csv`).

**Autor:** Renato Lima  
**Stack:** Databricks · Python · pandas · matplotlib  
**Fonte dos dados:** `/Volumes/workspace/default/o_phone/O_Phone_sales_dataset.csv`

---

## 🎯 Objetivo

Responder perguntas de negócio sobre o desempenho comercial de iPhones:

- Distribuição de vendas por país e modelo
- Faturamento total e ticket médio por período
- Modelos mais caros e mais vendidos
- Sazonalidade mensal das vendas

---

## 📁 Estrutura do Notebook

| Seção | Conteúdo |
|-------|----------|
| **1. Carga dos Dados** | Leitura do CSV com pandas (alternativa PySpark comentada) |
| **2. EDA** | Tipos, estatísticas descritivas, dimensões e valores nulos |
| **3. Análises por Dimensão** | País, modelo, top 10 mais caros, faturamento por país |
| **4. Series vs DataFrame** | Demonstração das duas estruturas principais do pandas |
| **5. Análise Temporal** | Conversão de datas, extração de mês/ano-mês, sazonalidade |
| **6. Ticket Médio Mensal** | Preço total / Quantidade vendida por período |
| **7. Visualização** | Gráfico de barras do faturamento mensal |

---

## 🔍 Principais Análises

### Distribuição de Mercado
- Contagem de vendas por **país** e por **modelo**
- Filtro de registros com rótulo `"iPhone"` para consistência dos dados

### Top 10 Modelos Mais Caros
- Ordenação por preço (descendente) antes do `head(10)`
- Agregações: soma, média, máximo e mínimo do painel de preços

### Faturamento por País
- `groupby("Country")["Price"].sum()` ordenado do maior para o menor

### Sazonalidade
- Coluna `Sale_Date` convertida para `datetime`
- Colunas derivadas: `Month` (número 1–12) e `Nome` (formato `YYYY-MM`)
- Faturamento e quantidade agrupados por mês e por ano-mês

### Ticket Médio
```
Ticket Médio = Price (soma) / Quantity (soma)
```
Calculado por ano-mês para identificar se a receita vem de **volume** ou **valor unitário**.

---

## 📊 Visualização

Gráfico de barras gerado com **matplotlib** mostrando o faturamento (`Price`) por período (`YYYY-MM`), permitindo identificar picos e quedas sazonais.

---

## ▶️ Como Executar

1. Faça upload do arquivo `O_Phone_sales_dataset.csv` no volume Databricks:  
   `/Volumes/workspace/default/o_phone/`
2. Importe o notebook `.py` no seu workspace Databricks.
3. Execute as células em ordem — cada seção é independente após a **Seção 1**.

> **Requisitos:** cluster com Python 3.x, bibliotecas `pandas` e `matplotlib` disponíveis (padrão nos clusters Databricks).

---

## 📦 Dependências

```python
import pandas as pd
import matplotlib.pyplot as plt
```

---

## 📝 Notas

- O dataset cabe em memória, por isso foi escolhido **pandas** em vez de PySpark (código PySpark disponível comentado na Seção 1).
- O filtro `.str.contains("iPhone")` protege contra rótulos inconsistentes no campo `iPhone_Model`.
- Colunas renomeadas para português (`Data`, `Preço`, `Quantidade`, `Mês`) nas saídas finais para facilitar a leitura.
