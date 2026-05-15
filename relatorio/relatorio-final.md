# Relatório Final: Predição de Evasão em Cursos de Tecnologia de uma Universidade Pública

**Descrição:** Este documento consolida o ciclo completo do processo de Descoberta de Conhecimento em Bancos de Dados (KDD) e Aprendizado de Máquina conduzido neste projeto. Utilizando o software Weka, o estudo aborda a criação de um modelo de Classificação proativo para a identificação precoce de alunos com risco de evasão no ensino superior público. 

---

## Sumário de Navegação
1. [Resumo do Projeto](#1-resumo-do-projeto)
2. [Definição do Problema e Fundamentação](#2-definição-do-problema-e-fundamentação)
3. [Geração de Dataset Sintético](#3-geração-de-dataset-sintético)
4. [Teste Piloto](#4-teste-piloto)
5. [Pré-processamento](#5-pré-processamento)
6. [Visualização de Dados](#6-visualização-de-dados)
7. [Treino e Teste (Modelagem)](#7-treino-e-teste-modelagem)
8. [Conclusão](#8-conclusão)

---

## 1. Resumo do Projeto
A evasão estudantil é um fenômeno crítico que gera prejuízos acadêmicos e socioeconômicos. Em vez de medir o abandono de forma reativa, este trabalho propõe a modelagem de uma tarefa de **Classificação Binária** para prever se um aluno evadirá (*Sim* ou *Não*) com base em seu comportamento no primeiro ano. Para a execução experimental, gerou-se de forma controlada via Inteligência Artificial uma base sintética realista contendo mais de 500 registros, submetida posteriormente a rigorosos testes, limpezas e validações com os algoritmos J48, Random Forest, Naive Bayes e k-NN no Weka.

---

## 2. Definição do Problema e Fundamentação
A formulação da nossa tarefa preditiva não foi definida de forma aleatória. Os atributos mapeados para o estudo englobam três grandes eixos apontados pela literatura de Mineração de Dados Educacionais: **Desempenho Acadêmico** (notas, faltas e reprovações), **Vínculo Institucional** (participação em projetos e recebimento de auxílios) e **Fatores Sociodemográficos** (conciliação com trabalho e idade de ingresso). 
* 🔗 **Para mais detalhes:** Leia a formulação completa em [`1-definicao-problema.md`](./1-definicao-problema.md) e o embasamento teórico em [`2-revisao-literatura.md`](./2-revisao-literatura.md).

---

## 3. Geração de Dataset Sintético
Para testar a capacidade de generalização dos modelos, construímos uma base rastreável via LLM que superou as exigências mínimas da disciplina. O dataset gerado via código Python (`pandas` e `random`) contém mais de 500 instâncias distribuídas em 4 perfis comportamentais humanos (incluindo "resiliência" e "fatores externos") para evitar o *overfitting* absoluto. Foram injetados propositalmente atributos irrelevantes (`Dia_Matricula`), *missing values*, *outliers* de idade e ruídos (frequências negativas).
* **Para mais detalhes:** Acompanhe a evolução lógica em [`../prompts/prompts_utilizados.txt`](../prompts/prompts.txttxt) Descrição completa em [`Descrição Dataset`](/dataset/descricao-dataset-original.md).


---

## 4. Teste Piloto
Antes de aplicarmos tratamentos mecânicos aos dados, realizamos uma análise exploratória inicial. Utilizamos o ambiente *Preprocess* do Weka diretamente nos dados brutos para investigar as distribuições das variáveis, confirmar a presença das inconsistências criadas no passo anterior e levantar hipóteses sobre como o ruído e os nulos impactariam o aprendizado do algoritmo.
* **Para mais detalhes:** Verifique nossas análises prévias em [`../analise-piloto/analise.md`](../analise-piloto/analise.md).

---

## 5. Pré-processamento
Nesta fase técnica, seguimos o princípio de que a qualidade da saída depende da entrada (*Garbage in, Garbage out*). Justificamos e aplicamos limpezas para o tratamento de valores faltantes (utilizando o filtro não supervisionado `ReplaceMissingValues` do Weka) e realizamos o controle das anomalias observadas no Teste Piloto para garantir a execução correta de classificadores mais sensíveis matematicamente, como o k-NN.
* **Para mais detalhes:** Leia a documentação técnica dos filtros em [`../preprocessamento/descricao_etapas.md`](../preprocessamento/descricao_etapas.md) e o suporte em [`../preprocessamento/analise_inicial.md`](../preprocessamento/analise_inicial.md).
* **Acesso à base tratada:** [`../dataset/dataset_preprocessado.arff`](../dataset/dataset-preprocessado.arff).

---

## 6. Visualização de Dados
Após a limpeza, os gráficos nativos do Weka foram utilizados de forma interpretativa para entender a dinâmica das classes. A visualização serviu como apoio analítico, permitindo enxergar as delimitações entre alunos evasores e regulares, o que ajudou a antecipar o peso de atributos decisivos (como o percentual de frequência) para os nós principais da Árvore de Decisão.
* **Para mais detalhes:** Acesse as interpretações em [`./3-descricao-visual-dados.md`](./3-descricao-visual-dados.md) e visualize os resultados extraídos em [`../imagens/visualizacoes/`](../imagens/visualizacoes/).

---

## 7. Treino e Teste (Modelagem)
A avaliação experimental submeteu a base limpa a 4 algoritmos clássicos de classificação: Árvore de Decisão (J48), Random Forest, k-NN (IBk) e Naive Bayes. Adotamos como padrão de avaliação a Validação Cruzada Estratificada (*10-fold cross-validation*). 

**Resultados Gerais:** A engenharia de dados sintéticos obteve grande sucesso, com a acurácia dos modelos oscilando entre os níveis realistas de ~77% a ~89%, provando que curamos o *overfitting* de 100%. Os algoritmos **Random Forest** e **J48** tiveram o maior destaque, alcançando altas taxas de *Recall* (Sensibilidade), métrica prioritária para o nosso objetivo, visto que no contexto universitário prezar pela identificação máxima da classe de "Evasão = Sim" é preferível a deixar que alunos em risco passem despercebidos.
* **Para mais detalhes:** Acesse a descrição completa, as Matrizes de Confusão e prints comprobatórios do Weka em [`Descrição da modelagem`](./4-modelagem-analises.md).

---

## 8. Conclusão
O projeto demonstrou na prática a viabilidade de aplicar o ciclo KDD para antever a evasão universitária. A construção detalhada do dataset sintético mostrou-se essencial para submeter os modelos a desafios do mundo real (ruídos, resiliência discente, fatores ausentes). As análises confirmaram que variáveis de desempenho acadêmico e condições sociodemográficas são cruciais, e o sistema preditivo — embasado nos algoritmos de árvores — apresentou excelente capacidade de soar o alerta preventivo, oferecendo um suporte valioso à gestão escolar para retenção de alunos.
