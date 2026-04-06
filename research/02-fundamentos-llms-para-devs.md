# Fundamentos de LLMs para desenvolvedores de software

**Se você sabe construir APIs, entende bancos de dados e já deployou software em produção, este material é para você.** LLMs (Large Language Models) são a nova primitiva de software — e você não precisa de PhD em machine learning para usá-los bem. Este guia explica, de dev para dev, tudo que você precisa saber para integrar LLMs nos seus sistemas com confiança técnica. Cada conceito é apresentado com analogias de engenharia de software, exemplos de código reais e dados de preços e capacidades atualizados até o início de 2026.

---

## 1. O que é um LLM em termos simples

### A analogia do compilador probabilístico

Imagine um compilador — ele recebe código-fonte e produz código de máquina seguindo regras determinísticas. Um LLM faz algo conceitualmente parecido, mas ao contrário: ele recebe texto (ou código, ou imagens) e **produz texto probabilisticamente**, token por token, com base em padrões aprendidos de trilhões de palavras. Não é um banco de dados que "armazena e recupera" informação. É mais parecido com **uma função gigante de autocompletar** que aprendeu padrões estatísticos da linguagem humana.

Se você precisa de uma analogia de engenharia: pense em um LLM como uma **API stateless** extremamente sofisticada. Você envia um request (o prompt), ele processa e retorna um response (a completion). Não tem sessão, não tem memória persistente, não mantém estado entre chamadas — a menos que você implemente isso na sua aplicação.

### Transformers: a arquitetura por trás

Todo LLM moderno é baseado na arquitetura **Transformer**, publicada pelo Google em 2017 no paper "Attention Is All You Need". Sem entrar em matemática, o conceito central é o **mecanismo de atenção** (self-attention): para cada palavra que o modelo processa, ele calcula quanto cada outra palavra no texto é relevante para entender aquela palavra específica.

Pense assim: quando você lê a frase "O banco está na margem do rio", seu cérebro usa o contexto "margem do rio" para entender que "banco" se refere a uma formação de areia, não a uma instituição financeira. O mecanismo de atenção faz algo análogo — ele permite que o modelo "olhe" para todas as palavras simultaneamente e pese a importância de cada uma para gerar a próxima.

Antes dos Transformers, modelos processavam texto sequencialmente (palavra por palavra, da esquerda para a direita). O Transformer **processa tudo em paralelo**, o que permite treinar modelos muito maiores em muito menos tempo com GPUs. Isso foi o breakthrough que tornou LLMs viáveis.

### O que faz um LLM diferente de software tradicional

| Software tradicional | LLM |
|---|---|
| Determinístico: mesma entrada → mesma saída | Probabilístico: mesma entrada pode gerar saídas diferentes |
| Lógica explícita escrita por devs | "Lógica" implícita aprendida de dados |
| Falha de forma previsível (exceções, error codes) | Pode falhar de forma convincente (alucinações) |
| Escala com compute linear | Escala com compute quadrático (atenção) |
| Você debugga lendo o código | Você "debugga" ajustando o prompt |
| Estado persistente (DB, filesystem) | Stateless por padrão — cada request é independente |

**O ponto crucial para devs:** um LLM não "entende" nada. Ele é extraordinariamente bom em **prever qual token vem a seguir** com base em padrões estatísticos. Essa capacidade simples, em escala massiva, produz resultados que parecem compreensão — mas a mecânica subjacente é fundamentalmente diferente de lógica programada.

> **📊 Diagrama sugerido:** Um fluxograma comparando o pipeline de um request HTTP tradicional (Client → API → Business Logic → DB → Response) com o pipeline de um LLM (Client → API → Tokenização → Transformer layers → Sampling → Detokenização → Response). Destaque que no software tradicional a lógica é determinística, enquanto no LLM há uma etapa probabilística de "sampling".

---

## 2. Tokens: como palavras viram números

### O problema fundamental

Computadores não entendem texto — entendem números. Antes que um LLM processe qualquer coisa, o texto precisa ser convertido em uma sequência de **tokens**, que são inteiros representando pedaços de texto. Tokenização é a "serialização" do texto para o modelo.

Um token **não é** necessariamente uma palavra. Pode ser uma palavra inteira ("hello" → 1 token), um pedaço de palavra ("tokenização" → vários tokens), um caractere único, ou até um byte. A regra prática para inglês é **1 token ≈ 4 caracteres** ou **~¾ de uma palavra**. Para português, é mais perto de **1 token ≈ 3 caracteres** — voltaremos a isso.

### BPE (Byte Pair Encoding): como o vocabulário é construído

A maioria dos LLMs modernos usa **Byte Pair Encoding** para construir seu vocabulário de tokens. O algoritmo é elegantemente simples:

1. **Comece com bytes:** o vocabulário inicial são os 256 valores possíveis de um byte. Qualquer texto UTF-8 pode ser representado.
2. **Conte pares:** escaneie o corpus de treinamento e conte a frequência de cada par adjacente de tokens.
3. **Merge o par mais frequente:** junte o par mais comum em um novo token. Adicione ao vocabulário.
4. **Repita:** volte ao passo 2. Continue até atingir o tamanho desejado do vocabulário.

**Exemplo concreto:**
```
Texto: "aaabdaaabac"
Passo 0: [a, a, a, b, d, a, a, a, b, a, c]
Par mais frequente: (a, a) → merge para "Z"
Passo 1: [Z, a, b, d, Z, a, b, a, c]
Par mais frequente: (a, b) → merge para "Y"
Passo 2: [Z, Y, d, Z, Y, a, c]
Par mais frequente: (Z, Y) → merge para "X"
Passo 3: [X, d, X, a, c]  → 5 tokens (comprimiu de 11)
```

Os vocabulários dos modelos atuais têm tamanhos diferentes: GPT-2 tem ~50.000 tokens, GPT-4 tem ~100.000 (encoding `cl100k_base`), e GPT-4o tem ~200.000 (encoding `o200k_base`). **Vocabulários maiores são mais eficientes para idiomas não-ingleses** porque conseguem representar subpalavras comuns em mais idiomas.

### Na prática com tiktoken

`tiktoken` é a biblioteca open-source da OpenAI para tokenização. É escrita em Rust com bindings Python e é **3-6x mais rápida** que alternativas.

