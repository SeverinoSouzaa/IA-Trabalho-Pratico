# ⚙️ Geração do Dataset Sintético: Rastreabilidade e Evolução

## 1. Objetivo

O objetivo desta etapa é documentar o processo de construção do nosso conjunto de dados sintético utilizando Modelos de Linguagem (LLMs). Como o fenômeno da evasão universitária é complexo, o foco não foi gerar dados aleatórios, mas sim **projetar matematicamente o comportamento humano**. Este documento demonstra a rastreabilidade da geração, garantindo o rigor metodológico exigido para a experimentação científica e evitando que o modelo de Aprendizado de Máquina sofresse de *overfitting* (um sobreajuste irreal onde o algoritmo apenas "decora" regras simples).

---

## 2. Exigências do Enunciado e Critérios Atendidos

A construção deste *dataset* foi estritamente guiada pelas exigências do enunciado do trabalho, garantindo que todos os requisitos obrigatórios fossem cumpridos em nossa base final:

* **Uso de LLMs:** A concepção das lógicas foi feita iterativamente via Inteligência Artificial.
* **Mínimo de 500 instâncias:** Garantido pelo script final gerando exatas 500 linhas.
* **Mínimo de 5 atributos:** Nossa base superou a exigência, contando com **10 atributos**.
* **Atributo Irrelevante Intencional:** Criamos o `Dia_Matricula` (Segunda a Sexta), que não possui correlação causal com a evasão, testando a capacidade do classificador de ignorar ruídos.
* **Valores Faltantes (*Missing Values*):** Inserimos propositalmente o caractere `?` em cerca de 5% dos registros numéricos.
* **Ruído:** Geramos 8 instâncias com frequências contendo valores negativos impossíveis (ex: `-11%`) simulando erros humanos em sistemas acadêmicos.
* **Outliers:** Injetamos idades extremas no ingresso (ex: 82, 85, 90 anos), discrepantes da distribuição principal dos alunos de graduação.

---

## 3. Extração dos Atributos: A Base na Literatura

Nenhum atributo foi escolhido por intuição. Para que a base sintética tivesse validade semântica e coerência com o problema, extraímos os fatores preditivos diretamente da nossa Revisão de Literatura:

* **Desempenho Acadêmico:** Considerado o maior peso para a evasão. Incluímos `Media_Semestral_Notas`, `Media_Disciplinas_Matriculadas`, `Frequencia_Pct` e `Reprovacoes`.
* **Aspectos Sociodemográficos:** Estudantes que precisam conciliar trabalho e estudo (fator de risco). Inserimos `Idade_Ingresso` e `Trabalha` (Sim/Não).
* **Vínculo Institucional:** O apoio e engajamento previnem o abandono. Modelamos com `Recebe_Auxilio` e `Participa_Projetos`.

---

## 4. Histórico de Prompts: Evolução e Justificativas

A base não ficou pronta na primeira tentativa. Conduzimos uma evolução cuidadosa nos *prompts* para calibrar a "ambiguidade" da inteligência artificial, superando limitações técnicas e teóricas.

### Versão 1: O Teste Ingênuo (Problema de Limites e Aleatoriedade)

**Objetivo:** Testar se a IA conseguiria formatar o CSV diretamente no chat baseando-se em intuições simples.

**Problema Encontrado:** Ao pedir as 500 linhas diretamente no chat, a IA esbarrava no limite de *tokens* e interrompia a geração pela metade. Além disso, as regras muito genéricas ("notas baixas = evasão") geravam uma distribuição irreal e aleatória, impedindo que algoritmos como a Árvore de Decisão encontrassem caminhos consistentes.

**Prompt 1 Utilizado:**

```text
Aja como um gerador de dados sintéticos para criar um dataset CSV com 500 instâncias voltado para tarefas de classificação em Machine Learning utilizando o software Weka.
O tema do dataset é evasão universitária em cursos de tecnologia de uma universidade pública.
O cabeçalho do CSV deve ser:
Media_Semestral_Notas,Media_Disciplinas_Matriculadas,Frequencia_Pct,Reprovacoes,Participa_Projetos,Recebe_Auxilio,Idade_Ingresso,Trabalha,Evasao
Regras:
* Alunos com notas baixas, baixa frequência e muitas reprovações devem possuir Evasao = Sim.
* Alunos com notas altas, alta frequência e poucas reprovações devem possuir Evasao = Nao.
* Gere os valores dentro de faixas realistas.
* Participa_Projetos, Recebe_Auxilio e Trabalha devem possuir valores Sim ou Nao.
* Gere dados coerentes para cursos de tecnologia.
* Crie exatamente 500 linhas.
* Gere o resultado diretamente em formato CSV.
```

