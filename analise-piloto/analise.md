# Teste_piloto_EvasãoEscolar

# Objetivo

O teste piloto tem como finalidade realizar uma análise exploratória preliminar do **dataset_evasao_v2.csv.arff** antes da aplicação definitiva das técnicas de pré-processamento e classificação no Weka. Essa etapa busca identificar possíveis inconsistências estruturais, padrões relevantes, valores faltantes, ruídos, outliers e relações entre os atributos acadêmicos utilizados na predição da evasão estudantil.

Além disso, o teste piloto permite verificar se o conjunto de dados foi gerado adequadamente e se os algoritmos conseguem processar o dataset sem falhas antes da execução final do experimento, garantindo que as decisões de pré-processamento sejam orientadas por evidências observadas nos dados e não aplicadas de forma mecânica.

# 1. Verificação Inicial do DataSet

## Objetivo da etapa

Verificar se o **dataset_evasao_v2.csv.arff** está estruturado corretamente para utilização no Weka e confirmar se os atributos foram reconhecidos adequadamente.

## Requisitos

| Verificação  | Esperado | Status |
| --- | --- | --- |
| Número de instâncias | Mínimo 500 | ✅ 500 Instâncias  |
| Número de atributos | Mínimo 5 | ✅ 10 atributos |
| Classe-alvo reconhecida | Nominal (Sim/Nao) | ✅ Evasao(Nominal) |
| Atributos numéricos | Reconhecidos corretamente | ✅ 5 atributos |
| Atributos categóricos | Reconhecidos corretamente | ✅ 4 atributos |
| Valores faltantes | Presença confirmada | ✅ Identificados |
| Erros de leitura | Nenhum | ✅ Carregados sem Falhas |

### Base de dados **dataset_evasao_v2.csv.arff**  sendo executada no weka

![image.png](teste-base-dados.png)

## Analise do Resultado

O arquivo **dataset_evasao_v2.csv.arff** foi carregado corretamente no Weka Explorer, sem apresentar erros de leitura ou inconsistências estruturais. Foram identificadas **500 instâncias** e **10 atributos**, atendendo aos requisitos mínimos estabelecidos no projeto. A classe-alvo **Evasao** foi reconhecida como atributo nominal, apresentando duas categorias: **Sim**, com 256 instâncias , e **Nao**, com 244 instâncias, confirmando que o dataset está bem balanceado entre as classes.
Os atributos numéricos Media_Semestral_Notas, Media_Disciplinas_Matriculadas, Frequencia_Pct, Reprovacoes, Participa_Projetos, Recebe_Auxilio, Idade_ingresso, Trabalha, Dia_Matricula foram interpretados corretamente pela ferramenta, permitindo a continuidade da análise exploratória. 

# 2. Análise Estatística dos Atributos

## Objetivo da etapa

Examinar o comportamento estatístico dos atributos acadêmicos e socioeconômicos do **dataset_evasao_v2.csv.arff** , observando distribuições, tendências centrais, dispersões e frequências, a fim de compreender o perfil geral dos estudantes representados no conjunto de dados e identificar possíveis anomalias antes do pré-processamento.

## Analise dos atributos

| Métrica | Objetivo |
| --- | --- |
| Valores mínimos e máximos | Identificar faixas dos atributos |
| Média  | Avaliar tendência central |
| Desvio Padrão | Verificar dispersão |
| Histogramas | Observar distribuição |
| Frequência das categorias | Analisar atributos nominais |

## Principais atributos a serem analisados

- Media_Semestral_Notas
- Media_Disciplinas_Matriculadas
- Frequencia_Pct
- Reprovacoes
- Participa_Projetos
- Recebe_Auxilio
- Idade_Ingresso
- Trabalha
- Dia_Matricula

### Media_Semestral_Notas

![image.png](attachment:956aa459-6583-4b16-bfc0-1e0980c3d11f:image.png)

## Interpretação

O atributo  **Media_Semestral_Notas** é do tipo **Numérico**, com **25 valores faltantes (5%)** e 80 valores distintos. As estatísticas exibidas pelo Weka apontam mínimo de **0**, máximo de **10**, média de **5,568** e desvio padrão de **3,377**. O histograma apresenta uma distribuição bimodal — há uma concentração de instâncias nos extremos, com alunos de notas muito baixas (0 a 2) associados predominantemente à classe Sim (evasão, em vermelho), e alunos de notas altas (8 a 10) associados à classe Nao (em azul). Essa separação clara entre as classes indica que a média semestral de notas é um dos atributos de maior poder preditivo para a evasão.