```python
import tiktoken

# Carregar o encoding do GPT-4o
enc = tiktoken.encoding_for_model("gpt-4o")  # retorna o200k_base

# Tokenizar uma frase
texto = "Inteligência artificial está transformando o mundo."
tokens = enc.encode(texto)
print(f"Texto: {texto}")
print(f"Tokens: {tokens}")
print(f"Quantidade: {len(tokens)} tokens")

# Ver como cada token mapeia para texto
for token_id in tokens:
    token_bytes = enc.decode_single_token_bytes(token_id)
    print(f"  {token_id} → {token_bytes}")

# Decodificar de volta para texto
texto_reconstruido = enc.decode(tokens)
print(f"Reconstruído: {texto_reconstruido}")
```

**Função utilitária para contar tokens:**
```python
import tiktoken

def contar_tokens(texto: str, modelo: str = "gpt-4o") -> int:
    """Conta tokens para um modelo OpenAI específico."""
    enc = tiktoken.encoding_for_model(modelo)
    return len(enc.encode(texto))

# Exemplos
print(contar_tokens("Hello, world!"))          # ~4 tokens
print(contar_tokens("Olá, mundo!"))             # ~5 tokens
print(contar_tokens("tokenização"))             # ~4 tokens
print(contar_tokens("antidisestablishmentarianism"))  # ~6 tokens
```

### O "imposto linguístico" do português

Aqui está um dado crucial para devs brasileiros: **português consome ~48% mais tokens que inglês** para expressar o mesmo conteúdo. Esse número vem do paper "Language Model Tokenizers Introduce Unfairness Between Languages" (Petrov et al., NeurIPS 2023), que mediu o "prêmio de tokenização" usando o corpus paralelo FLORES-200.

| Tokenizer | Prêmio do português vs inglês |
|---|---|
| GPT-2 (`r50k_base`) | **1.94x** (quase o dobro!) |
| GPT-4 (`cl100k_base`) | **1.48x** (~50% mais tokens) |
| GPT-4o (`o200k_base`) | ~**1.3-1.4x** (melhorou) |

**Por que isso acontece?** O corpus de treinamento dos tokenizadores é dominado por texto em inglês. Palavras inglesas comuns como "the", "and", "great" viram tokens únicos. Já palavras portuguesas são fragmentadas em pedaços menores. Compare:

```
Inglês:  "Have a great day!" → [Have] [a] [great] [day] [!]       = 5 tokens
Português: "Tenha um ótimo dia!" → [Ten][ha] [um] [ó][t][imo] [dia][!] = 8 tokens
```

**O caractere "ó" sozinho já é um token separado** porque acentos são menos frequentes no corpus de treinamento. Isso tem implicações diretas no seu bolso e na capacidade efetiva do modelo — voltaremos a isso nas seções de janela de contexto e custo.

**Comparação entre idiomas (tokenizer cl100k_base):**

| Idioma | Prêmio vs inglês |
|---|---|
| Inglês | 1.00x (baseline) |
| Português | ~1.48x |
| Espanhol | ~1.55x |
| Alemão | ~1.58x |
| Francês | ~1.60x |
| Japonês | ~2.30x |
| Árabe | ~3.04x |

### Contando tokens para a API da Anthropic (Claude)

A Anthropic **não publica um tokenizer local** — você precisa usar a API de contagem de tokens (gratuita):

```python
import anthropic

client = anthropic.Anthropic()

response = client.messages.count_tokens(
    model="claude-sonnet-4-20250514",
    messages=[{
        "role": "user",
        "content": "Qual é a capital do Brasil?"
    }],
)
print(f"Tokens de input: {response.input_tokens}")
```

**Dica prática:** para estimativas rápidas durante desenvolvimento, use tiktoken localmente (é offline e instantâneo). Para contagem precisa antes de chamadas caras à API da Anthropic, use o endpoint `count_tokens`.

> **📊 Diagrama sugerido:** Uma visualização lado a lado mostrando a mesma frase em inglês e português sendo tokenizada, com cada token colorido diferentemente. Mostrar claramente como a frase portuguesa se fragmenta em mais pedaços. Abaixo, um gráfico de barras comparando a contagem de tokens por idioma.

---

## 3. Janela de contexto

### O que é a janela de contexto

A janela de contexto é o **limite máximo de tokens que o modelo pode processar em uma única chamada** — incluindo tanto o input (seu prompt, system message, histórico de conversa, documentos) quanto o output (a resposta gerada). Pense nela como a "RAM" do modelo: tudo que ele precisa "lembrar" para gerar uma resposta precisa caber ali.

Se o seu prompt tem 10.000 tokens e o modelo gera 2.000 tokens de resposta, você usou **12.000 tokens** da janela de contexto.

### Tamanhos atuais dos principais modelos (abril 2026)

O mercado convergiu para **1 milhão de tokens** como padrão para modelos frontier:

| Modelo | Janela de contexto | Max output | Categoria |
|---|---|---|---|
| **Claude Opus 4.6** | 1M tokens | 128K (sync), 300K (batch) | Flagship reasoning |
| **Claude Sonnet 4.6** | 1M tokens | 128K (sync), 300K (batch) | Balanced |
| **Claude Haiku 4.5** | 200K tokens | 64K | Fast/budget |
| **GPT-5.4** | 1.05M tokens | 128K | Flagship |
| **GPT-4.1** | 1M tokens | 32K | Code-optimized |
| **GPT-4o** | 128K tokens | 16K | General purpose (legado) |
| **Gemini 2.5 Pro** | 1M tokens | 65K | Reasoning |
| **Gemini 2.5 Flash** | 1M tokens | 65K | Fast hybrid |
| **Llama 4 Scout** | **10M tokens** | varia por provider | Efficient long-context |
| **Llama 4 Maverick** | 1M tokens | varia por provider | Open-weight flagship |

**Para referência:** 1 milhão de tokens equivale a aproximadamente **750.000 palavras em inglês** — ou cerca de **10 livros inteiros**. Para português, por conta do prêmio de tokenização, é mais perto de **500.000 palavras** (~7 livros).

### O que acontece quando você excede a janela

