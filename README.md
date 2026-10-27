
# 💧 Aqua-Limne

### Pesquisa científica, qualidade da água e tecnologias digitais

O **Aqua-Limne** é um projeto de pesquisa científica desenvolvido no contexto do ensino médio, voltado à investigação de tecnologias e métodos computacionais aplicados ao monitoramento e à análise da qualidade da água.

A proposta integra conhecimentos de Ciências da Natureza, Matemática, Estatística e Computação, explorando como indicadores físico-químicos podem ser organizados, visualizados e analisados por meio de ferramentas digitais.

Este repositório apresenta uma aplicação demonstrativa de análise exploratória de dados, incluindo procedimentos estatísticos, identificação de observações potencialmente anômalas e um dashboard interativo desenvolvido com Google Apps Script.

> **Nota científica:** os dados utilizados nesta demonstração são externos e não representam medições realizadas pelo Aqua-Limne. Os alertas computacionais não constituem comprovação de contaminação ou diagnóstico da qualidade ambiental.

---

## 📌 Objetivo

Investigar a aplicação de indicadores físico-químicos e recursos computacionais no acompanhamento e na interpretação exploratória de dados relacionados à qualidade da água.

### Objetivos específicos

- Estudar indicadores físico-químicos associados à qualidade da água.
- Organizar e verificar a consistência de registros ambientais.
- Aplicar métodos estatísticos para identificar padrões e variações.
- Explorar técnicas de aprendizado de máquina para sinalização de observações incomuns.
- Desenvolver uma interface web para visualização interativa dos resultados.
- Promover a integração entre pesquisa científica e desenvolvimento tecnológico no ensino médio.

---

## 🌊 Indicadores analisados

A análise considera cinco indicadores principais:

| Indicador | Unidade | Descrição |
|---|---|---|
| pH | Adimensional | Expressa a acidez ou alcalinidade da água. |
| Oxigênio dissolvido | mg/L | Indica a concentração de oxigênio dissolvido na água. |
| Condutividade elétrica | µS/cm | Relaciona-se à capacidade da água de conduzir corrente elétrica. |
| Turbidez | NTU | Expressa a dispersão da luz causada por partículas presentes na água. |
| Temperatura | °C | Representa a condição térmica da água. |

A precipitação também estava presente no arquivo original, mas não foi incluída na análise multivariada principal devido à elevada proporção de valores ausentes.

---

## 🗂️ Origem do conjunto de dados

O conjunto de dados utilizado na demonstração foi identificado pelo nome:

`ef08_cetesb_set2026.csv`

A identificação associada ao arquivo aponta para a **CETESB — Companhia Ambiental do Estado de São Paulo**, órgão ambiental estadual responsável por atividades de monitoramento e controle ambiental.

**Site institucional da CETESB:**
https://cetesb.sp.gov.br/

### Informações sobre a base analisada

| Característica | Informação |
|---|---|
| Identificação do arquivo | `ef08_cetesb_set2026.csv` |
| Instituição indicada na identificação do arquivo | CETESB |
| Período dos registros | 1º a 30 de setembro de 2026 |
| Frequência dos registros | Horária |
| Total de registros | 697 |
| Indicadores principais | 5 |
| Registros completos utilizados na análise | 625 |
| Ambiente de análise | Google Colab / Python |

### Transparência sobre a procedência

A atribuição à CETESB foi mantida conforme a identificação associada ao conjunto de dados utilizado no estudo.

Entretanto, **a URL original de download, a autenticidade do arquivo e sua correspondência com uma publicação oficial específica ainda não foram verificadas independentemente**.

O endereço institucional apresentado acima não deve ser interpretado como um link direto ou confirmado para o download do CSV.

Caso a fonte oficial específica seja posteriormente localizada e confirmada, esta seção deverá ser atualizada com o endereço do conjunto de dados, a data de acesso e as condições de utilização.

**O Aqua-Limne não é apresentado como produtor ou responsável pelas medições contidas nessa base.**

---

## 🔬 Metodologia da análise exploratória

A análise foi desenvolvida em Python, utilizando o ambiente Google Colab.

O processo foi organizado em etapas de inspeção, tratamento, descrição estatística, investigação temporal e aplicação exploratória de aprendizado de máquina.

### 1. Inspeção inicial

Foram examinadas a estrutura da base, as variáveis disponíveis, os tipos de dados, a existência de duplicatas e possíveis inconsistências físicas nos indicadores.

