# Modelagem e Resultados

## **Naive Bayes (Probabilístico)**

- **Como funciona:** Baseia-se no Teorema de Bayes. Ele assume que cada atributo (como nota ou idade) contribui de forma independente para a probabilidade de um aluno evadir. É um modelo "simples", mas muito rápido.
- **Análise no Projeto:** Foi o nosso modelo de base (*baseline*). Ele apresentou a menor acurácia (**78,36%**). Isso ocorreu porque, na vida real e no nosso dataset, os atributos são dependentes (ex: quem trabalha geralmente tem menos tempo para estudar, afetando a nota). O Naive Bayes ignora essa correlação, sendo menos preciso aqui.

![alt text](../imagens/prints-weka/modelagem1.png)

![alt text](../imagens/prints-weka/modelagem2.png)

![alt text](../imagens/prints-weka/modelagem3.png)

Algoritmos usados: (Naive Bayes, J48, Random Forest, IBk (k =1), IBK *(k=5)* .

### Comparativo de Performance

| Algoritmo | Acurácia (%) | Recall (Sim) | Precision (Sim) |
| --- | --- | --- | --- |
| Naive Bayes | 78,36% | 0,719 | 0,833 |
| J48 | 87,34% | 0,884 | 0,870 |
| Random Forest | 89,38% | 0,888 | 0,902 |
| IBk (k=1) | 83,46% | 0,847 | 0,831 |
| IBk (k=5) | 82,85% | 0,783 | 0,867 |

### Destaque: Árvore de Decisão J48

- **Como funciona:** Cria uma estrutura de árvore baseada em "ganho de informação". Ele seleciona o atributo que melhor divide os dados em "Sim" ou "Não" para evasão.
- **Análise no Projeto:** Obteve excelentes **87,34%** de acurácia. O grande valor do J48 para a UFAM é a **explicabilidade**. Conseguimos ver visualmente que a **Frequência** é o gatilho principal. Se a frequência for baixa, o risco dispara, independentemente de outros fatores.
- **Descrição:** A visualização mostra que a `Frequencia_Pct` é o fator determinante. Alunos com menos de 69% de presença são o principal grupo de risco.

![alt text](../imagens/prints-weka/modelagem4.png)

![alt text](../imagens/prints-weka/modelagem5.png)

![alt text](../imagens/prints-weka/modelagem6.png)

![alt text](../imagens/prints-weka/modelagem7.png)

### Destaque: Matriz de Confusão (Random Forest)

- **Como funciona:** Em vez de uma árvore, ele cria uma "floresta" (no nosso caso, 100 árvores) e combina os resultados. É como se 100 especialistas analisassem o aluno e a decisão final fosse tomada por votação.
- **Análise no Projeto:** Foi o **campeão de performance** com **89,38%**. Ele conseguiu captar nuances que o J48 sozinho não viu, como a relação entre "Receber Auxílio" e a permanência de alunos com notas baixas. É o modelo que recomendamos para implementação prática.
- **Descrição:** O modelo mais assertivo, com apenas 28 falsos negativos em um universo de 490 instâncias.

![alt text](../imagens/prints-weka/modelagem8.png)

![alt text](../imagens/prints-weka/modelagem9.png)

![alt text](../imagens/prints-weka/modelagem10.png)

## Ajuste de Hiperparâmetros

- **Como funciona:** Classifica o aluno com base na "proximidade" dele com outros alunos no passado. Se o perfil de notas e faltas de um aluno novo é idêntico ao de 5 alunos que saíram, ele é classificado como "Sim".
- **Análise no Projeto:** Com **k=1**, ele foi muito sensível a ruídos, atingindo **83,46%**.
    - Com o **Ajuste de Hiperparâmetros (k=5 + Peso de Distância)**, subimos a **Precisão para 86,7%**. Isso mostrou que, ao olhar para um grupo maior de "vizinhos", o modelo se tornou mais confiável, evitando dar alarmes falsos de evasão desnecessariamente.
- **Algoritmo:** IBk (k-NN)
- **Mudança:** Alteração de $k=1$ para $k=5$ e aplicação de `distanceWeighting`.
- **Análise:** O ajuste aumentou a precisão do modelo para 86,7%, tornando os alertas de evasão mais confiáveis, embora menos sensíveis que a Random Forest.

**IBK k=1:**

![alt text](../imagens/prints-weka/modelagem11.png)

**IBK K=5 e aplicação de `distanceWeighting`.**

![alt text](../imagens/prints-weka/modelagem12.png)

## Conclusão Final

O projeto validou que atributos acadêmicos (Frequência e Notas) combinados com o uso de algoritmos de conjunto (Random Forest) permitem uma predição de evasão com quase **90% de acerto**. O dataset sintético gerado via prompts rastreáveis provou ser um ambiente de teste eficaz para o cenário da UFAM.