### Media_Disciplinas_Matriculadas

![image.png](attachment:e1273b86-ba03-47d8-a1a7-ce219e2cf544:image.png)

## Interpretação

O atributo **Media_Disciplinas_Matriculadas** é do tipo **Numérico**, sem valores faltantes (0%), com 8 valores distintos. O Weka exibe mínimo de **1**, máximo de **8**, média de **4,564** e desvio padrão de **2,295**. O histograma mostra que a maior concentração de instâncias está na faixa de 1 a 2 disciplinas, com forte presença da classe Nao (azul), sugerindo que alunos com menor carga matriculada tendem a permanecer. Nas faixas intermediárias (3 a 5) há maior mistura entre as classes, e nas faixas mais altas (6 a 8) observa-se leve predominância da classe Sim (evasão).

### Frequencia_Pct

![image.png](attachment:929c07d6-9ea8-483c-b843-89c00dbf5ff0:image.png)

## Interpretação

O atributo **Frequencia_Pct**  é do tipo **Numérico**, sem valores faltantes (0%), com 63 valores distintos. As estatísticas mostram mínimo de **-13**, máximo de **100**, média de **75,016** e desvio padrão de **21,184**. O valor mínimo negativo (-13) é fisicamente impossível para uma porcentagem de frequência e representa um **outlier intencional** inserido no dataset. No histograma, é possível observar barras isoladas à esquerda do zero, separadas da distribuição principal — evidência clara da presença desses outliers. A maior concentração de instâncias está na faixa de 75% a 100%, com predominância da classe Nao (azul), enquanto frequências mais baixas concentram a classe Sim (evasão).

### Reprovacoes

![image.png](attachment:0623cf19-214b-42b6-b881-b7c2db9a45ce:image.png)

## Interpretação

O atributo **Reprovacoes** é do tipo **Numérico**, sem valores faltantes (0%), com 7 valores distintos. O Weka exibe mínimo de **0**, máximo de **7**, média de **2,284** e desvio padrão de **2,492**. O histograma apresenta assimetria acentuada à esquerda — a barra de 0 reprovações concentra 246 instâncias, com forte predominância da classe Sim (evasão, em vermelho), o que inicialmente pode parecer contraditório, mas reflete que parte dos evadidos saiu antes de acumular reprovações. Nas faixas de 3 a 7 reprovações há maior presença da classe Nao (azul), indicando alunos que permaneceram mesmo com dificuldades.

### Participa_Projetos

![image.png](attachment:51f33751-edf4-496c-b05a-bc1d53e5517e:image.png)

## Interpretação

O atributo **Participa_Projetos** é do tipo **Nominal**, sem valores faltantes (0%), com 2 categorias distintas. A distribuição apresenta **Sim** com 375 instâncias e **Nao** com 125 instâncias. No histograma, a barra de quem participa (Sim, 375) mostra proporção equilibrada entre as duas classes de evasão, com leve predominância vermelha. Já a barra de quem não participa (Nao, 125) apresenta maior presença da classe Sim de evasão, sugerindo que a não participação em projetos acadêmicos está associada a maior risco de evasão.

### Recebe_Auxilio

![image.png](attachment:987dc01c-53eb-49a8-afea-360fc7b24442:image.png)

## Interpretação

O atributo **Recebe_Auxilio** é do tipo **Nominal**, sem valores faltantes (0%), com 2 categorias. A distribuição apresenta **Nao** com 302 instâncias e **Sim** com 198 instâncias. O histograma revela um padrão interessante: entre os que **não recebem auxílio** (302), há grande proporção da classe Sim (evasão, vermelho), enquanto entre os que **recebem auxílio** (198) a proporção de evasão é ainda maior em termos relativos, o que pode indicar que alunos em situação de vulnerabilidade econômica buscam auxílio justamente por estarem em risco.

### Idade_Ingresso

![image.png](attachment:2dd04e68-1bba-4321-8f14-11a79098cd3d:image.png)

## Interpretação

O atributo **Idade_Ingresso** é do tipo **Numérico**, com **24 valores faltantes (5%)** e 32 valores distintos. As estatísticas exibem mínimo de **17**, máximo de **90**, média de **32,013** e desvio padrão de **11,241**. O histograma mostra que a grande maioria das instâncias se concentra na faixa de 17 a 45 anos, com distribuição decrescente. Há uma barra isolada no extremo direito próxima ao valor 90, com apenas 9 e 1 instâncias — caracterizando um **outlier extremo intencional**, pois 90 anos é uma idade implausível para ingresso em graduação. Pelo critério IQR, idades acima de aproximadamente 61 anos são estatisticamente discrepantes e devem ser avaliadas no pré-processamento.

