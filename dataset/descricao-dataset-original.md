# Geração do Dataset Sintético: Rastreabilidade e Evolução

> **Documentação de Referência:** Todo o conteúdo textual bruto dos comandos enviados à Inteligência Artificial citados neste relatório encontra-se disponível para conferência na pasta [prompts utilizados](prompts/prompts.txt) [1, 2].

A construção da base de dados é a etapa fundamental deste projeto. Diferente de bases tradicionais extraídas de sistemas reais, nosso desafio foi criar um *dataset* sintético de forma controlada através de Modelos de Linguagem (LLMs). O objetivo não era gerar dados aleatórios, mas sim **projetar matematicamente o comportamento humano** [3, 4]. 

Abaixo, detalhamos o raciocínio por trás da escolha dos atributos, o atendimento aos requisitos da disciplina e a escada evolutiva (tentativa e erro) até a geração da base final [4].

---

## 1. Fundamentação Teórica: A Origem dos Nossos Dados

A inteligência do nosso modelo preditivo começou antes mesmo da geração no Python. Para que o *dataset* fosse cientificamente válido e coerente com cursos de tecnologia, os atributos selecionados no prompt foram extraídos estritamente das evidências apontadas na nossa **Revisão da Literatura** [5-8].

Os estudos mapearam que a evasão é orientada por três eixos principais, os quais traduzimos em atributos para o nosso classificador [5, 6]:

| Eixo Literário | Atributos Criados | Justificativa Baseada na Literatura |
| :--- | :--- | :--- |
| **Desempenho Acadêmico** | `Media_Semestral_Notas`<br>`Media_Disciplinas`<br>`Reprovacoes`<br>`Frequencia_Pct` | É o fator de maior peso. Autores como Brito Jr. (2018) e Araújo (2025) confirmam que o acúmulo de reprovações iniciais e a baixa frequência (faltas) disparam o abandono do curso [9, 10]. |
| **Sociodemográfico** | `Idade_Ingresso`<br>`Trabalha` | Conciliar trabalho e estudo é o grande desafio das Exatas. Trabalhos como os de Malerba (2023) relacionam diretamente a faixa etária e o desgaste físico/mental com a evasão [10, 11]. |
| **Vínculo Institucional** | `Recebe_Auxilio`<br>`Participa_Projetos` | O sentimento de pertencimento e o amparo econômico previnem o abandono, agindo como fatores de retenção, conforme apontado por Brito Jr. (2018) [10, 11]. |

---

## 2. Checklist de Requisitos do Enunciado

O projeto exigia a injeção intencional de anomalias estatísticas para simular a imperfeição de um ambiente de dados real e avaliar a robustez dos algoritmos no software Weka [3, 4, 7]. Nosso modelo final supriu **100% dos requisitos**:

- [x] **Mínimo de 500 instâncias:** Geramos exatamente 500 registros [12, 13].
- [x] **Mínimo de 5 atributos:** Nossa base é mais robusta, contando com **10 atributos** [13].
- [x] **Atributo Irrelevante:** Criamos o `Dia_Matricula` (Segunda a Sexta), uma variável totalmente desconexa causalmente da evasão, para testar filtros de Seleção de Atributos [13].
- [x] **Valores Faltantes (*Missing Values*):** Inserimos propositalmente o caractere `?` em cerca de 5% dos registros de idades e notas [14].
- [x] **Ruído:** Inserimos 8 instâncias contendo frequências com valores negativos improváveis (ex: `-10%`) simulando falhas humanas de digitação de coordenadores [14].
- [x] **Outliers:** Projetamos 10 idades de ingresso extremas (82, 85, 90 anos), bem distantes da distribuição padrão universitária [14].

---

## 3. Evolução e Rastreabilidade dos Prompts

A chegada ao *dataset* ideal não foi imediata. A equipe conduziu iterações para calibrar a "ambiguidade" da inteligência artificial. Se os dados fossem simples demais, os algoritmos sofreriam de *overfitting* (superajuste), alcançando 100% de precisão ilusória [4]. 

A seguir, a justificativa de nossa evolução:

### Versão 1: O Teste de Viabilidade no Chat
> *Objetivo:* Testar se a IA conseguiria formatar e entender as regras de evasão puramente por texto [15].

*   **O que fizemos:** Inserimos o cabeçalho e pedimos regras literais (notas baixas = evasão) [15].
*   **O problema:** O modelo de linguagem enfrentou restrições de limite de processamento de *tokens* e travou antes de gerar as 500 linhas. Além disso, a distribuição dos dados tornou-se uma "bagunça" estatística sem viés humano, onde a árvore de decisão do Weka ramificaria sem sentido pedagógico [1, 15].

### Versão 2: A Migração para Código e o *Overfitting*
> *Objetivo:* Superar o limite de linhas gerando um código em Python (`pandas`) e amarrar regras rígidas [1, 2].

*   **O que fizemos:** Solicitamos à IA que gerasse um script Python e delimitamos grupos com regras inflexíveis (ex: notas baixas + faltas = SEMPRE evasão) [2].
*   **O problema:** O código Python foi um sucesso técnico, mas um fracasso preditivo. No Weka, a Árvore de Decisão J48 atingiu **100% de Acurácia**. O modelo simplesmente "decorou" a regra matemática imposta no Python, anulando a complexidade humana. Tornou-se um modelo irreal para fins de mineração de dados educacionais [2, 12, 16].

### Versão 3: O Prompt Final (Engenharia de Comportamento Humano)
> *Objetivo:* Quebrar a regra determinística introduzindo "Falsos Positivos e Negativos" sociais para dificultar o trabalho dos classificadores [12, 16].

*   **A Solução Magistral:** No *Prompt 3*, nós ensinamos à IA 4 perfis distintos [16]:
    1.  **Grupo Evasão Clássico (35%)**
    2.  **Grupo Permanência Clássico (35%)**
    3.  **Grupo Resiliência (15%):** A sacada do modelo. Alunos com histórico péssimo de notas e reprovações, mas que, amparados por **bolsas de auxílio**, decidem não evadir [16].
    4.  **Grupo Fatores Externos (15%):** Alunos geniais, com notas altas, mas que evadem da universidade (simulando casos onde o discente passou em outro vestibular) [16].
*   **O Resultado:** Essa modelagem social reduziu a acurácia de predição do Weka para patamares científicos extremamente realistas (~88%), forçando os algoritmos a cruzar atributos como o `Recebe_Auxilio` para desempatar as decisões [13, 14, 16].

---

## 4. Arquitetura de Execução: Python e Google Colab

O último passo de nossa rastreabilidade consistiu na compilação do dado bruto. Como a própria IA estava limitada em exportar arquivos grandes com consistência [1, 15]:

1.  O nosso *Prompt 3* solicitou que a IA gerasse apenas a estrutura em linguagem de programação.
2.  Obtivemos um script fundamentado nas bibliotecas nativas `pandas` (para geração do *Dataframe* e manipulação de colunas estruturadas) e `random` (para aplicar as lógicas de porcentagens, pesos dos perfis resilientes e das inserções de anomalias exigidas) [14].
3.  Executamos esse código de forma isolada em um ambiente em nuvem (*Notebook* no **Google Colab**). 
4.  Ao final da compilação de poucos segundos, o Colab realizou o download de forma automática e limpa do nosso arquivo `dataset_evasao_v2.csv` [14], que posteriormente foi apenas formatado para a extensão `.arff` exigida nativamente pelo software Weka, dando início à nossa fase de modelagem [7, 17].

