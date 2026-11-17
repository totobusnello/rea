# Plano de evolução do REA para análise de aplicações e sistemas

Base examinada em 17/11/2026, commit `3f361d820fd4a54e037bf60726e79217586ad431`. O fork agora inclui a [skill reverse](../../.agents/skills/reverse/SKILL.md). As metas de eficiência e cobertura abaixo ainda precisam de medição.

## O que aproveitar do projeto

O REA já [importa traces Playwright v10](../playwright-traces.md), retém a evidência completa e permite consultar eventos específicos. O [avaliador de cobertura](../reconstruction-coverage.md) já registra dependências, contradições e lacunas. A [composição de capacidades](../capability-composition.md) separa contratos, provedores e interfaces CLI/MCP. Começaria pela skill: transformar uma pergunta sobre comportamento numa sequência curta de consultas e numa explicação verificável. Só acrescentaria um contrato ao servidor depois de demonstrar uma lacuna repetível.

## Produto entregue pela skill

O resultado é um estudo das especificações e dos elementos do produto e um roteiro para recriar cada jornada. O relatório liga elemento, regra, evidência, decisão de implementação e teste de aceitação. Uma equipe pode verificar a origem da regra e identificar onde tem liberdade para projetar sua própria solução. A [estrutura do relatório](../../.agents/skills/reverse/estudo.md) define as fichas, o índice de evidências e a cobertura das jornadas parciais.

A skill inclui uma fase técnica com REA entre o mapeamento da jornada e a consolidação das regras. Ela seleciona consultas por pergunta e artefato e registra como a evidência afeta o roteiro. Estudos visuais também podem ser concluídos. Para usar a versão do fork, copie a pasta inteira `.agents/skills/reverse` deste branch para a pasta de skills pessoais do cliente, preservando o nome `reverse`. No Claude Code use `~/.claude/skills/reverse` e invoque `/reverse`; no Codex use `~/.agents/skills/reverse` e invoque `$reverse`. Os materiais de tela e as fontes técnicas podem ser combinados conforme a pergunta. Os critérios deste plano medem a fidelidade do estudo e a utilidade do roteiro. Construir o produto é uma decisão posterior.

## Caso piloto

Pergunta: em que momento o app de notas considera uma edição salva? Preparar duas versões de um pequeno aplicativo próprio, com salvamento local e sincronização posterior, um trace gravado, o pacote distribuído e um contrato de API. Escrever o gabarito antes das análises. Incluir uma gravação com falha de sincronização e outra em que o armazenamento interno do servidor é deliberadamente invisível.

A saída deve mostrar o gesto, o evento de interface, a operação local, a chamada de sincronização e a mudança de estado visível. Para cada ligação, citar versão e origem reproduzível, como arquivo e símbolo, ID de evento ou operação declarada no contrato. Se a única observação for uma resposta HTTP de sucesso, registrar a persistência no servidor como desconhecida. Proximidade temporal, sozinha, sustenta uma hipótese.

## Ordem de implementação

| Entrega | Mudança proposta | Como decidir se está pronta |
|---|---|---|
| 1. Referência de qualidade e custo | Rodar o REA atual no piloto. Registrar acertos, lacunas, conclusões indevidas, chamadas por pergunta e tempo até a primeira resposta verificável. Adaptar a avaliação em tests/evaluation e o método de medição do catálogo. | Uma segunda pessoa consegue reproduzir a pontuação com o mesmo gabarito, versão e artefatos. |
| 2. Investigação por jornada | Evoluir a skill de diagnóstico. Reconhecer os insumos disponíveis, começar pela fonte de menor custo e consultar a próxima somente se resolver uma pergunta em aberto. Produzir cronologia, fluxo de dados e estados de sucesso e falha. | A execução distingue salvamento local de sincronização e cita evidência para cada ligação apresentada como observada. |
| 3. Cruzamento de evidências | Testar primeiro com as consultas existentes. Associar rota, módulo, evento e contrato por identificadores disponíveis. Preservar origens, versões, ligações ambíguas e contradições. Se a mesma junção exigir lógica duplicada nas interfaces, implementá-la no domínio e expô-la por CLI e MCP. | Ao retirar o trace ou trocar a versão do pacote, a conclusão afetada passa a inferida ou desconhecida. Dois eventos próximos e incompatíveis continuam separados. |
| 4. Menos repetição | Reutilizar o registro de evidência retido; pedir resumo antes de abrir páginas de detalhes. Medir leituras repetidas. Se justificável, indexar resultados derivados por hash do insumo, versão do analisador e opções relevantes. | Em cinco execuções pareadas por cenário, buscar 25% menos chamadas na mediana, mantendo a cobertura e zero novas conclusões indevidas no conjunto de teste. Incluir ensaio com dados alterados para verificar invalidação. |
| 5. Cobertura por plataforma | Levar o piloto para navegador, desktop Electron, app móvel empacotado e sistema com dois serviços. Usar o mesmo formato de relato e fontes específicas por plataforma. | Cada caso tem ao menos uma jornada, uma falha e uma lacuna intencional. A avaliação publica os resultados por plataforma. |
| 6. Distribuição em Codex e Claude Code | Testar a skill sozinha com arquivos fornecidos e com REA conectado pelo mecanismo oficial. Documentar ferramentas necessárias para cada caso e verificar as disponíveis na sessão. | Em perfis de teste limpos, ambos os clientes produzem um relatório básico. Se um provedor estiver indisponível, a saída identifica quais perguntas ainda podem ser respondidas. Preservar as aprovações do cliente. |

## Que informação cada plataforma deve acrescentar

| Alvo | Elementos a recuperar | Onde procurar |
|---|---|---|
| Site | Jornada entre rotas, mudança de estado, carregamento e recuperação de erro | Rotas do pacote, eventos e respostas de uma gravação fornecida |
| Desktop | Caminho da ação entre janela, processo principal e arquivo local | Pacote Electron, manipuladores de IPC e observações fornecidas |
| Móvel | Tela inicial da jornada, recurso utilizado, permissão declarada e evidência de uso | Manifesto, recursos do pacote e gravação da interação |
| Sistema | Contrato entre componentes, fronteira assíncrona, resultado e tratamento de falha | Contratos versionados, IDs de correlação e logs de teste fornecidos |
| Versões | Qual etapa mudou, qual evidência distingue as versões e qual impacto é observável | Mesma jornada repetida nas duas versões com os mesmos dados iniciais |

## Medição e decisão de lançamento

Fixar a versão do cliente, modelo, ferramentas, entradas e orçamento. Rodar as versões atual e candidata com os mesmos casos, alternando a ordem e separando execuções frias e com reuso. Calcular cobertura dividindo ligações corretas demonstradas pelas ligações demonstráveis do gabarito. Contar à parte afirmações falsas, desconhecidos corretamente preservados, chamadas, tempo e tokens realmente reportados pelo cliente. Quando uma métrica estiver indisponível, registrá-la como tal. O [guia de avaliação do catálogo](../mcp-catalog-evaluation.md) explica as condições do ensaio no Codex.

Próxima etapa de avaliação: comparar os relatórios do piloto com o gabarito, incluindo um cenário reservado de reabertura offline. Medir também quantas regras sustentadas possuem roteiro e teste rastreáveis e quantas lacunas foram corretamente preservadas. O resultado orienta o próximo investimento em correlação de fontes, cobertura por plataforma ou redução de custo.