Quando o total de input + output excede o limite, o comportamento depende do provider:

- **A maioria das APIs retorna um erro** (`400 Bad Request` ou similar) se o input sozinho exceder o limite.
- **Se o input cabe mas o output ficaria grande demais**, o modelo simplesmente para de gerar (trunca a resposta) ao atingir o limite de output tokens.
- **Claude 4.6 oferece "compaction"** (beta): quando a conversa se aproxima do limite, o modelo automaticamente resume o histórico anterior para liberar espaço — útil para chatbots de longa duração.

### Implicações práticas para devs

**Contexto efetivo ≠ contexto anunciado.** Pesquisas recentes (MECW, RULER, Chroma) mostram consistentemente que a qualidade de atenção do modelo cai para **50-65% do máximo anunciado**, especialmente para informações posicionadas no meio do contexto (o chamado "lost in the middle problem"). Traduzindo: um modelo com 1M de janela não necessariamente utiliza bem toda essa informação.

**Estratégias de gerenciamento de contexto:**

- **Coloque informações críticas no início e no final do prompt** — o modelo presta mais atenção nessas posições.
- **Para português, sua janela efetiva é ~33% menor.** Se o modelo tem 200K tokens de contexto, para conteúdo 100% em português, planeje como se fossem ~135K tokens de conteúdo equivalente.
- **Não confunda janela de contexto com limite de output.** Claude Opus 4.6 aceita 1M tokens de input, mas gera no máximo 128K tokens de output em modo síncrono.
- **Use prompt caching** (ver seção de custos) para reutilizar contexto entre chamadas sem reprocessar e repagar.

```python
# Verificando se seu prompt cabe na janela de contexto
import tiktoken

def verifica_contexto(prompt: str, modelo: str, max_context: int) -> dict:
    enc = tiktoken.encoding_for_model(modelo)
    tokens_input = len(enc.encode(prompt))
    tokens_restantes = max_context - tokens_input
    return {
        "tokens_input": tokens_input,
        "tokens_disponiveis_output": min(tokens_restantes, 16384),
        "percentual_usado": f"{(tokens_input/max_context)*100:.1f}%",
        "cabe": tokens_input < max_context
    }

resultado = verifica_contexto(meu_prompt, "gpt-4o", 128_000)
print(resultado)
```

> **📊 Diagrama sugerido:** Uma barra horizontal representando a janela de contexto de 1M tokens, dividida em seções coloridas: system prompt, histórico de conversa, documentos RAG, user message, e espaço reservado para output. Mostrar uma segunda barra comparando como o mesmo conteúdo em português ocupa ~1.5x mais espaço que em inglês.

---

## 4. Next-token prediction, temperatura, top-p e top-k

### Como LLMs geram texto (geração autoregressiva)

A mecânica de geração é surpreendentemente simples: **o modelo prevê um token de cada vez**, sempre olhando para tudo que veio antes. Ele recebe os tokens de input, calcula uma distribuição de probabilidade sobre todo o vocabulário (~100K-200K tokens possíveis) para o próximo token, seleciona um, adiciona à sequência, e repete. Isso é chamado de **geração autoregressiva**.

```
Input:     "O céu está"
Passo 1:   P("azul")=0.25, P("nublado")=0.15, P("claro")=0.12, ...
           → seleciona "azul"
Passo 2:   "O céu está azul" → P("e")=0.20, P("hoje")=0.15, P(".")=0.10, ...
           → seleciona "hoje"
Passo 3:   "O céu está azul hoje" → P(".")=0.35, P(",")=0.12, ...
           → seleciona "."
Resultado: "O céu está azul hoje."
```

Cada token gerado depende de **todos os tokens anteriores** (input + tokens já gerados). O modelo não "planeja" a frase inteira — ele literalmente faz uma escolha de cada vez. É por isso que às vezes respostas começam bem e "descarrilham" no meio.

### Temperatura: o dial de criatividade

A **temperatura** controla o quão "adventureiro" o modelo é na seleção de tokens. Tecnicamente, ela escala as probabilidades (logits) antes do sampling:

- **Temperatura 0.0**: O modelo **sempre escolhe o token mais provável** (greedy decoding). Output determinístico e repetível. Ideal para tarefas que precisam de consistência.
- **Temperatura 0.3-0.5**: Leve variação. Bom equilíbrio para a maioria dos casos de uso.
- **Temperatura 0.7-1.0**: Mais diversidade e criatividade. O modelo explora opções menos prováveis.
- **Temperatura >1.0**: Output cada vez mais aleatório e potencialmente incoerente.

**Exemplo prático — completando "A receita leva":**

| Temperatura | Output provável | Comportamento |
|---|---|---|
| 0.0 | "farinha, ovos e açúcar." | Sempre a mesma resposta |
| 0.3 | "farinha de trigo, manteiga e ovos." | Pequenas variações |
| 0.7 | "especiarias exóticas e um toque de limão siciliano." | Mais criativo |
| 1.5 | "sonhos derretidos em caramelo de dragão." | Aleatório, possivelmente sem sentido |

### Top-p (nucleus sampling): o filtro dinâmico

**Top-p** (também chamado de nucleus sampling) é um mecanismo diferente para controlar a aleatoriedade. Em vez de escalar as probabilidades, ele **filtra os tokens** para considerar apenas aqueles cuja probabilidade acumulada soma até `p`.

Com **top-p = 0.9**, o modelo considera apenas os tokens mais prováveis que juntos somam 90% da probabilidade total, descartando a "cauda longa" de tokens improváveis. Isso significa que o número de tokens considerados varia dinamicamente: quando o modelo está "confiante" (um token domina), poucos tokens são considerados; quando está "incerto", mais tokens entram no pool.

### Top-k: o filtro fixo

**Top-k** é mais simples: considera apenas os **k tokens mais prováveis**, independente das probabilidades. Com top-k=50, o modelo só escolhe entre os 50 tokens mais prováveis, descartando todo o resto.

### Quando usar o quê: guia prático