### Trabalha

![image.png](attachment:de21e191-98ba-437e-99c1-9874f87f04c0:image.png)

## Interpretação

O atributo **Trabalha** é do tipo **Nominal**, sem valores faltantes (0%), com 2 categorias. A distribuição apresenta **Sim** com 388 instâncias e **Nao** com 112 instâncias. O histograma evidencia que a grande maioria dos estudantes trabalha (388), e nesse grupo há proporção praticamente igual entre as classes de evasão. Entre os que não trabalham (112), observa-se predominância quase total da classe Sim (evasão, vermelho), o que é um achado relevante — pode indicar que alunos sem vínculo empregatício possuem outros fatores de risco mais determinantes.

### Dia_Matricula

![image.png](attachment:d80cb4ce-37d7-46c2-b19b-5e4da3e4a777:image.png)

****

## Interpretação

O atributo **Dia_Matricula** é do tipo **Nominal**, sem valores faltantes (0%), com **5 categorias distintas**: Quinta (92), Sexta (113), Terça (102), Quarta (91) e Segunda (102). O histograma mostra barras de alturas semelhantes para todos os dias da semana, e em cada barra a proporção entre as classes Sim e Nao de evasão é praticamente idêntica. Esse comportamento confirma que o dia da matrícula **não possui qualquer relação com a evasão**, validando-o como o **atributo irrelevante intencional** do dataset, que deverá ser removido no pré-processamento.

# **3. Avaliação da Classe-Alvo**

## Objetivo da etapa

Verificar a distribuição da variável de evasão e identificar possíveis desbalanceamentos entre as classes.

## Distribuição de classe

| Classe  | Quantidade  |
| --- | --- |
| Sim | 256 |
| Não | 244 |

A classe **Sim** apresentou quantidade ligeiramente superior à classe **Nao, com** diferença de apenas 12 instâncias entre elas. O dataset pode ser considerado **bem balanceado**, não caracterizando desbalanceamento relevante entre as classes.

## Possíveis impactos

| Situação Observada | Impacto Esperado |
| --- | --- |
| Classe perfeitamente equilibradas | Classificadores não serão tendenciosos por maioria |
| Sem necessidade de balanceamento | Filtros como Spread Subsample não serão necessários |

## Observação importante

Mesmo com o dataset balanceado, como o problema envolve a identificação precoce de alunos com risco de evasão, métricas como **Recall** e **F1-Score** continuam sendo mais relevantes do que apenas a acurácia, visto que é preferível errar identificando um aluno que não iria evadir do que deixar passar despercebido um aluno que efetivamente abandonaria o curso.

# 4. Verificação de Anomalias Intencionais do Dataset

## Objetivo da etapa

Esta etapa confirma se os elementos planejados durante a geração do dataset — valores faltantes, ruídos e outliers — foram corretamente inseridos e reconhecidos pelo Weka.

## Análise Feita

| Atributo | Elemento Verificado | O que observar no Weka | O que foi encontrado | Conclusão |
| --- | --- | --- | --- | --- |
| Medias_Semestrais_Notas | Valores faltantes | faltantesCampo **Missing** > 0 | 25 valores faltantes (5%) | Valores faltantes confirmados |
| Idade_Ingresso | Valores faltantes | Campo **Missing** > 0 | 24 valores faltantes (5%) | Valores faltantes confirmados |
| Frequencia_Pct | Ruído intencional | Campo **Minimum** negativo | Mínimo = **13** |  Ruído confirmado - frequência negativa é impossível |
| Idade_Ingresso | Outlier extremo | Campo **Maximum** elevado | Máximo = **90** |  Outlier confirmado - idade implausível para graduação |

## Observação

Os dados revelaram perfis acadêmicos bastante distintos entre os estudantes. Os atributos de desempenho acadêmico  **Media_Semestral**, **Frequencia_Pct** e **Reprovacoes** apresentaram maior potencial preditivo sobre a evasão, com separação visível entre as classes nos histogramas. Fatores socioeconômicos como **Recebe_Auxilio** e **Trabalha** também demonstraram padrões relevantes, sugerindo que condições externas influenciam na permanência do estudante. O atributo **Dia_Matricula** confirmou-se irrelevante, sem qualquer relação com a evasão, e deverá ser removido no pré-processamento.