---

### Versão 2: O Problema do *Overfitting* (Acurácia de 100%)

**Objetivo:** Melhorar a semântica estabelecendo domínios numéricos exatos (notas 0 a 10) e forçando a IA a criar dois grandes grupos ("características clássicas de evasão" vs "permanência").

**Problema Encontrado:** Ao engessar os padrões (ex: quem trabalha e tem nota baixa SEMPRE evade), o *dataset* ficou extremamente determinístico. No Weka, o algoritmo encontrou padrões óbvios e atingiu 100% de acurácia (*overfitting*). No mundo real, a previsibilidade perfeita não existe; a IA havia ignorado o fator da "resiliência humana". A limitação de tokens ao gerar CSV direto continuava sendo um obstáculo.

**Prompt 2 Utilizado:**

```text
Aja como um especialista em geração de dados sintéticos para Machine Learning.
Crie um dataset CSV com exatamente 500 instâncias para tarefas de classificação no Weka com foco na predição de evasão universitária em cursos de tecnologia de uma universidade pública.
Cabeçalho obrigatório:
Media_Semestral_Notas,Media_Disciplinas_Matriculadas,Frequencia_Pct,Reprovacoes,Participa_Projetos,Recebe_Auxilio,Idade_Ingresso,Trabalha,Evasao
Regras dos atributos:
* Media_Semestral_Notas: 0 a 10
* Media_Disciplinas_Matriculadas: 1 a 8
* Frequencia_Pct: 0 a 100
* Reprovacoes: 0 a 7
* Participa_Projetos: Sim/Nao
* Recebe_Auxilio: Sim/Nao
* Idade_Ingresso: 17 a 45
* Trabalha: Sim/Nao
* Evasao: Sim/Nao
Distribuição esperada:
* Parte dos alunos deve possuir características clássicas de evasão:
  * notas baixas
  * baixa frequência
  * muitas reprovações
  * trabalha
  * poucas disciplinas
* Parte dos alunos deve possuir características clássicas de permanência:
  * notas altas
  * alta frequência
  * participação em projetos
  * nenhuma reprovação
IMPORTANTE:
* Nem todos os alunos devem seguir padrões perfeitos.
* Evite gerar um dataset totalmente determinístico.
Gere diretamente o CSV.
```

---

### Versão 3 (Final): Engenharia de Comportamento Humano e Script Python

**Objetivo:** Quebrar a regra determinística inserindo "Falsos Positivos e Falsos Negativos" lógicos. Para resolver o problema técnico da exportação incompleta, mudamos a estratégia e solicitamos à IA que gerasse um **Código Python** em vez do CSV.

**A Solução Magistral:** Dividimos os alunos em 4 Grupos Probabilísticos:

1. **Evasão Clássico (35%)**
2. **Permanência Clássico (35%)**
3. **Resiliência (15%):** Alunos com notas e histórico ruins, mas que NÃO evadem porque recebem auxílio financeiro (bolsas).
4. **Fatores Externos (15%):** Alunos geniais (nota > 8.0, 0 reprovações) que EVADEM da universidade (simulando casos que passaram em outro vestibular).

Além disso, detalhamos todas as exigências acadêmicas do professor (Missing Values, Ruídos e Outliers) e a inclusão do atributo irrelevante `Dia_Matricula`. Ao rodar o script Python gerado pela IA no Google Colab (`pandas` e `random`), obtemos de forma instantânea e integral o arquivo `dataset_evasao_v2.csv`, com uma ambiguidade realista que reduziu a acurácia dos classificadores para parâmetros perfeitamente científicos e defensáveis.

**Prompt 3 Utilizado:**

