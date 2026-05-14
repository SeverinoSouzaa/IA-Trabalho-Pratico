## Predição de evasão em cursos de tecnologia de uma universidade pública: Uma abordagem baseada em Machine Learning e Classificação.

> **Descrição:** Este repositório documenta o ciclo completo de Descoberta de Conhecimento em Bancos de Dados (KDD) e Aprendizado de Máquina aplicado à educação. Utilizando o software **Weka 3.8**, o projeto cria e analisa um conjunto de dados sintético gerado por Inteligência Artificial para identificar precocemente perfis de alunos com risco de evasão em universidades públicas brasileiras. Projeto desenvolvido para a disciplina de Inteligência Artificial do Instituto de Ciências Exatas e Tecnologia da Universidade Federal do Amazonas (UFAM) ministrada pelo Prof. Dr. Andrey Rodrigues.

---

## Equipe Desenvolvedora

| Nome do Membro | Perfil GitHub | Função/Contribuição Principal |
| :--- | :--- | :--- |
| **Ana Clarissy** | [@usuario1](https://github.com/) | Teste Piloto |
| **Felipe Aliel** | [@usuario2](https://github.com/) | Teste Piloto |
| **Luan Serrão** | [luanzito21](https://github.com/luanzito21) | ? |
| **Luis Rauber** | [luisrauber](https://github.com/luisrauber) | ? |
| **Severino Souza** | [SeverinoSouzaa](https://github.com/SeverinoSouzaa) | Organização do Repositório, Definição e Revisão da literatura |
| **Valdecir Reis** | [@usuario4](https://github.com/) | Criação do DataSet |

---

## Sumário de Navegação

1. [Objetivo do Trabalho](#objetivo-do-trabalho)
2. [Etapas do Projeto (Metodologia)](#etapas-do-projeto-metodologia)
3. [Estrutura do Repositório](#estrutura-do-repositório)
4. [Acesso Rápido ao Relatório Final](#acesso-rápido-ao-relatório-final)

---

## Objetivo do Trabalho

A evasão em cursos de tecnologia no ensino superior público brasileiro é um problema crítico que gera perdas sociais, econômicas e profissionais. Dificuldades de conciliação de horários de trabalho, defasagens no ensino básico e questões financeiras figuram entre as maiores causas desse fenômeno. 

O objetivo central deste trabalho é atuar **proativamente na retenção estudantil**. Em vez de apenas observar as taxas de abandono ao final do curso, este projeto modela uma tarefa de **Classificação Binária** (Evasão: *Sim* ou *Não*) capaz de soar um alerta precoce baseando-se no comportamento do aluno logo no primeiro ano. 

Para isso, o projeto exigiu o desenvolvimento de uma inteligência robusta de simulação:
*   Criação de um *Dataset* sintético complexo via LLMs, injetando características humanas (ruídos, falsos positivos e falsos negativos) para refletir a imprevisibilidade real).
*   Testes, validações (Validação Cruzada 10-fold) e aplicações de pré-processamento orientadas pelas melhores práticas da literatura em Mineração de Dados Educacionais.
*   Comparação do poder preditivo de 4 grandes classificadores: Árvore de Decisão (J48), Random Forest, k-NN (IBk) e Naive Bayes, tendo como foco de sucesso a maximização do *Recall* (Sensibilidade) da classe de evadidos.

---

## Etapas do Projeto (Metodologia)

Todo o fluxo de trabalho foi rigidamente orientado pelas exigências do enunciado oficial da disciplina, executado passo a passo da seguinte maneira:

| Ordem | Fase do Projeto | Descrição e Execução (Conforme Enunciado) |
| :---: | :--- | :--- |
| **1º** | **Definição do Problema e Fundamentação** | Formulação da tarefa de Classificação, definição semântica de atributos acadêmicos e sociodemográficos e embasamento através de uma revisão bibliográfica sistemática da literatura de *Data Mining* educacional. |
| **2º** | **Geração de Dataset Sintético** | Construção rastreável da base via LLMs contendo mais de 500 instâncias, inserção intencional de *missing values*, anomalias, *outliers* de idade, ruídos (frequências negativas) e um atributo propositalmente irrelevante (`Dia_Matricula`). |
| **3º** | **Teste Piloto** | Análise exploratória realizada no ambiente *Preprocess* do Weka em dados brutos. Focada no levantamento de hipóteses de inconsistências antes da aplicação mecânica de qualquer filtro. |
| **4º** | **Pré-processamento** | Limpeza de dados com embasamento técnico: tratamento de valores nulos via filtro não supervisionado (`ReplaceMissingValues`), justificação de escolhas e tratamento da qualidade dos dados (*Garbage in, Garbage out*). |
| **5º** | **Visualização de Dados** | Utilização analítica e interpretativa dos gráficos gerados pelo software Weka no pós-processamento, orientando a escolha dos métodos preditivos e analisando o peso de nós (como a Frequência) para a árvore de decisão. |
| **6º** | **Treino e Teste (Modelagem)** | Avaliação experimental com os algoritmos clássicos abordados em sala para problemas de classificação. Uso rigoroso dos métodos, ajuste de hiperparâmetros e análise detalhada via Matriz de Confusão, Acurácia e *Recall*. |

---

## Estrutura do Repositório

Nossa organização foi pensada para garantir uma navegação fluida, preservando integralmente a estrutura mínima de submissão exigida pelo docente, com a adição de pastas de apoio metodológico para organizar os artefatos de texto mais extensos.

 ```text
  Raiz do Projeto
 ┣ 1-definicao-problema         
 ┃ ┗ definicao-fundamentacao.md  
 ┣ modelagem                   
 ┃ ┗ modelagem-resultados.md    
 ┣ dataset                     
 ┃ ┣ dataset_original.arff        
 ┃ ┗ dataset_preprocessado.arff   
 ┣ prompts                      
 ┃ ┗ prompts_utilizados.txt       
 ┣ preprocessamento             
 ┃ ┣ analise_inicial.md           
 ┃ ┗ descricao_etapas.md          
 ┣ imagens                      
 ┃ ┣ pipeline_geracao.png       
 ┃ ┣ arvore_j48.png               
 ┃ ┗ matriz_confusao.png          
 ┣ relatorio                    
 ┃ ┗ relatorio_final.md         
 ┣ LICENSE                      
 ┗ README.md
```



