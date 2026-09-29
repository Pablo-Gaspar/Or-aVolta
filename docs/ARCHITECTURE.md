# Arquitetura proposta (provisória)

**Status:** proposta a registrar em ADR após entrevistas e teste de limites/custos. Não existe código de aplicação neste pacote.

## Princípios

Começar com poucos componentes, renderizar o essencial rápido, minimizar JavaScript no navegador, separar organização/tenant em todas as operações e evitar dependências pagas antes de validar. Preferir arquitetura simples e observável a microserviços.

## Stack candidata

| Camada | Proposta | Motivo/condição |
|---|---|---|
| App web | Next.js App Router + TypeScript | Renderização server-first; Client Components somente para interação que precisa deles; dividir/lazy-load rotas pesadas. Confirmar compatibilidade operacional. |
| UI | Componentes acessíveis e CSS/Tailwind sob decisão de ADR | Evitar biblioteca excessiva; motion tokens e estados em `docs/UX_MOTION.md`. |
| Dados | PostgreSQL | Transações, integridade relacional e modelagem multi-tenant explícita. |
| Auth/DB gerenciada | Candidato: Supabase, sujeito a revisar preço, limites, backup, região e termos atuais | Conveniência pode reduzir trabalho, mas não presumir plano gratuito para uso comercial/produção. Alternativa deve ser fácil de migrar. |
| Testes | Vitest, teste de integração com DB de teste, Playwright | Pirâmide focada nas regras e nos fluxos que geram valor. |
| Qualidade | Biome, TypeScript, Knip, ArchContract, Commitlint, StrykerJS | Habilitar em fases; custos de CI avaliados. |
| Observabilidade | OpenTelemetry como instrumentação portável + Sentry para erros | APM backend futuro: comparar Datadog e New Relic e selecionar conforme custo/necessidade. |

## Desenho lógico

```text
Navegador (mobile-first)
        │ HTTPS / sessão autenticada
        ▼
Aplicação web (rotas server-first, validação no servidor)
        │ consultas autorizadas por organização
        ▼
PostgreSQL (org_id + políticas de acesso/tenant)

Aplicação ── traces/metrics/logs sanitizados ──► OpenTelemetry
Aplicação ── erros/contexto técnico ──────────► Sentry
OpenTelemetry ──► um backend APM escolhido (Datadog OU New Relic), se aprovado
```

## Entidades iniciais

- `organizations`: tenant e preferências mínimas.
- `memberships`: usuário, organização e papel mínimo.
- `customers`: organização, nome, contato opcional, timestamps.
- `opportunities` ou `quotes`: organização, cliente, título, valor opcional, status, enviado_em, next_follow_up_at, result, timestamps.

Toda entidade de negócio tem `organization_id`, chaves/indexes adequadas e política de acesso no backend/banco. Validar se `quotes` e `opportunities` devem ser uma entidade ou duas antes de migração definitiva. Não guardar conteúdo completo de conversa no MVP.

## Segurança e LGPD (baseline a validar com especialista)

- Autorização por tenant em cada caminho; teste de tentativa de IDOR/acesso cruzado.
- Princípio de menor privilégio, proteção de sessão, secrets fora do cliente e do git.
- Coletar apenas dados necessários; definir retenção, exportação, exclusão e canal de solicitação.
- Sanitizar telemetria; nunca enviar mensagem, telefone ou e-mail em nome de evento/tags.
- Backup/restore testado antes de manter dados comerciais reais. Confirmar região, retenção, suboperadores e contratos do fornecedor.
- Não afirmar conformidade legal; obter revisão adequada antes de operação comercial.

## Desempenho e escala

- Carregar por demanda rotas/componentes não críticos; não fazer lazy-load de elementos primários que atrasariam o primeiro uso.
- Paginar consultas; indexar `organization_id`, `status`, `next_follow_up_at` e chaves de junção conforme plano de consulta observado.
- Validar no servidor, evitar N+1, limitar payload e usar cache apenas quando autorização/invalidação estiverem claras.
- Definir metas de Core Web Vitals e p95 após medição com protótipo; não fabricar SLO sem linha de base.

## Deploy / ambientes

Local → preview por PR → staging → produção após merge aprovado em `main`, com CI e secrets separados por ambiente. Não usar banco de produção em E2E. Documentar migração para frente e rollback (preferir alterações compatíveis e rollout em etapas). Preços/limites de qualquer fornecedor devem ser reconfirmados no momento de escolher.

## ADRs a criar antes da implementação

`ADR-001` stack/hosting; `ADR-002` auth e isolamento multi-tenant; `ADR-003` solução de observabilidade e custo; `ADR-004` estratégia de deploy e backups; `ADR-005` modelo de dados orçamento/oportunidade. Cada decisão deve incluir contexto, opções, custos/riscos, escolha e gatilho de revisão.
