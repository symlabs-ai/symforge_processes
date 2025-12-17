# ForgeProcess — Roteiro Operacional & Estado de Execução

> Documento de referência para **symbiotas** e humanos seguirem o fluxo
> completo do ForgeProcess (MDD → BDD → Execution → Delivery → Feedback),
> com **checklists por etapa** e **arquivos obrigatórios**.
>
> Objetivo: evitar “atalhos” (ex.: pular Roadmap Planning e ir direto para TDD)
> e manter um ponto único de verdade sobre o estado atual da execução.
>
> **Regra operacional para symbiotas:** no início de **cada fase** (MDD, BDD,
> Execution, Delivery, Feedback), o symbiota responsável por aquela fase deve
> ser carregado/ativado para conduzir a execução junto ao usuário, atuando como
> facilitador e executor das tarefas daquela fase. A cada etapa concluída,
> esse symbiota (ou o orquestrador que o invocou) deve **atualizar o progresso**
> neste arquivo (`process/process_execution_state.md`), marcando os checkboxes
> relevantes e ajustando `current_phase`, `last_completed_step` e
> `next_recommended_step`.

---

## 0. Convenções gerais

- Sempre seguir a ordem macro (não inverter):
  - Intenção de valor → **MDD** → **BDD** → **Execution (Roadmap → TDD)** → **Delivery (Sprint + Review)** → **Feedback**.
- Arquitetura e backlog **NUNCA** são definidos dentro do TDD:
  - TDD implementa o que já está definido em `project/specs/roadmap/` (principalmente `BACKLOG.md`).
  - Roadmap Planning é o lugar para validar arquitetura, dependências e priorização.
- Persistência:
  - Artefatos em Markdown/YAML, versionados em Git.
  - Commits preferencialmente por etapa/fase, com mensagem clara.
- CLI-first (para produtos CLI, como forgeCodeAgent):
  - A interface primária de validação deve ser uma **CLI oficial** (ex.: `forge-code-agent ...`), não apenas a API Python.
  - Para cada funcionalidade exposta em `src/**` que faça parte de um ValueTrack, deve existir um comando correspondente na CLI oficial.
  - Scripts em `examples/` existem para **exercitar fluxos end-to-end via CLI oficial** (por sprint e por ValueTrack), não para testar apenas funções/mocks diretamente em Python.
- Symbiotas relevantes:
  - `mdd_coach`, `mdd_publisher`
  - `bdd_coach`
  - `roadmap_coach`, `execution_coach`, `mark_arc`
  - `forge_coder`
  - `sprint_coach`, `delivery_coach`
  - `bill_review`, `jorge_the_forge`

---

## 1. Estado atual do ForgeProcess (espelho do YAML)

> Campo de **estado vivo** (legível para humanos) espelhando o conteúdo de
> `process/state/forgeprocess_state.yml`. O YAML é a **fonte de verdade**;
> este bloco deve ser mantido em sincronia por agentes/symbiotas.

- [ ] `current_phase`: `null`
- [ ] `current_cycle`: `null`
- [ ] `current_sprint`: `null`
- [ ] `last_completed_step`: `null`
- [ ] `next_recommended_step`: `mdd.01.concepcao_visao`

> Convenção sugerida: atualizar primeiro `forgeprocess_state.yml` e, depois,
> refletir aqui os campos principais ao final de cada etapa significativa
> (pelo menos por fase) para facilitar handoffs entre agentes.

---

## 1.1 Planejamento de Ciclos (visão macro do produto)

> Preenchido durante Roadmap Planning (`execution.roadmap.06.cycle_planning`).
> Fonte de verdade: `project/specs/roadmap/CYCLE_PLAN.md` e `forgeprocess_state.yml`.

### Visão do Produto Completo

| Métrica | Valor |
|---------|-------|
| Total de ciclos planejados | `null` |
| Ciclos completos | `0` |
| Total de ValueTracks | `null` |
| Total de sprints estimados | `null` |

### Métricas por Três Dimensões

> O ForgeProcess adota três dimensões independentes:
> - **CUSTO**: Quanto custa (tokens × preço + horas × valor)
> - **ESFORÇO**: Quanto trabalho (tokens IA + horas humanas)
> - **PRAZO**: Quando fica pronto (tempo de ciclo em dias)

#### CUSTO

| Métrica | Estimado | Consumido | Variância |
|---------|----------|-----------|-----------|
| Tokens | `null` | `0` | - |
| Custo IA (USD) | `null` | `$0` | - |
| Horas humanas | `null` | `0` | - |
| Custo humano (USD) | `null` | `$0` | - |
| **Custo Total (USD)** | `null` | `$0` | - |

