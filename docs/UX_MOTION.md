# UX, loading e motion

## Fonte e lente de design

Skill indicada pelo usuário: [`kylezantos/design-motion-principles`](https://github.com/kylezantos/design-motion-principles), licença MIT, modos Create e Audit. A skill descreve uma síntese de trabalhos publicados de Emil Kowalski, Jakub Krehel e Jhey Tompkins; os três designers não são autores nem endorsers da skill. Para este CRM de produtividade, priorizar contenção e rapidez (lente Emil), polimento sutil (Jakub) e usar exploração criativa seletivamente em onboarding/empty states (Jhey).

Antes de criar/revisar animações, agente deve instalar/ler a skill (`npx skills add kylezantos/design-motion-principles`) ou consultar o repositório, carregar workflow Create/Audit apropriado e referências de acessibilidade/performance. Não dizer que ela foi instalada automaticamente neste repositório: integração ainda não foi executada.

## Contrato de estados por interface

| Estado | Comportamento esperado |
|---|---|
| Loading | Indicar o trabalho atual sem layout shift. Skeleton alinhado à forma do conteúdo apenas se a espera for perceptível; para ação local curta, feedback de botão/estado é suficiente. |
| Lazy loading | Dividir código por rota e adiar imagens/áreas pesadas não essenciais; não atrasar o conteúdo visível principal ou ação imediata. Exibir placeholder de dimensões conhecidas e fallback de erro onde necessário. |
| Empty | Explicar por que está vazio e oferecer próxima ação; não simular dados reais nem forçar animação decorativa. |
| Error | Preservar o que o usuário digitou quando seguro, explicar o próximo passo e permitir retry; não esconder erro atrás de spinner. |
| Success | Confirmar a mudança com status textual acessível; animação curta apenas se ajudar a perceber a transição. |
| Progress | Percentual só para tarefa com total/progresso mensurável. Operação indeterminada: status/indicador sem percentual fictício, com nome acessível. |

## Padrões de motion

- Motion deve explicar relação de causa, direção, continuidade ou feedback. A pergunta antes de cada animação: “isso ajuda a entender a mudança, ou só enfeita?”.
- Basear durações na frequência/contexto. Para utilitário frequente, quase instantâneo e discreto (em geral abaixo de 300 ms; 180 ms é uma referência, não regra universal). Respeitar resposta imediata.
- Entrada/saída de modal, drawer, toast e item de lista pode ser animada quando isso ajuda a orientar; garantir saída observável e não bloquear interação.
- Evitar animar cada card/título ao montar a página, stagger em listas longas, escala em todo hover, pulso contínuo, blur gratuito, bounce em ação utilitária e `scale(0)` inicial. Preferir `opacity`/`transform` e manter `will-change` apenas durante necessidade real.
- Ações acionadas por teclado não devem receber atraso de animação; mudanças de estado frequentes não precisam de movimento.

## Acessibilidade obrigatória

- Implementar `prefers-reduced-motion: reduce` removendo movimento não essencial e mantendo indicação/feedback alternativo.
- Operação assíncrona com semântica correta (`aria-busy`, região/status anunciado sem repetição abusiva, nome acessível, foco previsível). Não depender só de cor ou motion.
- Respeitar teclado/foco visível/esc leitores, evitar movimento contínuo e efeitos que possam causar desconforto vestibular.
- Não esconder conteúdo essencial até fim da animação. Animação não substitui atualização textual de estado.

## Aceite de uma Issue de UI

Critérios adequados ao escopo: loading/empty/error/success cobertos; skeleton onde a duração/percepção justifica; lazy-load seletivo; progresso verdadeiro ou feedback indeterminado; entrada/saída contextual; reduced-motion; foco/teclado; mobile; teste manual ou Playwright das transições relevantes; motion audit quando há mudança ampla de linguagem visual.

## Fontes consultadas

- [Repositório da skill](https://github.com/kylezantos/design-motion-principles)
- [SKILL.md da skill](https://github.com/kylezantos/design-motion-principles/blob/main/skills/design-motion-principles/SKILL.md)

A exigência do usuário de “skeleton, lazyloading, animação e progresso em todos os elementos” é interpretada como cobertura sistemática de **todos os estados e fluxos assíncronos**, não animação literal em cada elemento: a própria skill recomenda gate de frequência, evitar motion supérfluo e tornar `prefers-reduced-motion` obrigatório. Progresso percentual falso e skeleton em resposta instantânea degradam UX, então não serão implementados.
