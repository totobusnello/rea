---
name: reverse
description: Estuda um produto de referência, documenta suas especificações e elementos com evidência e entrega um roteiro de recriação e testes por jornada.
---

# Estudo de produto por jornada

Ao receber um produto, URL ou conjunto de materiais, entregue um estudo utilizável por uma equipe que nunca viu o original. Use o idioma e o formato solicitados. Por padrão, grave um relatório Markdown por produto na área de trabalho, com nome que identifique o caso. Se ele já existir, confira produto e versão antes de atualizar. Em retomadas preserve IDs e evidências anteriores, indicando mudanças de versão. Se nenhum alvo ou material foi indicado, peça essa informação.

## Investigar

1. Registre pergunta, produto, versão ou data de observação, plataforma, perfil de acesso, materiais disponíveis e limites. Faça um mapa das áreas e das jornadas com estado de cobertura (estudada, parcial ou apenas identificada). Priorize as jornadas pedidas e as decisões que alteram o comportamento. Para as apenas identificadas, dê um roteiro preliminar com as decisões pendentes.
2. Percorra cada jornada desde a entrada até o resultado. Registre o gesto, o estado antes e depois, dados que mudaram e o efeito que o usuário consegue conferir. Investigue variações relevantes: cancelar, voltar, atualizar, perder conexão, retomar em outro dispositivo, erro ou falta de permissão. Declare quais variações têm evidência.
3. Catalogue elementos por função: tela, controle, conteúdo, feedback e navegação. Documente rótulo, hierarquia, interação, estado e uso por teclado ou toque conforme o material permitir. Reutilize o identificador de um elemento compartilhado por várias jornadas. Aponte para o quadro de vídeo, captura ou seletor que permita reencontrá-lo.
4. Para cada regra importante, registre a fonte e um localizador preciso (instante, evento, arquivo e símbolo, operação e resposta). Qualifique a afirmação como observada, derivada, inferida ou desconhecida. A presença de código indica um comportamento possível. Confirmação de execução requer um evento compatível com o mesmo cenário e versão. Documente divergências sem escolher uma versão por conveniência.
5. Escolha a fonte de menor custo que resolva a próxima dúvida. Consulte resumos antes de abrir detalhes. Se faltar uma fonte, conclua a parte sustentada e registre o efeito da lacuna. Evidência num pacote de versão desconhecida não confirma a versão vista em tela. Para dados e integrações, diferencie entidade visível, operação observada e implementação interna proposta.

## Escolher fontes

| Fonte disponível | Contribuição e limite |
|---|---|
| Telas, vídeos, documentação e navegação comum | Reconstruir jornadas e estados visíveis. Identificar o que veio da documentação e o que ocorreu na interação. |
| REA e, para artefatos nativos, Ghidra | Consultar inventários, recursos e referências estáticas relevantes para a regra estudada. Reusar IDs dos registros Evidence. Uma propriedade de hardening só entra se tiver implicação concreta para o estudo. |
| Registro de execução do Frida fornecido | Vincular uma observação à função, ao build e à execução identificados. Assinalar se o experimento alterou o comportamento observado. |
| HAR ou flows do mitmproxy fornecidos | Relacionar método, rota, status e momento à ação visível quando houver vínculo demonstrável. Omitir credenciais e dados pessoais do relatório. |
| OpenAPI derivado por mitmproxy2swagger | Reconstruir o trecho observado do contrato. Citar o evento de origem e conferir a generalização de IDs, tipos opcionais e exemplos. A captura e sua conversão contam como uma origem. |
| Descrições de operações do api-anything | Extrair vocabulário, entradas e saídas documentadas para formular cenários. Indicar se o efeito foi observado. O estudo pode ser concluído com o catálogo existente. |

Essas fontes são opcionais. O fluxo padrão estuda materiais existentes e comportamento visível. Um roteiro de recriação descreve implementação própria com código, textos e ativos próprios.

## Entregar

Use a [estrutura do estudo](estudo.md). Faça cada afirmação relevante remeter à evidência; faça cada etapa do roteiro remeter à regra que a motiva. Uma escolha de arquitetura da recriação deve aparecer como decisão proposta. Quando uma falha impedir a análise, registre fonte afetada, motivo e a conclusão que permanece em aberto.

A conclusão inicial deve ter o mesmo grau de certeza da ficha. Se o texto reaparece após reabrir offline, o fato observado é a disponibilidade do texto naquela reabertura; o mecanismo de armazenamento e a sobrevivência ao encerramento do processo exigem evidência própria.

Antes de entregar, percorra o caminho inverso: escolha cada teste de aceitação, encontre sua regra e confirme que o localizador leva à evidência correspondente. Testes baseados em suposição devem aparecer como proposta ou pergunta. Identifique lacunas que mudariam o roteiro e a menor observação que poderia resolvê-las.