| Caso de uso | Temperatura | Top-p | Raciocínio |
|---|---|---|---|
| **Geração de código** | 0.0 - 0.2 | 0.9 | Código precisa ser determinístico e correto |
| **Extração de dados / JSON** | 0.0 | 1.0 | Precisão máxima, zero criatividade |
| **Chatbot de suporte** | 0.3 - 0.5 | 0.9 | Natural mas consistente |
| **Tradução** | 0.2 - 0.3 | 0.9 | Fiel ao original com fluidez |
| **Escrita criativa** | 0.7 - 1.0 | 0.95 | Diversidade e surpresa |
| **Brainstorming** | 0.9 - 1.2 | 0.95 | Máxima diversidade |

**Regra de ouro:** ajuste temperatura **ou** top-p, não ambos ao mesmo tempo (a maioria das APIs permite, mas o efeito combinado é difícil de prever). Na prática, **temperatura é o parâmetro mais usado**. Top-k é mais raro em APIs comerciais mas comum em modelos open-source.

> **📊 Diagrama sugerido:** Uma visualização mostrando uma distribuição de probabilidade sobre tokens (gráfico de barras), com três cenários lado a lado: temperatura 0.0 (barra mais alta destacada), temperatura 0.7 (distribuição mais achatada, várias barras viáveis), e temperatura 1.5 (distribuição quase uniforme, caos). Abaixo, mostrar como top-p "corta" a distribuição em um threshold cumulativo.

---

## 5. Tipos de modelo: qual usar e quando

### O panorama em 2026

Modelos de LLM se dividem em categorias com trade-offs distintos de **custo, velocidade e qualidade**. Escolher o modelo certo é como escolher o banco de dados certo — você não usa PostgreSQL para cache em tempo real, e não usa Redis como data warehouse.

### Modelos de raciocínio (reasoning models)

Esses modelos "pensam antes de responder" — gastam tokens internos em raciocínio passo a passo (chain-of-thought estendido) antes de produzir a resposta final. São os mais capazes, mas também os mais lentos e caros.

- **Claude Opus 4.6** — O modelo mais capaz da Anthropic. Lidera benchmarks de código (80.8% SWE-bench) e contexto longo. $5/$25 por MTok.
- **o3 / o3-pro** (OpenAI) — Modelos de raciocínio dedicados. o3-pro é o mais potente ($20/$80 por MTok), projetado para problemas que exigem raciocínio profundo.
- **Gemini 2.5 Pro** (Google) — Modelo de raciocínio com orçamento de "thinking" configurável. $1.25/$10 por MTok.
- **DeepSeek R1** — Open-source (MIT), 671B parâmetros MoE. Raciocínio forte a custo quase zero se self-hosted.

**Quando usar:** problemas de matemática complexa, planejamento multi-etapa, análise de código complexo, decisões que exigem avaliação de múltiplos fatores.

### Modelos rápidos e eficientes

Projetados para latência baixa e custo mínimo. Ideais para tarefas simples em alto volume.

- **Claude Haiku 4.5** — $1/$5 por MTok. Rápido e capaz para classificação, extração, respostas simples.
- **GPT-5.4 nano** — $0.20/$1.25 por MTok. O mais barato da OpenAI.
- **GPT-4o-mini** — $0.15/$0.60 por MTok. Ainda muito popular por ser extremamente barato.
- **Gemini 2.5 Flash** — $0.30/$2.50 por MTok. Raciocínio híbrido (ajustável) a preço acessível.
- **Gemini 2.0 Flash** — $0.10/$0.40 por MTok. O mais barato entre modelos competentes (sendo descontinuado em junho 2026).

**Quando usar:** classificação de texto, extração de entidades, sumarização simples, roteamento de queries, qualquer tarefa de alto volume onde latência importa mais que raciocínio profundo.

### Modelos otimizados para código

- **GPT-4.1** — Explicitamente otimizado para código e seguimento de instruções. 1M de contexto, $2/$8 por MTok. Excelente para tarefas de codificação.
- **Claude Code** (usa Opus/Sonnet) — Agente de codificação que lê codebases inteiros, edita arquivos, roda comandos e cria PRs.
- **Qwen3-Coder-480B** — Open-weight, especializado em código de contexto longo.
- **Codex** (OpenAI) — Ferramenta CLI agentic usando GPT-5.4 para tarefas em repositórios.

### Modelos de propósito geral

O "meio-termo" para a maioria das aplicações.

- **Claude Sonnet 4.6** — $3/$15 por MTok. O "workhorse" da Anthropic. 1M de contexto, bom em tudo.
- **GPT-5.4** — $2.50/$15 por MTok. Flagship da OpenAI. 1.05M de contexto.
- **Gemini 2.5 Pro** — $1.25/$10 por MTok. Competitivo em preço com raciocínio forte.
- **Llama 4 Maverick** — Open-weight, 1M de contexto. 17B parâmetros ativos de 400B total (MoE).

### Framework de decisão para devs

```
Preciso de raciocínio profundo ou código complexo?
  → SIM: Claude Opus 4.6 / o3-pro / Gemini 2.5 Pro
  → NÃO: ↓

É uma tarefa simples em alto volume (>10K requests/dia)?
  → SIM: GPT-4o-mini / Gemini 2.5 Flash / Claude Haiku 4.5
  → NÃO: ↓

É principalmente geração/análise de código?
  → SIM: GPT-4.1 / Claude Sonnet 4.6 (coding mode)
  → NÃO: ↓

Tarefa de propósito geral com boa qualidade:
  → Claude Sonnet 4.6 / GPT-5.4 / Gemini 2.5 Pro
```

**Dica prática:** comece sempre com o modelo mais barato que pode funcionar. Teste com Haiku/Flash/mini. Se a qualidade não for suficiente, suba para Sonnet/GPT-4.1. Só use Opus/o3-pro quando realmente necessário. Essa abordagem pode reduzir custos em **10-50x** sem perda significativa de qualidade para muitos use cases.

> **📊 Diagrama sugerido:** Um gráfico scatter plot com "Custo por MTok (output)" no eixo X e "Qualidade/Capacidade (benchmark composto)" no eixo Y. Cada modelo como um ponto rotulado, agrupado por cor (Anthropic=roxo, OpenAI=verde, Google=azul, Open-source=laranja). Isso permite visualizar o trade-off custo-qualidade de cada modelo.

---

## 6. O que modelos NÃO conseguem fazer

### Alucinações: o bug que parece feature

