# Instruções obrigatórias para agentes de código

Estas instruções valem para Claude, Manus e qualquer agente/modelo que trabalhe neste repositório. Em caso de conflito, siga as regras mais restritivas de segurança e as decisões documentadas em `docs/`.

## 1. Antes de alterar qualquer coisa

- Leia este arquivo, `README.md`, `CONTRIBUTING.md` e a documentação pertinente em `docs/`.
- Confirme a Issue GitHub da tarefa. Correção, melhoria, nova função, documentação, refatoração, segurança, teste e infraestrutura também precisam de Issue.
- Se não houver Issue, **não implemente**: solicite autorização/acesso para abrir uma Issue ou apresente um rascunho para aprovação. Não invente número de Issue.
- Confirme escopo, fora de escopo e critérios de aceite. Divida tarefas grandes em Issues menores, mantendo vínculo com a Issue-pai.
- Não altere decisões de produto que ainda são hipóteses sem registrar a evidência e a decisão.

## 2. GitHub: fluxo obrigatório

- Uma Issue por unidade de trabalho revisável, com tipo (`bug`, `feature`, `improvement`, `docs`, `security`, `chore`), contexto, resultado esperado e critérios de aceite verificáveis.
- Criar branch a partir de `main`: `feat/<issue>-<slug>`, `fix/<issue>-<slug>`, `docs/<issue>-<slug>` ou `chore/<issue>-<slug>`.
- Não fazer commit/push diretamente em `main`; não contornar revisão ou CI.
- Abrir PR para toda mudança. A descrição do PR deve conter `Closes #<número>` para fechar Issue; usar `Refs #<número>` quando a Issue continuar aberta. Incluir resumo, risco, migrações, screenshots quando houver UI e testes executados.
- Não afirmar que um deploy ocorreu sem verificar o status real do pipeline. PR não é deploy: produção é atualizada apenas pelo workflow após merge aprovado em `main`.
- Falha de CI, permissão ou conector: pare no bloqueio, relate a causa e peça o acesso necessário. Não tente contornar controles.

## 3. Qualidade e testes

- Escreva/atualize testes junto com a mudança. A correção não está concluída se critérios de aceite ou testes falharem.
- Para lógica: unitários; persistência/API: integração; fluxo crítico do usuário: Playwright E2E.
- Verifique lint/format (`Biome`), tipos, testes, dependências não utilizadas (`Knip`) e contratos arquiteturais (`ArchContract`). Use Commitlint para mensagens convencionais quando configurado.
- Adicione cobertura via Codecov quando autorizado/configurado. Mutation testing com StrykerJS deve ser habilitado para regras críticas e executado em job apropriado; registre o custo de CI e não reduza cobertura para “passar”.
- Não marque verificações como aprovadas sem executá-las. Informe comandos, resultado e qualquer limitação.

## 4. Produto, privacidade e segurança

- Escopo atual: CRM mínimo de orçamento/follow-up para prestadores pequenos de serviços de climatização, sujeito à validação. Não adicione envio automatizado, cobrança, fiscal, estoque ou IA sem nova decisão/Issue.
- Trate dados de clientes como pessoais: minimize coleta, limite retenção, proteja segredos, aplique isolamento por organização no backend e não use dados reais em fixtures/logs.
- Toda leitura/escrita deve verificar autenticação e vínculo à organização no servidor. Nunca confie somente na UI ou em `organization_id` enviado pelo browser.
- Não registre tokens, conteúdo de orçamento, telefone, e-mail ou identificadores pessoais em logs/eventos de analytics. Não inclua segredos no repositório.
- Mudanças de schema precisam de migração revisável e plano de reversão compatível.

## 5. Interface, motion e acessibilidade

- Antes de criar/revisar motion, instalar/ler e seguir a skill [`kylezantos/design-motion-principles`](https://github.com/kylezantos/design-motion-principles) em modo Create ou Audit, conforme a tarefa.
- Para este SaaS de produtividade: Emil Kowalski como lente primária (contenção/velocidade), Jakub Krehel secundária (polimento), Jhey apenas seletivamente em onboarding/estados vazios.
- Cada tela assíncrona precisa tratar loading, erro, vazio e sucesso. Use skeleton para dados estruturais quando a espera for perceptível; evite flash/skeleton em respostas instantâneas. Use progresso percentual apenas quando houver progresso mensurável; caso contrário, feedback indeterminado acessível.
- Lazy-load rotas e componentes pesados fora do caminho crítico. Não atrasar conteúdo/controles primários nem carregar sob demanda algo necessário para a ação imediata.
- Adicione entrada/saída/transição somente quando esclarecer mudança de estado; prefira transições discretas, sobretudo em ações frequentes. Animações iniciadas por teclado e ações repetidas não devem atrasar a resposta.
- Respeite `prefers-reduced-motion`; forneça alternativa sem movimento. Prefira `transform`/`opacity`, evite layout thrash, pulsing contínuo, blur decorativo, hover-scale em tudo, stagger indiscriminado e motion automático de conteúdo estático.
- UI precisa ser navegável por teclado, ter foco visível, contraste adequado e semântica/ARIA correta. Teste loading/erro/vazio em viewport móvel.

## 6. Conclusão da tarefa

Ao finalizar, reporte: Issue/PR, arquivos mudados, critérios de aceite, testes/comandos e resultado, riscos pendentes e estado do deploy (com evidência). Se o acesso ao GitHub estiver indisponível, forneça patch e texto de Issue/PR, mas deixe claro que não foram publicados.
