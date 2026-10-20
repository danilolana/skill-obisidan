---
name: obsidian
description: Conecta este chat ao cofre Obsidian "Danilo Second Brain" (D:\Obsidian\Danilo Second Brain) e passa a alimentá-lo durante toda a conversa. Ativado quando o usuário digita /obsidian ou pede para conectar/salvar/alimentar o Obsidian. A partir da ativação, tudo que o usuário passar e tudo que for feito no chat vira nota no cofre, criando pastas e arquivos conforme necessário.
---

# /obsidian — conexão viva com o cofre

**Cofre:** `D:\Obsidian\Danilo Second Brain` (no Git Bash: `/d/Obsidian/Danilo Second Brain`)

Ao ser ativada, esta skill vale **até o fim do chat**. Não é uma ação única: depois de ativada, você alimenta o cofre continuamente, sem o usuário precisar pedir de novo.

## 1. Ao ativar

1. Confirme que o cofre existe (`Test-Path`). Se não existir, avise o usuário e pare; nunca crie um cofre novo por conta própria.
2. Mapeie o estado atual: liste as pastas de primeiro nível e leia as notas-índice (MOC) das pastas relevantes ao assunto do chat. Se houver `_CLAUDE.md` ou `index.md` na raiz, leia primeiro.
3. Descubra a qual projeto/área este chat pertence (pelo diretório de trabalho, pelo assunto, ou pergunte uma vez se for ambíguo). Pastas existentes hoje: `Escola`, `Pessoal`, `Texan Group`, `Veme`. Assuntos novos ganham pasta nova.
4. Responda em uma linha: cofre conectado, qual pasta/projeto foi identificado. Sem relatório longo.

Se o usuário passou conteúdo junto com o `/obsidian`, trate-o já como a primeira entrada (passo 2 abaixo).

## 2. Enquanto o chat segue: o que registrar

Registre no cofre, sem esperar pedido:

- **Tudo que o usuário passar**: informações, links, textos, arquivos, imagens, decisões, contatos, requisitos.
- **Tudo que você fizer no chat**: o que foi construído/alterado, commits, comandos relevantes, descobertas, erros e como foram resolvidos, resultados de pesquisa.
- **Decisões** (com data e quem decidiu), **pendências/tarefas** e **pessoas** mencionadas.

Não registre: conversa trivial, tentativas descartadas sem aprendizado, segredos (senhas, tokens, chaves de API, credenciais). Se o usuário passar um segredo, registre apenas onde ele está guardado, nunca o valor.

Frequência: atualize ao fim de cada bloco de trabalho significativo (algo foi decidido, criado, corrigido ou descoberto), e faça uma passada final quando o usuário encerrar ou pedir. Não escreva a cada mensagem.

## 3. Onde escrever

Segue a convenção que o cofre já usa:

- Uma **pasta por projeto/área**, com uma **nota-índice (MOC) de mesmo nome** da pasta (ex.: `Veme/Veme.md`) que lista as demais notas com `[[wikilinks]]`.
- Notas recorrentes por projeto: `Decisões <Projeto>.md` (por data, mais recente embaixo da data) e `Pendências <Projeto>.md`.
- Imagens e arquivos em `<Pasta>/Anexos/`, embutidos com `![[arquivo.png]]`.
- **Registro do chat**: nota `<Pasta>/Sessões/AAAA-MM-DD - <assunto curto>.md` com o resumo do que foi feito neste chat (criada na primeira gravação, atualizada nas seguintes). Linke-a no MOC.
- Assunto pessoal/solto sem projeto: `Pessoal/`.
- Crie pastas e arquivos novos livremente quando o conteúdo pedir. Ao criar uma nota nova, **sempre** linke-a a partir do MOC ou de uma nota existente (nenhuma nota órfã).

**Antes de criar, procure.** Busque por nome e por conteúdo (`Grep`/`Glob` no cofre) se o assunto já tem nota. Se tiver, atualize em vez de duplicar. Só afirme que algo não existe depois de buscar de verdade.

## 4. Formato das notas

Português do Brasil, Markdown do Obsidian (consulte a skill `obsidian-markdown` para a sintaxe). Frontmatter padrão do cofre:

```yaml
---
title: <Título>
tags:
  - <projeto>
  - <tipo>
tipo: <empresa | projeto | registro | sessao | pessoa | referencia | ...>
criado: AAAA-MM-DD
atualizado: AAAA-MM-DD
---
```

- Ao editar nota existente, atualize `atualizado` e preserve o que o usuário já escreveu (acrescente, não reescreva, salvo pedido).
- Use `[[wikilinks]]` para toda pessoa, projeto e conceito que tenha ou mereça nota; callouts (`> [!note]`, `> [!warning]`) para destaques; tabelas para dados comparáveis; `- [ ]` para pendências.
- Datas absolutas (AAAA-MM-DD), nunca "hoje"/"ontem".
- Marque como "a confirmar" o que não for certo. Nunca invente fatos, datas ou nomes.
- Quando a informação veio do usuário, deixe isso claro ("informado por você"); quando foi decisão dele, registre como decisão.

## 5. Como escrever os arquivos

- **Padrão:** escreva direto no sistema de arquivos com `Write`/`Edit`, caminho absoluto sob `D:\Obsidian\Danilo Second Brain`. Funciona com o Obsidian aberto ou fechado e não depende de nada mais.
- **Opcional:** com o Obsidian aberto, a CLI (`obsidian vault="Danilo Second Brain" search query="..."`, `backlinks`, `property:set`) ajuda em busca e backlinks. Detalhes na skill `obsidian-cli`. Se a CLI falhar, siga pelo sistema de arquivos.
- Nunca grave fora do cofre, nunca apague nota existente sem o usuário pedir, e não mexa em `.obsidian/` (configuração do app), exceto se o usuário pedir.

## 6. Ao final de cada gravação

Diga em uma ou duas linhas o que foi salvo e onde (com caminho relativo ao cofre). Sem listar o conteúdo inteiro.
