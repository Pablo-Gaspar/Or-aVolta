# Contribuição e fluxo de entrega

## Pré-requisitos

- Acesso ao repositório GitHub e permissões compatíveis com a tarefa.
- Issue aprovada com objetivo, escopo e critérios de aceite.
- Depois da definição da stack: versões fixadas de Node/runtime, package manager e comandos documentados.

## Fluxo

1. **Issue**: crie/consulte uma Issue para toda mudança. Use um item do backlog em `docs/ROADMAP_ISSUES.md` como rascunho; GitHub atribui o número real ao publicar.
2. **Planejar**: decomponha em tarefas pequenas. Para feature, defina comportamento, estados, riscos e testes. Para correção, registre passos de reprodução e resultado esperado.
3. **Branch**: crie `feat/<n>-<slug>`, `fix/<n>-<slug>`, `docs/<n>-<slug>` ou `chore/<n>-<slug>` a partir da `main` atualizada.
4. **Implementar**: mantenha o PR focado; inclua migrações e testes necessários. Nunca inclua segredos/dados reais.
5. **Validar**: execute os checks locais descritos no projeto e registre resultados no PR. UI: inclua evidência visual e valide teclado, mobile e reduced motion.
6. **Pull Request**: use o template; inclua `Closes #<n>` se o PR concluir a Issue, ou `Refs #<n>` se não concluir. Explique risco, rollout e rollback.
7. **Revisar/mesclar**: aguarde CI verde e revisão necessária. Não faça push direto para `main`, não desative checks para contornar falhas.
8. **Deploy**: após merge, pipeline autorizado promove o build. Verifique health check e logs; registre release/rollback. Não faça deploy manual de produção.

## Template para título de commit

Conventional Commits: `feat:`, `fix:`, `docs:`, `test:`, `refactor:`, `chore:`. Quando Commitlint estiver configurado, o hook/CI valida formato. Exemplo: `feat: registrar retorno de orçamento (#42)`.

## Definition of Done

- Issue relacionada e critérios de aceite atendidos.
- Revisão e PR com vínculo explícito à Issue.
- Lint, typecheck, testes pertinentes e CI verdes.
- Sem secrets, logs de PII ou regressões de acesso entre organizações.
- UI com loading/erro/vazio/sucesso e motion acessível quando aplicável.
- Migração/rollback e observabilidade considerados.
- Deploy descrito com evidência ou explicitamente marcado como ainda não realizado.
