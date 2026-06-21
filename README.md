# Teste de Aprendizagem de Pares Associados (PAL)

## 1. Resumo

Este projeto consiste em uma implementação digital, baseada em navegador, do Teste de Aprendizagem de Pares Associados (PAL). Trata-se de um paradigma neuropsicológico clássico, projetado para avaliar a memória episódica visuoespacial, uma função cognitiva primariamente associada à integridade do lobo temporal medial, em particular do hipocampo.

Esta versão foi desenvolvida com uma interface de alto contraste (fundo preto) e utiliza estímulos visuais abstratos com cores vibrantes para maximizar o "sinal perceptual" e minimizar estratégias de mediação verbal. A ferramenta é autocontida em um único arquivo HTML, não requer servidor e foi otimizada para uso em **smartphones e tablets (iPhone/iPad)** com layout totalmente responsivo.

---

## 2. Fundamentação Teórica

A memória episódica refere-se à capacidade de codificar, armazenar e evocar informações sobre eventos autobiográficos contextualmente específicos (o "o quê", "onde" e "quando"). Déficits nesta modalidade de memória são um marcador precoce e proeminente em diversas condições neurológicas, notavelmente na Doença de Alzheimer e no Comprometimento Cognitivo Leve (CCL).

O teste avalia especificamente a aprendizagem associativa visuoespacial (padrão–localização), desafiando o participante a aprender e recordar a associação entre um estímulo visual (o "o quê") e sua localização espacial (o "onde"). Estudos de neuroimagem funcional demonstram consistentemente a ativação do hipocampo e de estruturas adjacentes durante a execução da tarefa, com a ativação aumentando em função da carga de memória exigida. Vale registrar que o PAL é **hipocampo-dependente, mas não hipocampo-exclusivo**: há contribuição frontal/executiva (manutenção de associações e estratégia de busca), de modo que um déficit no PAL não localiza lesão por si só.

---

## 3. Metodologia da Implementação

A presente implementação foi desenvolvida com HTML5, CSS3 (TailwindCSS) e JavaScript ES6+, com foco em fidelidade ao paradigma CANTAB PAL, portabilidade e responsividade.

### 3.1. Versões disponíveis

A tela inicial permite escolher a versão do teste:

| Versão | Estágios (padrões / caixas) | Tentativas por estágio | Duração aprox. |
| ------ | --------------------------- | ---------------------- | -------------- |
| **Completo** | 2/6 · 4/6 · 6/6 · 8/8 | até 6 | ~10–12 min |
| **Rápido (smartphone)** | 2/6 · 4/6 · 6/6 | até 4 | ~4–5 min |

O número de caixas acompanha a estrutura clássica do CANTAB: **6 caixas** nos estágios de 2/4/6 padrões e **8 caixas** no estágio de 8 padrões.

### 3.2. Tentativa de familiarização

Por padrão, o teste inicia com uma **tentativa de familiarização** (não contabilizada nas métricas). Isso segue a recomendação da literatura para mitigar **efeitos de prática** — um ponto sensível em testes de memória visual, sobretudo em desenhos longitudinais e *within-subject*. A familiarização pode ser desativada na tela inicial.

### 3.3. Estrutura da tarefa

* **Fase de Apresentação (Codificação):** no início de cada tentativa de estágio, os padrões são exibidos sequencialmente, cada um dentro de uma caixa (2500 ms na versão completa; 2000 ms na rápida).
* **Fase de Recordação (Evocação):** os padrões são exibidos um a um no centro da tela, em ordem aleatória. O participante seleciona a caixa correspondente — **uma seleção por padrão por tentativa**.
* **Feedback corretivo (re-encoding):** ao errar, a caixa incorreta é sinalizada e a **posição correta é destacada**, reforçando a reaprendizagem.
* **Falha na tentativa:** qualquer erro na fase de recordação invalida a tentativa do estágio; **toda a sequência é reapresentada** na tentativa seguinte.
* **Sucesso:** o estágio é concluído quando o participante acerta **todos** os padrões sem nenhum erro.
* **Descontinuação:** se o estágio não for concluído dentro do número máximo de tentativas, o teste é encerrado e **não avança** para estágios mais difíceis (regra de descontinuação do CANTAB).

