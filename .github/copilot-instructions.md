---
name: Manual Base do Repositório (Copilot)
description: Executa demandas de manutenção com mínimo diff, sem mudanças estéticas, preservando estrutura e comportamento. Registra extras em docs/SUGESTOES.md.
---

# Manual Base do Repositório (Copilot)

Este arquivo (`.github/copilot-instructions.md`) define regras globais e obrigatórias para qualquer ajuste, correção ou melhoria neste repositório.

Além destas regras base, este repositório pode ter instruções complementares por papel em `.github/instructions/*.instructions.md` (Frontend, Backend, DB, QA, DevOps, Segurança, Documentação/Manuais, Observabilidade/Dashboards, Performance, Code Review). Essas instruções complementam este manual, mas não podem reduzir as exigências de mínimo diff e não ampliação de escopo.

---

## Objetivo

Aplicar correções e melhorias com o menor impacto possível, preservando comportamento, estilo e estrutura do projeto.

---

## Instruções complementares por papel (quando existirem)

Considere também os arquivos abaixo, quando aplicáveis ao escopo do PR:

- `.github/instructions/10-frontend.instructions.md`
- `.github/instructions/20-backend.instructions.md`
- `.github/instructions/30-db.instructions.md`
- `.github/instructions/40-qa.instructions.md`
- `.github/instructions/50-devops.instructions.md`
- `.github/instructions/60-security.instructions.md`
- `.github/instructions/70-docs-manual.instructions.md`
- `.github/instructions/75-observability-dashboard.instructions.md`
- `.github/instructions/80-performance.instructions.md`
- `.github/instructions/90-code-review.instructions.md`
- `.github/instructions/95-laravel-migration.instructions.md` (opt-in, usar só quando solicitado)

Regra de conflito:
- Se houver conflito entre instruções, siga sempre a opção mais conservadora (menor diff, menor risco, menor escopo) e documente no PR.

---

## Regras globais (obrigatórias)

1) Não alterar nada apenas por estética (formatação, nomes, ordem, espaçamento, comentários, etc.).
2) Focar exclusivamente no que foi solicitado. Não ampliar escopo.
3) Efetuar a menor quantidade de alteração possível (mínimo diff).
4) Não renomear variáveis, métodos, classes, arquivos, rotas, tabelas, colunas ou chaves apenas por estética.
5) Não refatorar sem necessidade funcional. Se uma refatoração for indispensável para cumprir a demanda, explicar no PR.
6) Manter a estrutura e o padrão de desenvolvimento do projeto (ex.: Controller -> Services -> Repositories, e SQL/queries onde já ficam hoje).
7) Preservar a indentação e formatação de SQL existente. Não reformatar queries.
8) Não alterar comportamentos silenciosamente. Se houver mudança de comportamento, declarar explicitamente.
9) Se surgirem melhorias extras não solicitadas, NÃO implementar. Registrar em `docs/SUGESTOES.md` com:
   - o que é
   - por que vale a pena
   - risco/impacto
   - esforço estimado
10) Garantir que o código resultante rode no ambiente alvo do projeto (ex.: PHP 8.3). Não introduzir dependências sem pedir.
11) Antes de finalizar, revisar se o diff ficou mínimo.
12) Rodar/validar o que for possível (tests/lint/build). Se não houver como rodar, declarar no PR.

---

## Feedback do manual (opcional, apenas quando houver)

Se, durante a execução da demanda, você perceber que faltou uma regra, houve ambiguidade, ou uma informação importante não estava documentada e isso atrapalhou a execução correta do PR:

- Não altere este manual automaticamente.
- Inclua no PR uma seção chamada "Sugestões para aprimorar as instruções do Copilot" contendo bullets curtos com:
  - problema observado (ex.: ambiguidade, regra faltante, padrão não descrito)
  - sugestão objetiva de texto para incluir no manual (1 a 3 frases)
  - impacto se não corrigir (ex.: risco de ampliar diff, risco de comportamento inesperado)

Se não houver sugestão real, não crie a seção.

---

## Estimativa de esforço (humano)

- Em todo PR, incluir uma estimativa de esforço humano (Dev Sênior) em horas.
- Usar faixa (min–max) e listar premissas (ex.: ambiente pronto, cobertura de testes, necessidade de homologação).
- Não usar o tempo de execução do agente como referência.

---

## Título do PR e título do commit final (Conventional Commits)

- O PR deve ter um título no formato Conventional Commits: `<tipo>(<escopo opcional>): <descrição>`.
- O agente deve sugerir:
  1) Título do PR (Conventional Commits)
  2) Título do commit final (Conventional Commits), considerando o que foi alterado
- Preferência de merge: "Squash and merge", para o commit final herdar o título do PR.
- Se o repositório não usar squash, o agente deve sugerir o título/mensagem do merge commit para ser colado no momento do merge.

---

## Formato de entrega

- Criar uma branch e um Pull Request.
- O PR deve ter:
  a) resumo objetivo do que foi feito  
  b) lista de arquivos alterados  
  c) como validar/testar  
  d) riscos/observações (se houver)
- Commits pequenos e descritivos (um commit por intenção). Evitar “mega commit”.

### Estrutura OBRIGATÓRIA do PR Description

Todo PR DEVE seguir esta estrutura exata, nesta ordem:

1. **Resumo** (2-3 frases descrevendo o que foi feito)

2. **📊 Estimativa de Esforço (Humano - Dev Sênior)** ← OBRIGATÓRIO, sempre logo após o resumo
   ```
   **Tempo estimado para cobrança**: X-Y horas faturáveis
   
   **Premissas**:
   - Ambiente de desenvolvimento já configurado
   - [Outras premissas relevantes]
   
   **Breakdown** (opcional, mas recomendado):
   - Análise/entendimento: X min
   - Implementação: Y min
   - Testes: Z min
   - Documentação: W min
   ```

3. **Arquivos Alterados** (lista com número de linhas)

4. **Como Validar/Testar** (passo a passo numerado)

5. **Riscos/Observações** (se houver)

6. **Sugestões para Aprimorar as Instruções do Copilot** (apenas se houver sugestões reais; não criar se não houver)

**Importante**: A seção "📊 Estimativa de Esforço" DEVE aparecer logo após o Resumo, ANTES de qualquer outra seção técnica, e SEMPRE com este emoji 📊 para fácil identificação visual.


---

## Como executar uma demanda

Ao receber uma demanda:
1) Identifique exatamente o que foi pedido e o que não foi pedido.
2) Aplique a menor mudança possível para cumprir.
3) Se algo importante estiver ambíguo ou arriscado, não adivinhe: escolha a solução mais conservadora e documente no PR.
4) Se notar melhorias fora do escopo, registrar em `docs/SUGESTOES.md` e parar por aí.