# 5. Análise dos valores ausentes

## Objetivo da etapa

Identificar atributos com dados faltantes e avaliar os possíveis impactos no treinamento dos modelos de classificação.

## Atributos com valores ausentes

### Media_Semestral_Notas

![image.png](attachment:7e6ff2f3-b8a5-46cc-8534-a0349e991d78:image.png)

### Idade_Ingressos

![image.png](attachment:4b22a3ee-35d4-4ef1-8944-e0715655b715:image.png)

| **Atributo**  | **Quantidade** | **Percentual** |
| --- | --- | --- |
| Media_Semestral_Notas | 25 | 5% |
| Idade_Ingressos | 24 | 5% |
| Demais Atributos  | 0 | 0 |

Os valores ausentes foram distribuídos de forma controlada nos atributos **Media_Semestral_Notas** e **Idade_Ingressos**, simulando de maneira realista a incompletude comum em registros acadêmicos de instituições públicas. Apesar de representarem uma proporção pequena do total, esses atributos possuem relevância direta para a predição da evasão, sendo necessário o tratamento adequado antes da etapa de modelagem.

## Tratamento sugerido

| Atributo | Tipo | Estratégia | Jusitificativa |
| --- | --- | --- | --- |
| Media_Semestral_Notas | Numérico | Substituição pela média | Média de 5,568 é representativa da distribuição |
| Idade_Ingresso | Numérico | Substituição pela mediana | Outliers extremos (máx = 90) tornam a mediana mais robusta |

É recomendado fazer uma filtragem com ReplaceMissingValues para ser aplicado na etapa de pre-processamento

# 6. Identificação de ruídos e inconsistências

## Objetivo da etapa

Verificar a presença de padrões incomuns ou valores inconsistentes nos registros do dataset que possam comprometer o treinamento dos modelos.

### Frequencia_Pct

![image.png](attachment:90be9d1d-e753-4320-a7e9-248e6dd8f99a:image.png)

## Interpretação

O principal ruído identificado está no atributo **Frequencia_Pct**, que apresenta valores negativos como -**13**, fisicamente impossíveis para uma porcentagem de frequência. Esses registros foram inseridos intencionalmente para simular erros de digitação comuns em sistemas acadêmicos reais. Apesar de representarem uma pequena parcela dos dados, podem distorcer estatísticas e enviesar os modelos, sendo necessário seu tratamento no pré-processamento.

# 7. Identificação dos outliers

## Objetivo da etapa

Identificar registros com valores extremos e avaliar sua relevância para o problema de predição de evasão, utilizando o critério da Amplitude Interquartil (IQR).

## Método utilizado -  Critério IQR (Amplitude Interquartil)

O método IQR é uma técnica estatística que define os limites aceitáveis para os valores de um atributo. Qualquer valor fora desses limites é considerado um outlier.
 

| Conceito | Descrição |
| --- | --- |
| Q1 | Valor que separa os 25% menores dados |
| Q3 | Valor que separa os 75% menores dados |
| IQR | Diferença entre Q3 e Q1 |
| Limite Inferior | Q1 − 1,5 × IQR — valores abaixo disso são outliers |
| Limite Superior | Q3 + 1,5 × IQR — valores acima disso são outliers |

### Frequencia_Pct

![image.png](attachment:2b194acf-8e1a-4ab1-9670-58fa72917e4e:image.png)

### Idade_Ingresso

![image.png](attachment:e39416aa-148f-490f-9c6f-a28e16b7261b:image.png)

## Outliers Observados

| **Atributo** | **Q1** | **Q3** | **IQR** | **Limite** | **Valor Extremo Econtrado** | **Interpretação** |
| --- | --- | --- | --- | --- | --- | --- |
| Frequencia_Pct | 57 | 92 | 35 | < 4,5 | -13 | Frequência negativa — impossível e intencional |
| Idade_Ingresso | 24 | 39 | 15 | > 61 | 90 | Idade implausível para ingresso na graduação |

## Interpretação

Os outliers identificados foram inseridos intencionalmente no dataset para simular situações de inconsistência real em registros acadêmicos. O valor de -13 em **Frequencia_Pct** representa um erro de registro evidente, enquanto a idade de 90 anos em **Idade_Ingresso** caracteriza um outlier extremo incompatível com o perfil esperado de um estudante de graduação. Ambos deverão ser avaliados e tratados na etapa de pré-processamento — seja por remoção ou substituição — com a devida justificativa metodológica.

# 8. Relação entre os atributos

## Objetivo da etapa