```text
Aja como um Especialista em Ciência de Dados e Mineração de Dados Educacionais. Sua tarefa é atuar como um gerador de dados sintéticos para criar um dataset em formato CSV (separado por vírgulas) com exatamente 500 instâncias. Este dataset será utilizado no software Weka para treinar modelos de Aprendizado de Máquina (Classificação) focados em prever a "Evasão" de alunos de cursos de tecnologia em uma universidade pública.

REGRAS DE ATRIBUTOS (O cabeçalho do CSV deve ser exatamente este): Media_Semestral_Notas,Media_Disciplinas_Matriculadas,Frequencia_Pct,Reprovacoes,Participa_Projetos,Recebe_Auxilio,Idade_Ingresso,Trabalha,Dia_Matricula,Evasao

DOMÍNIO DOS ATRIBUTOS:
1. Media_Semestral_Notas: Numérico (0.0 a 10.0).
2. Media_Disciplinas_Matriculadas: Numérico (1 a 8). (Reflete o desânimo do aluno. 5 a 8 é o normal do período; 1 a 3 indica que o aluno está pegando poucas matérias).
3. Frequencia_Pct: Numérico (0 a 100).
4. Reprovacoes: Numérico (0 a 7). (Quantidade de reprovações nas disciplinas)
5. Participa_Projetos: Nominal (Sim, Nao).
6. Recebe_Auxilio: Nominal (Sim, Nao). (Auxílio financeiro da universidade).
7. Idade_Ingresso: Numérico (17 a 45).
8. Trabalha: Nominal (Sim, Nao).
9. Dia_Matricula: Nominal (Segunda, Terca, Quarta, Quinta, Sexta) -> Atributo intencionalmente irrelevante gerado de forma totalmente aleatória.
10. Evasao: Nominal (Sim, Nao) -> Classe Alvo.

REGRAS DE DISTRIBUIÇÃO E COMPORTAMENTO (MUITO IMPORTANTE PARA EVITAR OVERFITTING): O dataset não pode ser 100% determinístico. Para simular a realidade, distribua as 500 instâncias nas 4 lógicas abaixo:
* Grupo 1 - Padrão de Evasão Clássico (Aprox. 35% dos dados): Alunos desanimados. Media_Semestral_Notas < 5.0, Media_Disciplinas_Matriculadas entre 1 e 3, Frequencia_Pct < 70%, Reprovacoes >= 3, Trabalha = Sim, Recebe_Auxilio = Nao. Para este grupo, Evasao = Sim.
* Grupo 2 - Padrão de Permanência Clássico (Aprox. 35% dos dados): Alunos engajados. Media_Semestral_Notas >= 7.0, Media_Disciplinas_Matriculadas entre 5 e 8, Frequencia_Pct >= 80%, Reprovacoes = 0, Participa_Projetos = Sim. Para este grupo, Evasao = Nao.
* Grupo 3 - Resiliência (Aprox. 15% dos dados): Alunos com dificuldades, mas que NÃO evadem (geralmente ajudados por bolsas). Media_Semestral_Notas < 5.0, Reprovacoes >= 2, Trabalha = Sim, MAS Recebe_Auxilio = Sim e Evasao = Nao. (Simula alunos persistentes).
* Grupo 4 - Fatores Externos (Aprox. 15% dos dados): Alunos excelentes que EVADEM. Media_Semestral_Notas > 8.0, Media_Disciplinas_Matriculadas entre 5 e 8, Frequencia_Pct > 90%, Reprovacoes = 0, Participa_Projetos = Sim, MAS Evasao = Sim. (Simula alunos que mudaram de curso ou passaram em outro vestibular).

ANOMALIAS OBRIGATÓRIAS (Para cumprir exigências acadêmicas):
1. Missing Values: Insira o caractere "?" em cerca de 5% dos dados nos atributos Idade_Ingresso e Media_Semestral_Notas.
2. Ruído: Crie 8 instâncias onde a Frequencia_Pct receba valores negativos impossíveis (ex: -10, -5).
3. Outliers: Crie 10 instâncias onde a Idade_Ingresso seja extrema e distante da distribuição principal (ex: 82, 85, 90).

INSTRUÇÃO DE SAÍDA: Como 500 linhas excedem o limite de resposta, por favor, gere um código em linguagem Python completo e pronto para uso, utilizando as bibliotecas pandas e random. O código deve conter perfeitamente as lógicas de probabilidades, pesos e regras dos Grupos 1, 2, 3 e 4 e das Anomalias descritas acima. Ao ser executado, o script deve salvar automaticamente um arquivo chamado "dataset_evasao_v2.csv". Não gere as linhas agora, apenas me entregue o código Python.
```

---

## 5. Fluxo de Geração / Pipeline

Esta etapa representa visualmente o fluxo completo de desenvolvimento do *dataset* sintético, desde a concepção teórica baseada na literatura até a geração automatizada do arquivo final utilizado no Weka. O pipeline demonstra a sequência metodológica adotada para garantir coerência semântica, rastreabilidade, controle de qualidade e realismo estatístico no conjunto de dados.

![alt text](../imagens/pipeline-geracao.png)