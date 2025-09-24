# Teste de Aprendizagem de Pares Associados (PAL)

## 1. Resumo

Este projeto consiste em uma implementação digital, baseada em navegador, do Teste de Aprendizagem de Pares Associados (PAL). Trata-se de um paradigma neuropsicológico clássico, projetado para avaliar a memória episódica visuoespacial, uma função cognitiva primariamente associada à integridade do lobo temporal medial, em particular do hipocampo.

Esta versão foi desenvolvida com uma interface de alto contraste (fundo preto) e utiliza estímulos visuais abstratos com cores vibrantes para maximizar o “sinal perceptual” e minimizar estratégias de mediação verbal. A ferramenta é autocontida em um único arquivo HTML e não requer instalação de servidor, sendo ideal para aplicação em contextos clínicos e de pesquisa.

---

## 2. Fundamentação Teórica

A memória episódica refere-se à capacidade de codificar, armazenar e evocar informações sobre eventos autobiográficos contextualmente específicos (o “o quê”, “onde” e “quando”). Déficits nesta modalidade de memória são um marcador precoce e proeminente em diversas condições neurológicas, notavelmente na Doença de Alzheimer e no Comprometimento Cognitivo Leve (CCL).

O teste avalia especificamente a aprendizagem associativa visuoespacial, desafiando o participante a aprender e recordar a associação entre um estímulo visual (o “o quê”) e sua localização espacial (o “onde”). Estudos de neuroimagem funcional demonstram consistentemente a ativação do hipocampo e de estruturas adjacentes durante a execução da tarefa, com a ativação aumentando em função da carga de memória exigida. A sensibilidade do teste a disfunções do lobo temporal medial o torna uma ferramenta valiosa para a detecção precoce de declínio cognitivo e para o monitoramento da progressão de doenças neurodegenerativas.

---

## 3. Metodologia da Implementação

A presente implementação foi desenvolvida utilizando tecnologias web modernas (HTML5, CSS3 com TailwindCSS e JavaScript ES6+) para garantir portabilidade e uma interface de usuário clara e responsiva.

### 3.1. Estrutura da Tarefa

O teste segue uma estrutura de dificuldade progressiva, composta por quatro estágios:

| Estágio | Nº de padrões |
| ------: | ------------: |
|       1 |             2 |
|       2 |             4 |
|       3 |             6 |
|       4 |             8 |

**Tentativas de Estágio:** o participante tem um máximo de **4 tentativas** para completar cada estágio.

* **Fase de Apresentação (Codificação):** no início de cada tentativa de estágio, os padrões visuais são exibidos sequencialmente, cada um dentro de uma de oito caixas. O tempo de exposição de cada estímulo é de **2500 ms**.
* **Fase de Recordação (Evocação):** após a apresentação, os padrões são exibidos um a um no centro da tela. O participante deve selecionar a caixa correta.
* **Tentativas por Item:** para cada padrão apresentado na fase de recordação, o participante tem até **2 tentativas** para acertar a localização.
* **Falha na Tentativa de Estágio:** se o participante cometer **qualquer erro** durante a fase de recordação (mesmo na segunda tentativa de um item), a tentativa do estágio é considerada falha. O teste prossegue para a próxima tentativa do mesmo estágio, **reapresentando todos os estímulos**.
* **Sucesso na Tentativa de Estágio:** um estágio é considerado completo quando o participante acerta a localização de **todos os padrões sem erros**.

### 3.2. Estímulos

Para mitigar o uso de estratégias de memorização verbal, o teste utiliza um conjunto de **20 estímulos visuais abstratos (SVG)**, com **cores vibrantes** e **alto contraste**, sem associação semântica óbvia. Um conjunto único de estímulos é utilizado para cada aplicação do teste, garantindo que **nenhuma forma se repita** entre os estágios.

### 3.3. Critérios de Interrupção

O teste é encerrado automaticamente se uma das seguintes condições for atendida:

* O participante completa com sucesso **todos os estágios**;
* O participante **falha em completar um estágio após 4 tentativas**;
* O participante acumula **10 erros** no total (contabilizando **apenas a primeira tentativa errada de cada item**).

---

## 4. Métricas Coletadas e Análise de Dados

Ao final do teste, um conjunto de métricas é calculado, inspirado na metodologia do CANTAB:

* **Nível Máximo Concluído (1ª Tentativa de Estágio):** estágio de maior dificuldade concluído **na primeira tentativa** do estágio.
* **Total de Erros (PALTE):** soma de todas as **primeiras seleções incorretas** para cada item ao longo do teste (**não** contabiliza o segundo erro do mesmo item).
* **Total de Erros Ajustado (PALTEA):** **PALTE** acrescido de **penalidade de 10 pontos** para cada estágio não concluído.
* **Erros Médios para o Sucesso (PALMETS):** média de erros (**PALTE do estágio**) nos estágios concluídos com sucesso.
* **Tentativas Médias para o Sucesso:** média do número de **tentativas de estágio (1–4)** necessárias para concluir com sucesso cada estágio.
* **Acertos na 1ª Tentativa (Item):** número total de vezes em que o participante acertou a localização de um padrão **na primeira tentativa do item**, **na primeira tentativa** do estágio.

### 4.1. Exportação de Dados

Os resultados podem ser exportados em três formatos (**CSV**, **JSON**, **PDF**) e em dois níveis de detalhe:

* **Resumo:** inclui apenas as métricas principais.
* **Detalhado:** inclui as métricas principais, um **resumo por estágio** e um **log completo** de cada tentativa (estímulo, resposta, tempo de reação, tentativa do item, tentativa do estágio e acerto).

---

## 5. Instruções de Uso

1. Abra o arquivo **`index.html`** em um navegador moderno (e.g., Google Chrome, Firefox, Edge).
2. Insira um identificador para o sujeito no campo **“ID do Sujeito”**.
3. Clique em **“Iniciar Teste”** e siga as instruções apresentadas na tela.
4. Após a conclusão ou interrupção do teste, a **tela de resultados** será exibida.
5. Utilize os **botões de exportação** para salvar os dados no **formato** e **nível de detalhe** desejados.
