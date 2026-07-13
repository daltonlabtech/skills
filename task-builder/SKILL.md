---
name: task-builder
description: Estrutura padronizada para escrever tarefas técnicas claras e executáveis para equipes de desenvolvimento. Use quando o usuário pedir para criar, redigir ou estruturar uma tarefa para desenvolvedor (em ClickUp, Linear, Notion, Jira ou em texto livre).
---

# SKILL: Criação de Tarefas Técnicas

## Descrição

Habilidade para criar tarefas técnicas bem estruturadas para a equipe de desenvolvimento. A descrição da tarefa traz o **problema, as decisões já fechadas e o resultado esperado** — não prescreve como o dev deve resolver. O "como" é decisão do desenvolvedor.

## Estrutura de uma Tarefa

### 1. CONTEXTO (obrigatório)
- **Objetivo:** Explicar de onde surgiu a demanda e qual problema/melhoria queremos resolver
- **Características:**
  - Pode ser longo, mas precisa ser cristalino
  - O desenvolvedor deve ler e entender perfeitamente a situação
  - Deve contextualizar o estado atual e o que motivou a necessidade da tarefa
  - Incluir informações relevantes sobre o impacto ou uso atual do sistema
- **Citações literais de usuários/clientes são permitidas** quando comunicam tom, urgência ou peso emocional que a paráfrase perderia. Não decorativo — use só quando a fala traz informação que a redação neutra não captura.

### 2. REQUISITOS DECIDIDOS (opcional)
- **Quando usar:** Quando houver decisões fechadas em reunião, alinhamento com cliente, ou definição de produto que o dev **não deve reabrir** durante a execução.
- **O que entra:**
  - Copy específico já aprovado (ex: texto exato de um popup, mensagem de erro)
  - Regras de negócio definidas (ex: "máximo 5 valores ranqueados, sem empate")
  - Escopo recortado (ex: "aplicar para todos os 6 formulários da metodologia")
  - Restrições explícitas (ex: "NÃO clicar no botão Atualizar antes de investigar")
- **O que NÃO entra:** sugestões, opiniões do autor da tarefa, alternativas técnicas em aberto.

### 3. BLOQUEIO (opcional)
- **Quando usar:** Quando há dependência externa pendente que afeta ou impede execução (ex: definição de copy ainda não chegou do cliente; acesso a sistema que precisa ser liberado).
- **Conteúdo:** O que está pendente, de quem depende, e o que muda quando a dependência for resolvida.

### 4. RESULTADO ESPERADO (obrigatório)
- **Objetivo:** Definir comportamentos específicos em situações específicas
- **Formato:** "Em qual situação → Como o sistema deve se comportar"
- **Características:**
  - Facilita testes pelo desenvolvedor
  - Define cenários claros para validação
  - Especifica o comportamento esperado em cada caso
  - Exemplos:
    - "Ao iniciar a conversa, o agente deve [comportamento X]"
    - "Quando o cliente perguntar sobre Y, o agente deve [comportamento Z]"
    - "Se o usuário demonstrar W, o sistema deve [comportamento K]"

### 5. REFERÊNCIAS (obrigatório quando houver)
- **Objetivo:** Fornecer links e recursos relevantes
- **Características:**
  - Apenas links que agregam à execução da tarefa
  - Links de documentação, gravações de reunião, anotações, APIs, tarefas relacionadas
  - Sem feedbacks extensos ou comentários de usuários (citações ficam no CONTEXTO, com critério)

## O que NÃO incluir

- **Solução técnica prescrita** — o "como" é decisão do desenvolvedor. A tarefa traz o problema e o resultado esperado; o dev escolhe a implementação.
- **Benefícios Esperados** — Irrelevante para execução técnica
- **Observações Importantes** — Não agrega à execução
- **Prazo Sugerido** — Não cabe na descrição da tarefa
- **Responsável Sugerido** — Definido na atribuição da tarefa
- **Mensagens/scripts exemplo** — Quando o copy for decidido, ele entra como REQUISITO DECIDIDO, não como exemplo
- **Requisitos Técnicos genéricos** — Substituídos por RESULTADO ESPERADO

## Convenções de Nomenclatura

### Formato do Nome da Tarefa
**[NomeCliente] Descrição curta**

Para bugs, prefixar com `Bug:`. Para UX/melhoria visual, `UX:`. Para infra/operação, sem prefixo ou `Op:`.

Exemplos:
- `[AB Carreiras] Bug: Top 5 Valores permite conclusão com mais de 5 valores ranqueados em caso de empate`
- `[InsideMoney] Melhorias no Fluxo de Atendimento`
- `[ClienteX] UX: Adicionar loading em formulários durante submissão`

**Características:**
- Nome enxuto e objetivo (mas pode ser longo se a especificidade ajudar a localizar)
- Identificação clara do cliente entre colchetes
- Para bugs, o título idealmente captura **sintoma** ou **comportamento errado**, não apenas a área