#### ESFORÇO

| Métrica | Estimado | Consumido | Variância |
|---------|----------|-----------|-----------|
| Tokens (IA) | `null` | `0` | - |
| Horas (humano) | `null` | `0` | - |

#### PRAZO

| Métrica | Estimado | Decorrido | Variância |
|---------|----------|-----------|-----------|
| Tempo de ciclo (dias) | `null-null` | `0` | - |
| Data início | `null` | - | - |
| Data alvo entrega | `null-null` | - | - |
| Paralelização aplicada | `não` | - | - |

### Alocação de ValueTracks por Ciclo

| Ciclo | Nome | ValueTracks | Custo (USD) | Prazo (dias) | Status |
|-------|------|-------------|-------------|--------------|--------|
| cycle-01 | - | - | $0 | 0-0 | pending |
| cycle-02 | - | - | $0 | 0-0 | pending |
| cycle-03 | - | - | $0 | 0-0 | pending |

### Ciclo Atual — Detalhes

- **Nome do ciclo**: `null`
- **ValueTracks neste ciclo**: `[]`
- **ValueTracks concluídos**: `[]`
- **Sprints concluídos**: `0`
- **Sprints estimados**: `null`
- **Custo estimado**: `$null`
- **Custo consumido**: `$0`
- **Prazo estimado**: `null-null dias`
- **Dias decorridos**: `0`

> Esta seção responde: "Quanto falta para terminar o produto?"
> Atualizar ao final de cada ciclo ou quando CYCLE_PLAN.md for revisado.
> Referência: `process/guides/forgeprocess-metricas-hibridas.md`

---

## 2. Bootstrap do projeto

- [ ] Verificar estrutura mínima:
  - [ ] Diretórios: `process/`, `project/`, `project/specs/`, `src/`, `tests/`
  - [ ] Arquivos: `process/PROCESS.yml`, `process/README.md`
- [ ] Criar hipótese inicial (se não existir):
  - [ ] `project/docs/hipotese.md` (template: `process/templates/template_hipotese.md`)
- [ ] Atualizar estado (YAML + este arquivo):
  - [ ] `current_phase = mdd`
  - [ ] `last_completed_step = mdd.01.concepcao_visao`
  - [ ] `next_recommended_step = mdd.02.sintese_executiva`

---

## 3. Fase MDD — Market Driven Development

Referência: `process/mdd/PROCESS.yml`

> Symbiota responsável pela fase (etapas 3.1 a 3.6): `mdd_coach`.
> Revisor de processo ao final da fase: `jorge_the_forge` (audita se o MDD seguiu o ForgeProcess).

### 3.1 Etapa 01 — Concepção da Visão

- Entradas:
  - [ ] `project/docs/hipotese.md`
- Saídas (criar/preencher):
  - [ ] `project/docs/visao.md` (template: `process/templates/template_visao.md`)
- Critério de conclusão:
  - [ ] Visão aprovada pelo stakeholder (decisão `validar_visao = approved`)
  - Atualizar estado:
    - [ ] `last_completed_step = mdd.01.concepcao_visao`
    - [ ] `next_recommended_step = mdd.02.sintese_executiva`

### 3.2 Etapa 02 — Síntese Executiva

- Entradas:
  - [ ] `project/docs/visao.md`
- Saídas:
  - [ ] `project/docs/sumario_executivo.md` (template: `process/templates/template_sumario_executivo.md`)
  - [ ] (opcional) `project/output/docs/sumario_executivo.pdf` — gerado por `mdd_publisher`
- Critério de conclusão:
  - [ ] Síntese aprovada (`validar_sintese = approved`)
  - Atualizar estado:
    - [ ] `last_completed_step = mdd.02.sintese_executiva`
    - [ ] `next_recommended_step = mdd.03.pitch_valor`

### 3.3 Etapa 03 — Pitch de Valor

- Entradas:
  - [ ] `project/docs/visao.md`
  - [ ] `project/docs/sumario_executivo.md`
- Saídas:
  - [ ] `project/docs/pitch_deck.md` (template: `process/templates/template_pitch_deck.md`)
  - [ ] (opcional) `project/output/docs/pitch_deck.pptx` — gerado por `mdd_publisher`
- Critério de conclusão:
  - [ ] Pitch aprovado (`validar_pitch = approved`)
  - Atualizar estado:
    - [ ] `last_completed_step = mdd.03.pitch_valor`
    - [ ] `next_recommended_step = mdd.04.validacao_publica`

