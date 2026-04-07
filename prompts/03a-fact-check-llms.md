Preciso verificar todas as afirmacoes faticas, dados numericos e citacoes que usamos no artigo CC-101 Part 2 ("Desmistificando os Modelos de Linguagem"). O artigo explica fundamentos de LLMs para devs e faz varias claims especificas que precisam ser checadas contra fontes primarias.

Aqui estao os pontos que precisam de verificacao, organizados por secao:

## Tokenizacao

- A regra pratica de "1 token = ~4 caracteres em ingles" e "~3 caracteres em portugues" ainda e precisa para os tokenizers atuais? Teste com os tokenizers do Claude (tiktoken nao se aplica, mas compare com o que a Anthropic documenta), GPT-4o e Gemini.

- O estudo de Petrov et al. (NeurIPS 2023) sobre "tokenization premium" entre idiomas: confirme os numeros que citamos (GPT-2: 1.94x, GPT-4: 1.48x, GPT-4o: ~1.3-1.4x para portugues vs ingles). O paper original reporta exatamente esses valores? Houve errata ou atualizacao? Outros estudos confirmaram ou contestaram esses numeros desde entao?

- BPE comeca com 256 valores de byte? Isso e correto para todas as implementacoes modernas ou existem variacoes (SentencePiece, Unigram)?

- Os vocabularios variam entre ~100K e ~200K tokens? Confirme os tamanhos reais: cl100k_base (GPT-4), o200k_base (GPT-4o), o tokenizer do Claude.

## Context window

- Confirme as janelas de contexto e output maximo de cada modelo listado na tabela (dados de abril 2026):
  - Claude Opus 4.6: 1M input, 128K sync / 300K batch output
  - Claude Sonnet 4.6: 1M input, 64K sync / 300K batch output
  - Claude Haiku 4.5: 200K input, 64K output
  - GPT-5.4: 1.05M input, 128K output
  - GPT-4.1: 1M input, 32K output
  - Gemini 2.5 Pro: 1M input, 65K output
  - Llama 4 Scout: 10M input

- A afirmacao de que "1M tokens = ~750K palavras em ingles (~10 livros)" e precisa? Qual e o tamanho medio de um livro em palavras?

- "Lost in the middle": o paper de Liu et al. (2023) ainda e a referencia principal? Houve estudos mais recentes que confirmaram, refinaram ou contradisseram esses achados? A estimativa de "atenção efetiva em 50-65% da janela" tem base em algum estudo especifico ou e uma aproximacao nossa?

- A estimativa de "~87K tokens de conteudo equivalente" para portugues numa janela de 200K: como chegamos nesse numero? A matematica fecha? (200K * 0.65 efetivo * ajuste linguistico = ?)

## Geracao de texto

- "Geracao autorregressiva" e o termo tecnico correto? Confirme que o paper "Attention Is All You Need" (2017) e a referencia adequada para isso ou se ha uma referencia melhor.

- O paper original dos Transformers e de 2017 e foi publicado pelo Google? Confirme autoria (Vaswani et al.) e afiliacao (Google Brain + University of Toronto).

- "Antes dos Transformers, modelos processavam texto sequencialmente" e uma simplificacao justa? RNNs e LSTMs processavam sequencialmente, mas CNNs para NLP ja faziam processamento paralelo. Vale nuancar isso?

## Atencao

- O custo do mecanismo de atencao escala de forma quadratica com o tamanho do contexto? Isso e verdade para vanilla attention, mas modelos modernos usam tecnicas como FlashAttention, sparse attention, linear attention. A afirmacao ainda e valida como regra geral?

- "Modelos cobram mais por token de output porque cada token exige um calculo de atencao contra toda a sequencia anterior": essa e realmente a razao principal do preco diferenciado? Ou o custo de output e maior por causa do KV cache, da natureza sequencial da decodificacao, ou outros fatores?

## Temperatura e top-p

- A tabela de guia por caso de uso (temperatura 0.0-0.2 para codigo, 0.7-1.0 para escrita criativa, etc.) tem base em alguma recomendacao oficial dos providers ou e consenso da comunidade? Encontre fontes que sustentem essas faixas.

- "Ajuste temperatura OU top-p, nao os dois ao mesmo tempo": isso e uma recomendacao oficial de algum provider ou um conselho pratico da comunidade? A OpenAI, por exemplo, recomenda isso explicitamente?

## Familias de modelos

- Claude Opus 4.6 lidera benchmarks de codigo com 80.8% no SWE-bench: confirme esse numero na fonte (swebench.com). Algum outro modelo ultrapassou esse score desde a publicacao?

- Precos por MTok de cada modelo listado: confirme contra as paginas de pricing oficiais de Anthropic, OpenAI e Google. Precos mudam frequentemente, entao verifique os valores mais recentes.

- Llama 4 Scout tem realmente 10M de contexto? E Maverick tem 1M com 17B parametros ativos de 400B total? Confirme contra o blog post oficial da Meta.

- DeepSeek R1 e realmente open-source com licenca MIT? Confirme a licenca exata e o numero de parametros (671B).

## Limitacoes

- "Codigo gerado por IA carrega 2.74x mais vulnerabilidades segundo a Veracode": confirme esse numero exato no relatorio citado. O estudo era especifico para algum modelo ou linguagem? Qual era a metodologia?

## Custos

- A tabela de precos (Anthropic, OpenAI, Google) com valores de cache read: confirme todos os valores contra as paginas oficiais de pricing.

- "Batch API oferece 50% de desconto": isso e verdade para todos os providers ou so para a Anthropic? Confirme a janela de processamento (24h).

- "Combinando batch + caching na Anthropic, o desconto pode chegar a 95%": como se chega nesse numero? A matematica: cache read a 10% do preco + batch a 50% = 0.10 * 0.50 = 5% do preco original = 95% de desconto? A Anthropic confirma que batch e cache sao cumulativos?

- A estimativa de "~50% a mais em custo para portugues" e consistente com os numeros de tokenizacao que citamos antes? Se o premium e 1.3-1.4x (melhor caso), o custo extra seria 30-40%, nao 50%.

## Meta

- Todas as URLs nas referencias ainda estao ativas? Verifique cada link.
- Alguma referencia tem DOI que deveriamos incluir?
- Existem estudos mais recentes (2025-2026) que deveriam substituir ou complementar as referencias que usamos?

Organize os achados por secao, indicando para cada claim: CONFIRMADO (com fonte), IMPRECISO (com correcao sugerida), INCORRETO (com dado correto), ou NAO VERIFICAVEL (explicando por que). Priorize fontes primarias (papers, docs oficiais, paginas de pricing) sobre fontes secundarias (blog posts, artigos de terceiros).
