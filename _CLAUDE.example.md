---
title: _CLAUDE
tags:
  - cofre
  - organizacao
tipo: referencia
criado: 2026-10-25
atualizado: 2026-10-25
---

# Guia de organização do cofre

Fonte única da estrutura. A skill `/obsidian` lê este arquivo ao ativar e o mantém atualizado.

## Estrutura (primeiro nível)

| Pasta | O que guarda | Índice (MOC) |
| :--- | :--- | :--- |
| `Veme/` | Empresa Veme | [[Veme]] |
| `Texan Group/` | Empresa Texan Group e seus produtos | [[Texan Group]] |
| `Pessoal/` | Vida pessoal, pessoas, tecnologia pessoal, calendário | [[Pessoal]] |
| `Projetos/` | Projetos avulsos, sem empresa | uma nota por projeto (ex.: [[Radar IA]]) |
| `Arquivo/` | Obsoleto, criada só quando necessário | `Arquivo.md` |

## Subestrutura por empresa/projeto

- **Veme:** `01 Marca`, `02 Site` (com `Sessões`), `03 Link Hub` (com `Sessões`), `04 Comercial` (`Precificação`, `Família Ana Clara`), `05 Ideias`, `Anexos` (`Marca`, `Site`, `Equipe e vídeo`).
- **Texan Group:** uma pasta por produto (`HealthX`, `OraculoX`, `Texan Hub`, `Texan Talxs`), cada uma com `Sessões/` e `Planejamento/` (decisões, pendências, plano de prompts, reunião); `Anexos/` dentro do produto que usa a imagem.
- **Pessoal:** `Pessoas`, `Tecnologia` (com `Sessões`), `Calendário`.

## Tipo de nota → destino

| `tipo` | Destino |
| :--- | :--- |
| `empresa` / `projeto` (índice) | raiz da própria pasta, nome igual ao da pasta |
| `sessao` | `Sessões/` do tema ou produto, `AAAA-MM-DD - assunto.md` |
| decisões / pendências | `Planejamento/` do produto, ou raiz do tema (Veme: `02 Site`) |
| `pessoa` | `Pessoal/Pessoas/`, com link para o projeto relacionado |
| `referencia` | pasta do tema; geral vai para `Pessoal/Tecnologia` |
| imagem, vídeo, PDF | `Anexos/` do tema (subpasta se já existir) |
| sem projeto | `Pessoal/` |

## Regras

- Toda nota é linkada de um índice ou de outra nota. Sem órfãs.
- Mover = `mv` em arquivo; links `[[nome]]` seguem valendo. Atualizar o índice depois.
- Obsoleto vai para `Arquivo/`. Só apaga com pedido explícito.
- Mudou a estrutura? Atualize esta nota.
