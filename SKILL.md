---
name: obsidian
description: Conecta este chat ao cofre Obsidian "Danilo Second Brain" (/mnt/Disco/Obsidian/Danilo Second Brain), alimenta-o durante toda a conversa e mantém a organização. Ativado quando o usuário digita /obsidian ou pede para conectar/salvar/alimentar o Obsidian. Com "/obsidian organizar" faz uma varredura e reorganiza o cofre (propõe, e aplica após aprovação).
---

# /obsidian — conexão viva com o cofre

**Cofre:** `/mnt/Disco/Obsidian/Danilo Second Brain` (Linux Fedora KDE; o HD é montado fixo via fstab em `/mnt/Disco`)

Ao ser ativada, esta skill vale **até o fim do chat**. Depois de ativada, você alimenta o cofre continuamente, sem o usuário pedir de novo.

**A estrutura do cofre fica em `_CLAUDE.md` na raiz** (árvore, tabela tipo → destino, regras). Ela é a fonte única: leia-a, siga-a e mantenha-a atualizada. Esta skill não repete a lista de pastas.

## 1. Ao ativar

1. Confirme que o cofre existe (`test -d`). Se não existir, avise e pare; nunca crie um cofre novo.
2. Leia `_CLAUDE.md`. Liste as pastas de primeiro nível (listagem real, não de memória) e leia o MOC das pastas relevantes ao assunto. Se `_CLAUDE.md` não existir, crie-o descrevendo a estrutura atual.
3. Descubra a qual projeto/área o chat pertence (diretório de trabalho, assunto, ou pergunte uma vez se ambíguo). Assunto novo ganha pasta nova, seguindo a subestrutura do `_CLAUDE.md`.
4. Responda em uma linha: cofre conectado e qual pasta/projeto foi identificado.

Se o usuário passou conteúdo junto com `/obsidian`, trate-o já como primeira entrada. Se passou `organizar`, vá para a seção 7.

## 2. Enquanto o chat segue: o que registrar

Registre sem esperar pedido:

- **Tudo que o usuário passar**: informações, links, textos, arquivos, imagens, decisões, contatos, requisitos.
- **Tudo que você fizer**: o que foi construído/alterado, commits, comandos relevantes, descobertas, erros e como foram resolvidos, resultados de pesquisa.
- **Decisões** (com data e quem decidiu), **pendências** e **pessoas** mencionadas.

Não registre: conversa trivial, tentativas descartadas sem aprendizado, segredos (senhas, tokens, chaves, credenciais). Se o usuário passar um segredo, registre só onde está guardado, nunca o valor.

Frequência: ao fim de cada bloco de trabalho significativo (algo decidido, criado, corrigido ou descoberto) e numa passada final quando o usuário encerrar. Não escreva a cada mensagem.

## 3. Onde escrever

Use a tabela **tipo → destino** do `_CLAUDE.md`. Princípios fixos:

- Uma pasta por empresa/projeto/área, com **índice (MOC) de mesmo nome** que linka as subpastas e os índices de cada tema com `[[wikilinks]]`.
- **O índice não repete tudo.** Liste subpastas e notas principais; sessões ficam em `Sessões/` do tema e o índice cita só as recentes ou aponta para a pasta.
- **Notas agrupadas por tema** em subpastas (`01 Marca`, `Planejamento`, etc.), nunca soltas na raiz da empresa, exceto o MOC.
- **Pessoas** vão para `Pessoal/Pessoas/` e linkam o projeto relacionado (e o MOC do projeto linka a pessoa).
- **Registro do chat:** `<tema>/Sessões/AAAA-MM-DD - <assunto curto>.md` (criada na primeira gravação, atualizada nas seguintes), linkada do MOC.
- **Anexos** em `Anexos/` do tema, embutidos com `![[arquivo]]`. Nome: `<projeto>-<assunto>[-data].ext`. Evite arquivos acima de ~5 MB; se for essencial, avise o usuário e registre o tamanho.
- Assunto pessoal/solto sem projeto: `Pessoal/`.
- Ao criar nota nova, **sempre** linke-a de um MOC ou nota existente (nenhuma órfã). Criar pasta nova de primeiro nível ou tema novo: atualize o `_CLAUDE.md`.

**Antes de criar, procure.** Busque por nome e conteúdo (`Grep`/`Glob`) se o assunto já tem nota. Se tiver, atualize em vez de duplicar. Só afirme que algo não existe depois de buscar.

