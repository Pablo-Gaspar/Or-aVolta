# Product brief — OrçaVolta

**Status:** hipótese de negócio para validação. **Não** representa demanda comprovada.

## Tese

Pequenas empresas locais de manutenção/instalação de ar-condicionado deixam orçamentos sem follow-up porque o processo vive em conversas, anotações e memória. Um mini-CRM que mostra o próximo retorno e registra o resultado pode reduzir esquecimento e tornar o pipeline visível sem obrigar a equipe a implantar um ERP.

## Público inicial (ICP hipótese)

- Técnico autônomo ou equipe local de 1–5 pessoas.
- Faz orçamento após contato/visita e acompanha diversos pedidos ao mesmo tempo.
- Usa celular como principal ferramenta; pode usar WhatsApp, mas não quer migrar todo o atendimento.
- Não pressupor maturidade digital, volume mínimo nem disposição a pagar: descobrir nas entrevistas.

## Jobs-to-be-done

1. Quando envio um orçamento, quero registrar o valor, o status e quando devo retornar, para não depender da memória.
2. Ao começar o dia, quero ver quem está aguardando resposta e quais retornos estão atrasados.
3. Quando o cliente decide, quero marcar ganho/perda e entender o resultado dos orçamentos enviados.

## Resultado de produto a testar

O usuário consegue registrar orçamento em menos de 60 segundos e concluir sua lista diária de follow-up sem procurar em conversas. Verificar por teste de usabilidade; não tratar o tempo como promessa antes de medir.

## MVP: incluir

- Conta e organização, com isolamento de dados obrigatório.
- Cadastro mínimo de clientes (nome e um meio de contato opcional).
- Oportunidade/orçamento: título, valor, data, status, próxima ação/retorno, notas operacionais mínimas.
- Pipeline simples: novo → orçamento enviado → ganho/perdido; sem etapas configuráveis no primeiro corte.
- Lista “hoje / atrasados / próximos”, ordenada por prioridade/data.
- Marcar como ganho/perdido, reagendar retorno e filtrar por status.
- Exportação simples dos próprios registros se for pequena e segura (avaliar antes de incluir).
- Onboarding curto, estados vazios úteis e ajuda de demonstração sem dados pessoais.

## Não incluir no primeiro MVP

Envio automático via WhatsApp/SMS/e-mail; integração de API de terceiros; emissão fiscal; contabilidade; pagamentos; estoque; folha; agenda complexa; assinatura digital; automações com regras; IA generativa; permissões avançadas; aplicativo nativo. Considerar somente após evidência de necessidade, custo e conformidade.

## Métricas de aprendizagem

- **Ativação:** organização registra um cliente, cria um orçamento e agenda retorno.
- **Aha:** usuário volta e marca um retorno concluído/resultado sem assistência.
- **Uso:** proporção de orçamentos ativos com próxima data de ação.
- **Valor percebido:** usuário relata follow-up feito mais rápido ou oportunidade recuperada, com evidência qualitativa.
- **Negócio:** pilotos que aceitam pagar após período combinado. Não usar cadastro/visita à landing page isoladamente como prova de product-market fit.

## Hipóteses que precisam de evidência

- Follow-up é uma dor relevante e frequente neste nicho.
- Prestadores registrarão os orçamentos em uma ferramenta separada.
- Lembretes de retorno geram valor suficiente para pagamento recorrente.
- O usuário aceita operação manual (copiar mensagem/abrir app de mensagens), sem automação inicial.
- O preço, canal de aquisição e suporte são sustentáveis.

## Preço e posicionamento

Testar disposição a pagar com entrevistas e pilotos; não fixar preço como decisão final. Uma faixa de teste pode ser proposta depois de entender valor e alternativas. Evitar assinatura grátis permanente antes de estimar suporte, churn e custo de servir.

## Decisões abertas

Marca/domínio; stack e hospedagem; canal de venda; preço; requisitos de retenção/exportação; se clientes desejam orçamento em PDF; política de acesso por colaborador. Resolver com evidência, Issues e ADRs, não por preferência técnica isolada.
