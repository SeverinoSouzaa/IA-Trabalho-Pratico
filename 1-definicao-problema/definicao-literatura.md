### Definição do Problema:
**Título do Projeto:** Predição de evasão em cursos de tecnologia de uma universidade pública: Uma abordagem baseada em Machine Learning e Classificação.

**1. Tema**

O trabalho insere-se no campo da Inteligência Artificial, especificamente na aplicação de algoritmos de Machine Learning (Aprendizado de Máquina) em tarefas de Classificação dentro da área de Mineração de Dados Educacionais (MDE). O foco é a descoberta de padrões e a construção de modelos preditivos para identificar precocemente discentes com propensão ao abandono em cursos de tecnologia (como Sistemas de Informação e Ciência da Computação) de uma universidade pública. O projeto será conduzido integralmente na ferramenta **Weka**, utilizando um *dataset* sintético gerado especificamente para este fim

---

**2. Contextualização do Problema**

A evasão no ensino superior é um fenômeno educacional global e um desafio grave no Brasil, afetando tanto o desenvolvimento acadêmico quanto o econômico. Dados do INEP frequentemente revelam altas taxas médias de abandono nas instituições brasileiras, variando de 18% a 25%.

No âmbito específico dos cursos de Exatas e Tecnologia, a realidade é ainda mais crítica. Cursos ligados à área de computação (como Ciência da Computação e Sistemas de Informação) apresentam historicamente alguns dos maiores índices de evasão do país, ultrapassando os 40% em certas instituições públicas. O abandono na área de tecnologia caracteriza-se pela falta de integração acadêmica e por desafios específicos, como:

- **Defasagem na formação básica:** Alunos que ingressam na universidade pública com lacunas no ensino médio sofrem com altas taxas de reprovação em disciplinas iniciais da base tecnológica (como Cálculo, Fundamentos da Matemática e Lógica de Programação), gerando frustração imediata.
- **Fatores sociodemográficos e de mercado:** A necessidade de conciliar trabalho e estudo, dificuldades financeiras ou o rápido desvio do aluno de tecnologia diretamente para o mercado de trabalho (mesmo antes de se formar) impulsionam o abandono.

---

**3. Motivação e Justificativa**

A evasão universitária em uma instituição pública gera um triplo impacto negativo — social, acadêmico e financeiro. Quando um aluno de tecnologia abandona o curso em uma universidade pública, há um claro desperdício de investimentos governamentais sem o devido retorno efetivo e uma subutilização de professores e infraestrutura. Paralelamente, o mercado de tecnologia sofre com uma alta demanda e uma enorme escassez de mão de obra qualificada.

A motivação principal deste projeto é atuar proativamente. Tradicionalmente, as universidades apenas registram a evasão de forma reativa. Por meio da criação de um modelo de predição com Aprendizado de Máquina, é possível identificar os alunos com perfil evasor **antes** que o abandono se concretize. Isso justifica e viabiliza a implementação de medidas paliativas pela gestão do curso (coordenadores e professores), propiciando intervenções cirúrgicas, como a oferta de cursos de nivelamento, auxílios estudantis, tutorias de programação ou apoio psicológico àqueles em grupo de risco.


---

### Revisão da Literatura
> resultados obtidos com base nas análises de 5 literaturas que abordam o problema de evasão acadêmica

### 1. Resumo Estruturado da Revisão de Literatura

**Quais técnicas de aprendizado de máquina são mais utilizadas para esse problema?**
A tarefa principal explorada nos estudos para o problema de evasão é a **Classificação**. A técnica mais frequentemente utilizada e recomendada em ambientes educacionais é a **Árvore de Decisão** (comumente implementada pelo algoritmo J48 no Weka), destacando-se pela sua explicabilidade e transparência, características essenciais para justificar pedagogicamente e juridicamente possíveis intervenções em alunos de risco. Outros algoritmos amplamente aplicados e comparados incluem Redes Neurais Artificiais (RNA/MLP), Regressão Logística, Floresta Aleatória (*Random Forest*), Máquinas de Vetores de Suporte (SVM) e *k-Nearest Neighbors* (k-NN).

**Quais atributos (features) aparecem com mais frequência?**
Os atributos preditivos extraídos dos históricos e perfis dos discentes concentram-se em três eixos principais:

