# OrçaVolta — CRM de orçamentos e follow-up

> **Hipótese de produto, ainda não validada:** um CRM simples para pequenos prestadores de serviço de climatização/manutenção (1–5 pessoas) não perderem oportunidades depois de enviar um orçamento.

O produto reúne contatos, orçamentos e próximos retornos em uma tela leve. O MVP **não** envia mensagens automaticamente, não emite nota fiscal e não tenta substituir um ERP. O objetivo inicial é testar se o acompanhamento de orçamentos é uma dor frequente e pagável.

## Problema que queremos testar

Prestadores recebem pedidos por vários canais, fazem visitas e enviam orçamentos; depois, o acompanhamento fica em conversas, anotações ou memória. Oportunidades ficam sem resposta e não há uma visão simples de “quem preciso chamar hoje?”. Esta descrição é uma hipótese, não uma pesquisa de mercado concluída.

## Usuário inicial

Técnicos autônomos e pequenas equipes locais de instalação/manutenção de ar-condicionado. Não expandir para todos os segmentos antes de validar um primeiro nicho.

## MVP proposto

- Cadastro de clientes e oportunidades.
- Registro manual de orçamento, valor, data de envio, status e próxima data de retorno.
- Quadro/lista de pipeline e painel “retornos de hoje / atrasados”.
- Ações para marcar ganho, perda ou próximo retorno; motivo de perda opcional.
- Experiência responsiva, acessível, com estados de carregamento, vazio, erro e sucesso.
- Convite/organização e isolamento de dados por empresa antes de qualquer piloto com dados reais.

**Fora do MVP:** disparo automático de WhatsApp/e-mail, pagamentos, emissão fiscal, estoque, folha, contratos com assinatura, IA, integrações pagas e relatórios complexos.

## Como medir validação

Antes de investir em integrações ou infraestrutura paga: entrevistar 15–20 prestadores do nicho, demonstrar um protótipo clicável, testar um fluxo de orçamento e follow-up e buscar 3–5 pilotos com compromisso explícito de uso/pagamento. Os números são critérios de aprendizado propostos, não garantia de sucesso.

## Regras de trabalho

1. Toda correção, melhoria, nova função, tarefa técnica ou documentação que altere o projeto começa em uma **GitHub Issue** com escopo e critérios de aceite.
2. Trabalhar em branch por Issue; não fazer push direto em `main`.
3. Toda mudança entra por **Pull Request**. A descrição deve citar `Closes #<número>` (ou `Fixes #<número>` / `Refs #<número>` conforme apropriado) e os testes executados.
4. Deploy de produção só após merge aprovado em `main` e verificações verdes; nunca publicar diretamente da estação de trabalho.
5. Instruções completas para agentes estão em [`AGENTS.md`](AGENTS.md); processo em [`CONTRIBUTING.md`](CONTRIBUTING.md).

## Documentação

- [Resumo do produto e escopo](docs/PRODUCT_BRIEF.md)
- [Plano de validação](docs/VALIDATION_PLAN.md)
- [Backlog inicial de Issues](docs/ROADMAP_ISSUES.md)
- [Arquitetura proposta](docs/ARCHITECTURE.md)
- [Qualidade e observabilidade](docs/QUALITY_OBSERVABILITY.md)
- [Motion, loading e acessibilidade](docs/UX_MOTION.md)
- [Prompts detalhados para Claude](prompts/CLAUDE_PROMPTS.md)

## Estado atual

Este repositório ainda não contém a aplicação. O projeto GitHub [Pablo-Gaspar/Or-aVolta](https://github.com/Pablo-Gaspar/Or-aVolta) está associado ao projeto Manus; as Issues iniciais **#1–#13** já foram criadas e a publicação desta documentação está rastreada pela **#14**. Nome, nicho, stack, preço e hospedagem continuam decisões provisórias a confirmar pela validação. A documentação está sendo entregue por PR, sem merge ou deploy automático.

## Princípio de investimento

Validar com entrevistas, protótipo e operação manual antes de pagar por anúncios, APIs de mensagens, observabilidade comercial ou automação. Verifique limites, termos e preços atuais de cada fornecedor antes de contratar; não presumimos que planos gratuitos sejam permanentes ou adequados a produção.