**Alucinação** é quando o modelo gera informação que parece correta mas é factualmente falsa — com total confiança. Não é um bug no sentido tradicional; é uma consequência inevitável de como LLMs funcionam.

**Por que acontecem:** o modelo é treinado para gerar o texto mais provável, não o texto mais verdadeiro. Se o padrão estatístico de "X escreveu o livro Y" é forte o suficiente nos dados de treinamento, o modelo vai afirmar isso mesmo se for falso. O modelo não tem um "verificador de fatos" interno — ele não distingue entre gerar "Paris é a capital da França" e "Paris é a capital da Itália". Ambas são sequências de tokens plausíveis.

**Cenários de maior risco:** citações acadêmicas (modelos inventam papers que não existem), dados numéricos específicos, URLs, nomes de APIs ou funções, eventos recentes, e qualquer informação que requer precisão exata.

### Raciocínio: padrão ou lógica?

Existe um debate ativo sobre se LLMs "raciocinam" ou apenas "reconhecem padrões". A posição técnica mais defensável em 2026: **LLMs são extraordinariamente bons em reconhecimento de padrões que se parece com raciocínio**, especialmente modelos de raciocínio como o3 e Claude Opus com extended thinking. Eles resolvem problemas de lógica, matemática e código que pareciam impossíveis há dois anos. Mas falham em formas que um raciocinador verdadeiro não falharia — por exemplo, mudanças triviais na formulação de um problema podem fazer o modelo errar algo que "deveria" saber.

**Para devs, a implicação prática é:** não confie no output de um LLM sem verificação em contextos onde erros têm custo alto. Trate o LLM como um **colega júnior muito rápido** — produtivo mas que precisa de code review.

### Limitações concretas que todo dev precisa saber

- **Sem dados em tempo real:** sem ferramentas externas (web search, APIs), o modelo só sabe o que existia até seu knowledge cutoff de treinamento. Claude Opus 4.6 tem cutoff de início de 2025; GPT-4o de outubro de 2023.
- **Sem memória persistente por padrão:** cada chamada de API é independente. O modelo não "lembra" da conversa anterior a menos que você envie o histórico completo no prompt. Persistência de memória é responsabilidade da sua aplicação.
- **Matemática não é o forte.** LLMs melhoraram muito, mas ainda falham em aritmética complexa, especialmente com números grandes. Para cálculos precisos, use tool calling para executar código Python — nunca confie no modelo para fazer contas.
- **"Confiante e errado" é o modo padrão de falha.** Diferente de software que lança exceções, o modelo raramente diz "não sei". Ele tende a fabricar uma resposta plausível. Isso é perigoso em produção.
- **Limite de output:** mesmo com janelas de contexto de 1M tokens, o output é limitado (128K para Claude, 65K para Gemini). Se você precisa gerar documentos muito longos, precisará de múltiplas chamadas com estratégia de continuação.
- **Viés dos dados de treinamento:** modelos refletem os vieses presentes nos dados em que foram treinados. Para aplicações sensíveis, isso requer avaliação e mitigação cuidadosa.

### Como mitigar essas limitações na prática

```python
# Exemplo: forçar o modelo a admitir incerteza
system_prompt = """Você é um assistente técnico preciso.
REGRAS CRÍTICAS:
1. Se não tem certeza de um fato, diga explicitamente "Não tenho certeza sobre isso."
2. Nunca invente URLs, nomes de papers, ou citações.
3. Para cálculos matemáticos, mostre o passo a passo.
4. Se a pergunta requer dados após sua data de treinamento, diga que não tem essa informação.
"""

# Exemplo: usar tool calling para matemática precisa
tools = [{
    "name": "calculadora",
    "description": "Executa cálculos matemáticos precisos. USE SEMPRE para qualquer operação numérica.",
    "input_schema": {
        "type": "object",
        "properties": {
            "expressao": {"type": "string", "description": "Expressão Python válida. Ex: '1547 * 382 + 0.15'"}
        },
        "required": ["expressao"]
    }
}]
```

> **📊 Diagrama sugerido:** Um "scorecard de confiabilidade" visual tipo semáforo mostrando categorias de tarefa (código, texto criativo, fatos, matemática, raciocínio lógico, dados recentes) com indicadores verde/amarelo/vermelho para o nível de confiabilidade do LLM em cada uma. Incluir ícones de ferramentas (tool calling, RAG, verificação humana) como "remédios" para as categorias amarela/vermelha.

---

## 7. Custo: input tokens, output tokens e como otimizar

### O modelo de precificação

LLMs são cobrados por token processado, dividido em duas categorias: **input tokens** (tudo que você envia: system prompt, mensagens, documentos) e **output tokens** (o que o modelo gera). **Output tokens sempre custam mais** — geralmente 3-5x mais que input — porque gerar cada token requer um forward pass completo pelo modelo.

### Tabela de preços dos principais modelos (abril 2026)

Preços em USD por **1 milhão de tokens** (MTok):

| Modelo | Input / MTok | Output / MTok | Cache read / MTok |
|---|---|---|---|
| **Claude Opus 4.6** | $5.00 | $25.00 | $0.50 |
| **Claude Sonnet 4.6** | $3.00 | $15.00 | $0.30 |
| **Claude Haiku 4.5** | $1.00 | $5.00 | $0.10 |
| **GPT-5.4** | $2.50 | $15.00 | $0.25 |
| **GPT-5.4 mini** | $0.75 | $4.50 | $0.075 |
| **GPT-5.4 nano** | $0.20 | $1.25 | $0.02 |
| **GPT-4.1** | $2.00 | $8.00 | $0.50 |
| **GPT-4o** | $2.50 | $10.00 | $1.25 |
| **GPT-4o-mini** | $0.15 | $0.60 | $0.075 |
| **o3** | $2.00 | $8.00 | $0.50 |
| **o4-mini** | $0.55 | $2.20 | $0.275 |
| **Gemini 2.5 Pro** | $1.25 | $10.00 | $0.125 |
| **Gemini 2.5 Flash** | $0.30 | $2.50 | $0.03 |
| **Gemini 2.5 Flash-Lite** | $0.10 | $0.40 | $0.01 |

