# CC-101 Part 2 — Illustration Prompts for Gemini Image Generation

Style guide for all images: flat design infographic style, clean lines, vibrant but not neon colors, white or very light gray background, LEGO-inspired brick shapes (rounded rectangular blocks with visible studs on top), no photorealism, no 3D rendering, minimal shadows, clear readable labels in Portuguese, consistent color palette across all images (blue for English, orange for Portuguese, green for correct/selected, red for wrong/danger, gray for neutral).

---

## 0. O que é um token: texto vira peças

Ilustração horizontal lida da esquerda pra direita, mostrando a transformação de texto em tokens. Toda a imagem em português.

No lado esquerdo, uma frase escrita em texto normal, como se fosse digitada numa tela: "Eu gosto de chocolate". O texto está em fonte limpa, preta, sem decoração.

No centro, uma seta larga apontando pra direita com o texto "tokenização" escrito dentro da seta.

No lado direito, a mesma frase desmontada em peças LEGO individuais dispostas numa fileira horizontal. Cada peça tem duas informações visíveis: o fragmento de texto escrito na face de cima da peça, e o número inteiro (ID do token) escrito na face frontal da peça. As peças têm tamanhos diferentes dependendo do fragmento:

- Peça grande (amarela): "Eu" / ID: 15711
- Peça grande (azul): " gosto" / ID: 45892
- Peça pequena (verde): " de" / ID: 347
- Peça grande (vermelha): " chocolate" / ID: 28401

Abaixo da fileira de peças, o texto: "Computadores não entendem texto. Entendem números."

Abaixo disso, uma segunda linha menor mostrando a variação de granularidade: a palavra "tokenização" sozinha, desmontada em 4 peças pequenas: "token" / "iza" / "ção" — com uma anotação: "Uma palavra pode virar várias peças."

Estilo infográfico flat, fundo branco, peças LEGO com studs visíveis no topo. Os IDs dos tokens são números inventados mas plausíveis (5 dígitos). Sem setas além da seta central de transformação. Sem texto em inglês.

---

## 1. Tokenização: inglês vs português

A clean side-by-side infographic comparing English and Portuguese tokenization using LEGO bricks. Left panel labeled "Inglês" with a blue header: a horizontal row of 5 large, wide LEGO bricks in solid colors (blue, green, yellow, teal, gray), each brick has a word printed on it: "Have", "a", "great", "day", "!". Below the row: "5 tokens". Right panel labeled "Português" with an orange header: a horizontal row of 8 noticeably narrower and smaller LEGO bricks: "Ten", "ha", "um", "ó", "t", "imo", "dia", "!". The bricks for "ó" and "t" are visibly the smallest. Below the row: "8 tokens". Above each row, the full sentence is printed: "Have a great day!" and "Tenha um ótimo dia!". Between the two panels, centered text: "+60% mais peças pra dizer a mesma coisa". Flat design, no arrows, no flow lines, just bricks as objects on a white background.

---

## 2. A mesa de contexto (context window)

A top-down perspective view of a rectangular table surface (the "mesa") with a subtle 3D tilt. The table has a clear fixed border. Inside, three horizontal zones with different colors: left zone (25% width, light blue) labeled "Seu input: instrução, histórico, arquivos"; middle zone (50% width, light yellow, noticeably dimmer) labeled "Contexto de referência"; right zone (25% width, light green) labeled "Resposta sendo construída". Along the right edge of the table, a small stack of LEGO bricks falls off the edge with a label "Não cabe na mesa = não existe pro modelo". Along the bottom edge, a thin gradient bar runs the full width: bright on the left, dim in the middle, bright on the right, with a label beneath: "Atenção do modelo: forte nas bordas, fraca no meio". The table edge is labeled "1M tokens (varia por modelo)". Flat infographic style, top-down view, clean and minimal.

---

## 3. Geração autorregressiva: uma peça por vez

Ilustração estilo comic-strip com três painéis horizontais lado a lado. Cada painel mostra uma superfície LEGO (base com studs) vista de cima com leve ângulo. Toda a imagem em português. Os dados abaixo devem ser seguidos EXATAMENTE como escritos.