> **Nota metodológica:** versões anteriores incluíam um limite global de 10 erros e duas tentativas por item. Ambos foram **removidos** por não fazerem parte do paradigma CANTAB e por comprometerem a comparabilidade das métricas (especialmente do PALTEA).

### 3.4. Estímulos

Para mitigar estratégias de memorização verbal, o teste utiliza um conjunto de **20 estímulos visuais abstratos (SVG)**, com cores vibrantes e alto contraste, sem associação semântica óbvia. Os estímulos são sacados **sem reposição** a partir de um pool embaralhado, garantindo que **nenhuma forma se repita** dentro de uma aplicação.

---

## 4. Métricas Coletadas

As métricas seguem a nomenclatura do CANTAB:

* **Estágios concluídos:** número de estágios completados com sucesso.
* **Padrões alcançados (PALNPR):** número de padrões do último estágio alcançado.
* **Maior estágio na 1ª tentativa:** maior estágio concluído já na primeira tentativa.
* **Total de Erros (PALTE):** soma de todas as seleções incorretas ao longo do teste.
* **Total de Erros Ajustado (PALTEA):** PALTE acrescido de uma estimativa de erros para os estágios **não concluídos** (penalidade proporcional ao número de padrões do estágio). Trata-se de uma aproximação transparente do ajuste do CANTAB, que compensa a descontinuação precoce. *Menor = melhor.*
* **Memória de 1ª Tentativa (PALFAMS):** número de localizações acertadas na **primeira tentativa** de cada estágio. *Maior = melhor.*
* **Tentativas médias para o sucesso:** média do número de tentativas necessárias para concluir cada estágio.
* **Latência média (corretas):** tempo médio de reação das respostas corretas (ms).

> PALTEA e PALFAMS são as duas métricas mais reportadas na literatura e são independentes entre si.

### 4.1. Exportação de Dados

Os resultados podem ser exportados em três formatos (**CSV**, **JSON**, **PDF**) e em dois níveis de detalhe:

* **Resumo:** apenas as métricas principais.
* **Detalhado:** métricas principais, resumo por estágio e log completo de cada tentativa (estímulo, posição correta/clicada, acerto, tentativa do estágio e tempo de reação).

---

## 5. Responsividade

* Layout adaptado a **iPhone e iPad** (retrato e paisagem), com tratamento de *safe-area* (notch) e correção da altura real de viewport no Safari/iOS (`100dvh`).
* O tabuleiro é sempre quadrado e nunca ultrapassa a tela, ajustando-se por largura (retrato) ou altura (paisagem).
* Toque otimizado (sem realce de toque, sem zoom acidental).

---

## 6. Instruções de Uso

1. Abra o arquivo **`index.html`** em um navegador moderno (Chrome, Safari, Firefox, Edge).
2. Insira o **ID do Sujeito**.
3. Escolha a **versão** (Completo ou Rápido) e decida sobre a **familiarização**.
4. Clique em **"Iniciar Teste"** e siga as instruções na tela.
5. Ao final, utilize os **botões de exportação** para salvar os dados.

---

## 7. Limitações

* O PAL é sensível, mas não específico do hipocampo (há contribuição frontal/executiva).
* O **PALTEA** aqui é uma aproximação do ajuste original do CANTAB; cutoffs de estudos publicados não são diretamente transponíveis, pois dependem da versão (número de padrões, regra de descontinuação e faixa de escore).
* Esta ferramenta é destinada a **pesquisa e educação**, não substituindo o CANTAB licenciado nem constituindo dispositivo médico.