### 3.4 Etapa 04 — Validação Pública Inicial

- Entradas:
  - [ ] `project/docs/visao.md`
  - [ ] `project/docs/sumario_executivo.md`
  - [ ] `project/docs/pitch_deck.md`
- Saídas:
  - [ ] `project/docs/sites/site_A.md` (template: `process/templates/template_site.md`)
  - [ ] `project/docs/sites/site_B.md` (template: `process/templates/template_site.md`)
  - [ ] `project/docs/sites/site_C.md` (template: `process/templates/template_site.md`)
  - [ ] (opcionais) `project/output/docs/sites/site_*.html` — por `mdd_publisher`
  - [ ] `project/docs/resultados_validacao.md` (template: `process/templates/template_resultados_validacao.md`)
  - [ ] (opcional) `project/output/docs/resultados_validacao.html`
- Critério de conclusão:
  - [ ] Stakeholder confirma que dados de validação estão prontos (`validar_landing_pages = approved`)
  - Atualizar estado:
    - [ ] `last_completed_step = mdd.04.validacao_publica`
    - [ ] `next_recommended_step = mdd.05.avaliacao_estrategica`

### 3.5 Etapa 05 — Avaliação Estratégica

- Entradas:
  - [ ] `project/docs/resultados_validacao.md`
- Saídas (uma ou mais, dependendo da decisão):
  - [ ] `project/docs/aprovacao_mvp.md` (template: `process/templates/template_aprovacao_mvp.md`)
  - [ ] `project/docs/revisao_estrategica.md` (template: `process/templates/template_revisao_estrategica.md`)
  - [ ] `project/docs/rejeicao_projeto.md` (template: `process/templates/template_rejeicao_projeto.md`)
- Critério de conclusão:
  - [ ] Decisão do stakeholder (`decisao_mvp` = `approved` | `needs_revision` | `rejected`)
  - Se `needs_revision`: voltar para Etapa 01 e atualizar estado.
  - Se `rejected`: macro-processo termina (`end_projeto_rejeitado`).
  - Se `approved`:
    - [ ] `next_recommended_step = mdd.06.handoff_bdd`

### 3.6 Etapa 06 — Handoff para BDD

- Entradas:
  - [ ] `project/docs/aprovacao_mvp.md`
- Saídas:
  - [ ] `project/docs/handoff_bdd.md` (template: `process/templates/template_handoff_bdd.md`)
- Critério de conclusão:
  - [ ] Handoff concluído (`return_approved`)
  - Atualizar estado:
    - [ ] `current_phase = bdd`
    - [ ] `last_completed_step = mdd.06.handoff_bdd`
    - [ ] `next_recommended_step = bdd.01.mapeamento_comportamentos`

---

## 4. Fase BDD — Behavior Driven Development

Referência: `process/bdd/PROCESS.yml`

> Symbiota responsável pela fase (etapas 4.1 a 4.6): `bdd_coach`.
> Revisor de processo ao final da fase: `jorge_the_forge` (audita se o BDD seguiu o ForgeProcess).

### 4.1 Etapa 01 — Mapeamento de Comportamentos

- Entradas:
  - [ ] `project/docs/visao.md`
  - [ ] `project/docs/aprovacao_mvp.md`
- Saídas:
  - [ ] `project/specs/bdd/drafts/behavior_mapping.md`
- Critério de conclusão:
  - [ ] Mapeamento aprovado (`validar_mapeamento = approved`)
  - Atualizar estado:
    - [ ] `last_completed_step = bdd.01.mapeamento_comportamentos`
    - [ ] `next_recommended_step = bdd.02.features_gherkin`

### 4.2 Etapa 02 — Escrita de Features Gherkin

- Entradas:
  - [ ] `project/specs/bdd/drafts/behavior_mapping.md`
- Saídas:
  - [ ] `project/specs/bdd/**/*.feature` (cenários Given/When/Then, linguagem de negócio)
- Critério de conclusão:
  - [ ] Features aprovadas (`validar_features = approved`)
  - Atualizar estado:
    - [ ] `last_completed_step = bdd.02.features_gherkin`
    - [ ] `next_recommended_step = bdd.03.organizacao_tagging`

### 4.3 Etapa 03 — Organização e Tagging

- Entradas:
  - [ ] `project/specs/bdd/**/*.feature`
- Saídas:
  - [ ] Estrutura de pastas organizada (10_, 20_, 30_, etc.) em `project/specs/bdd/`
  - [ ] Tags aplicadas (@ci-fast, @ci-int, @e2e) em todas as features
  - [ ] `project/specs/bdd/README.md` atualizado