Painel 1 — título "Passo 1" no topo: três peças LEGO cinza já encaixadas na base, com os textos "O", "céu", "está". À direita delas, um espaço vazio marcado com "?". Abaixo da base, três peças candidatas flutuam: uma peça verde com "azul (25%)" é a maior e mais destacada; uma peça amarela com "nublado (15%)"; uma peça cinza clara com "claro (12%)". Uma seta pontilhada sai de "azul" e aponta pra cima em direção ao espaço vazio.

Painel 2 — título "Passo 2" no topo: quatro peças na base: "O", "céu", "está", "azul" (esta última em verde). Espaço vazio com "?" à direita. Abaixo, candidatas: "e (20%)", "hoje (15%)", ". (10%)". Seta pontilhada de "hoje" pro espaço vazio.

Painel 3 — título "Passo 3" no topo: cinco peças na base: "O", "céu", "está", "azul", "hoje". Espaço vazio com "?" à direita. Abaixo, candidatas: ". (35%)" maior, ", (12%)" menor. Seta pontilhada de "." pro espaço vazio.

Abaixo dos três painéis, legenda centralizada em negrito: "Sem plano. Uma peça por vez. Sempre."

Estilo infográfico flat, cores consistentes entre painéis, labels limpos. Fundo branco.

---

## 4. Mecanismo de atenção: o modelo acende o que importa

A top-down view of the same rectangular mesa from illustration 2, now populated with seven LEGO bricks in a row: "O", "banco", "está", "na", "margem", "do", "rio". The brick "banco" is highlighted with a bold golden border and slightly elevated. From "banco", radial glow lines emanate outward to each other brick. The lines to "margem" and "rio" are thick, bright, and vivid orange. The lines to "O", "está", "na", "do" are thin and very faded gray. The bricks "margem" and "rio" glow brightly (orange halo), while the other bricks are dimmer. Above the mesa: "Qual 'banco' é esse?". Below the mesa: "O modelo 'acende' as peças mais relevantes." A small legend in the corner shows a thick bright line labeled "atenção forte" and a thin faded line labeled "atenção fraca". No directional arrows, only radial glow lines. Flat infographic, warm color palette.

---

## 5. Temperatura: quão fundo a mão vai na caixa

Ilustração com uma única caixa LEGO grande no centro da imagem, vista de frente com corte frontal para mostrar o interior. Toda a imagem em português. Nenhuma palavra em inglês.

A caixa: retangular, alta, vista de frente com a parede frontal removida (corte transversal). No topo da caixa, o texto "Vocabulário" (este texto aparece UMA ÚNICA VEZ, apenas aqui). Dentro da caixa, as peças estão organizadas em camadas de cima pra baixo: camada do topo com três peças LEGO grandes e azuis; camada do meio com peças verdes menores; camada de baixo com peças pequenas e coloridas misturadas; e no fundo absoluto, uma única peça vermelha em formato de roda.

Quatro linhas horizontais tracejadas cortam a caixa em quatro profundidades, cada uma com um label à direita indicando a temperatura e o comportamento:

- Linha 1 (no topo da caixa, tocando as peças azuis): "0.0 — Sempre a mesma peça"
- Linha 2 (entre as peças azuis e verdes): "0.3 — Pequenas variações"
- Linha 3 (no meio da caixa, entre as peças verdes): "0.7 — Criativo"
- Linha 4 (no fundo, tocando a roda vermelha): "1.5 — Incoerente"

Um braço robótico simples entra pela abertura superior da caixa. A posição do braço pode estar em qualquer uma das profundidades.

Todos os labels devem estar alinhados à direita da caixa, centralizados verticalmente na sua respectiva linha. Estilo infográfico flat, fundo branco, linhas limpas. Sem grid 2x2, sem painéis separados. Uma única composição com uma única caixa.

---

## 6. Famílias de modelos: do Duplo ao Technic

