---
name: task-builder-v2
description: Versão 2 da task-builder da Dalton Lab. Escreve tarefas técnicas claras para o time de dev E preenche a ficha da task no ClickUp (cliente/tag, tipo, prioridade, estimativa, lista, responsável), quebra tasks grandes, registra bloqueio com dono e data, diz como validar e, depois de criar, avisa no canal #sla-tech do Slack marcando o dev. Use quando a usuária pedir para criar, redigir, revisar ou estruturar uma task para desenvolvedor, transformar um chamado/reunião/pedido de cliente em task, ou disser "task-builder v2", "cria a task", "escreve a task", "abre task no ClickUp".
---

# Task Builder v2

> Evolução da `task-builder` (que continua valendo e não foi alterada).
> O corpo da task segue o mesmo padrão. A v2 acrescenta: **ficha da task**, **regra de tamanho**, **bloqueio rastreável**, **como validar**, **notas técnicas internas** e **checklist antes de criar**.
> Motivo: no ClickUp do TechTeam (nov/2026) as descrições são boas, mas faltam dono, tamanho, motivo de bloqueio e critério de fechamento — e as sprints acumulam tasks antigas.

## Modo rápido (padrão — feito para quem tem TDAH)

A PM não precisa preencher nada. Ela só cola o pedido.

1. **A PM cola o pedido** do jeito que vier: texto solto, áudio transcrito, link de chamado, trecho de reunião.
2. **Claude faz no máximo 3 perguntas, numa mensagem só**, e só o que não deu para deduzir:
   - Qual cliente?
   - Qual dev?
   - É urgente?
   (Se já der para saber pelo pedido, não pergunta.)
3. **Claude devolve a ficha em 5 linhas**, nada mais:
   ```
   📌 [Cliente] Tipo: título
   👤 Dev · 🏷️ tag · ⚡ prioridade
   ⏱️ M · 2 h — motivo em uma linha
   📂 Lista: Backlog / Sprint N
   ✅ Pronto quando: [critério em uma linha]
   ```
   A descrição completa fica guardada; só mostrar se a PM pedir ("mostra a descrição").
4. **A PM responde "pode criar"** (ou corrige: "é P", "é do Thiago"). Só então Claude:
   - cria a task no ClickUp;
   - **avisa no Slack, canal `#sla-tech`, marcando o dev responsável** (ver "Aviso no Slack");
   - devolve à PM os 2 links (task + mensagem), em uma linha.
   O "pode criar" já vale para os dois passos; não perguntar de novo.

Regras do modo rápido:
- Nada de parágrafos explicando o que vai fazer. Ficha e pronto.
- Se faltar informação que não é uma das 3 perguntas, Claude decide pelo padrão e mostra na ficha (a PM corrige se quiser).
- Várias tasks de uma vez → uma ficha de 5 linhas por task, numeradas; a PM responde "pode criar todas" ou "cria 1 e 3".

## Princípios (iguais à v1)

- **Problema > Solução** — a task diz o que está errado e o que precisa ser verdade no final; o "como" é do dev.
- **Decisões > Sugestões** — só entra como requisito o que foi decidido.
- **Testável** — o resultado esperado vira roteiro de teste.
- **Clareza > Brevidade** no CONTEXTO; **brevidade** em todo o resto.

## Passo a passo

1. **Procurar antes de criar.** Buscar no ClickUp se já existe task igual ou parecida (mesmo cliente + mesmo sintoma).
   - Existe e está aberta → **atualizar/mover** a existente, não duplicar. Nunca recriar uma task só porque virou a sprint.
   - Existe e está fechada, mas o problema voltou → criar nova e citar a antiga em REFERÊNCIAS.
2. **Separar fato de suposição.** Cada informação da demanda é: decisão (vai para REQUISITOS), fato observado (CONTEXTO), hipótese técnica (NOTAS TÉCNICAS) ou dúvida em aberto (perguntar à PM antes de criar).
3. **Checar o tamanho** (ver "Regra de tamanho"). Grande demais → propor a quebra antes de escrever.
4. **Escrever o corpo** no template abaixo.
5. **Montar a ficha** (campos do ClickUp, fora da descrição).
6. **Mostrar o rascunho à PM e só criar no ClickUp depois do "pode criar".**
7. **Avisar no Slack** (`#sla-tech`), marcando o dev responsável.

## Aviso no Slack (#sla-tech)

Depois de criar a task no ClickUp, postar **uma mensagem por task** no canal privado `#sla-tech`.

- Achar o canal com a busca de canais do Slack pelo nome `sla-tech` (incluir canais privados).
- Achar o dev com a busca de usuários do Slack pelo nome (ex.: "Thiago Andrade") e marcar com `<@ID_DO_DEV>`. Nunca escrever o nome solto: só a marcação avisa a pessoa.
- Se não achar o dev no Slack, postar sem marcação e avisar a PM.
- Mensagem curta (o time tem TDAH), neste formato:

```
🎫 Nova task para <@ID_DO_DEV>
*[Cliente] Tipo: título*
⚡ Prioridade · ⏱️ Estimativa · 📂 Lista
✅ Pronto quando: [critério em uma linha]
🔗 [link da task no ClickUp]
```

- Task urgente: começar com `🚨 URGENTE ·` antes de "Nova task".
- Se a PM editar uma task já criada (trocar dev, prioridade), **não** postar de novo, a menos que ela peça.

## Título

`[PROTOCOLO] [Cliente] Tipo: sintoma ou resultado em linguagem simples`

- `[PROTOCOLO]` só quando veio de chamado (ex.: `[UNYMOS-0008]`).
- Cliente **sempre primeiro e entre colchetes**, com o mesmo nome da tag (ex.: `[Dalton Varejo]`, não `Dalton Varejo:` nem `UX: [Dalton Varejo]`).
- Tipos fechados (use só estes):
  - `Bug:` algo que funcionava ou deveria funcionar e não funciona.
  - `Feature:` capacidade nova.
  - `Ajuste:` mudança pequena em algo que já existe (regra, texto, comportamento).
  - `UX:` mudança de tela, navegação ou visual.
  - `Op:` infra, deploy, carga de dados, operação.
  - `Discovery:` levantar requisitos/estudar antes de construir.
- Bug: o título descreve o **sintoma**, não a área. Ex.: `[IPAlpha] Bug: agente marca atendimento em horário já ocupado`.

## Corpo da task (template)

```markdown
## CONTEXTO
[De onde veio a demanda, estado atual, quem é afetado e qual o impacto.
Citação literal do cliente só quando traz tom/urgência que a paráfrase perde.]

## REQUISITOS DECIDIDOS   <!-- opcional -->
- [Decisão fechada: copy aprovado, regra de negócio, escopo recortado, restrição]
- Fora do escopo: [o que NÃO faz parte desta task, se houver risco de confusão]

## BLOQUEIO   <!-- opcional; se existir, status = blocked -->
- O que falta: [...]
- Depende de: [pessoa/cliente/empresa]
- Desde: [dd/mm]   · Próxima cobrança: [dd/mm]
- Quando destravar: [o que muda]

## RESULTADO ESPERADO
**Ao [situação]:**
- O sistema deve [comportamento]

**Quando [outra situação]:**
- O sistema deve [comportamento]

**Se [caso de borda/erro]:**
- O sistema deve [comportamento]

## COMO VALIDAR
- Quem aceita: [interno (PM/dev) ou cliente: nome]
- Onde testar: [ambiente/URL de homologação, conta/dado de teste]
- Pronto quando: [todos os cenários do RESULTADO ESPERADO passam em ...]

## REFERÊNCIAS
- [Chamado / reunião / gravação / task relacionada: link]

## NOTAS TÉCNICAS INTERNAS   <!-- opcional -->
[Pistas para o dev: arquivos, logs, hipóteses. Sempre marcar como
"hipótese, não confirmado". Nunca é a solução obrigatória.]
```

Regras do corpo:
- RESULTADO ESPERADO sempre tem **pelo menos um caso de borda/erro** (`Se ...`).
- COMO VALIDAR é obrigatório: é o que permite tirar a task de "testes humanos/externos" e fechar.
- Não entra no corpo: benefícios esperados, prazo, responsável, opinião do autor, solução prescrita. Prazo e responsável vão na **ficha**.

## Ficha da task (campos do ClickUp)

Preencher na criação; mostrar à PM junto com o rascunho.

| Campo | Regra |
|---|---|
| Lista | Pedido novo → **Backlog**. Só vai para a sprint atual se a PM decidir na planning ou se for urgente. Chamado de cliente ainda não aprovado → lista **Chamados**. |
| Tag | Tag do cliente/produto, minúscula com hífen (ex.: `unymos`, `dalton-varejo`, `jeisys-education`). Usar tag existente; não inventar variação. |
| Responsável | Sempre um dev. Se a PM ainda não decidiu, perguntar — **não criar task sem dono na sprint**. |
| Prioridade | **Urgente:** cliente parado ou dado errado em produção. **Alta:** compromisso com data ou bloqueia outra task. **Normal:** padrão. **Baixa:** melhoria sem prazo. |
| Estimativa | **Obrigatória. Claude gera** na escala P 30 min / M 2 h / G 4 h / GG 8 h (ver "Como estimar") e a PM só valida. Nunca subir task sem estimativa. |
| Data de entrega | Só quando houver compromisso real (demo, contrato, cliente). Não inventar. |
| Tipo | O mesmo do título (Bug/Feature/Ajuste/UX/Op/Discovery). Se o espaço tiver campo "Tipo", preencher também. |