**Nota:** Google oferece um **free tier** generoso para Gemini 2.5 Flash e Pro via Google AI Studio, com limites de rate mais baixos. Excelente para prototipagem.

### Estimando custos para um projeto

```python
def estimar_custo_mensal(
    requests_por_dia: int,
    tokens_input_medio: int,
    tokens_output_medio: int,
    preco_input_mtok: float,
    preco_output_mtok: float,
    dias: int = 30
) -> dict:
    """Estima custo mensal de uso de LLM API."""
    total_requests = requests_por_dia * dias
    total_input = total_requests * tokens_input_medio
    total_output = total_requests * tokens_output_medio

    custo_input = (total_input / 1_000_000) * preco_input_mtok
    custo_output = (total_output / 1_000_000) * preco_output_mtok
    custo_total = custo_input + custo_output

    return {
        "requests_total": f"{total_requests:,}",
        "custo_input": f"${custo_input:,.2f}",
        "custo_output": f"${custo_output:,.2f}",
        "custo_total_mensal": f"${custo_total:,.2f}",
        "custo_por_request": f"${custo_total/total_requests:.4f}"
    }

# Exemplo: chatbot com Claude Sonnet 4.6
# 1000 conversas/dia, ~2000 tokens input, ~500 tokens output
resultado = estimar_custo_mensal(
    requests_por_dia=1000,
    tokens_input_medio=2000,
    tokens_output_medio=500,
    preco_input_mtok=3.00,   # Claude Sonnet 4.6 input
    preco_output_mtok=15.00  # Claude Sonnet 4.6 output
)
print(resultado)
# {'requests_total': '30,000', 'custo_input': '$0.18',
#  'custo_output': '$0.23', 'custo_total_mensal': '$0.41',
#  'custo_por_request': '$0.0000'}
# Nota: 30K requests simples = ~$400/mês com Sonnet se cada
# request tiver prompts mais longos (ex: 10K input, 2K output)
```

**Cenário realista — chatbot de suporte com RAG:**

| Parâmetro | Valor |
|---|---|
| Requests/dia | 5.000 |
| System prompt + contexto RAG | ~8.000 tokens input |
| Resposta média | ~1.000 tokens output |
| Modelo | Claude Sonnet 4.6 |
| Custo input/mês | (5000 × 30 × 8000 / 1M) × $3.00 = **$3.600** |
| Custo output/mês | (5000 × 30 × 1000 / 1M) × $15.00 = **$2.250** |
| **Total mensal** | **~$5.850** |
| Com prompt caching (90% hit) | Input cai de $3.600 para ~$720 → **Total ~$2.970** |
| Com Haiku em vez de Sonnet | **~$1.950** (sem cache) |

### Estratégias de otimização de custo

**1. Prompt caching** — A otimização mais impactante. Todos os três grandes providers oferecem cache reads a **~10% do preço de input**. Se seu system prompt ou contexto RAG é repetitivo entre requests, caching pode reduzir custos de input em **90%**.

**2. Batch API** — Todos os providers oferecem **50% de desconto** para processamento assíncrono (janela de 24h). Se seu caso de uso não é real-time (análise de documentos, classificação em massa), use batch.

**3. Seleção de modelo** — Não use Opus para classificar sentimentos. A diferença entre Haiku ($1/$5) e Opus ($5/$25) é **5x no input e 5x no output**. Muitas tarefas que parecem "precisar" de um modelo grande funcionam perfeitamente com modelos menores.

**4. Reduza tokens de input:**
- System prompts mais concisos (cada palavra custa dinheiro, especialmente em português).
- Considere escrever system prompts em inglês (economiza ~33% de tokens se o modelo entende o contexto bilingue).
- Resuma históricos de conversa longos em vez de enviar a conversa completa.
- Em RAG, retorne apenas chunks relevantes, não documentos inteiros.

**5. Controle tokens de output:**
- Use `max_tokens` para limitar a resposta.
- Peça respostas concisas no prompt.
- Para extração de dados, peça JSON direto — evita tokens gastos com "Claro! Aqui está a informação que você pediu:..."

**6. Combine batch + caching** — Na Anthropic, isso pode dar desconto de até **95%**: 50% do batch × 90% do cache read.

**Impacto do "imposto do português" no custo:** Para os mesmos conteúdos, aplicações em português custam **~50% a mais** em tokens de input do que a mesma aplicação em inglês. Em uma conta de $5.000/mês, isso representa ~$1.650 extras. Prompt caching mitiga significativamente esse custo adicional.

> **📊 Diagrama sugerido:** Um gráfico de barras empilhadas mostrando o custo mensal do mesmo chatbot (5K requests/dia) usando diferentes modelos (Opus → Sonnet → Haiku → GPT-4o-mini → Gemini Flash), com as barras divididas em input (azul) e output (vermelho). Uma segunda versão do gráfico mostrando o impacto de cada otimização (caching, batch, modelo menor) como reduções incrementais.

---

## 8. Conceitos emergentes

### Chain-of-thought: por que "pense passo a passo" funciona

Adicionar "pense passo a passo" ao final de um prompt pode **melhorar dramaticamente** a qualidade das respostas em tarefas de raciocínio. Isso é **Chain-of-Thought (CoT) prompting**, e funciona por três mecanismos:

1. **Expansão do contexto de trabalho:** cada passo intermediário vira parte do contexto para o próximo, criando uma "memória de trabalho" crescente.
2. **Atenção fortalecida:** passos intermediários permitem que o mecanismo de self-attention capture dependências que seriam perdidas em uma resposta direta.
3. **Autocorreção:** trabalhar em etapas dá ao modelo oportunidades de detectar e corrigir erros.

```python
# Sem CoT — modelo erra com frequência em problemas multi-etapa
prompt_direto = "Uma loja tem 45 maçãs. Vende 30% na segunda. Recebe 20 na terça. Quantas tem?"

# Com CoT zero-shot — dramaticamente melhor
prompt_cot = """Uma loja tem 45 maçãs. Vende 30% na segunda. Recebe 20 na terça. 
Quantas tem?

Vamos pensar passo a passo."""

# Com CoT few-shot — o melhor resultado
prompt_few_shot_cot = """Q: João tem 10 maçãs. Dá 4 e recebe 5. Quantas tem?
A: Início: 10. Dá 4: 10-4=6. Recebe 5: 6+5=11. Resposta: 11.

Q: Uma loja tem 45 maçãs. Vende 30% na segunda. Recebe 20 na terça. Quantas tem?
A:"""
```

