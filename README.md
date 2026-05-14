# Trabalho Prático 1: Predição de Evasão em Cursos de Tecnologia

> **Descrição:** Este repositório documenta o ciclo completo de Descoberta de Conhecimento em Bancos de Dados (KDD) e Aprendizado de Máquina aplicado à educação. Utilizando o software **Weka 3.8**, o projeto cria e analisa um conjunto de dados sintético gerado por Inteligência Artificial para identificar precocemente perfis de alunos com risco de evasão em universidades públicas brasileiras. Projeto desenvolvido para a disciplina de Inteligência Artificial (ITI370) do Instituto de Ciências Exatas e Tecnologia da Universidade Federal do Amazonas (UFAM).

---

## Equipe Desenvolvedora

| Nome do Membro | Matrícula | Perfil GitHub | Função/Contribuição Principal |
| :--- | :--- | :--- | :--- |
| **[Seu Nome/Colega 1]** | `12345678` | [@usuario1](https://github.com/) | Estruturação do Dataset e Prompts |
| **[Colega 2]** | `12345678` | [@usuario2](https://github.com/) | Pré-processamento e Teste Piloto |
| **[Colega 3]** | `12345678` | [@usuario3](https://github.com/) | Modelagem (Treino e Teste) |
| **[Colega 4]** | `12345678` | [@usuario4](https://github.com/) | Documentação e Revisão de Literatura |

---

## Sumário de Navegação

1. [Objetivo do Trabalho](#-objetivo-do-trabalho)
2. [Etapas do Projeto (Metodologia)](#-etapas-do-projeto-metodologia)
3. [Estrutura do Repositório](#-estrutura-do-repositório)
4. [Acesso Rápido ao Relatório Final](#-acesso-rápido-ao-relatório-final)

---

## Objetivo do Trabalho

A evasão em cursos de tecnologia no ensino superior público brasileiro é um problema crítico que gera perdas sociais, econômicas e profissionais. Dificuldades de conciliação de horários de trabalho, defasagens no ensino básico e questões financeiras figuram entre as maiores causas desse fenômeno. 

O objetivo central deste trabalho é atuar **proativamente na retenção estudantil**. Em vez de apenas observar as taxas de abandono ao final do curso, este projeto modela uma tarefa de **Classificação Binária** (Evasão: *Sim* ou *Não*) capaz de soar um alerta precoce baseando-se no comportamento do aluno logo no primeiro ano. 

Para isso, o projeto exigiu o desenvolvimento de uma inteligência robusta de simulação:
*   Criação de um *Dataset* sintético complexo via LLMs, injetando características humanas (ruídos, falsos positivos e falsos negativos) para refletir a imprevisibilidade real e evitar a "decoreba" dos algoritmos (*overfitting*).
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
| **6º** | **Treino e Teste (Modelagem)** | Avaliação experimental com 4 algoritmos clássicos abordados em sala. Uso rigoroso do método de Validação Cruzada Estratificada (*10-fold cross-validation*), ajuste de hiperparâmetros e análise detalhada via Matriz de Confusão, Acurácia e *Recall*. |

---

## Estrutura do Repositório

Nossa organização foi pensada para garantir uma navegação fluida, preservando integralmente a estrutura mínima de submissão exigida pelo docente, com a adição de pastas de apoio metodológico para organizar os artefatos de texto mais extensos.

```text
📦 Raiz do Projeto
 ┣ 📂 1-definicao-problema         # [Pasta de Apoio] Documentação e Literatura
 ┃ ┗ 📜 definicao-fundamentacao.md   # Definição do problema e embasamento teórico
 ┣ 📂 modelagem                    # [Pasta de Apoio] Análise técnica da classificação
 ┃ ┗ 📜 modelagem-resultados.md      # Discussão das Matrizes de Confusão e Métricas
 ┣ 📂 dataset                      # [Pasta Obrigatória] Bases de Dados
 ┃ ┣ 📜 dataset_original.arff        # Base bruta gerada pelo script
 ┃ ┗ 📜 dataset_preprocessado.arff   # Base limpa e tratada após filtros do Weka
 ┣ 📂 prompts                      # [Pasta Obrigatória] Rastreabilidade da IA
 ┃ ┗ 📜 prompts_utilizados.txt       # Escada evolutiva (4 versões) dos comandos LLM
 ┣ 📂 preprocessamento             # [Pasta Obrigatória] Limpeza de Dados
 ┃ ┣ 📜 analise_inicial.md           # Relato do Teste Piloto e exploração visual
 ┃ ┗ 📜 descricao_etapas.md          # Justificativa do uso de filtros (Missing Values)
 ┣ 📂 imagens                      # [Pasta Obrigatória] Resultados Visuais
 ┃ ┣ 🖼️ pipeline_geracao.png         # Fluxo metodológico de criação dos dados
 ┃ ┣ 🖼️ arvore_j48.png               # Grafo visual gerado pelo Weka
 ┃ ┗ 🖼️ matriz_confusao.png          # Prints comprobatórios dos acertos/erros
 ┣ 📂 relatorio                    # [Pasta Obrigatória] Síntese Executiva
 ┃ ┗ 📜 relatorio_final.md           # O documento resumo de todo o experimento
 ┣ 📜 LICENSE                      # Licença de uso do código/dados
 ┗ 📜 README.md                    # Este sumário de navegação

--------------------------------------------------------------------------------
Acesso Rápido ao Relatório Final
Se você é o avaliador do projeto e deseja visualizar de forma rápida e direta a consolidação dos resultados obtidos no Weka, o fechamento dos objetivos propostos e a análise comportamental de nossos algoritmos (J48, Naive Bayes, k-NN e Random Forest), preparamos um documento executivo que resume nossa jornada.
Clique aqui para ler o Relatório Final Completo
***