## Como estimar (Claude gera, PM valida)

Os devs da Dalton Lab trabalham com IA e são rápidos. Estimar o tempo **real de um dev do time**, não o de um dev "médio de mercado". Errar para mais infla o painel de esforço.

| Tamanho | Tempo | Quando usar |
|---|---|---|
| **P** | **30 min** | Trocar texto, cor, configuração ou instrução do prompt; bug com causa óbvia; pedir um dado novo na conversa e usar numa integração que já existe. |
| **M** | **2 h** | Ajuste num fluxo inteiro (conversa + o que ela dispara); bug com causa conhecida que mexe em 2 lugares. |
| **G** | **4 h** | Feature pequena; bug que precisa investigar a causa; mexe em 3+ partes do sistema. |
| **GG** | **8 h** | Feature com várias telas, integração externa nova ou carga de dados. |

- Escolher sempre um desses 4 tamanhos.
- Na ficha, escrever tamanho + tempo + **uma linha de motivo** (ex.: "G · 4 h — bug sem causa confirmada, envolve n8n + painel").
- Na dúvida entre dois tamanhos, escolher o **menor**; a PM sobe se precisar.
- Se a PM disser quanto o dev leva ("o Thiago faz em 1 h"), usar o tamanho mais próximo e não discutir.
- Se a skill `triagem-de-tasks` estiver disponível, pode usar o histórico do dev para calibrar.
- Acima de 8 h → não estimar; propor a quebra (regra abaixo).

## Regra de tamanho

Quebrar em mais de uma task (ou task-mãe + subtasks) quando **qualquer** item abaixo for verdadeiro:
- estimativa acima de **8 h** (GG);
- mais de **5 cenários** no RESULTADO ESPERADO;
- mistura tipos (ex.: Bug + Feature nova);
- partes que podem ir para produção separadas.

Épico (ex.: "entrega de 15/01") vira **task-mãe** com data de entrega; cada parte entregável vira subtask com seu próprio RESULTADO ESPERADO.

## Checklist antes de mostrar à PM

- [ ] Procurei duplicata no ClickUp
- [ ] Título no formato `[Cliente] Tipo: ...`
- [ ] CONTEXTO explica o problema sem prescrever solução
- [ ] RESULTADO ESPERADO tem caso de borda
- [ ] COMO VALIDAR diz quem aceita e onde testar
- [ ] Se tem BLOQUEIO: dono + desde quando + próxima cobrança
- [ ] Ficha completa (lista, tag, responsável, prioridade, estimativa)
- [ ] Estimativa gerada por mim, com uma linha de motivo
- [ ] Cabe em ≤ 8 h, senão propus a quebra
- [ ] Hipóteses técnicas estão em NOTAS TÉCNICAS, marcadas como hipótese
- [ ] Depois de criar: aviso postado no `#sla-tech` com o dev marcado

## Exemplo curto

**Título:** `[UNYMOS-0008] [Unymos] Bug: IA repete "Você já está com um atendente" e transbordo não acontece em sessão aberta`

**Ficha:** Lista Sprint atual (urgente) · Tag `unymos` · Responsável Fabio · Prioridade Alta · Estimativa G · 4 h (bug sem causa confirmada, envolve n8n + painel)

```markdown
## CONTEXTO
Em teste de disparo, um atendimento com sessão aberta não foi transferido ao
atendente quando pedido. Num novo disparo, a IA passou a repetir "Você já está
com um atendente" sem ninguém atendendo. O cliente fica preso sem atendimento.

## REQUISITOS DECIDIDOS
- O transbordo pedido vale mesmo com sessão aberta.
- Fora do escopo: mudar o texto da mensagem de transbordo.

## RESULTADO ESPERADO
**Ao pedir transbordo com sessão aberta:**
- A conversa vai para o atendente na hora e aparece como transferida no painel.

**Quando um novo disparo reabre a conversa sem atendente ativo:**
- A IA volta a atender normalmente.

**Se já houver atendente ativo:**
- A IA não responde e o painel mostra a conversa como transferida.

## COMO VALIDAR
- Quem aceita: cliente (Unymos), após teste interno da PM
- Onde testar: homologação do Uny Dashboard, sessão de teste Pax Domini
- Pronto quando: os 3 cenários acima passam

## REFERÊNCIAS
- Chamado UNYMOS-0008 no status.daltonlab.ai

## NOTAS TÉCNICAS INTERNAS
Hipótese, não confirmado: flag de pausa do agente não é resetada no novo disparo.
```