- Critério de conclusão:
  - [ ] Organização e tags aprovadas (`validar_organizacao = approved`)
  - Atualizar estado:
    - [ ] `last_completed_step = bdd.03.organizacao_tagging`
    - [ ] `next_recommended_step = bdd.04.tracks_yml`

### 4.4 Etapa 04 — Criação de tracks.yml

- Entradas:
  - [ ] `project/specs/bdd/**/*.feature`
  - [ ] `project/docs/visao.md`
- Saídas:
  - [ ] `project/specs/bdd/tracks.yml`
- Critério de conclusão:
  - [ ] tracks.yml aprovado (`validar_tracks = approved`)
  - Atualizar estado:
    - [ ] `last_completed_step = bdd.04.tracks_yml`
    - [ ] `next_recommended_step = bdd.05.skeleton_automacao`

### 4.5 Etapa 05 — Skeleton de Automação

- Entradas:
  - [ ] `project/specs/bdd/**/*.feature`
- Saídas:
  - [ ] `tests/bdd/test_*_steps.py`
  - [ ] `tests/bdd/conftest.py`
  - [ ] `pytest.ini`
- Critério de conclusão:
  - [ ] Skeleton aprovado (`validar_skeleton = approved`)
  - Atualizar estado:
    - [ ] `last_completed_step = bdd.05.skeleton_automacao`
    - [ ] `next_recommended_step = bdd.06.handoff_roadmap`

### 4.6 Etapa 06 — Handoff para Roadmap Planning

- Entradas:
  - [ ] `project/specs/bdd/**/*.feature`
  - [ ] `project/specs/bdd/tracks.yml`
  - [ ] `tests/bdd/`
- Saídas:
  - [ ] `project/specs/bdd/HANDOFF_BDD.md`
- Critério de conclusão:
  - [ ] Tech lead confirma completude (`decisao_completude = complete`)
  - Atualizar estado:
    - [ ] `current_phase = execution.roadmap_planning`
    - [ ] `last_completed_step = bdd.06.handoff_roadmap`
    - [ ] `next_recommended_step = execution.roadmap.00.validacao_stakeholder`

---

## 5. Fase Execution — Roadmap Planning + TDD

Referência: `process/execution/PROCESS.yml`

### IMPORTANTE — Ordem obrigatória dentro de Execution

- [ ] **NUNCA** iniciar `execution.tdd.*` direto logo após BDD.
- [ ] Sempre seguir:
  - [ ] `execution.roadmap_planning` → gerar `project/specs/roadmap/*`
  - [ ] **só depois** `execution.tdd` (TDD Workflow)
- TDD só começa se:
  - [ ] `project/specs/roadmap/ROADMAP.md` existir
  - [ ] `project/specs/roadmap/BACKLOG.md` existir
  - [ ] Ambiente de testes e hooks de pre-commit estiverem configurados (virtualenv, pytest/pytest-bdd, pre-commit + ruff conforme `env/setup-git.txt`)

### 5.1 Roadmap Planning (execution.roadmap_planning)

Referência: `process/execution/roadmap_planning/PROCESS.yml`

> Symbiotas por intervalo de etapas desta fase:
> - Etapas 5.1.1–5.1.2 (validação arquitetural + stack/ADRs): `mark_arc` (análise arquitetural ForgeBase).
> - Etapas 5.1.3–5.1.6 (dependências, quebra, estimativa, backlog): `roadmap_coach`.

#### 5.1.1 Etapa 00 — Validação Arquitetural com Stakeholders

- Entradas:
  - [ ] `project/docs/visao.md`
  - [ ] `project/specs/bdd/*.feature`
  - [ ] `project/specs/bdd/tracks.yml`
- Saídas:
  - [ ] `project/specs/roadmap/ARCHITECTURAL_QUESTIONNAIRE.md`
  - [ ] `project/specs/roadmap/ARCHITECTURAL_DECISIONS_APPROVED.md`
- Critério de conclusão:
  - [ ] Stakeholder aprova propostas (`decisao_aprovacao_arquitetura = approved`)

#### 5.1.2 Etapa 01 — Definição Arquitetural e Stack (ADR)

- Entradas:
  - [ ] `project/specs/roadmap/ARCHITECTURAL_DECISIONS_APPROVED.md`
- Saídas:
  - [ ] `project/specs/roadmap/TECH_STACK.md`
  - [ ] `project/specs/roadmap/ADR.md`
  - [ ] `project/specs/roadmap/adr/*.md`
  - [ ] `project/specs/roadmap/HLD.md`
  - [ ] `project/specs/roadmap/LLD.md`

