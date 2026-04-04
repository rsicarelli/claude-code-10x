Faca uma analise tecnica profunda da arquitetura do Claude Code.

Comece pelo loop agentico. Quero entender o ciclo completo: como uma query do usuario se transforma em plano, como o plano dispara chamadas de ferramentas, como as observacoes alimentam a proxima iteracao e como a resposta final e montada. Descreva esse fluxo com clareza suficiente para alguem reimplementar.

Liste todas as tools disponiveis (Read, Write, Edit, Bash, Glob, Grep, Agent, etc.) e explique como a orquestracao entre elas funciona. Como o modelo decide qual tool usar? Existe priorizacao?

Explique o conceito de "harness" -- o software que envolve o modelo. Qual e a responsabilidade do harness vs a responsabilidade do modelo? Como o system prompt instrui o modelo, e qual e a sua estrutura?

Quero entender o gerenciamento da janela de contexto em detalhe: o que o Claude Code decide manter, o que descarta, e como essas decisoes sao tomadas. Como funciona o modelo de permissoes que controla o que a IA pode e nao pode fazer?

Cubra todo o sistema de configuracao: settings.json, CLAUDE.md, hooks, skills e MCP. Qual e a hierarquia entre eles? Explique os modos de operacao (interativo, plan, headless) e quando cada um faz sentido.

Para fechar, faca uma comparacao arquitetural com Cursor, Copilot e outras ferramentas. Onde o Claude Code fez escolhas de design diferentes, e por que?

Busque docs oficiais da Anthropic, blog posts e analises do codigo-fonte.
