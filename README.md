# 📊 Bank Marketing Analysis (PT) — Power BI Dashboard

> Análise exploratória de dados de campanhas de marketing de um banco português, com foco na conversão de depósitos a prazo.

---

## 📌 Índice

- [Sobre o Projeto]
- [Objetivos da Análise]
- [Dataset]
- [Ferramentas Utilizadas]
- [Estrutura do Dashboard]
- [Medidas DAX e Colunas Calculadas]
- [Principais Conclusões]
- [Recomendações]
- [Como Visualizar]

---

## 📁 Sobre o Projeto

Este projeto foi desenvolvido com base no dataset **Bank Marketing** do [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Bank+Marketing).

Os dados dizem respeito a campanhas de marketing realizadas por telefone por uma instituição bancária portuguesa. O objetivo principal é compreender o perfil dos clientes e identificar os fatores que influenciam a aquisição de um **depósito a prazo bancário** (variável `y`).

---

## 🎯 Objetivos da Análise

- Compreender o Perfil Sociodemográfico dos Clientes
- Analisar dos Outliers
- Identificar a Relação entre Variáveis Financeiras e a Conversão
- Verificar Correlações entre Variáveis Numéricas
- Calcular Probabilidades Condicionais de Compra

---

## 🛠️ Ferramentas Utilizadas

| Ferramenta | Utilização |
|---|---|
| **Power BI Desktop** | Construção do dashboard e visualizações |
| **DAX** | Criação de medidas e colunas calculadas |
| **UCI ML Repository** | Fonte dos dados |

---

## 📂 Estrutura do Dataset

| Variável | Tipo | Descrição |
|---|---|---|
| `age` | Numérica | Idade do cliente |
| `job` | Categórica | Profissão |
| `marital` | Categórica | Estado civil |
| `education` | Categórica | Nível de escolaridade |
| `default` | Binária | Incumprimento (yes/no) |
| `balance` | Numérica | Saldo bancário médio anual |
| `housing` | Binária | Possui casa própria (yes/no) |
| `loan` | Binária | Possui empréstimo pessoal (yes/no) |
| `contact` | Categórica | Tipo de contacto |
| `month` | Categórica | Mês do último contacto |
| `duration` | Numérica | Duração da chamada (em segundos) |
| `campaign` | Numérica | Nº de contactos nesta campanha |
| `previous` | Numérica | Nº de contactos em campanhas anteriores |
| `y` | Binária | **Variável alvo** — adquiriu o depósito? |

> ⚠️ Este dataset utiliza **ponto e vírgula** como separador no ficheiro CSV.

---

## 📊 Dashboard — 5 Páginas

### Página 1 — Visão Geral