### 2. Verificação dos valores ausentes

Foi identificada uma interrupção contínua de 72 horas nas medições dos cinco indicadores principais, entre 18 e 21 de setembro de 2026.

A precipitação apresentou 288 valores ausentes, correspondentes a aproximadamente 41,32% dos registros.

Para as análises multivariadas, foram selecionados os 625 registros completos dos cinco indicadores principais, sem preenchimento artificial da lacuna temporal.

### 3. Estatística descritiva

Foram calculadas medidas como:

- Média;
- Mediana;
- Desvio-padrão;
- Valores mínimos e máximos;
- Quartis.

Também foram examinadas distribuições, séries temporais e médias móveis.

### 4. Análise das relações entre indicadores

Foram utilizadas correlações de Pearson para investigar associações estatísticas entre os indicadores.

As relações foram examinadas no conjunto completo, em períodos separados pela interrupção dos registros e por meio de variações horárias consecutivas.

As correlações identificadas não foram interpretadas como relações de causa e efeito.

### 5. Detecção exploratória de anomalias

Foi aplicado o algoritmo **Isolation Forest**, da biblioteca scikit-learn, utilizando os cinco indicadores padronizados.

A configuração principal utilizou:

- 200 estimadores;
- `contamination = 0.05`;
- `random_state = 42`;
- `n_jobs = -1`.

O algoritmo sinalizou 32 registros como anomalias potenciais.

### 6. Comparação estatística

Os alertas do Isolation Forest foram comparados com um procedimento baseado em Z-score, considerando valores com distância superior a três desvios-padrão da média em pelo menos um indicador.

### 7. Análise de sensibilidade

Foram examinadas configurações de contaminação de 2%, 5% e 10%, mantendo os demais parâmetros do algoritmo.

O objetivo foi observar a estabilidade dos registros sinalizados diante de diferentes limiares de classificação.

---

## 📊 Principais resultados

### Integridade e disponibilidade dos registros

| Resultado | Valor |
|---|---:|
| Registros originais | 697 |
| Registros completos para análise multivariada | 625 |
| Registros com ausência nos cinco indicadores principais | 72 |
| Duração da interrupção | 72 horas |
| Valores ausentes de precipitação | 288 |
| Percentual ausente de precipitação | 41,32% |

### Estatísticas descritivas

| Indicador | Média | Desvio-padrão | Mínimo | Máximo |
|---|---:|---:|---:|---:|
| pH | 7,84 | 0,71 | 6,35 | 9,22 |
| Oxigênio dissolvido (mg/L) | 5,62 | 1,80 | 0,89 | 10,97 |
| Condutividade elétrica (µS/cm) | 141,01 | 2,15 | 135,05 | 150,07 |
| Turbidez (NTU) | 3,18 | 0,82 | 1,56 | 5,87 |
| Temperatura (°C) | 20,15 | 1,28 | 18,73 | 24,32 |

Os valores correspondem aos 625 registros completos utilizados na análise.

### Comparação entre os métodos de detecção

| Classificação | Registros |
|---|---:|
| Sinalizados apenas pelo Isolation Forest | 25 |
| Sinalizados apenas pelo Z-score | 1 |
| Sinalizados pelos dois métodos | 7 |
| Não sinalizados por nenhum dos métodos | 592 |
| Total analisado | 625 |

O Isolation Forest sinalizou 32 registros, enquanto o critério de Z-score sinalizou oito.

Essa diferença não demonstra superioridade ou maior precisão de um método, pois os critérios de classificação são distintos e não existe uma referência independente de eventos ambientais confirmados.

### Sensibilidade do Isolation Forest

| Contaminação configurada | Alertas | Percentual observado |
|---|---:|---:|
| 2% | 13 | 2,08% |
| 5% | 32 | 5,12% |
| 10% | 63 | 10,08% |

Todos os 13 alertas da configuração de 2% também apareceram na configuração de 5%, e todos os 32 alertas da configuração de 5% apareceram na configuração de 10%.

Os registros mais incomuns concentraram-se principalmente em episódios de 21 e 27 de setembro de 2026.

Esses resultados indicam observações que merecem investigação adicional, mas não comprovam eventos de contaminação ou falhas de medição.

---

## 🖥️ Dashboard interativo