**Nota importante:** modelos de raciocínio (o3, Claude com extended thinking, Gemini com thinking) **já fazem CoT internamente** — não precisa pedir. CoT explícito é mais útil com modelos gerais como GPT-4o ou Claude Sonnet sem extended thinking.

### Few-shot vs zero-shot: a escada de complexidade

| Técnica | O que é | Quando usar |
|---|---|---|
| **Zero-shot** | Só a instrução, sem exemplos | Tarefas simples e bem definidas |
| **One-shot** | Um exemplo | Clarificar formato/tom |
| **Few-shot** | 2-10 exemplos | Tarefas complexas, formato específico |

**Comece sempre com zero-shot.** Modelos frontier em 2026 são muito mais capazes de seguir instruções sem exemplos do que modelos de 2023. Escale para few-shot apenas quando zero-shot não der resultado satisfatório.

```python
# Zero-shot: classificação de sentimento
prompt_zero = """Classifique o sentimento como POSITIVO, NEGATIVO ou NEUTRO.

Texto: "O atendimento foi péssimo, nunca mais volto."
Sentimento:"""

# Few-shot: classificação com nuance
prompt_few = """Classifique o sentimento como POSITIVO, NEGATIVO ou NEUTRO.

Texto: "O produto é bom, mas a entrega atrasou demais."
Sentimento: NEGATIVO

Texto: "Preço justo pelo que oferece."
Sentimento: NEUTRO

Texto: "Superou todas as expectativas!"
Sentimento: POSITIVO

Texto: "Funciona, mas já vi melhores por esse preço."
Sentimento:"""
```

### RAG: dando memória e conhecimento ao modelo

**Retrieval-Augmented Generation (RAG)** resolve o problema mais frustrante de LLMs: eles não sabem nada sobre seus dados internos, documentação privada ou informações atualizadas. A arquitetura é elegante para devs que já entendem de bancos de dados:

```
Query do usuário
    → Embedding (converte texto em vetor numérico)
    → Busca no vector DB (encontra documentos similares)
    → Re-ranking (ordena por relevância)
    → Injeta top-K documentos no prompt
    → LLM gera resposta baseada nos documentos
```

**Na prática, é como um "SELECT * FROM knowledge WHERE content SIMILAR TO query LIMIT 5"**, onde a busca é semântica (por significado) em vez de lexical (por palavras exatas).

**Stack típico de RAG em 2026:**

- **Embedding models:** OpenAI `text-embedding-3-large`, Cohere Embed, ou modelos open-source como BGE-M3
- **Vector databases:** Pinecone, Weaviate, pgvector (extensão PostgreSQL), Chroma, Milvus, Qdrant
- **Frameworks:** LlamaIndex (melhor para RAG puro), LangChain/LangGraph (melhor para orquestração complexa)
- **Busca híbrida:** combine busca vetorial + BM25 (keyword) com re-ranking. Consistentemente supera qualquer abordagem isolada.

**RAG vs Fine-tuning — quando usar cada um:**

- **Dados mudam frequentemente** → RAG (atualiza o vector DB, não o modelo)
- **Precisa de dados em tempo real** → RAG (busca live)
- **Precisa mudar tom/estilo do modelo** → Fine-tuning
- **Orçamento limitado** → RAG (sem custo de treinamento)
- **Precisa de ambos** → Combine: fine-tune para estilo do domínio + RAG para dados atuais

### Function calling / Tool use: LLMs como orquestradores

Function calling transforma o LLM de um gerador de texto em um **orquestrador de sistemas**. O modelo decide quando chamar uma ferramenta externa e gera os parâmetros corretos em JSON. Criticamente: **o modelo não executa nada** — ele apenas decide e parametriza. Sua aplicação executa a função e retorna o resultado.

```python
import anthropic

client = anthropic.Anthropic()

# Definir ferramentas disponíveis
tools = [
    {
        "name": "buscar_pedido",
        "description": "Busca informações de um pedido pelo número. Use quando o usuário perguntar sobre status de pedido.",
        "input_schema": {
            "type": "object",
            "properties": {
                "numero_pedido": {
                    "type": "string",
                    "description": "Número do pedido (ex: PED-12345)"
                }
            },
            "required": ["numero_pedido"]
        }
    }
]

# Chamar o modelo com ferramentas
response = client.messages.create(
    model="claude-sonnet-4-20250514",
    max_tokens=1024,
    tools=tools,
    messages=[{
        "role": "user",
        "content": "Qual o status do meu pedido PED-98765?"
    }]
)

# Se stop_reason == "tool_use", executar a ferramenta
for block in response.content:
    if block.type == "tool_use":
        # Sua aplicação executa a busca real no banco
        resultado = buscar_no_banco(block.input["numero_pedido"])

        # Enviar resultado de volta ao modelo
        response_final = client.messages.create(
            model="claude-sonnet-4-20250514",
            max_tokens=1024,
            tools=tools,
            messages=[
                {"role": "user", "content": "Qual o status do meu pedido PED-98765?"},
                {"role": "assistant", "content": response.content},
                {"role": "user", "content": [{
                    "type": "tool_result",
                    "tool_use_id": block.id,
                    "content": json.dumps(resultado)
                }]}
            ]
        )
```

### Agentes e MCP: o futuro (que já chegou)

**Agentes** combinam LLMs + tools + planejamento + memória + autonomia. Diferente de um chatbot que responde queries, um agente **percebe, planeja e age** para alcançar objetivos com mínima intervenção humana.

O **Model Context Protocol (MCP)**, introduzido pela Anthropic em novembro de 2024, se tornou o padrão de facto para conectar LLMs a ferramentas externas — como um "USB-C para IA". Em dezembro de 2025, foi doado para a Linux Foundation, com **97 milhões de downloads mensais de SDK** e adotado por OpenAI, Google, Microsoft e mais de 10.000 servidores ativos.

**Por que MCP importa para devs:** em vez de implementar integrações custom para cada modelo e cada ferramenta, você implementa um MCP server uma vez e qualquer modelo/aplicação que suporte MCP pode usá-lo.