## 4. Formato das notas

Português do Brasil, Markdown do Obsidian (sintaxe na skill `obsidian-markdown`). Frontmatter padrão:

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

- Ao editar nota existente, atualize `atualizado` e preserve o que o usuário escreveu (acrescente, não reescreva, salvo pedido).
- `[[wikilinks]]` para toda pessoa, projeto e conceito com nota; callouts (`> [!note]`, `> [!warning]`) para destaques; tabelas para dados comparáveis; `- [ ]` para pendências.
- Datas absolutas (AAAA-MM-DD), nunca "hoje"/"ontem".
- Marque "a confirmar" o que não for certo. Nunca invente fatos, datas ou nomes.
- Informação do usuário: deixe claro ("informado por você"); decisão dele: registre como decisão.

## 5. Como escrever os arquivos

- **Padrão:** `Write`/`Edit` direto no sistema de arquivos, caminho absoluto sob o cofre. Funciona com o Obsidian aberto ou fechado.
- **Mover/renomear:** use `mv` (links `[[nome]]` resolvem por nome). Se algum link usar caminho (`[[Pasta/Nota]]`), corrija-o. Atualize o MOC depois.
- **Opcional:** com o Obsidian aberto, a CLI (`obsidian vault="Danilo Second Brain" search query="..."`, `backlinks`, `property:set`) ajuda em busca e backlinks (skill `obsidian-cli`). Se falhar, siga pelo sistema de arquivos.
- Nunca grave fora do cofre e não mexa em `.obsidian/`, exceto se o usuário pedir.

## 6. Apagar e arquivar

- **Nunca apague** sem pedido explícito do usuário.
- Conteúdo obsoleto: mova para `Arquivo/` (crie a pasta e `Arquivo.md` se não existir), registre no `Arquivo.md` o que é e por que foi arquivado, e **pergunte** se pode apagar de vez. Apague só com a confirmação.
- Ao apagar ou arquivar, remova ou ajuste as menções nos MOCs.

## 7. Modo `/obsidian organizar`

Varredura e reorganização, em duas fases:

1. **Diagnóstico (somente leitura):** liste a árvore; encontre notas soltas na raiz de empresa/pasta, notas fora do destino da tabela do `_CLAUDE.md`, pastas vazias, anexos soltos fora de `Anexos/`, duplicatas, pastas de versões antigas, notas de teste ou obsoletas, MOCs desatualizados. Rode a checagem de links (abaixo).
2. **Proposta:** apresente o plano em lista curta `origem → destino`, separando "mover", "arquivar" e "apagar (precisa de confirmação)". **Só aplique após aprovação do usuário.**
3. **Aplicação:** `mv`/criação de pastas, atualização dos MOCs, do `_CLAUDE.md` e de links com caminho. Termine com a checagem de links e um resumo de uma linha por grupo de mudanças. Registre a reorganização em uma sessão (`Pessoal/Tecnologia/Sessões` ou onde fizer sentido).

Para mudanças pequenas e óbvias feitas durante o trabalho normal (ex.: mover a nota que você mesmo acabou de criar para o lugar certo), não precisa de aprovação.

## 8. Checagem de links (ao final de gravações grandes e no modo organizar)

Verifique `[[wikilinks]]` e embeds `![[arquivo]]` sem destino, e notas órfãs (sem backlink). Exemplo:

```bash
python3 - <<'EOF'
import os,re
V="/mnt/Disco/Obsidian/Danilo Second Brain"
names=set()
for r,d,f in os.walk(V):
    if '.git' in r or '.obsidian' in r: continue
    for x in f: names.add(os.path.splitext(x)[0]); names.add(x)
for r,d,f in os.walk(V):
    if '.git' in r or '.obsidian' in r: continue
    for x in f:
        if x.endswith('.md'):
            t=open(os.path.join(r,x),encoding='utf-8').read()
            for m in re.findall(r'!?\[\[([^\]|#\\]+)',t):
                if m.strip().split('/')[-1] not in names: print(x,'->',m)
EOF
```

Corrija o que for quebrado ou avise o usuário se o destino for ambíguo.

## 9. Ao final de cada gravação

Diga em uma ou duas linhas o que foi salvo e onde (caminho relativo ao cofre). Sem listar o conteúdo inteiro.