O Aqua-Limne disponibiliza uma aplicação web demonstrativa desenvolvida com **Google Apps Script**, conectada a uma planilha do **Google Sheets**.

https://aqualimne.s.gy/dashboard

A interface foi organizada em quatro áreas:

### Sobre o Projeto

Apresenta o Aqua-Limne, seus objetivos e sua proposta de investigação científica.

### Dashboard

Permite:

- Filtrar os registros por período;
- Selecionar indicadores físico-químicos;
- Visualizar séries temporais;
- Examinar médias diárias;
- Consultar estatísticas descritivas;
- Identificar lacunas nos registros;
- Visualizar os alertas potenciais do Isolation Forest;
- Comparar classificações de 2%, 5% e 10%.

### Metodologia

Explica, em linguagem acessível, os procedimentos de análise estatística e de aprendizado de máquina utilizados na demonstração.

### Fonte dos Dados

Apresenta informações sobre a procedência declarada do conjunto de dados, os critérios de análise e as limitações da interpretação.

---

## 🛠️ Tecnologias utilizadas

| Tecnologia | Aplicação |
|---|---|
| Python | Processamento e análise exploratória |
| Google Colab | Ambiente de execução da análise |
| Pandas | Organização e manipulação dos dados |
| NumPy | Operações numéricas |
| Matplotlib | Visualização estatística |
| scikit-learn | Padronização e Isolation Forest |
| Google Sheets | Armazenamento dos dados do dashboard |
| Google Apps Script | Backend e publicação do aplicativo web |
| HTML, CSS e JavaScript | Interface do aplicativo |
| Google Charts | Gráficos interativos |

---

## 📁 Organização do repositório

```text
aqualimne/
│
├── README.md
│
├── analise_exploratoria.ipynb
│
├── ef08_cetesb_set2026.csv
│
└── LICENSE
```

---

## ⚠️ Limitações científicas

A aplicação possui caráter exploratório e demonstrativo.

Entre suas principais limitações estão:

- A procedência oficial específica do arquivo ainda precisa ser confirmada.
- Os registros analisados não foram produzidos pelo Aqua-Limne.
- A base contém uma interrupção contínua de 72 horas nos indicadores principais.
- A variável precipitação apresenta elevada proporção de valores ausentes.
- As correlações estatísticas não estabelecem causalidade.
- A classificação do Isolation Forest depende de parâmetros e características dos dados.
- Não foram utilizados rótulos independentes para validar os alertas ambientais.
- O dashboard não substitui análises laboratoriais, monitoramento regulamentar ou avaliação especializada.

Os resultados devem ser interpretados como apoio à investigação científica, e não como diagnóstico conclusivo da qualidade da água.

---

## 🎓 Contexto educacional

O Aqua-Limne busca aproximar a pesquisa científica do cotidiano de estudantes do ensino médio.

A proposta estimula a formulação de perguntas, o pensamento crítico, a interpretação de evidências e o uso responsável de tecnologias digitais.

O desenvolvimento da plataforma também permite explorar conceitos de programação, estatística, visualização de dados e investigação ambiental.

---

## 🔭 Possibilidades de desenvolvimento

Entre as possibilidades de continuidade estão:

- Integração com dados experimentais obtidos em futuras atividades de monitoramento;
- Ampliação das ferramentas de visualização;
- Investigação de novos métodos estatísticos;
- Estudo de critérios de interpretação ambiental;
- Melhoria da documentação e da reprodutibilidade das análises;
- Aperfeiçoamento da interface para uso educacional.

Essas possibilidades representam perspectivas de desenvolvimento, não funcionalidades já implementadas.

---

## 📚 Referência institucional dos dados

**CETESB — Companhia Ambiental do Estado de São Paulo.**

Site institucional: https://cetesb.sp.gov.br/

Arquivo analisado: `ef08_cetesb_set2026.csv`.

**Observação:** a referência acima identifica a instituição associada ao nome do arquivo. A publicação oficial específica e a URL de obtenção do conjunto de dados ainda precisam ser confirmadas.

---

## 💧 Sobre o Aqua-Limne

O Aqua-Limne é uma iniciativa de pesquisa científica que explora as relações entre qualidade da água, análise de dados e desenvolvimento tecnológico no contexto educacional.

Seu propósito é contribuir para a aprendizagem científica por meio da investigação, da experimentação computacional e da comunicação transparente dos resultados.

**Aqua-Limne — Ciência, água e tecnologia.**
