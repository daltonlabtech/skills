# Dalton Lab Skills

Skills para Claude Code usadas pelo time Dalton Lab.

## Instalação

**Pré-requisito:** ter o `skills` CLI instalado.

```bash
npm install -g skills-sh
```

**Instalar as skills:**

```bash
skills add daltonlabtech/skills -g
```

Isso instala todas as skills globalmente em `~/.claude/skills/`.

## Atualizar

```bash
skills update
```

## Skills disponíveis

| Skill | Descrição |
|-------|-----------|
| `daltonlab-lp-conversion` | Diagnóstico e construção de landing pages de alta conversão — ICP psicográfico, níveis de consciência de Schwartz, checklist tático |
| `llm-council` | Roda uma decisão por um conselho de 5 conselheiros com lentes de pensamento distintas, peer-review anônimo e síntese final de um chairman (metodologia LLM Council do Karpathy) |
| `task-builder` | Estrutura padronizada para escrever tarefas técnicas claras e executáveis para equipes de desenvolvimento (ClickUp, Linear, Notion, Jira ou texto livre) |