1. **Desempenho Acadêmico:** Representa o fator de maior peso na predição, englobando coeficiente de rendimento/médias de notas, índices de aprovação/reprovação (especialmente em disciplinas de base nos primeiros semestres) e percentual de frequência/faltas.
2. **Sociodemográficos:** Idade no ingresso, gênero, etnia e distância/cidade de moradia em relação ao campus.
3. **Vínculo Institucional:** Forma de ingresso (SiSU, vestibular), existência de bolsas de auxílio, participação em projetos (pesquisa/extensão) e status de trancamentos.

**Quais são os principais desafios mencionados nos estudos?**

- **Desbalanceamento de Classes e Volume de Dados:** Na maioria das bases de dados universitárias há uma disparidade enorme entre a quantidade de evadidos e formados ou regulares, o que pode enviesar o aprendizado do algoritmo e requer o uso de filtros de balanceamento. Além disso, bases muito pequenas podem gerar um sobreajuste (*overfitting*), onde o modelo decora os dados de treino, mas falha em prever novos casos.
- **Qualidade e Disponibilidade dos Dados:** Extrair, tratar ruídos, imputar valores nulos em históricos e a ausência de cruzamento com dados sociais/psicológicos restringe a capacidade dos modelos.
- **Interpretabilidade vs. Complexidade:** O desafio de escolher entre algoritmos "caixa-preta" (como Redes Neurais, que podem ter acurácia alta, mas não explicam o motivo da classificação) e algoritmos interpretáveis (como Árvores de Decisão), que viabilizam o embasamento legal ao lidar com o desligamento de alunos e ações da gestão acadêmica.

**Quais técnicas de pré-processamento de dados são utilizadas?**
O pré-processamento é vital na mineração de dados educacionais. As técnicas mais reportadas englobam a **limpeza e remoção de registros inconsistentes ou irrelevantes** (como instâncias com dados vitais ausentes ou alunos com status de trancados/ativos, já que não servem para classificar o destino final). Ocorre o forte uso de **Transformação de Dados**, incluindo a **discretização**, convertendo valores numéricos contínuos (como distâncias e idades) em conceitos categóricos ou faixas de valores (ex: A, B, C; Baixo, Médio, Alto); a **binarização/dummy variables**, transformando variáveis como gênero ou tipo de ingresso em '0' e '1'; além do **balanceamento de amostras** utilizando filtros como o *Spread Subsample* do Weka.

**Quais métricas de avaliação são mais comuns?**
A **Acurácia** (taxa global de acertos) é a métrica base reportada em todos os estudos. No entanto, para o problema da evasão, dá-se ênfase especial à **Sensibilidade (*Recall*)**, pois é essencial minimizar falsos negativos (deixar de identificar o aluno que de fato vai evadir). A **Precisão**, o **F1-Score** (média harmônica entre precisão e sensibilidade) e a análise visual da **Matriz de Confusão** são igualmente reportados para compreender os cenários de acertos e erros práticos dos classificadores.

---

### 2. Tabela Comparativa dos Artigos