#### 5.1.3 Etapa 02 — Análise de Dependências

- Entradas:
  - [ ] `project/specs/bdd/tracks.yml`
  - [ ] `project/specs/bdd/**/*.feature`
- Saídas:
  - [ ] `project/specs/roadmap/dependency_graph.md`

#### 5.1.4 Etapa 03 — Quebra de Features

- Entradas:
  - [ ] `project/specs/bdd/**/*.feature`
  - [ ] `project/specs/roadmap/dependency_graph.md`
- Saídas:
  - [ ] `project/specs/roadmap/feature_breakdown.md`

#### 5.1.5 Etapa 04 — Estimativa e Priorização

- Entradas:
  - [ ] `project/specs/roadmap/feature_breakdown.md`
  - [ ] `project/specs/roadmap/dependency_graph.md`
- Saídas:
  - [ ] `project/specs/roadmap/estimates.yml`

#### 5.1.6 Etapa 05 — Criação do Roadmap e Backlog

- Entradas:
  - [ ] `project/specs/roadmap/estimates.yml`
  - [ ] `project/specs/roadmap/dependency_graph.md`
- Saídas:
  - [ ] `project/specs/roadmap/ROADMAP.md`
  - [ ] `project/specs/roadmap/BACKLOG.md`
- Critério de conclusão:
  - [ ] Tech lead aprova roadmap (`decisao_aprovacao_roadmap = approved`) — aprovador: _stakeholder/tech lead deste projeto_
  - Atualizar estado:
    - [ ] `current_phase = execution.tdd`
    - [ ] `last_completed_step = execution.roadmap.05.roadmap_backlog`
    - [ ] `next_recommended_step = execution.tdd.01.selecao_tarefa`

### 5.2 TDD Workflow (execution.tdd)

Referência: `process/execution/tdd/PROCESS.yml`

> Symbiota responsável por esta fase: `forge_coder` (seleciona tarefa, escreve e consolida testes/steps BDD e, quando necessário, faz ajustes mínimos em `src/**`, sempre guiado pelo backlog).
> Regra: **TDD SEMPRE parte de um item do `BACKLOG.md` e entrega uma suíte de testes (e, opcionalmente, código inicial) pronta para ser consolidada em Delivery.**

#### 5.2.1 Phase 1 — Seleção da Tarefa e BDD Scenarios

- Entradas:
  - [ ] `project/specs/roadmap/BACKLOG.md`
  - [ ] `project/specs/bdd/**/*.feature`
- Saídas:
  - [ ] `tests/bdd/test_*_steps.py` (arquivo de teste preparado/focado na tarefa)

#### 5.2.2 Phase 2 — Test Setup (RED)

- Entradas:
  - [ ] `project/specs/bdd/**/*.feature`
- Saídas:
  - [ ] `tests/bdd/test_*.py` com teste falhando (RED)

#### 5.2.3 Phase 3 — Minimal Implementation (GREEN - Testes)

- Entradas:
  - [ ] `tests/bdd/test_*.py`
- Saídas:
  - [ ] `tests/**/*.py` verdes para a tarefa selecionada (cobertura comportamental garantida pelo `forge_coder`).
  - Observação: durante `execution.tdd.*`, priorizar ajustes em testes e o mínimo de código em `src/**` necessário para validar o comportamento; a consolidação e refatoração maior em `src/**` acontece nas sessões de Delivery/Sprint, ainda com o `forge_coder` como executor principal.

> Revisor de processo ao final da fase 5 (Execution): `jorge_the_forge` (audita se Roadmap Planning + TDD seguiram o ForgeProcess, incluindo relação com BDD, backlog e limites de escopo do forge_coder entre Execution/TDD e Delivery).

### Handoff Execution → Delivery

- Critério para encerrar a Fase 5 (Execution) em um ciclo:
  - [ ] `project/specs/roadmap/ROADMAP.md` e `project/specs/roadmap/BACKLOG.md` existentes e aprovados (5.1 concluída).
  - [ ] Tarefas selecionadas do backlog cobertas por testes BDD/pytest verdes (`tests/bdd/**`) para o escopo deste ciclo (5.2.3 concluída para essas tarefas).
  - [ ] Revisão de processo da Fase 5 realizada por `jorge_the_forge`, confirmando aderência ao ForgeProcess e limites de escopo do `forge_coder` entre Execution/TDD e Delivery.