## Template de Tarefa

```markdown
# [Cliente] Título Curto

## CONTEXTO

[Explicação detalhada de onde surgiu a demanda, qual o estado atual do sistema,
e qual problema/melhoria queremos resolver. Pode ser longo, mas deve ser cristalino.
Citações literais permitidas quando comunicam tom/urgência crítica.]

## REQUISITOS DECIDIDOS   <!-- opcional -->

- Decisão 1 (copy específico, regra, restrição)
- Decisão 2
- Decisão 3

## BLOQUEIO   <!-- opcional -->

[O que está pendente, de quem depende, e o que muda quando resolver.]

## RESULTADO ESPERADO

**Ao [situação/cenário]:**
- O sistema deve [comportamento esperado]
- Deve [outro comportamento]

**Quando [outra situação]:**
- O sistema deve [comportamento esperado]

**Se [condição específica]:**
- O sistema deve [comportamento esperado]

## REFERÊNCIAS

- Link relevante 1: [URL]
- Link relevante 2: [URL]
```

## Exemplo Completo

```markdown
# [AB Carreiras] Bug: Top 5 Valores permite conclusão com mais de 5 valores ranqueados em caso de empate

## CONTEXTO

A metodologia da AB define que o mentorado **deve ranquear exatamente 5 valores** no Top 5. O sistema atualmente permite que o cliente conclua o formulário mesmo quando há empate entre o 5º e o 6º (ou demais) valor — gerando 6+ valores ranqueados como "Top 5".

A Jamile foi enfática na reunião (11/05) sobre dois pontos:

1. **O cliente PRECISA desempatar antes de concluir.** Não é um aviso passivo — é um bloqueio.
2. **O cenário de empate é a regra, não a exceção.** Citações dela: *"o que vai acontecer geralmente é o cinco e o seis terem a mesma nota"* e *"tem cliente que vai ter 5, 6, 7, 8, 9, 10 com a mesma nota — tem cliente que põe 10 em tudo. É uma loucura"*.

## REQUISITOS DECIDIDOS

- Bloqueio total da conclusão enquanto houver mais de 5 valores ranqueados no Top 5 (por empate)
- Copy do popup ao tentar concluir em estado de empate:
  > **Você está com mais de 5 valores no seu Top 5 por causa de empate. Para concluir, desempate os valores na posição 5 (e demais empatados).**
- Mesma regra se aplica em edição pós-conclusão (mentorado pode editar a qualquer momento — se a edição produzir empate, o mesmo bloqueio se aplica)

## RESULTADO ESPERADO

**Ao tentar concluir o Top 5 Valores com mais de 5 valores ranqueados:**
- O sistema deve bloquear a conclusão
- Deve exibir o popup com o copy decidido acima
- Deve destacar visualmente os valores empatados para que o usuário identifique o que ajustar

**Quando o usuário desempata e fica com exatamente 5 valores únicos no Top 5:**
- O sistema deve permitir a conclusão sem fricção

**Se o mentorado editar o Top 5 após concluir e a edição produzir empate:**
- O sistema deve aplicar o mesmo bloqueio, exibindo o mesmo popup

## REFERÊNCIAS

- Reunião 11/05 — anotações: https://docs.google.com/document/d/1BwbzUHWLek5MjpJeTNqjf9nt3MRTWOI0KyorXIpGPAI
- Reunião 11/05 — gravação: https://drive.google.com/file/d/1NVxVkzdcH9MJUz1miGTt0Cf5WJVd-Sjb/view
```

## Processo de Criação

1. **Receber demanda** — Entender o contexto do cliente/usuário
2. **Identificar decisões fechadas** — O que já foi acordado e o dev não deve reabrir?
3. **Identificar bloqueios** — Há dependência externa pendente?
4. **Escrever CONTEXTO** — Estado atual, motivação, impacto. Citações literais quando agregam.
5. **Listar REQUISITOS DECIDIDOS** (se houver) — Copy, regras, restrições.
6. **Documentar BLOQUEIO** (se houver) — Pendência + dependência + o que muda quando resolver.
7. **Especificar RESULTADO ESPERADO** — Cenários condicionais (Ao / Quando / Se).
8. **Adicionar REFERÊNCIAS** — Links que agregam à execução.

## Princípios

- **Clareza > Brevidade** — O contexto pode ser longo se isso trouxer clareza.
- **Problema > Solução** — Descrever o que está errado e o que precisa ser verdade no final; o "como" é decisão do dev.
- **Decisões > Sugestões** — Registrar o que foi acordado em reunião/com o cliente, não o que o autor da tarefa acha.
- **Testabilidade** — Resultado esperado deve facilitar testes (formato condicional ajuda).
- **Foco** — Apenas informações relevantes para execução técnica.
- **Padronização** — Seguir sempre a mesma estrutura, omitindo as seções opcionais que não se aplicam.