| Artigo | Técnica(s) Utilizada(s) | Atributos Utilizados | Tarefa | Técnicas de Pré-processamento | Métricas de Avaliação | Principais Contribuições |
| --- | --- | --- | --- | --- | --- | --- |
| **Araújo (2025)***2025_tcc_gbaraujo.pdf* | *Random Forest*, Regressão Logística, Árvore de Decisão, k-NN, *Gradient Boosting*, SVM, *Naive Bayes*. | Médias semestrais de notas, de frequência e de carga horária cursada no 1º semestre do curso. | Classificação. | Limpeza de valores nulos, substituição por médias semestrais, descarte de instâncias irrelevantes (alunos ativos). | Acurácia, Precisão, Sensibilidade (*Recall*), F1-Score. | Atestou que as médias de frequência e nota isoladas já no 1º semestre são fortíssimos indicadores preditivos. Obteve 96% de recall com *Random Forest*. |
| **Malerba (2023)***Dissertação_2024074.pdf* | Regressão Logística, *Gradient Boosting*, *XGBoost*, *Random Forest*, Árvore de Decisão, RNA, SVM, k-NN. | Base de 34 features (*Kaggle*): dados demográficos (idade, estado civil), de bolsas, unidades curriculares matriculadas/aprovadas, e notas por semestre. | Classificação. | Remoção de valores ausentes, tratamento de outliers e normalização numérica (*StandardScaler*, *MaxAbsScaler*). | Acurácia, Precisão, Sensibilidade, F1-Score, Matriz de Confusão. | Criou fluxos distintos: detectores complexos para intervenção com ajuda pedagógica/psicológica, e detectores interpretáveis (Árvore de Decisão) visando proteção jurídica na hora do desligamento definitivo. |
| **Brito Junior (2018)***UsodeMineraçãodeDados_Brito_2018.pdf* | *K-means* (Agrupamento) e Árvore de Decisão/J48 (Classificação). | Faixa etária, moradia, médias de matrícula, reprovação em 4 disciplinas de base, tempo de permanência, auxílios e participação em pesquisa. | Agrupamento e Classificação. | Extração manual de PDFs para texto, discretização de idades em faixas e remoção de atributos fora do escopo. | Acurácia e Matriz de Confusão. | Evidenciou que alunos que ultrapassam o 8º semestre normal, que reprovam nas disciplinas iniciais de base de TI e sem projetos de monitoria têm altíssima probabilidade de evadir. |
| **Noetzold e Pertile (2021)***brfufrgs,+215764final.pdf* | Árvore de Decisão (J48). | Idade, sexo, distância da instituição (gerado via API), forma de ingresso, aprovações, trancamentos, médias e frequências. | Classificação. | Integração de dados em 3 agrupamentos históricos, discretização de contínuos (conceitos A, B, C; Baixo, Médio, Alto) e balanceamento com filtro *Spread Subsample* do Weka. | Acurácia (Taxa de classificação correta). | Refutou a hipótese que a distância do campus ou as melhorias em infraestrutura impactassem na evasão. A taxa de aprovação e a idade foram os atributos de maior peso. |
| **Toledo (2021)***tecnicasclassificacaoevasaouniversitaria.pdf* | Árvore de Decisão (J48), k-NN (IBk) e Redes Neurais (RNA/MLP). | Etnia, período atual, coeficiente, ano de ingresso, escore de vestibular/SiSU, idade, sexo e dados de escola pública. | Classificação. | Binarização (*dummy variables*) de categorias como tipo de ingresso e raça, e exclusão rigorosa de classes irrelevantes (alunos falecidos, trancados ou de transferências). | Acurácia, Precisão, Sensibilidade (*Recall*) e Matriz de Confusão. | Confirmou as métricas acadêmicas como cruciais. Demonstrou o fenômeno do *overfitting* quando usados todos os atributos, provando que um modelo RNA atrelado à seleção de variáveis provê os melhores resultados gerais. |

---

### Síntese Metodológica e Tabela de Adoção**

A tabela a seguir consolida a espinha dorsal do nosso projeto, atuando como um guia diretivo para as próximas etapas práticas de experimentação no software Weka. Sua construção é o resultado de uma intersecção cuidadosa entre os estudos da disciplina com as melhores práticas extraídas da revisão da literatura científica.

| Referência do Projeto | Técnica(s) Utilizada(s) | Atributos Utilizados | Tipo de Tarefa | Técnicas de Pré-processamento | Métricas de Avaliação |
| --- | --- | --- | --- | --- | --- |
| Predição de evasão em cursos de tecnologia de uma universidade pública | **Base da Aula:** Árvore de Decisão (J48), k-NN (IBk), Naive Bayes.**Extra da Literatura:** *Random Forest*. | **Acadêmicos:** Médias semestrais de notas, Número de reprovações,  media de disciplinas matriculadas, Frequência (%), Participa de projetos? (Sim/Não). **Pessoais:** Idade no ingresso, Recebe Bolsa Auxílio?  Situação de Trabalho" (ex: Trabalha atualmente?(Sim/Não).**Ruído Obrigatório:** Dia da semana da matrícula. | Classificação (Alvo: "Evasão" ou "Não Evasão"). | Identificação/tratamento de valores nulos (ex: *ReplaceMissingValues*), discretização de variáveis (ex: idade em faixas), tratamento de outliers via Amplitude Interquartil e análise de ruídos intencionais. | Validação Cruzada (*10-fold cross-validation*).Matriz de Confusão, Acurácia, Precisão, Sensibilidade (*Recall*) e *F1-Score* (F-Measure). |
