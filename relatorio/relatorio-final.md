# 🎓 Relatório Executivo Final: Predição de Evasão Universitária

> **Resumo:** Este documento sintetiza o ciclo completo do processo de Descoberta de Conhecimento em Bancos de Dados (KDD) executado neste projeto, desde a definição do problema até a aplicação de técnicas de Machine Learning. Utilize os links em cada seção para explorar os artefatos detalhados em nosso repositório [1].

---

## 1. Definição do Problema e Fundamentação
O projeto visa solucionar um problema crítico e global: a alta taxa de evasão em cursos de tecnologia no ensino superior público [3]. Atuando de forma proativa, nosso objetivo é prever alunos com propensão ao abandono escolar através da tarefa de **Classificação Binária** (Evasão: *Sim/Não*) [3]. 

A escolha dos nossos atributos (como frequência, reprovações, vínculos institucionais e condições sociodemográficas) bem como os algoritmos a serem aplicados foram fundamentados em uma rigorosa revisão sistemática da literatura de Mineração de Dados Educacionais [2, 3].
* 🔗 **Aprofunde-se:** [Leia a Definição Completa do Problema](1-definicao-problema.md) | [Veja a Revisão de Literatura](2-revisao-literatura.md)

---

## 2. Geração de Dataset Sintético
Para testar nossos modelos sem os vieses comuns de *overfitting* absoluto (onde a IA apenas "decora" o resultado), nosso conjunto de dados foi inteiramente projetado via Modelos de Linguagem (LLMs) gerando um script em Python [2]. 

A base final possui mais de 500 instâncias e atende a todos os requisitos da disciplina, incorporando perfis humanos complexos (como "resiliência"), além da presença intencional de *outliers* de idade, instâncias com ruído (frequências negativas) e um atributo irrelevante proposital (`Dia_Matricula`) [2, 3].
* 🔗 **Aprofunde-se:** [Explore o Histórico de Prompts](../prompts/prompts_utilizados.txt) | [Veja o Pipeline de Geração (Imagem)](../imagens/pipeline_geracao.png)
* 💾 **Acesso aos Dados:** [Baixe o Dataset Original (.arff)](../dataset/dataset_original.arff)

---

## 3. Teste Piloto e Análise Exploratória
Antes de aplicar qualquer filtro mecanicamente, conduzimos uma análise exploratória dos dados brutos no ambiente do Weka [2]. Esta etapa foi crucial para validarmos estatisticamente as inconsistências, verificarmos a distribuição das classes (Evasão Sim/Nao) e levantarmos as hipóteses de impacto dos ruídos no aprendizado da máquina, comprovando a eficácia da geração sintética [2].
* 🔗 **Aprofunde-se:** [Acesse a Documentação do Teste Piloto](../analise-piloto/analise.md)

---

## 4. Pré-processamento
A etapa de limpeza seguiu as melhores práticas da mineração de dados (*Garbage in, Garbage out*) [3]. Os valores faltantes (*missing values*) gerados propositalmente na etapa de criação foram contornados através de ferramentas internas do Weka, aplicando o filtro não supervisionado `ReplaceMissingValues` e ajustando os ruídos de modo justificado para possibilitar a execução de classificadores sensíveis [2, 3].
* 🔗 **Aprofunde-se:** [Veja a Descrição das Etapas de Pré-processamento](../preprocessamento/descricao_etapas.md) | [Confira também nossa Análise Inicial](../preprocessamento/analise_inicial.md)
* 💾 **Acesso aos Dados:** [Baixe o Dataset Pré-processado (.arff)](../dataset/dataset_preprocessado.arff)

---

## 5. Visualização de Dados
Utilizamos os recursos visuais do Weka no pós-processamento como ferramentas analíticas para compreender as separações entre as classes e como cada atributo se relaciona com o abandono do curso [2]. Essas representações gráficas guiaram a compreensão do poder de discriminação de atributos vitais (como `Frequencia_Pct` e notas) e nortearam as escolhas para a fase de modelagem [2].
* 🔗 **Aprofunde-se:** [Acesse as Imagens de Visualização no Weka](../imagens/visualizacoes/)

---

## 6. Treino e Teste (Modelagem)

> 🚧 **STATUS: EM DESENVOLVIMENTO** 🚧  
> *A execução experimental dos classificadores e a validação estão sendo conduzidas no Weka. Esta seção será atualizada com as análises das matrizes de confusão, métricas de Acurácia e Recall e ajuste de hiperparâmetros (como o número k do k-NN) para os algoritmos definidos (Árvore de Decisão, Naive Bayes, k-NN e Random Forest) [2, 3].*

<!-- 
ESPAÇO RESERVADO PARA FUTURA ATUALIZAÇÃO 
Aqui entrarão:
1. A justificativa do uso da Validação Cruzada (Cross-validation).
2. A Tabela Comparativa de resultados (Acurácia, Precisão, Recall e F-Measure).
3. A análise da Matriz de Confusão com as evidências de acerto e erro de cada perfil.
4. Links para os prints comprobatórios do Weka em: ../imagens/prints_weka/
-->

