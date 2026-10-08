# Riscos de doenças cardiovasculares

Dashboard simples em **AngularJS 1.8** + **Chart.js** que lê o `heart.csv` (dataset do Kaggle) e mostra visualmente como a taxa de doença cardíaca varia conforme alguns fatores de risco.

> Projeto educacional, feito para estudar AngularJS. **Não substitui avaliação médica.**

## Como rodar localmente

Não precisa de Node, npm nem build. Só é preciso servir os arquivos por HTTP, porque abrir o `index.html` com duplo clique (`file://`) faz o navegador bloquear a leitura do CSV.

1. Coloque o `heart.csv` na raiz do projeto, ao lado do `index.html`.
2. Inicie um servidor local na pasta do projeto:

   ```bash
   python3 -m http.server 8000     # no Windows: python -m http.server 8000
   ```

   Ou, se preferir Node.js:

   ```bash
   npx serve .
   ```

3. Abra <http://localhost:8000>.

O CSV é carregado automaticamente. Se ele não for encontrado, use o botão **Carregar outro CSV** ou **Usar dados de demonstração** (dados fictícios, só para testar o layout).

> Os scripts do AngularJS e do Chart.js vêm do cdnjs, então é preciso conexão com a internet.

## Entendendo os gráficos

Em todos os gráficos de barras, o valor é a **porcentagem de pacientes com doença cardíaca dentro de cada grupo**. Ao passar o mouse, o tooltip mostra também o `n` (quantos pacientes há no grupo).

| Gráfico | O que mostra | Faixas usadas |
|---|---|---|
| **Por faixa etária** | Taxa de doença em cada faixa de idade | <40, 40–49, 50–59, 60–69, 70+ |
| **Por sexo** | Taxa de doença entre homens e mulheres | Masculino, Feminino |
| **Por colesterol** | Taxa de doença por nível de colesterol total (mg/dl) | <200, 200–239, 240+ |
| **Por pressão em repouso** | Taxa de doença por pressão arterial em repouso (mmHg) | <120, 120–139, 140–159, 160+ |
| **Por frequência cardíaca máxima** | Taxa de doença por frequência máxima atingida no teste de esforço (bpm) | <120, 120–139, 140–159, 160+ |
| **Distribuição geral** | Quantidade de pacientes com e sem doença | — |

Os quatro indicadores no topo (pacientes, % com doença, idade média e colesterol médio) respondem ao filtro de **Sexo**, assim como todos os gráficos, **exceto** o de sexo, que sempre compara os dois grupos.

### Como interpretar

- Procure o **padrão entre as barras**: a taxa sobe, desce ou fica estável conforme a faixa aumenta?
- Faixas com poucos pacientes (`n` baixo) variam muito e não são confiáveis. Observe o `n` no tooltip.
- Os gráficos mostram **associação, não causa**. Um fator associado a mais doença não prova que ele a provoca.
- O dataset é pequeno (cerca de 300 pacientes na versão mais comum) e não representa a população em geral.

## Sobre o dataset

O Heart.csv existe em algumas versões no Kaggle, com nomes de colunas diferentes. O projeto aceita estas variações (sem diferenciar maiúsculas de minúsculas):

| Campo | Nomes aceitos |
|---|---|
| Idade | `Age` |
| Sexo | `Sex` (`1`/`M`/`male` = masculino) |
| Colesterol | `Chol`, `Cholesterol` |
| Pressão em repouso | `RestBP`, `trestbps`, `RestingBP` |
| Freq. cardíaca máxima | `MaxHR`, `thalach` |
| Doença cardíaca | `AHD`, `target`, `HeartDisease`, `num`, `output` |

Pontos de atenção:

- Valores de colesterol ou pressão iguais a `0` são tratados como **dado ausente** e ignorados.
- Em alguns datasets o significado de `target` pode ser invertido. Confira na página do dataset se `1` representa doença. O projeto assume que sim.

## Tecnologias

- [AngularJS 1.8.3](https://angularjs.org/) (suporte oficial encerrado em dezembro de 2021, usado aqui para fins de estudo)
- [Chart.js 4.4.1](https://www.chartjs.org/)