# Estrutura do estudo

Abra com a conclusão mais útil para quem vai recriar o produto. Identifique versão, ambiente, perfil, abrangência e data. Use tabelas quando facilitarem a comparação e diagramas quando a sequência de estados for difícil de acompanhar. Ajuste a extensão à complexidade do caso.

## Mapa e catálogo

- Para cada jornada J, indique objetivo, início, fim, telas, dependências e cobertura.
- Para cada elemento E, descreva papel, localização, estados observáveis, ações, feedback e jornadas em que aparece. Inclua referências às fontes. Quando duas telas usam o mesmo controle de forma diferente, descreva a diferença.
- Registre as entidades visíveis, os campos e relações demonstráveis, a persistência observada e as integrações relevantes. Explicite as fronteiras de visibilidade.

## Ficha de cada jornada

1. Identifique usuário, pré-condições, gatilho e objetivo. Descreva a sequência principal, os caminhos alternativos, erros e retomada, conforme a cobertura disponível.
2. Enumere as regras R com condição → ação → efeito. Em cada regra, cite os elementos E, os registros de evidência F, o grau de certeza e eventuais explicações concorrentes.
3. Explique um aprendizado concreto: qual problema a interação resolve, qual o custo para o usuário e em que contexto faria sentido adaptá-la. Identifique interpretações de intenção como hipóteses.
4. Escreva o roteiro desta jornada em ordem de dependência: elementos e modelo de dados mínimos, transições a implementar, integrações ou substitutos locais, decisões em aberto e marcos verificáveis. Relacione cada etapa às regras R. Para uma jornada parcial, identifique as etapas condicionais.
5. Para cada regra que muda o resultado, inclua um teste com estado inicial, ação, resultado esperado e evidência de referência. Marque separadamente testes sugeridos e executados. Se houver um cenário reservado, registre a previsão antes de consultá-lo e anote o resultado.

## Índice de evidências e continuidade

Cada F aponta para fonte, versão ou data, localizador e fato específico. Em fonte derivada, identifique o registro pai. Guarde referências reproduzíveis sem copiar conteúdo pessoal. Encerre com prioridades de recriação, dependências entre jornadas e a próxima verificação que melhor resolveria uma incerteza relevante.
