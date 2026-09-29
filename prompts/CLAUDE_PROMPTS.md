# Prompts de trabalho para Claude

Use estes prompts no Claude Code com o repositório aberto. Substitua os campos entre `<...>`. `AGENTS.md` é a regra permanente e prevalece sobre prompts pontuais.

## 0. Inicialização de qualquer sessão

```text
Você está no repositório OrçaVolta. Antes de agir, leia AGENTS.md, README.md, CONTRIBUTING.md e a documentação pertinente em docs/. Este produto é uma hipótese ainda não validada: CRM leve para follow-up de orçamentos de prestadores de climatização pequenos. Não expanda o escopo.

A regra de trabalho é obrigatória: toda correção, melhoria, função, documentação, teste, refatoração ou infraestrutura tem uma GitHub Issue primeiro e termina em Pull Request vinculado com `Closes #N` ou `Refs #N`. Não invente números. Confirme que a Issue #<N> existe e leia seus critérios; se não existir ou você não tiver acesso, pare e peça o acesso necessário. Não faça push direto em main nem deploy manual.

Diga qual Issue vai trabalhar, o que vai alterar, o que não vai alterar e como vai validar. Faça a menor mudança que atende critérios. Execute checks reais e relate comandos/resultados. Ao concluir, prepare uma descrição de PR que mencione a Issue e indique se o deploy ainda não ocorreu.
```

## 1. Descoberta e validação (sem código de produto)

```text
Leia docs/PRODUCT_BRIEF.md e docs/VALIDATION_PLAN.md. Trabalhe somente na Issue #<N> de pesquisa. Não escreva código nem presuma que a dor está comprovada.

Crie roteiro de entrevista não indutivo para prestadores de instalação/manutenção de ar-condicionado. Priorize perguntas sobre episódios passados, processo atual, volume, impacto, alternativas e custo de não agir. Defina um formato de síntese anônima separando evidência, interpretação e próxima hipótese. Não invente entrevistas, métricas, dados de mercado ou depoimentos. Não inclua nome/telefone/endereço de entrevistado em arquivos do GitHub.

Entregue roteiro, modelo para anotações e critérios de decisão para continuar/ajustar/parar. Se editar docs, mantenha a mudança vinculada à Issue e proponha PR; registre o que ainda precisa ser observado em campo.
```

## 2. Arquitetura e decisão técnica

```text
Trabalhe exclusivamente na Issue #<N>. Leia AGENTS.md, docs/ARCHITECTURE.md e os arquivos existentes antes de propor stack. Priorize performance percebida, simplicidade operacional e custo total, sem assumir que tiers gratuitos duram ou servem produção.

Faça reconnaissance do repositório; apresente opções concretas e trade-offs para frontend/server rendering, auth, banco PostgreSQL, deploy, backups, telemetria e teste. Verifique fontes oficiais atuais para preço/limites se isso for necessário; não use resultados de busca incompletos como evidência. Registre a decisão em um ADR aprovado pela Issue antes de adicionar dependências ou criar arquitetura irreversível.

Para multi-tenant, documente validação no servidor e isolamento por organização no banco, além de teste negativo de acesso cruzado. Não codifique credenciais nem habilite serviço externo pago. Abra PR com Issue vinculada.
```

## 3. Implementar uma Issue de software

```text
Implemente somente a Issue #<N>: <título>. Leia o conteúdo da Issue e AGENTS.md. Confirme que Issue existe e os critérios são testáveis. Antes de editar, resuma plano curto e arquivos/áreas prováveis; não amplie escopo sem nova Issue.

Se houver mudança de UI/motion, consulte a skill design-motion-principles: `npx skills add kylezantos/design-motion-principles` se o ambiente permitir, leia o workflow Create correspondente e `references/accessibility.md` / `references/performance.md`. Para auditoria de UI use modo Audit. Não alegue execução da skill se não a consultou. Aplique lens de SaaS de produtividade: contenção/velocidade primeiro, polimento sutil depois, experimentação apenas quando fizer sentido.

Implemente testes unitários para regra de negócio, integração para persistência/API e Playwright para jornada crítica aplicável. Cobrir estados loading/skeleton, vazio, erro e sucesso; lazy-load sem atrasar caminho crítico; progresso numérico apenas quando mensurável; respeitar prefers-reduced-motion, teclado, foco, mobile e privacidade. Nunca logue PII.

Execute lint/format, typecheck, testes pertinentes, Knip/ArchContract quando configurados e checks disponíveis. Não diga “passou” sem executar. Ao terminar, resuma arquivos, riscos e testes. Prepare PR conciso com `Closes #<N>` na descrição, screenshots se houver UI, migração/rollback se houver DB. Não faça merge ou deploy; aguarde fluxo autorizado.
```

## 4. Revisão de motion e acessibilidade

```text
Audite as telas/componentes alterados pela Issue #<N> usando o modo Audit de kylezantos/design-motion-principles. Leia a skill e referências de accessibility, performance, audit-checklist e anti-checklist pertinentes. Para este SaaS, ponderar Emil como primário, Jakub como secundário e Jhey seletivamente.

Verifique gaps em estados condicionais, loading/erro/vazio/sucesso, entradas/saídas, keyboard-initiated motion, frequência de interação, prefers-reduced-motion, foco, semântica, movimento contínuo, CSS de layout e padrões de motion gerado sem propósito. Não recomendar animação indiscriminada em todos os elementos.

Entregue achados classificados por severidade com arquivo/linha, impacto e correção proposta. Se a Issue autorizar correção, implemente no mesmo escopo; caso contrário, proponha Issues separadas e não modifique arquivos.
```

## 5. Revisão final de PR e checklist de release

```text
Faça revisão independente da PR da Issue #<N>. Não assuma que o código do agente anterior está correto. Compare diff com critérios de aceite; procure bugs, regressões de autorização/tenant, vazamento de PII, migrations inseguras, falhas loading/error, acessibilidade, tipos frouxos, dependências supérfluas e testes frágeis.

Execute os checks disponíveis e reporte evidência exata. Confira descrição do PR contém `Closes #<N>` ou `Refs #<N>`, motivo, riscos, screenshots e testes. Não aprove/deploy se houver falha crítica ou CI pendente. Não faça merge nem deploy sem processo/autorização configurados. Em release, confirmar CI verde, staging/smoke, monitoramento, rollback e link de execução real.
```

## 6. Rascunhar Issues a partir de uma decisão aprovada

```text
Leia a decisão/documento aprovado e transforme cada unidade independente de trabalho em rascunho de GitHub Issue. Não publique Issue sem acesso/solicitação explícita. Cada rascunho deve ter título, tipo/labels, problema/contexto, resultado esperado, escopo e critérios de aceite verificáveis, testes necessários, dependências, risco de dados/privacidade e Definition of Done. Evite duplicatas e não invente números. Um PR futuro de implementação sempre deve mencionar o número real da Issue.
```
