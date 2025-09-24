# Teste de Aprendizagem de Pares Associados

## 1. Resumo
Este projeto consiste em uma implementação digital, baseada em navegador, do Teste de Aprendizagem de Pares Associados. Trata-se de um paradigma neuropsicológico clássico, projetado para avaliar a memória episódica visuoespacial, uma função cognitiva primariamente associada à integridade do lobo temporal medial, em particular do hipocampo.  

Esta versão foi desenvolvida com base em estímulos visuais abstratos e não nomeáveis para minimizar estratégias de mediação verbal.  

A ferramenta é autocontida em um único arquivo HTML e não requer instalação de servidor, sendo ideal para aplicação em contextos clínicos e de pesquisa.

---

## 2. Fundamentação Teórica
A memória episódica refere-se à capacidade de codificar, armazenar e evocar informações sobre eventos autobiográficos contextualmente específicos (o "o quê", "onde" e "quando").
Déficits nesta modalidade de memória são um marcador precoce e proeminente em diversas condições neurológicas, notavelmente na Doença de Alzheimer e no Comprometimento Cognitivo Leve (CCL).  

O teste avalia especificamente a aprendizagem associativa visuoespacial, desafiando o participante a aprender e recordar a associação entre um estímulo visual (o "o quê") e sua localização espacial (o "onde"). Estudos de neuroimagem funcional demonstram consistentemente a ativação do hipocampo e de estruturas adjacentes durante a execução da tarefa, com a ativação aumentando em função da carga de memória exigida. A sensibilidade do teste a disfunções do lobo temporal medial o torna uma ferramenta valiosa para a detecção precoce de declínio cognitivo e para o monitoramento da progressão de doenças neurodegenerativas.

---

## 3. Metodologia da Implementação
A presente implementação foi desenvolvida utilizando tecnologias web modernas (HTML5, CSS3 com TailwindCSS, e JavaScript ES6+) para garantir portabilidade e uma interface de usuário clara e responsiva.

### 3.1. Estrutura da Tarefa
O teste segue uma estrutura de dificuldade progressiva, composta por quatro estágios:

- **Estágio 1:** 2 padrões  
- **Estágio 2:** 4 padrões  
- **Estágio 3:** 6 padrões  
- **Estágio 4:** 8 padrões  

Cada estágio compreende duas fases:

- **Fase de Apresentação (Codificação):** Os padrões visuais são exibidos sequencialmente, cada um dentro de uma de oito caixas dispostas em um arranjo circular.
- O participante é instruído a memorizar a localização de cada padrão. O tempo de exposição de cada estímulo foi fixado em 2500ms.
- 
- **Fase de Recordação (Evocação):** Os padrões previamente apresentados são exibidos, um de cada vez, no centro da tela. A tarefa do participante é selecionar
- a caixa na qual o padrão correspondente foi originalmente apresentado.

### 3.2. Estímulos
Para mitigar o uso de estratégias de memorização verbal, o teste utiliza um conjunto de 20 estímulos visuais abstratos (SVG), 
que não possuem uma associação semântica óbvia. Um conjunto único de estímulos é utilizado para cada aplicação do teste, garantindo que nenhuma forma se repita entre os estágios.

### 3.3. Critérios de Interrupção
O teste é encerrado automaticamente se uma das seguintes condições for atendida:

- O participante completa com sucesso todos os estágios.  
- O participante acumula um total de **10 erros** ao longo da tarefa.  

---

## 4. Métricas Coletadas e Análise de Dados
Ao final do teste, um conjunto de métricas é calculado, inspirado na metodologia do CANTAB:

- **Nível Máximo Concluído (1ª Tentativa):** O estágio de maior dificuldade que o participante conseguiu completar acertando a localização de todos os padrões na primeira tentativa.  
- **Total de Erros:** A soma de todas as seleções incorretas feitas pelo participante durante a fase de recordação em todos os estágios.  
- **Total de Erros Ajustado:** O número total de erros acrescido de uma penalidade de 10 erros para cada estágio que o participante não conseguiu completar.  
- **Erros Médios para o Sucesso:** A média de erros cometidos nos estágios que o participante completou com sucesso.  
- **Total de Acertos na 1ª Tentativa:** O número total de vezes que o participante acertou a localização de um padrão em sua primeira tentativa.  

### 4.1. Exportação de Dados
Os resultados podem ser exportados em três formatos (CSV, JSON, PDF) e em dois níveis de detalhe:

- **Resumo:** Inclui apenas as métricas principais.  
- **Detalhado:** Inclui as métricas principais, um resumo do desempenho por estágio e um log completo de cada tentativa individual (incluindo estímulo, resposta, tempo de reação e acerto).  

---

## 5. Instruções de Uso
1. Abra o arquivo `pares_associados.html` em um navegador de internet moderno (e.g., Google Chrome, Firefox, Edge).  
2. Insira um identificador para o sujeito no campo **"ID do Sujeito"**.  
3. Clique em **"Iniciar Teste"** e siga as instruções apresentadas na tela.  
4. Após a conclusão ou interrupção do teste, a tela de resultados será exibida.  
5. Utilize os botões de exportação para salvar os dados no formato e nível de detalhe desejado.  
