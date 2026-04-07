Você é um designer de informação que pensa visualmente. Sua tarefa é ler o artigo CC-101 Part 2 ("Desmistificando os Modelos de Linguagem") com os olhos de alguém que aprende vendo, não lendo. Alguém que passa reto por um parágrafo de texto mas para pra absorver uma ilustração bem feita.

O artigo usa LEGO como analogia central pra explicar como LLMs funcionam. A audiência são devs de software com 2+ anos de experiência, sem background em IA/ML. O artigo já tem alguns diagramas Mermaid, mas o receio é que eles não estejam ajudando o suficiente na compreensão. Vários conceitos abstratos poderiam ser muito mais claros com a ilustração certa.

## O que você precisa fazer

Para cada seção do artigo (listadas abaixo), responda:

1. **Qual é o conceito central que o leitor precisa absorver nesta seção?** (uma frase)
2. **O diagrama/ilustração atual ajuda?** Se sim, por quê. Se não, o que falta.
3. **Qual seria a ilustração ideal?** Descreva em detalhe: o que aparece visualmente, que elementos usa, como se lê (da esquerda pra direita? de cima pra baixo?), e por que essa forma é a mais eficaz pra esse conceito específico.
4. **Formato recomendado**: diagrama Mermaid, ilustração estática (PNG/SVG), animação GIF, tabela visual, infográfico comparativo, ou outro?
5. **Nível de prioridade**: essencial (o conceito não fica claro sem isso), importante (melhora bastante a compreensão), ou nice-to-have (complementa mas não é crítico).

## As seções do artigo

### 1. O que é um token
O leitor precisa entender que texto vira números (tokens), que um token nem sempre é uma palavra, e que português gasta mais tokens que inglês pra dizer a mesma coisa.

Diagrama atual: um bloco de código comparando tokenização EN vs PT, e um diagrama Mermaid mostrando a mesma comparação como fluxo de peças.

### 2. A janela de contexto
O leitor precisa entender que a mesa (context window) tem tamanho fixo, que entrada e resposta compartilham o mesmo espaço, e que o modelo "enxerga" melhor o começo e o fim do que o meio (lost in the middle).

Diagrama atual: tabela de tamanhos por modelo, e um Mermaid simples mostrando "Começo (atenção forte) — Meio (atenção fraca) — Final (atenção forte)".

### 3. Como o modelo gera texto
O leitor precisa entender que o modelo coloca uma peça por vez, sem plano, escolhendo a mais provável a cada passo (geração autorregressiva).

Diagrama atual: tabela passo-a-passo ("O céu está ___" → candidatos → escolhido), e um Mermaid mostrando o loop de geração.

### 4. O mecanismo de atenção
O leitor precisa entender que pra cada token, o modelo "acende" os tokens anteriores que mais importam e "apaga" os irrelevantes. Também precisa entender o custo quadrático (dobrar a mesa quadruplica o trabalho).

Diagrama atual: Mermaid mostrando a frase "O banco está na margem do rio" com setas de atenção forte/fraca entre tokens.

### 5. Como o modelo escolhe entre as opções (temperatura e top-p)
O leitor precisa entender que temperatura controla o quão "fundo na caixa" o modelo vai pra escolher a próxima peça. Baixa = previsível, alta = criativo/caótico.

Diagrama atual: tabela com exemplos de temperatura (0.0 a 1.5) completando "A receita leva...".

### 6. As famílias de modelos
O leitor precisa entender que existem categorias de modelos (raciocínio, rápido, código, open-weight) com trade-offs de capacidade vs custo.

Diagrama atual: nenhum diagrama. Só listas com bullet points.

### 7. O que modelos não conseguem fazer
O leitor precisa entender alucinações (confiança sem verificação), limites de memória (mesa limpa entre conversas), e que 45% do código gerado tem falhas de segurança.

Diagrama atual: nenhum.

### 8. Quanto custa
O leitor precisa entender que tokens = dinheiro, que output custa mais que input, que português paga um "imposto" de 30-50%, e que existem formas de otimizar (caching, batch, seleção de modelo).

Diagrama atual: tabela de preços e texto. Nenhum diagrama visual.

## Critérios pra uma boa ilustração

- **Deve ser autoexplicativa**: alguém que só olha as ilustrações (sem ler o texto) deve conseguir entender o conceito central de cada seção.
- **Deve usar a analogia LEGO**: peças, mesa, caixa, manual, montagem. A ilustração deve reforçar a metáfora, não criar uma nova.
- **Deve ser simples**: poucos elementos, sem ruído visual. Se precisa de legenda pra ser entendida, tá complicada demais.
- **Deve progredir**: as ilustrações como conjunto devem contar uma história visual. Da peça (token) à mesa (context window) à montagem (geração) à conferência (atenção) à escolha (temperatura) aos kits (famílias) às falhas (limitações) ao preço (custo).
- **Deve respeitar a sequência de leitura**: o leitor ainda não sabe o que é atenção quando está na seção de tokens. Cada ilustração deve usar apenas conceitos que já foram apresentados.

## O que NÃO quero

- Diagramas genéricos de "como funciona um LLM" copiados de papers acadêmicos
- Ilustrações que exigem conhecimento de IA/ML pra entender
- Infográficos lotados de dados que parecem dashboards
- Clipart ou ilustrações infantis
- Representações de cérebro/neurônios (são tecnicamente incorretas e criam expectativas erradas)

## Formato da entrega

Para cada seção, entregue:

```
## Seção N: [nome]

**Conceito central:** [uma frase]

**Diagrama atual:** [funciona / não funciona / parcialmente — e por quê]

**Ilustração proposta:**
- Tipo: [Mermaid / PNG / SVG / GIF / infográfico]
- Descrição visual: [descreva em detalhe o que aparece, como se estivesse briefando um ilustrador]
- Direção de leitura: [esquerda→direita / cima→baixo / radial / comparativo lado a lado]
- Texto na imagem: [quais labels/legendas aparecem]
- Por que esse formato: [por que essa forma visual é a melhor pra esse conceito]

**Prioridade:** [essencial / importante / nice-to-have]
```

Ao final, inclua uma seção "Visão geral do sistema visual" que descreva como as ilustrações se conectam como uma narrativa visual progressiva, e se há alguma ilustração-mestra (tipo um infográfico de página inteira) que valeria a pena criar pra amarrar tudo.