- Ao concluir Execution para o ciclo atual:
  - Atualizar estado neste arquivo:
    - [ ] `current_phase = delivery.sprint`
    - [ ] `last_completed_step = execution.tdd.phase_3_minimal_implementation`
    - [ ] `next_recommended_step = delivery.sprint.sprint_planning`
  - Orquestração:
    - [ ] Carregar/ativar `sprint_coach` e `forge_coder` para iniciar a Fase 6 (Sprint Planning e Session Implementation).

---

## 6. Fase Delivery — Sprint + Review

Referência: `process/delivery/PROCESS.yml`

### 6.1 Sprint (delivery.sprint)

Referência: `process/delivery/sprint/PROCESS.yml`

> Symbiota responsável por facilitar a fase (etapas 6.1.1–6.1.5): `sprint_coach`.
> Symbiota executor de código nas etapas de implementação/commit (6.1.3 e 6.1.5): `forge_coder`.

#### 6.1.1 Sprint Planning

- Entradas:
  - [ ] `project/specs/roadmap/BACKLOG.md`
- Saídas:
  - [ ] `project/sprints/sprint-N/planning.md`

#### 6.1.2 Session Mini-Planning

- Entradas:
  - [ ] `project/sprints/sprint-N/planning.md`
- Saídas:
  - [ ] `project/sprints/sprint-N/sessions/session-M.md`

#### 6.1.3 Session Implementation

> Symbiota executor de código na sessão: `forge_coder` (implementa features usando TDD, seguindo arquitetura ForgeBase).

- Entradas:
  - [ ] `project/sprints/sprint-N/sessions/session-M.md`
- Saídas:
  - [ ] `src/**/*.py`
  - [ ] `tests/**/*.py`

#### 6.1.4 Session Review

- Entradas:
  - [ ] `src/**/*.py`
  - [ ] `tests/**/*.py`
- Saídas:
  - [ ] `project/sprints/sprint-N/sessions/session-M.md` atualizado com resultado

#### 6.1.5 Session Commit

- Saídas:
  - [ ] `project/sprints/sprint-N/progress.md`
- Critério:
  - [ ] Se `sprint.has_remaining_sessions()` → repetir mini-planning/implementation/review/commit.
  - [ ] Senão → `session_complete` e Delivery chama Review.

### 6.2 Review (delivery.review)

Referência: `process/delivery/review/PROCESS.yml`

#### 6.2.1 Day 1 — bill-review (Technical)

- Entradas:
  - [ ] `src/**/*.py`
  - [ ] `tests/**/*.py`
  - [ ] `project/specs/bdd/**/*.feature`
- Saídas:
  - [ ] `project/sprints/sprint-N/review.md`

#### 6.2.2 Day 2 — Jorge the Forge (Process)

- Entradas:
  - [ ] `project/sprints/sprint-N/review.md`
  - [ ] `project/sprints/sprint-N/planning.md`
  - [ ] `project/sprints/sprint-N/progress.md`
- Saídas:
  - [ ] `project/sprints/sprint-N/jorge-process-review.md`

#### 6.2.3 Day 3 — Stakeholder Review & Deploy

- Entradas:
  - [ ] `project/sprints/sprint-N/review.md`
  - [ ] `project/sprints/sprint-N/jorge-process-review.md`
- Saídas:
  - [ ] `project/sprints/sprint-N/stakeholder-approval.md`
- Decisão:
  - [ ] Se `approved` e `!backlog.has_pending_items()` → `deployed`.
  - [ ] Se `needs_fixes` → volta a Sprint.
  - [ ] Se `needs_revision`/`rollback` → Execution precisa revisar (típico).
- Atualizar estado:
  - [ ] `current_phase = feedback` (quando `return_deployed`)
  - [ ] `last_completed_step = delivery.review.stakeholder_review`
  - [ ] `next_recommended_step = feedback.feedback_collect`

> Revisores ao final da fase 6 (Delivery):
> - `bill_review` — revisão técnica da sprint e do incremento entregue;
> - `jorge_the_forge` — revisão de processo da sprint (compliance com ForgeProcess).

#### 6.2.4 Demo Script por Sprint (focado em E2E)