A horizontal spectrum bar running left to right on a white background. Left end labeled "Mais rápido / mais barato", right end labeled "Mais capaz / mais caro". Above the spectrum, four LEGO kit boxes are positioned at different points along it, each drawn to look like a simplified LEGO product box. Box 1 (far left, light blue): "Modelos Rápidos" — shows large simple Duplo-style bricks on the box art. Below: "Haiku · GPT-4o-mini · Flash" and "$0.15–$1/MTok". Box 2 (center-left, teal): "Modelos de Código" — shows medium regular LEGO bricks. Below: "GPT-4.1 · Claude Code". Box 3 (center-right, dark blue): "Modelos de Raciocínio" — shows Technic gears and axles on box art. Below: "Opus · o3-pro · Gemini 2.5 Pro" and "$1.25–$20/MTok". Box 4 (far right, slightly below the spectrum, green): "Open-weight" — shows an open box with all pieces visible and exposed. Below: "Llama 4 · DeepSeek R1" and "Você monta e adapta." Below the entire spectrum, a rule in bold: "Comece pelo mais barato que pode funcionar." Flat infographic style, clean product-box silhouettes.

---

## 7. Limitações: alucinação e mesa limpa

A two-panel illustration. Left panel titled "Alucinações": A small LEGO building on a mesa, viewed at a 3/4 angle. The front face of the building looks perfect — neat, colorful, well-assembled bricks forming a complete facade with a door and windows. But the back and side are visible in the 3/4 view, revealing that the building is completely hollow — no back wall, no internal structure, just a facade. An arrow pointing to the front: "Parece correto." An arrow pointing to the hollow back: "Sem verificação interna." Right panel titled "Mesa limpa entre conversas": Two stacked scenes separated by a dashed line. Top scene: a mesa with a complete LEGO construction on it, labeled "Conversa 1 — montagem completa." Bottom scene: the same mesa, completely empty and clean, labeled "Conversa 2 — mesa zerada." Between them, a broom icon. Below: "Se precisar lembrar, você recoloca na mesa." Flat infographic, clean and impactful.

---

## 8a. Custo: consultar vs construir

Ilustração lado a lado comparando o custo de input vs output com a metáfora LEGO. Toda a imagem deve estar em português. Nenhuma palavra em inglês aparece na imagem.

Lado esquerdo: título "Input — consultar" no topo. Uma mão humana despeja um monte de peças LEGO soltas sobre uma mesa de madeira. As peças caem espalhadas, empilhadas de qualquer jeito. Uma etiqueta de preço verde pendurada na pilha: "$3 por 1M peças". Nenhum outro texto neste lado.

Lado direito: título "Output — construir" no topo. A mesma mesa, mas agora um braço robótico segura uma única peça LEGO com precisão, encaixando-a no topo de uma construção organizada. Um cone de luz (spotlight) ilumina toda a superfície da mesa. Uma etiqueta de preço vermelha pendurada no braço: "$15 por 1M peças". Abaixo da construção, o texto: "Cada peça exige olhar a mesa inteira antes de encaixar."

Abaixo das duas cenas, uma legenda centralizada: "Consultar é jogar peças na mesa. Construir é encaixar uma por vez. Por isso output custa 3–5x mais."

Estilo: infográfico flat, linhas limpas, fundo branco ou cinza muito claro, peças LEGO estilizadas com studs visíveis. Sem texto em inglês em nenhum lugar da imagem.

---

## 8b. O imposto linguístico: três camadas, um problema

A vertical cascade of three layers, read top to bottom, each showing the same comparison between English (blue) and Portuguese (orange), with each layer building on the previous one. Layer 1 labeled "Mais peças" (callback to section 1): two short horizontal rows of LEGO bricks side by side. The English row has 5 large bricks. The Portuguese row has 8 smaller bricks. Same total row width, different brick count. A small "=" sign between the two final constructions shows they represent the same content. Layer 2 labeled "Menos espaço na mesa" (callback to section 2): two identical table surfaces side by side. The English table has ample empty space remaining after placing its bricks. The Portuguese table is noticeably more crowded with the same content taking up more surface area — less breathing room. Layer 3 labeled "Conta mais cara" (this section): two identical cash register displays or simple receipt slips side by side. The English receipt shows "$100". The Portuguese receipt shows "$135". The Portuguese receipt has a highlighted "+35%" badge. A vertical arrow runs along the left side connecting all three layers, labeled: "Mesmo problema, três camadas." At the bottom, a single caption: "O português consome mais peças, ocupa mais mesa e custa mais. Não são três problemas." Flat infographic, clean vertical flow, blue and orange color coding consistent throughout all three layers.
