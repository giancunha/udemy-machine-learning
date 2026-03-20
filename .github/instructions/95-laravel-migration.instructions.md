---
applyTo: "**/*.php,**/*.inc,**/*.sql,composer.json,composer.lock,**/routes/*.php,**/app/**/*.php,**/database/**/*.php,**/resources/views/**/*.php,**/*.blade.php"
name: Migração para Laravel (opt-in)
description: Diretrizes para migração incremental do legado para Laravel. Estas regras só valem quando a demanda pedir explicitamente.
---

# Migração para Laravel (opt-in)

## Gatilho de uso (obrigatório)
Estas instruções só devem ser aplicadas quando a demanda mencionar explicitamente:
- "migração para Laravel", ou
- "usar o papel Migração para Laravel", ou
- citar este arquivo: `.github/instructions/95-laravel-migration.instructions.md`

Se a demanda não fizer isso, ignore este arquivo completamente.

## Objetivo
Ajudar a migrar partes do projeto para Laravel de forma incremental, com baixo risco, sem big bang e sem ampliar escopo.

## Princípios
1) Migração incremental (padrão "strangler"): mover por módulo ou rota, em etapas pequenas.
2) Preservar comportamento e URLs sempre que possível.
3) Evitar mudanças cosméticas e manter mínimo diff por PR.
4) Não alterar schema de banco sem solicitação explícita.
5) Sempre deixar claro no PR: o que foi migrado, o que ainda é legado, e como validar.

## Padrões de arquitetura (quando for código Laravel)
- Controllers: apenas requisição, validação e resposta.
- Lógica: em Services.
- Acesso a dados: em Repositories.
- Não colocar SQL em handlers/roteadores (ex.: `listaPrincipal.php`). SQL fica nas Classes/Repositories, seguindo o padrão do projeto.
- Manter ações/handlers em ordem alfabética onde essa convenção já existe.

## Estratégia recomendada (alto nível)
1) Escolher um módulo pequeno e bem delimitado.
2) Migrar primeiro endpoints e regras de negócio antes de telas complexas.
3) Para DB existente: mapear tabelas sem renomear, sem alterar chave primária e sem "limpar" nomes.
4) Se precisar de Blade, migrar views por tela, mantendo assets e comportamento.
5) Criar passos de rollback claros (como desfazer a rota ou voltar para a implementação legado).

## Checklist do PR (quando usar este papel)
- Rotas migradas listadas no PR
- Como testar localmente e em homologação
- Impactos e riscos
- Plano de rollback
- Se algo não foi possível por falta de informação, registrar no PR (não adivinhar)
