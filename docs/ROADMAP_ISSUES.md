# Roadmap e rascunhos de GitHub Issues

**Status:** Issues #1–#13 foram publicadas em [Pablo-Gaspar/Or-aVolta](https://github.com/Pablo-Gaspar/Or-aVolta/issues). A publicação desta documentação está vinculada à [Issue #14](https://github.com/Pablo-Gaspar/Or-aVolta/issues/14). Os números abaixo seguem a mesma ordem do backlog e são IDs internos de referência; abra uma Issue adicional para novo trabalho e ajuste critérios com evidência das entrevistas.

| Issue GitHub | Rascunho deste documento |
|---:|---|
| [#1](https://github.com/Pablo-Gaspar/Or-aVolta/issues/1) | Validar a dor de follow-up no nicho de climatização |
| [#2](https://github.com/Pablo-Gaspar/Or-aVolta/issues/2) | Definir stack, ADRs e scaffold inicial |
| [#3](https://github.com/Pablo-Gaspar/Or-aVolta/issues/3) | Configurar pipeline CI e governança de PR |
| [#4](https://github.com/Pablo-Gaspar/Or-aVolta/issues/4) | Criar fundação visual e estados da interface |
| [#5](https://github.com/Pablo-Gaspar/Or-aVolta/issues/5) | Implementar autenticação e isolamento por organização |
| [#6](https://github.com/Pablo-Gaspar/Or-aVolta/issues/6) | Cadastrar e listar clientes com dados mínimos |
| [#7](https://github.com/Pablo-Gaspar/Or-aVolta/issues/7) | Registrar orçamentos e acompanhar status |
| [#8](https://github.com/Pablo-Gaspar/Or-aVolta/issues/8) | Painel de retornos de hoje e atrasados |
| [#9](https://github.com/Pablo-Gaspar/Or-aVolta/issues/9) | Adicionar testes E2E dos fluxos críticos |
| [#10](https://github.com/Pablo-Gaspar/Or-aVolta/issues/10) | Instrumentar erros e telemetria com OpenTelemetry + Sentry |
| [#11](https://github.com/Pablo-Gaspar/Or-aVolta/issues/11) | Implementar contratos arquiteturais e quality gates |
| [#12](https://github.com/Pablo-Gaspar/Or-aVolta/issues/12) | Política de privacidade, exportação e exclusão |
| [#13](https://github.com/Pablo-Gaspar/Or-aVolta/issues/13) | Preparar staging e deploy controlado por PR |

## Epics e ordem sugerida

| Ordem | Epic | Objetivo | Gate |
|---|---|---|---|
| 0 | Descoberta | Verificar dor e público | Entrevistas e protótipo demonstram sinal |
| 1 | Base do produto | Scaffold, CI, autenticação e isolamento | Acesso por organização testado |
| 2 | Fluxo de orçamento | Clientes, pipeline e retorno diário | Fluxo central funciona em mobile |
| 3 | Confiabilidade | Testes, observabilidade, segurança | CI e alertas operacionais úteis |
| 4 | Piloto | Deploy controlado e feedback | Pilotos consentidos e custo limitado |

## Issue 0 — Validar a dor de follow-up no nicho de climatização

**Tipo:** pesquisa/produto · **Labels sugeridas:** `research`, `product`, `P0`

**Contexto:** hipótese do Product Brief ainda não foi verificada. **Tarefa:** conduzir 15–20 entrevistas sem vender a solução prematuramente; registrar evidência anônima, frequência do problema, alternativas, impacto e disposição a testar/pagar.

**Critérios de aceite:** roteiro neutro documentado; critérios do plano de validação revistos após cinco conversas; síntese separa fatos e inferências; decisão explícita de continuar, ajustar nicho ou parar; nenhuma PII desnecessária incluída no GitHub.

## Issue 1 — Definir stack, ADRs e scaffold inicial

**Tipo:** melhoria/infraestrutura · **Labels:** `architecture`, `chore`, `P1`

**Contexto:** escolher stack após confirmar viabilidade de deploy/limites. Proposta inicial: Next.js App Router + TypeScript com renderização server-first, PostgreSQL via serviço gerenciado compatível, validação server-side e UI mobile-first.

**Critérios de aceite:** ADR registra decisão e alternativas/custos; projeto inicia localmente conforme README; versões e package manager fixados; secrets fora do git; CI valida lint, tipos e testes básicos; nenhum serviço pago habilitado automaticamente.

## Issue 2 — Configurar pipeline CI e governança de PR

**Tipo:** melhoria/infraestrutura · **Labels:** `ci`, `quality`, `P1`

**Critérios de aceite:** PR template exige Issue, escopo, evidências e testes; checks em branch protection são documentados/configurados; workflow executa Biome, typecheck, unitários e verificação de dependências; integração de Codecov é opcional até token/conta autorizado; deploy não ocorre em push direto.

## Issue 3 — Criar fundação visual e estados da interface

**Tipo:** nova função · **Labels:** `frontend`, `design-system`, `accessibility`, `P1`

**Critérios de aceite:** tokens mínimos e componentes de status documentados; telas assíncronas cobrem loading/skeleton, vazio, erro e sucesso; lazy-loading só em rotas/componentes não críticos; movimento respeita `prefers-reduced-motion`; teclado não sofre atraso; Playwright verifica fluxo de loading e navegação por teclado no que for viável.

## Issue 4 — Implementar autenticação e isolamento por organização

**Tipo:** nova função · **Labels:** `security`, `backend`, `P1`

**Critérios de aceite:** usuário acessa somente sua organização; toda leitura/escrita confere autorização no servidor/DB, não só na UI; testes negativos tentam acesso cruzado; migrações versionadas; logout e sessão expirada têm estado claro; nenhum segredo é exposto no cliente.

## Issue 5 — Cadastrar e listar clientes com dados mínimos

**Tipo:** nova função · **Labels:** `frontend`, `backend`, `P1`

**Critérios de aceite:** criar, visualizar, editar e pesquisar cliente com campos mínimos; validação e mensagens úteis; isolamento por organização; vazio/loading/erro; testes unitários e de integração; não capturar PII que não seja necessária.

## Issue 6 — Registrar orçamentos e acompanhar status

**Tipo:** nova função · **Labels:** `product`, `frontend`, `backend`, `P1`

**Critérios de aceite:** registrar cliente, título, valor opcional, data, status e próxima ação; transições válidas entre novo, enviado, ganho e perdido; motivo de perda opcional; histórico suficiente sem guardar mensagem do cliente; servidor aplica regras e organização; testes de regras de negócio e validação.

## Issue 7 — Painel de retornos de hoje e atrasados

**Tipo:** nova função · **Labels:** `product`, `frontend`, `P1`

**Critérios de aceite:** lista ordena retornos vencidos e de hoje de forma previsível; usuário pode reagendar ou marcar resultado; atualizações são confirmadas; estados vazio/loading/erro definidos; responsivo e acessível; E2E cobre fluxo de retorno.

## Issue 8 — Adicionar testes E2E dos fluxos críticos

**Tipo:** melhoria de qualidade · **Labels:** `testing`, `playwright`, `P1`

**Critérios de aceite:** Playwright cobre login/organização, criar orçamento e concluir retorno; testes não usam dados reais nem ambiente de produção; fixtures isoladas; relatório legível no CI; retry não mascara falha sistemática.

## Issue 9 — Instrumentar erros e telemetria com OpenTelemetry + Sentry

**Tipo:** melhoria/observabilidade · **Labels:** `observability`, `P1`

**Critérios de aceite:** erros não tratados aparecem com contexto técnico e trace/correlation ID; não há PII em breadcrumbs/tags; health check e documentação operacional existem; alertas testados em staging; sampling/limites documentados; variável/secrets configurados fora do repositório; fornecedor e custo aprovados.

**Fase posterior:** validar exportadores compatíveis com Datadog ou New Relic, escolher um backend de APM mediante necessidade/orçamento; não duplicar ingestão simultânea por padrão.

## Issue 10 — Implementar contratos arquiteturais e quality gates

**Tipo:** melhoria de qualidade · **Labels:** `architecture`, `quality`, `P1`

**Critérios de aceite:** Biome, ArchContract, Knip, Commitlint e StrykerJS avaliados/configurados conforme stack; CI explica como corrigir cada falha; Stryker mede regras de domínio selecionadas; custo/tempo de execução monitorado; itens pesados podem rodar em job agendado até haver justificativa para bloquear todos os PRs.

**Nota de nomenclatura:** interpretamos “Comilint” como **Commitlint** e “Stryke” como **StrykerJS**; confirmar antes de codificar. ArchContract é uma ferramenta/contrato separado do linter.

## Issue 11 — Política de privacidade, exportação e exclusão

**Tipo:** nova função/segurança · **Labels:** `privacy`, `security`, `P1`

**Critérios de aceite:** inventário de dados e finalidade; política de retenção e exclusão definida; fluxo de exportação/exclusão planejado; eventos/logs sem conteúdo de cliente; processo de incidente e responsável identificados; revisão especializada necessária antes de uso comercial.

## Issue 12 — Preparar staging e deploy controlado por PR

**Tipo:** infraestrutura · **Labels:** `deployment`, `ops`, `P2`

**Critérios de aceite:** preview isolado para PR quando suportado; staging sem dados pessoais reais; produção atualiza somente após merge aprovado e checks verdes; health check e smoke test pós-deploy; rollback documentado/testado; deploy e URLs conferidos, sem declarar release antes da evidência.

## Publicação no GitHub

Ao criar cada Issue, escolher o item correspondente e criar uma Issue independente (GitHub atribuirá o número). Para subtarefas, relacionar epic/Issue-pai. Usar esses títulos como rascunho, não copiar números fictícios. Depois, toda PR deve mencionar a Issue real em sua descrição.
