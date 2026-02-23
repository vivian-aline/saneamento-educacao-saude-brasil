# Desigualdade no saneamento básico e impactos em educação e saúde no Brasil

Análise exploratória da relação entre saneamento básico, frequência escolar e disponibilidade de médicos por estado no Brasil, utilizando dados públicos do IBGE e visualização no Looker Studio.

Projeto desenvolvido de forma individual e organizado como parte do meu portfólio para atuação como Analista de Dados Pleno.

---

## 1. Problema e contexto

O acesso ao saneamento básico no Brasil ainda apresenta desigualdades significativas entre estados e regiões, afetando diretamente a qualidade de vida e o desenvolvimento social.  
Neste projeto, investigo se estados com melhor infraestrutura de saneamento básico apresentam também:

- maior frequência escolar;
- maior oferta de médicos por habitante.

**Pergunta central:**

> Como o acesso ao saneamento básico se relaciona com indicadores de educação (frequência escolar) e saúde (médicos por habitante) nos estados brasileiros?

Este tipo de análise pode apoiar decisões de políticas públicas e priorização de investimentos em infraestrutura, educação e saúde.

---

## 2. Dados utilizados

Os dados foram obtidos de bases públicas do **IBGE** e disponibilizados em formato CSV.

Principais arquivos de dados:

- `AbastAgua.csv`: percentuais de acesso a diferentes formas de abastecimento de água por estado.
- `DestLixo.csv`: percentuais de coleta de lixo por serviço de limpeza e outros destinos.
- `Esgoto.csv`: percentuais de acesso à rede geral de esgoto e demais formas de escoamento.
- `SaneamentoBasico.csv`: percentual da população com acesso simultâneo a água, esgoto e coleta de lixo (saneamento básico integrado).
- `Frequenciaescolar.csv`: frequência escolar por faixa etária (6–10, 11–14, 15–17, 18–24 anos).
- `medicoestado.csv`: número de médicos por 10.000 habitantes por estado (2010–2023).
- `Censodemografico2022.csv`: população total por município/UF (Censo Demográfico 2022).

Ferramentas e stack técnica:

- **Linguagem:** Python 3  
- **Principais bibliotecas:** `pandas`, `matplotlib`, `seaborn`  
- **Visualização interativa:** Google Looker Studio  

---

## 3. Metodologia

### 3.1. Preparação e limpeza dos dados

No notebook principal foram realizados os seguintes passos:

- Leitura dos arquivos CSV com `pandas` (água, lixo, esgoto, saneamento, frequência escolar, médicos, censo).
- Padronização da coluna de identificação dos estados (por exemplo, `Estados e Capitais` / `Estados` / `UF`).
- Verificação e tratamento de valores nulos com `fillna(0)` em colunas percentuais e numéricas.
- Ajustes de tipos de dados (`int64`, `float64`, `object`) para permitir cálculos e junções.
- Limpeza do Censo 2022, removendo colunas de códigos e mantendo apenas UF, município e população total.

### 3.2. Integração e criação de indicadores

Com os dados limpos, foram realizadas integrações e cálculos:

- Filtragem apenas dos **estados brasileiros**, removendo linhas de capitais quando necessário.
- Ordenação de estados por:
  - maior/menor acesso à rede de distribuição de água;
  - maior/menor coleta de lixo por serviço de limpeza;
  - maior/menor cobertura de rede de esgoto;
  - maior/menor acesso ao saneamento básico integrado.
- Criação de um dataset integrado com:
  - `Rede de distribuição` (água tratada);
  - `Coletado diretamente por serviço de limpeza`;
  - `Rede geral` (esgoto);
  - `Acesso ao saneamento básico`.
- Cálculo da **matriz de correlação** entre essas variáveis de infraestrutura.
- Junção dos indicadores de saneamento com:
  - frequência escolar média (a partir das faixas etárias);
  - número de médicos por 10.000 habitantes (ano de 2023);
  - população total por estado.

### 3.3. Análises exploratórias

As principais análises exploratórias conduzidas foram:

1. **Rankings por infraestrutura**
   - Estados com maior e menor acesso à água tratada.
   - Estados com maior e menor coleta de lixo por serviço de limpeza.
   - Estados com maior e menor cobertura de rede de esgoto.
   - Estados com maior e menor acesso ao saneamento básico integrado.

2. **Integração de infraestrutura**
   - Identificação dos estados com melhor e pior combinação simultânea de água, lixo, esgoto e saneamento básico.

3. **Correlação entre variáveis**
   - Correlação entre variáveis de infraestrutura (água, lixo, esgoto, saneamento básico integrado).
   - Correlação entre saneamento básico e frequência escolar média.
   - Correlação entre saneamento básico e médicos por 10.000 habitantes.
   - Correlação entre saneamento básico e população total.

4. **Visualizações**
   - Heatmap de correlação entre água, lixo, esgoto e saneamento básico.
   - Gráficos para destacar estados com maior e menor infraestrutura.
   - Visualizações interativas no dashboard (Looker Studio).

---

## 4. Principais insights

Alguns resultados relevantes da análise:

- **Forte desigualdade regional**
  - Estados do Sudeste, especialmente São Paulo, apresentam os melhores índices de saneamento básico integrado (acesso simultâneo a água, lixo e esgoto).
  - Estados do Norte e Nordeste concentram os piores indicadores de saneamento básico.

- **Esgoto é o maior gargalo**
  - A cobertura de rede de esgoto é o serviço com maior disparidade.
  - Alguns estados têm coberturas muito baixas, enquanto outros superam 90%.

- **Associação com saúde e educação**
  - Correlação positiva entre acesso ao saneamento básico e número de médicos por habitante.
  - Correlação positiva entre saneamento básico e frequência escolar média.
  - Correlação positiva entre saneamento básico e população total, sugerindo que regiões com melhor infraestrutura tendem a atrair e reter mais pessoas.

Esses resultados indicam que a infraestrutura de saneamento básico está fortemente associada a melhores indicadores de educação e saúde.

---

## 5. Conclusões e recomendações

- Saneamento básico funciona como um fator estruturante para outros indicadores sociais, como educação e saúde.
- A desigualdade entre estados reforça a necessidade de:
  - investimentos prioritários em infraestrutura nas regiões com menor acesso;
  - políticas integradas entre saneamento, saúde e educação;
  - incentivos para atração e retenção de médicos e professores em áreas com baixa infraestrutura.

Do ponto de vista de análise de dados, o projeto demonstra:

- capacidade de trabalhar com múltiplas fontes de dados públicas;
- integração de bases heterogêneas (saneamento, educação, saúde, demografia);
- exploração de correlações e geração de insights acionáveis para políticas públicas.

---

## 6. Dashboard no Looker Studio

Os resultados foram sintetizados em um painel interativo, permitindo explorar os indicadores por estado e região:

🔗 [Dashboard no Looker Studio](https://lookerstudio.google.com/reporting/0413c8a2-9c37-4620-b5a1-fe45e82776a9)

---

## 7. Estrutura do repositório

organização de pastas e arquivos:

```bash
.
├── data/
│── raw/          # CSVs originais do IBGE
├── notebooks/
│   └── eda_saneamento_escola_medicos.ipynb
├── dashboards/
│   └── eda_saneamento_escola_medicos.pdf
└── README.md