![Dashboard Preview](https://github.com/diogovent/Bank-Marketing-Analysis-PT/blob/main/1.png)

Apresentação dos principais indicadores do dataset:

| Indicador | Valor |
|---|---|
| Total de Clientes | 45.211 |
| Taxa de Conversão | 11,7% |
| Idade Média | 41 anos |
| Saldo Médio | 1.362,27 € |

**Visuais incluídos:**
- Gráfico de violino — distribuição de idades por profissão
- Gráfico circular — tipo de contacto utilizado (cellular 64,77% / unknown 28,8% / telephone 6,43%)

---

### Página 2 — Perfil do Cliente

![Dashboard Preview](https://github.com/diogovent/Bank-Marketing-Analysis-PT/blob/main/2.png)

Análise do perfil sociodemográfico dos clientes.

**Visuais incluídos:**
- Tabela com Nº de Clientes por Profissão — As profissões mais comuns são **blue-collar (9.732)** e **management (9.458)**
- **Heatmap — Escolaridade vs Empréstimo:** Isto nos diz que os clientes que têm o nivel de educação terciário e que não têm
emprestimos (16%) são a os clientes que mais adquiriram um novo emprestimo
- **Heatmap — Estado Civil vs Profissão:** A célula onde se cruza single com student tem o valor 0,29, significa que 29% dos
clientes solteiros e estudantes compraram o depósito enquanto divorced com retired tem 0,28 ou seja 28% dos reformados
divorciados também compraram. Estes são os dois perfis que mais se destacam no heatmap, aparecem com a cor mais escura, e são
portanto os grupos com maior probabilidade de adquirir o produto.

---

### Página 3 — Análise Financeira

![Dashboard Preview](https://github.com/diogovent/Bank-Marketing-Analysis-PT/blob/main/3.png)

Exploração das variáveis financeiras e correlações numéricas.

**Visuais incluídos:**
- Gráfico de dispersão — Idade vs Saldo: Reparamos que não existe uma relação entre a idade dos clientes com o seu nivel de saldo
- Gráfico de barras — Média do saldo por posse de casa (quem não tem casa apresenta saldo médio mais elevado, ~1.600€)

**Correlações de Pearson:**

| Par de Variáveis | Coeficiente | Interpretação |
|---|---|---|
| Idade / Saldo | 0,10 | Correlação muito fraca |
| Idade / Duração | 0,00 | Sem correlação |
| Saldo / Duração | 0,02 | Sem correlação relevante |
| Campanha / Previous | -0,03 | Sem correlação relevante |

> 💡 Nenhuma das variáveis numéricas apresenta correlação linear forte entre si.

---

### Página 4 — Outliers

![Dashboard Preview](https://github.com/diogovent/Bank-Marketing-Analysis-PT/blob/main/4.png)

Identificação e análise dos outliers na variável `balance` através do **método IQR (Interquartil)**.

**Método utilizado:**

**Resultados:**
- Total de outliers identificados: **526 clientes**
- A proporção de clientes que adquiriram o depósito é **semelhante** entre outliers (~13%) e não-outliers (~11,5%)
- A média de idades é praticamente igual entre os dois grupos (~41 anos)
- O mês de **maio** concentra a maior proporção de contactos em ambos os grupos

---

### Página 5 — Conversão

![Dashboard Preview](https://github.com/diogovent/Bank-Marketing-Analysis-PT/blob/main/5.png)

Análise da probabilidade de compra do depósito a prazo em função de variáveis binárias e do historial de contacto.

**Principais conclusões:**

| Grupo | Taxa de Conversão (yes) |
|---|---|
| Sem casa própria | 16,7% |
| Com casa própria | 7,7% |
| Sem empréstimo | 12,66% |
| Com empréstimo | 6,68% |
| Sem incumprimento | 11,8% |
| Com incumprimento | 6,38% |

**Probabilidade Condicional:**
- Clientes **contactados anteriormente** (`previous > 0`): **~23% de probabilidade** de compra
- Clientes **nunca contactados**: **~9% de probabilidade** de compra
- Total de clientes com contacto anterior: **8.257**

> 💡 Ter sido contactado em campanhas anteriores **mais do que duplica** a probabilidade de aquisição do produto.

---

## 🔍 Principais Conclusões

1. **Perfil mais propenso a comprar:** cliente solteiro, estudante ou reformado, com escolaridade terciária e sem empréstimo activo
2. **O saldo não é determinante** para a conversão, outliers e não-outliers convertem de forma semelhante
3. **Ter casa própria ou empréstimo reduz a conversão**, possivelmente por já existirem compromissos financeiros
4. **O contacto prévio é o factor mais relevante**, clientes já abordados têm o dobro da probabilidade de converter
5. **Maio é o mês com mais contactos**, tanto para outliers como para o conjunto geral

---

## 💡 Recomendações

1. **Priorizar clientes já contactados anteriormente** - A probabilidade de conversão é mais do dobro face a clientes sem historial de contacto.
2. **Focar as campanhas em clientes sem casa própria e sem empréstimo** — Estes perfis apresentam consistentemente taxas de conversão mais elevadas.
3. **Segmentar por perfil sociodemográfico** — Clientes solteiros, estudantes ou reformados com escolaridade terciária são os mais propensos a adquirir o produto.
4. **Não descartar clientes com saldos extremos (outliers)** — Estes convertem de forma semelhante aos restantes, pelo que não devem ser excluídos das campanhas.

---

## 📌 Como Visualizar

1. Faz o download do ficheiro `.pbix` disponível neste repositório
2. Abre no **Power BI Desktop** (gratuito)
3. Navegue pelas 5 páginas do dashboard

Ou então pode abrir por este link: https://app.powerbi.com/groups/me/reports/ace82cfb-963a-4dd2-9a4c-daff0dc5a562/4d61f9bcc5025a073207?experience=power-bi

---

## 👤 Autor

Desenvolvido como projecto de análise de dados para portfólio pessoal.

---

*Dataset original: [UCI Machine Learning Repository — Bank Marketing](https://archive.ics.uci.edu/ml/datasets/Bank+Marketing)*
