# Qualidade, testes e observabilidade

## Ferramentas e decisão para o MVP

| Necessidade | Padrão proposto | Fase |
|---|---|---|
| Formatação/lint | Biome (format + lint), mais `tsc --noEmit` | CI de cada PR |
| Fronteiras/contratos | ArchContract e testes de módulos/dependências | CI de cada PR, depois do ADR da arquitetura |
| Código/dependências não usados | Knip | CI de cada PR, com exceções documentadas |
| Mensagens de commit | Commitlint (assumindo que “Comilint” significa Commitlint) | hook local + CI |
| Mutation testing | StrykerJS (assumindo que “Stryke” significa Stryker) | módulo de domínio; job separado/agendado no início; mover para PR gate se tempo aceitável |
| Unitário | Vitest ou runner compatível com stack final | cada PR |
| Integração | testes de serviços/repos com banco de teste isolado | cada PR |
| E2E | Playwright: jornada central e regressão crítica | smoke em PR e suíte completa em main/nightly |
| Cobertura | Codecov, se token/conta autorizado | status check e tendência; não usar percentual global como substituto de qualidade |
| Erros | Sentry, com scrub de PII e amostragem conservadora | staging e piloto, após aprovação de fornecedor |
| Instrumentação | OpenTelemetry SDK/exporter | baseline de traces/metrics/logs técnicos |
| APM backend | Datadog **ou** New Relic, escolhendo depois por necessidade/custo | evolução; não enviar tudo a ambos por padrão |

“Comilint” e “Stryke” foram tratados como prováveis typos de Commitlint e StrykerJS. Confirmar a intenção antes de adicionar dependências. ArchContract é diferente de lint: deve validar contratos/fronteiras estabelecidos no ADR.

## Regras de cobertura e checks

- Cobrir regras de negócio, autorização, tenant isolation e datas de follow-up. Proposta inicial: alvo de 80% para módulo de domínio crítico após a baseline existir; cobertura global não é gate inicial sem medir o estado real.
- Os critérios de merge devem ser explícitos, estáveis e executáveis; CI verde antes de merge.
- Codecov token, Sentry DSN e credenciais de APM são secrets de environment, nunca committed. Serviços externos só são ativados com custos/termos revistos.
- Playwright deve usar dados seed sintéticos, ambiente de teste e permissões mínimas. Nenhum teste automatizado escreve em produção.
- Teste de arquitetura não pode proibir mudança válida por contrato implícito; contratos são versionados/documentados e atualizados via Issue/PR.
- Stryker é caro em CPU/tempo quando executado amplamente. Começar por funções centrais e reportar duração; executar separadamente/nightly até justificar gate em todo PR.

## Casos E2E mínimos

1. Usuário cria/abre a organização, registra cliente e orçamento.
2. Orçamento com retorno para hoje aparece no painel.
3. Usuário conclui ou reagenda o retorno e confirma a mudança.
4. Tentativa de usuário de outra organização não revela nem altera dados (complementar com testes backend/RLS).
5. Estados loading, erro e vazio são legíveis em viewport mobile; navegação essencial por teclado funciona.

## Observabilidade operacional

- Correlation/trace IDs conectam requisição e erro; instrumentar início de request, operações de banco e falhas, sem conteúdo de usuário.
- Métricas iniciais: taxa de erro, latência p50/p95 dos endpoints críticos, falha de jobs (se houver), disponibilidade/health check. Baseline antes de limites/alertas.
- Sentry agrupa exceções e preserva stack útil; sanitizar headers/body/breadcrumbs; desligar captura de dados pessoais.
- Health check não revela secrets nem estado interno detalhado.
- Criar painel mínimo e alerta acionável em staging; testar alerta e procedimento de triagem. Não instalar simultaneamente múltiplos APMs sem motivo e orçamento.
- Logs estruturados com nível, serviço, ambiente, request/trace ID e resultado; retenção mínima necessária.

## Entrega contínua

Checks em PR → preview descartável → aprovação/merge → pipeline main → smoke test/health check → observação inicial → rollback documentado. Release não deve suceder check falho nem depender de credenciais locais. Usuário/operador deve saber qual pipeline e ambiente publicar após stack definida.