Analisar visualmente as relações entre os atributos acadêmicos e a variável de evasão, identificando padrões que orientem a escolha dos algoritmos.

### Media_Semestral_Notas x Evasao

![image.png](attachment:68e668b1-6324-4a1c-824b-8c91c4d471b5:image.png)

### Frequencia_Pct x Reprovacoes

![image.png](attachment:4adce875-dc3f-497f-97f4-052b12046f52:image.png)

### Media_Semestral_Notas x Reprovacoes

![image.png](attachment:d4214cc6-90c6-4bfb-b8ee-efb55ab503ac:image.png)

### Dia_Matricula x Evasao

![image.png](attachment:95b97a2b-118f-4aca-9011-dfb3f1dd430c:image.png)

## Relações Observadas

| Relação | Comportamento esperado | Comportamento Esperado |
| --- | --- | --- |
| Media_Semestral_Notas x Evasao | Alunos com notas baixas tendem a evadir mais. | Concentração de evasão (Sim) em notas de 0 a 2 e permanência (Nao) em notas de 8 a 10. |
| Frequencia_Pct x Reprovacoes | Menor frequência associada a maior número de reprovações. | Frequências baixas (abaixo de 75%) correlacionam-se com o aumento das reprovações e evasão. |
| Media_Semestral_Notas x Reprovacoes | Notas baixas acompanhadas de alto índice de reprovações. | Alunos com média próxima a zero concentram-se na classe de evasão, mesmo sem acumular muitas reprovações. |
| Dia_Matricula x Evasao | Nenhuma correlação significativa. | Distribuição uniforme das classes em todos os dias da semana. |

## Interpretação

Os padrões observados apresentaram total coerência com o domínio educacional, validando as hipóteses iniciais do projeto. Atributos como **Media_Semestral_Notas**, **Frequencia_Pct** e **Reprovacoes** demonstraram uma separação visual nítida entre as classes de evasão, o que confirma o alto potencial preditivo dessas variáveis para os algoritmos de classificação. A análise sugere que o baixo rendimento acadêmico e a infrequência são indicadores precoces de abandono, permitindo uma intervenção preventiva.

# 9. Avaliação de atributos irrelevantes

## Objetivo da etapa

Identificar atributos sem relação direta com a evasão acadêmica que possam introduzir ruído nos modelos de classificação.

### Dia_Matricula

![image.png](attachment:4c20f2db-5f57-4f52-ae65-54927b037a9e:image.png)

## Atributos analisados

| **Atributo**  | **Tipo** | **Motivo Irrelevância** | **Ação Sugerida** |
| --- | --- | --- | --- |
| Dia_Matricula | Nominal | Distribuição uniforme entre todos os dias — sem relação com evasão | Remover com o filtro **Remove** no weka |

## Interpretação

O atributo **Dia_Matricula** foi inserido intencionalmente como atributo irrelevante, representando uma informação administrativa sem qualquer poder preditivo sobre a evasão. O histograma confirma que a proporção entre as classes Sim e Nao é praticamente idêntica em todos os dias da semana (Quinta: 92, Sexta: 113, Terça: 102, Quarta: 91, Segunda: 102), evidenciando a ausência de relação semântica com o problema. Esse atributo deverá ser removido antes do treinamento dos modelos.

# Considerações finais

## Resultados do Teste Piloto

O teste piloto demonstrou que o **dataset_evasao_v2.csv.arff** está estruturalmente adequado para uso no Weka e apresenta coerência com o problema de predição de evasão acadêmica em cursos de tecnologia. A análise exploratória identificou com precisão:

- Valores faltantes controlados nos atributos **Media_Semestral_Notas** (25) e **Idade_Ingresso**(24);
- Ruído intencional em **Frequencia_Pct**, com valores negativos fisicamente impossíveis;
- *Outliers* identificados em **Frequencia_Pct** e **Idade_Ingresso**, ambos documentados e interpretáveis no contexto educacional;
- Relações coerentes entre os atributos acadêmicos e a variável de evasão.

## **Interpretação**

A conclusão deste teste piloto é que o conjunto de dados possui qualidade suficiente para avançar para as etapas de pré-processamento, treinamento e avaliação dos algoritmos de classificação. A interpretação dos dados reforça que o sucesso dos modelos dependerá de decisões orientadas pelos achados desta análise, como a limpeza dos ruídos em frequência e a remoção de atributos administrativos irrelevantes, garantindo que o aprendizado de máquina foque nos padrões que realmente impactam o fenômeno da evasão.