- Antes ou durante a etapa de Review/Stakeholder Validation, o `forge_coder` deve:
  - [ ] Criar (ou atualizar) um script de demo específico da sprint em `examples/` (ex.: `examples/sprint1_demo.sh`, `examples/sprint2_demo.sh`),
        **apenas quando houver algo a demonstrar em termos de fluxo end-to-end** (por exemplo, integração com provider real, MCP, gateway externo).
  - [ ] Garantir que o script:
        - explique no início, via `echo`, o que será demonstrado;
        - use o runtime atual do projeto (via instalação local ou `PYTHONPATH`) **para chamar a CLI oficial do produto** (ex.: `forge-code-agent run ...`, `forge-code-agent stream ...`), em vez de invocar diretamente funções Python internas;
        - execute um cenário equivalente a pelo menos um teste `@e2e` (ou, na ausência de marcação explícita, um fluxo que dependa de integrações externas reais);
        - seja simples de rodar para o stakeholder (`./examples/sprintN_demo.sh`).
  - [ ] Em sprints que só entregam lógica interna/mocks (sem integrações externas), o uso de `examples/` é opcional; a validação pode ser feita exclusivamente via testes automatizados (`pytest`, BDD, etc.).
  - [ ] Referenciar o script de demo em `project/sprints/sprint-N/review.md` e em `project/sprints/sprint-N/stakeholder-approval.md` como parte das demos executadas, quando aplicável.

#### 6.2.5 Scripts de ValueTrack por Ciclo (CLI-first)

- Ao concluir um ValueTrack em nível de ciclo (por exemplo, execução via CLI, tools/files, observabilidade), o time deve:
  - [ ] Criar um script agregador em `examples/` (ex.: `examples/valuetrack_code_agent_execution.sh`) que:
        - utilize **somente a CLI oficial** para demonstrar, em sequência, todas as funcionalidades cobertas por aquele ValueTrack;
        - possa ser rodado pelo stakeholder como demo de “fechamento de ciclo” para aquele ValueTrack.
  - [ ] Atualizar o feedback de ciclo correspondente (`project/docs/feedback/cycle-XX.md`) mencionando esse script como referência principal de demo E2E do ValueTrack.

### Handoff Delivery → Feedback

- Critério para encerrar a Fase 6 (Delivery) em um ciclo:
  - [ ] `project/sprints/sprint-N/review.md` consolidado (bill-review técnico concluído).
  - [ ] `project/sprints/sprint-N/jorge-process-review.md` consolidado (review de processo concluído).
  - [ ] `project/sprints/sprint-N/stakeholder-approval.md` com decisão `approved`.
  - [ ] `!backlog.has_pending_items()` para o escopo definido do ciclo/sprint.
- Ao atingir esses critérios:
  - Confirmar as checkboxes de “Atualizar estado” na seção 6.2.3:
    - [ ] `current_phase = feedback`
    - [ ] `last_completed_step = delivery.review.stakeholder_review`
    - [ ] `next_recommended_step = feedback.feedback_collect`
  - Orquestração:
    - [ ] Encerrar a sprint corrente.
    - [ ] Carregar/ativar `jorge_the_forge` (ou agente equivalente) para conduzir a Fase 7 (Feedback), registrando métricas, aprendizados e decisões de próximo ciclo.

---

## 7. Fase Feedback — Reflexão e Próximos Ciclos

Referência: macro em `process/PROCESS.yml` (phases.feedback)

### 7.1 Coletar Feedback

- Entradas (exemplos):
  - [ ] Métricas operacionais (logs, observabilidade) — neste ciclo, centradas em testes/verdes e entregas de sprint.
  - [ ] KPIs de valor definidos na visão / tracks — para o MVP atual (execução básica via CLI + tools/files + resiliência).
- Saídas:
  - [ ] Registro de métricas e observações (`project/docs/feedback/cycle-01.md`)

### 7.2 Analisar Feedback

- Atividades:
  - [ ] Analisar dados, comparar com KPIs
  - [ ] Sugerir ajustes de visão, novos ValueTracks ou encerrar ciclo
  - [ ] Conduzir uma **revisão geral de ciclo** (liderada por `jorge_the_forge`), identificando melhorias de processo, gaps de artefatos e ajustes de papéis entre symbiotas.

### 7.3 Decisões de ciclo