```
Host (sua app com LLM) ←→ MCP Client ←→ MCP Server ←→ Sistema externo
                                          (tools, resources, prompts)
```

**Frameworks de agentes principais em 2026:**
- **OpenAI Agents SDK** — Minimalista, 4 primitivas: Agents, Tools, Handoffs, Guardrails.
- **LangGraph** — Orquestração baseada em grafos, máximo controle.
- **Claude Code** — Agente de codificação autônomo com multi-agent spawning.

**A hierarquia prática para devs que estão começando:**

1. **Prompt engineering** (CoT, few-shot) → sempre começa aqui, é grátis e rápido
2. **RAG** → quando o modelo precisa acessar seus dados
3. **Fine-tuning** → quando precisa mudar comportamento consistente
4. **Tool use** → quando o modelo precisa agir no mundo (APIs, DBs)
5. **Agentes** → quando precisa de workflows autônomos multi-etapa
6. **MCP** → para padronizar como agentes se conectam a tudo

> **📊 Diagrama sugerido:** Uma "pirâmide de complexidade" com as 6 camadas acima empilhadas, do mais simples (prompting, na base) ao mais complexo (MCP/Agentes, no topo). Setas laterais indicando quando "subir" para a próxima camada. Um segundo diagrama mostrando a arquitetura de RAG com seus componentes (vector DB, embedding, retriever, LLM) em formato de arquitetura de sistema — algo familiar para devs.

---

## Glossário de termos-chave

| Termo | Definição |
|---|---|
| **Alucinação (Hallucination)** | Quando o modelo gera informação factualmente incorreta com aparência de confiança. Não é um "bug" mas uma consequência do design probabilístico. |
| **Atenção (Attention)** | Mecanismo do Transformer que permite ao modelo ponderar a relevância de cada token em relação aos demais ao processar texto. |
| **Batch API** | Modo de processamento assíncrono (geralmente 24h de janela) oferecido pelos providers com ~50% de desconto nos tokens. |
| **BPE (Byte Pair Encoding)** | Algoritmo de tokenização que iterativamente mescla os pares de bytes/caracteres mais frequentes para construir um vocabulário de subpalavras. |
| **Chain-of-thought (CoT)** | Técnica de prompting que pede ao modelo para "pensar passo a passo", melhorando resultados em tarefas de raciocínio. |
| **Completion** | O texto gerado pelo modelo em resposta a um prompt. Também chamado de "response" ou "output". |
| **Context window (Janela de contexto)** | Número máximo de tokens (input + output) que o modelo pode processar em uma única chamada. |
| **Embedding** | Representação de texto como um vetor numérico de alta dimensão, usado para busca semântica em RAG. |
| **Extended thinking** | Modo em que modelos de raciocínio (Claude Opus, o3) gastam tokens "pensando" internamente antes de responder, melhorando qualidade em tarefas complexas. |
| **Few-shot prompting** | Incluir 2-10 exemplos no prompt para guiar o modelo sobre formato e comportamento esperado. |
| **Fine-tuning** | Retreinar (parcialmente) um modelo existente com seus próprios dados para adaptar comportamento, estilo ou conhecimento. |
| **Function calling / Tool use** | Capacidade do modelo de decidir quando e como chamar ferramentas externas, gerando JSON com parâmetros para sua aplicação executar. |
| **Geração autoregressiva** | Processo de gerar texto um token de cada vez, onde cada token depende de todos os anteriores. |
| **Greedy decoding** | Seleção do token mais provável a cada passo (equivalente a temperatura 0). Determinístico mas pode ser monótono. |
| **Knowledge cutoff** | Data limite dos dados de treinamento do modelo. Ele não "sabe" nada que aconteceu depois. |
| **LoRA (Low-Rank Adaptation)** | Técnica de fine-tuning eficiente que ajusta apenas um subconjunto pequeno de parâmetros do modelo, reduzindo custo de treinamento. |
| **MCP (Model Context Protocol)** | Protocolo aberto (JSON-RPC 2.0) que padroniza como LLMs se conectam a ferramentas e dados externos. Criado pela Anthropic, mantido pela Linux Foundation. |
| **MoE (Mixture of Experts)** | Arquitetura onde o modelo tem muitos parâmetros totais, mas ativa apenas um subconjunto (especialistas) para cada token, reduzindo custo computacional. |
| **MTok** | "Million tokens" — unidade padrão de precificação. $3/MTok = $0.000003 por token. |
| **Nucleus sampling (top-p)** | Método de sampling que seleciona entre os tokens mais prováveis cuja probabilidade acumulada atinge um threshold `p`. |
| **Prompt caching** | Funcionalidade dos providers que armazena prompts repetitivos para reutilização, cobrando ~10% do preço normal de input em cache reads. |
| **RAG (Retrieval-Augmented Generation)** | Arquitetura que combina busca em base de conhecimento com geração por LLM, permitindo respostas fundamentadas em documentos específicos. |
| **Sampling** | Processo de selecionar o próximo token a partir da distribuição de probabilidade gerada pelo modelo. Temperatura, top-p e top-k são parâmetros de sampling. |
| **System prompt** | Instrução enviada ao modelo que define seu comportamento, personalidade e regras. Processada antes das mensagens do usuário. |
| **Temperatura** | Parâmetro que controla a aleatoriedade do sampling. 0 = determinístico; >1 = cada vez mais aleatório. |
| **Token** | Unidade fundamental de processamento do LLM. Pode ser uma palavra, subpalavra, caractere ou byte. Texto é convertido em tokens antes de ser processado. |
| **Top-k** | Método de sampling que considera apenas os k tokens mais prováveis, descartando o resto. |
| **Transformer** | Arquitetura de rede neural baseada em mecanismos de atenção, publicada em 2017, que é a base de todos os LLMs modernos. |
| **Vector database** | Banco de dados otimizado para armazenar e buscar vetores de alta dimensão (embeddings), essencial para RAG. Exemplos: Pinecone, pgvector, Weaviate. |
| **Zero-shot prompting** | Dar uma instrução ao modelo sem nenhum exemplo, confiando em seu conhecimento pré-treinado. |