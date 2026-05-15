# Analise_Inicial

# Análise Inicial e Seleção de Filtros

Este documento apresenta o processo de análise inicial do dataset **dataset_evasao_v2.csv.arff** e o raciocínio técnico utilizado para selecionar os filtros de pré-processamento aplicados no Weka.

A etapa de pré-processamento é indispensável em projetos de Machine Learning, pois dados com inconsistências, valores ausentes ou atributos irrelevantes comprometem diretamente a capacidade dos algoritmos de identificar padrões significativos. Como estudado em sala de aula, o princípio do **"Garbage in, Garbage out"** reforça que a qualidade dos dados de entrada é determinante para a qualidade dos modelos gerados.

Antes da aplicação dos filtros, foi realizada uma análise exploratória do dataset (documentada em analise-piloto.md) com o objetivo de identificar:

- presença de valores faltantes
- existência de outliers e ruídos intencionais
- atributos sem poder preditivo sobre a evasão
- variáveis contínuas que se beneficiariam de discretização

Com base nesses achados, foram definidos os filtros descritos a seguir.

> Os filtros foram aplicados nesta ordem para garantir que cada etapa opere sobre dados já estabilizados pelas anteriores, evitando conflitos de índice entre atributos.
> 

# 1. Tratamento de Valores Faltantes (ReplaceMissingValues)

## **Problema Identificado**

Durante o teste piloto, foram identificados **49 valores faltantes** distribuídos em dois atributos:

- **Media_Semestral_Notas** — 25 valores ausentes (5%)
- **Idade_ingresso** — 24 valores ausentes (5%)

A presença de valores **?** pode causar:

- falha na execução de algoritmos como k-NN e Naive Bayes
- geração de vieses estatísticos durante o treinamento
- perda de instâncias caso fossem removidas manualmente

### Solução Aplicada

```html
weka.filters.unsupervised.attribute.ReplaceMissingValues
```

O filtro substitui automaticamente os valores ausentes pela **média do atributo** para variáveis numéricas, preservando todas as instâncias do dataset.

### Impacto no Dataset

- Campo **Missing** zerado em todos os atributos
- Todas as 500 instâncias preservadas
- Dataset compatível com todos os algoritmos de classificação

# 2. Substituição de Outliers Negativos (MathExpression)

## Problema Identificado

O atributo **Frequencia_Pct** apresentou **8 instâncias com valores negativos**, sendo o mínimo registrado de **-13**. Uma porcentagem de frequência negativa é fisicamente impossível, caracterizando um ruído intencional inserido no dataset para simular erros de digitação comuns em sistemas acadêmicos reais.

Esses valores poderiam:

- distorcer a média e o desvio padrão do atributo
- introduzir padrões falsos nos classificadores
- comprometer a consistência semântica dos dados

### Solução Aplicada

```html
weka.filters.unsupervised.attribute.MathExpression
```

com a expressão:

**ifelse(A < 0, 0, A)**

Essa expressão substitui qualquer valor negativo por **0**, preservando as instâncias no dataset.

### Impacto no Dataset

- Valor mínimo de **Frequencia_Pct** passou de **13 para 0**
- Nenhuma instância foi removida
- Distribuição do atributo corrigida e semanticamente válida

# 3. Marcação de Idades Implausíveis (NumericCleaner)

## Problema Identificado

O atributo **Idade_Ingresso** apresentou **~10 instâncias acima de 61,5 anos**, incluindo o outlier extremo de **90 anos**. Pelo critério IQR calculado no teste piloto (Q1=24, Q3=39, IQR=15, limite superior=61,5), essas idades são estatisticamente discrepantes e semanticamente implausíveis para ingresso em graduação.

Esses registros poderiam:

- enviesar modelos baseados em distância como o k-NN
- distorcer a média do atributo após o **ReplaceMissingValues**
- introduzir perfis de estudantes inexistentes na realidade

### Solução Aplicada

```html
weka.filters.unsupervised.attribute.NumericCleaner
```

com os parâmetros:

- **attributeIndices: 7**
- **maxThreshold:** **61.5**
- **maxDefault:** **NaN**

O filtro marca como **missing** todas as idades acima de 61,5 anos, preparando essas instâncias para remoção na etapa seguinte.

### Impacto no Dataset

- Instâncias com idade acima de 61,5 anos marcadas como **?**
- Dataset preparado para remoção direcionada pelo próximo filtro

# 4. Remoção de Instâncias com Missing (RemoveWithValues)

## Problema Identificado