- [ ] Decisão 1 — Visão precisa mudar?
  - [ ] Se **sim**:
    - [ ] `current_phase = mdd`
    - [ ] `next_recommended_step = mdd.01.concepcao_visao`
  - [ ] Se **não**:
    - [ ] Decisão 2 — Há mais ValueTracks a implementar?
      - [ ] Se “continuar”:
        - [ ] `current_phase = bdd`
        - [ ] `next_recommended_step = bdd.01.mapeamento_comportamentos`
      - [ ] Se "completo":
        - [ ] Antes de considerar o ciclo completo, verificar:
          - [ ] Para cada ValueTrack crítico que dependa de integrações externas (ex.: providers reais, MCPs, gateways), existe **pelo menos um cenário BDD marcado com `@e2e`** passando em ambiente controlado.
          - [ ] Os testes de integração correspondentes (`pytest -m e2e` ou suíte equivalente) foram executados com sucesso pelo menos uma vez neste ciclo.
          - [ ] Qualquer limitação conhecida (ex.: provider ainda simulado) está explicitamente registrada em `project/docs/feedback/cycle-XX.md` e **não** é mascarada como entrega completa.
        - [ ] **E2E CLI-First Validation** (obrigatório):
          - [ ] Estrutura `tests/e2e/cycle-XX/` criada com scripts para todos os VTs e STs do ciclo.
          - [ ] Stakeholder executou `./tests/e2e/cycle-XX/run-all.sh` e validou o resultado.
          - [ ] Todos os tracks passaram (0 falhas).
          - [ ] Logs de evidência salvos em `tests/e2e/cycle-XX/evidence/`.
          - [ ] Referência: `process/delivery/e2e/E2E_VALIDATION_PROCESS.md`
        - [ ] Somente após esses critérios, marcar `end_ciclo_completo`.
        - [ ] Consolidar as melhorias de processo identificadas na revisão geral do ciclo em `project/recommendations.md`, com:
          - `owner_symbiota` explícito,
          - `status` inicial (`pending`),
          - notas sobre a discussão/validação com stakeholders.
        - [ ] Garantir que o `sprint_coach` leia `project/recommendations.md` no planejamento da próxima sprint e acione as recomendações pertinentes.

> Revisão e registro de aprendizados ao final da fase 7 (Feedback):
> - `jorge_the_forge` é responsável por consolidar aprendizados de processo e atualizar artefatos de feedback;
> - `bill_review` pode ser invocado para revisar implicações técnicas identificadas no feedback, mas o registro formal de aprendizados é conduzido por Jorge.

---

## 8. Regras específicas para symbiotas (resumo rápido)

- `forge_coder`:
  - [ ] Nunca iniciar trabalho em TDD se `project/specs/roadmap/BACKLOG.md` não existir.
  - [ ] Em caso de ausência, registrar no contexto: “É necessário rodar Roadmap Planning antes do TDD” e solicitar intervenção de `roadmap_coach`.
  - [ ] Durante `execution.tdd.*`, tratar `src/**` como read-only sempre que possível, focando em criar/alterar `tests/**` (step definitions e testes) e `project/specs/bdd/**`.
  - [ ] Durante `delivery.sprint.*`, implementar e commitar código em `src/**` seguindo TDD e a arquitetura definida em Execution.
  - [ ] Trabalhar sempre em cima de itens do backlog definidos e aprovados; não inventar escopo novo durante a sprint.
- `roadmap_coach`:
  - [ ] Sempre produzir pelo menos: `TECH_STACK.md`, `HLD.md`, `LLD.md`, `ROADMAP.md`, `BACKLOG.md`.
- `execution_coach`:
  - [ ] Garantir que o fluxo BDD → Roadmap Planning → TDD seja respeitado, sem pular etapas.
  - [ ] Manter `current_phase` e `next_recommended_step` coerentes ao transitar entre `execution.roadmap_planning`, `execution.tdd` e `delivery.sprint`.
- `mark_arc`:
  - [ ] Conduzir a análise arquitetural nas etapas 00 e 01 de Roadmap Planning, alinhando decisões à arquitetura ForgeBase.
  - [ ] Apoiar a criação de TECH_STACK, ADRs, HLD e LLD coerentes com as regras do ForgeBase.
- `bdd_coach`:
  - [ ] Garantir que **todo ValueTrack** relevante do MDD está coberto por features e mapeado em `tracks.yml`.
- `sprint_coach`:
  - [ ] Facilitar Sprint Planning e Session Mini-Planning, mantendo `planning.md`, `sessions/*.md` e `progress.md` atualizados.
  - [ ] Coordenar o trabalho do `forge_coder` dentro de cada sessão de sprint.
- `delivery_coach`:
  - [ ] Coordenar a fase de Delivery como um todo, garantindo que sprint e review sigam o processo descrito em `process/delivery/`.
  - [ ] Orquestrar a execução de `bill_review` e `jorge_the_forge` no final de cada sprint.
- `bill_review` e `jorge_the_forge`:
  - [ ] Usar este arquivo como referência de “fluxo ideal” ao avaliar compliance.

Este arquivo deve ser atualizado incrementalmente durante a execução
para refletir o estado real do projeto e servir de **roteiro único**
para agentes humanos e symbiotas.
