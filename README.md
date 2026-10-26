# skill-obisidan

Skill `/obsidian` para Claude: conecta o chat ao cofre Obsidian, e passa a alimentá-lo durante toda a conversa (decisões, pendências, pessoas, registro de sessões).

## Instalação

Copie `SKILL.md` para uma pasta `obsidian/` dentro do diretório de skills do Claude, por exemplo:

```
~/.claude/skills/obsidian/SKILL.md
```

## Uso

Digite `/obsidian` no chat. A skill vale até o fim da conversa.

> Ajuste o caminho do cofre no `SKILL.md` se o seu estiver em outro local.

## Estrutura do cofre (`_CLAUDE.md`)

A skill lê um `_CLAUDE.md` na raiz do cofre com a árvore de pastas, a tabela tipo → destino e as regras de organização. Se não existir, ela cria um a partir da estrutura atual. `_CLAUDE.example.md` é um exemplo para copiar e adaptar.

## Modo organizar

`/obsidian organizar` faz uma varredura do cofre, propõe os movimentos (origem → destino) e só aplica após sua aprovação.