Após a aplicação do **NumericCleaner**, as instâncias com idades implausíveis foram marcadas como **?** no atributo **Idade_Ingresso** e precisam ser eliminadas do dataset.

### Solução Aplicada

```html
weka.filters.unsupervised.instance.RemoveWithValues
```

com os parâmetros:

- **attributeIndex:** **7**
- **matchMissingValues:** **True**

O filtro remove todas as instâncias que possuem valor missing no atributo **Idade_Ingresso**.

### Impacto no Dataset

- Total de instâncias reduzido de **500 para ~490**
- Outliers extremos de idade eliminados
- Dataset semanticamente consistente com o perfil real de estudantes

# 5. Remoção de Atributo Irrelevante (Remove)

## Problema Identificado

O atributo **Dia_Matricula** foi confirmado no teste piloto como **irrelevante** para a predição da evasão. Sua distribuição de classes era praticamente idêntica em todos os dias da semana (Quinta: 92, Sexta: 113, Terça: 102, Quarta: 91, Segunda: 102), sem qualquer separação entre evadidos e não evadidos.

Manter esse atributo poderia:

- introduzir ruído desnecessário nos modelos
- aumentar a complexidade sem ganho preditivo
- prejudicar a interpretabilidade dos classificadores

### Solução Aplicada

```html
weka.filters.unsupervised.attribute.Remove
```

com o parâmetro:

- **attributeIndices:** **9**

O filtro é aplicado após os tratamentos de outliers para evitar deslocamento de índices.

### Impacto no Dataset

- Número de atributos reduzido de **10 para 9**
- Modelos focados apenas em atributos com relevância acadêmica
- Redução do risco de aprendizado de padrões espúrios

# 6. Discretização de Variável Contínua (Discretize)

## Problema Identificado

O atributo **Idade_Ingresso**, mesmo após a remoção dos outliers, é uma variável numérica contínua com ampla faixa de valores. Algoritmos como Árvore de Decisão e Naive Bayes trabalham melhor com variáveis categóricas quando os dados possuem agrupamentos naturais.

Além disso, o conceito de faixa etária é mais interpretável do ponto de vista pedagógico do que um valor numérico isolado.

### Solução Aplicada

```html
weka.filters.unsupervised.attribute.Discretize
```

com os parâmetros:

- **attributeIndices:** **7**
- **bins:** **4**
- **useEqualFrequency:** **False**

O filtro transforma **Idade_Ingresso** em **4 faixas etárias** geradas automaticamente pelo Weka. Este é o **filtro extra não explorado em sala de aula**, exigido pelo enunciado do trabalho.

### Impacto no Dataset

- **Idade_Ingresso** convertida de **numérico para nominal**
- 4 faixas etárias criadas automaticamente
- Interpretabilidade dos modelos aprimorada
- Compatibilidade ampliada com Naive Bayes e Árvore de Decisão

# Resumo dos Filtros Aplicados

| Ordem | Filtro | Atributo | Problema Tratado | Impacto |
| --- | --- | --- | --- | --- |
| 1º | **ReplaceMissingValues** | **Media_Semestral_Notas, Idade_Ingresso** | 49 valores faltantes | Missing = 0 em todos os atributos |
| 2º | **MathExpression** | **Frequencia_Pct** | Valores negativos (mín = -13) | Mínimo passou para 0 |
| 3º | **NumericCleaner** | **Idade_Ingresso** | Idades acima de 61,5 anos | Marcadas como missing |
| 4º | **RemoveWithValues** | **Idade_Ingresso** | Instâncias com missing | 500 → ~490 instâncias |
| 5º | **Remove** | **Dia_Matricula** | Atributo irrelevante | 10 → 9 atributos |
| 6º | **Discretize** | **Idade_Ingresso** | Variável contínua | Numérico → Nominal (4 faixas) |

# Conclusão

A análise inicial permitiu identificar com clareza os problemas presentes no dataset e definir uma sequência estruturada de filtros para corrigi-los. Cada decisão foi fundamentada nos achados do teste piloto, garantindo que o pré-processamento fosse conduzido com rigor metodológico e não de forma arbitrária.

Ao final das seis etapas, o dataset **dataset_evasao_v2.arff** passou a estar livre de valores ausentes, sem outliers extremos, sem atributos irrelevantes e com variáveis em formato adequado para os algoritmos de classificação. Essas transformações aumentam a confiabilidade dos modelos gerados e reduzem o risco de aprendizado de padrões espúrios, preparando o conjunto de dados para a etapa de modelagem e avaliação no Weka.
