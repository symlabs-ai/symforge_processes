# BDD — SUMMARY_FOR_AGENTS

Resumo rápido para LLMs e symbiotas atuando na fase de
**Behavior Driven Development (BDD)**.

## 1. Visão Rápida

- Fase que transforma **valor validado (MDD)** em **especificação executável**.
- Trabalha com **features Gherkin** em PT‑BR e **tracks.yml**.
- Saída alimenta Execution (Roadmap + TDD).

## 2. Etapas Principais (IDs)

Ver detalhes em `process/bdd/BDD_PROCESS.md` e `process/docs/PROCESS_IDS.md`.

- `bdd.01.mapeamento_comportamentos` — Mapeamento de Comportamentos  
  - De `docs/visao.md` + `docs/aprovacao_mvp.md` → `specs/bdd/drafts/behavior_mapping.md`.
- `bdd.02.features_gherkin` — Escrita de Features Gherkin  
  - De behavior mapping → `specs/bdd/**/*.feature`.
- `bdd.03.organizacao_tagging` — Organização e Tagging  
  - Estrutura `specs/bdd/` + tags (@ci-fast/@ci-int/@e2e).
- `bdd.04.tracks_yml` — Criação de tracks.yml  
  - Mapeia ValueTracks ↔ features ↔ métricas.
- `bdd.05.skeleton_automacao` — Skeleton de Automação  
  - Cria `tests/bdd/test_*_steps.py`, `tests/bdd/conftest.py`, `pytest.ini`.
- `bdd.06.handoff_roadmap` — Handoff para Roadmap Planning  
  - Gera `specs/bdd/HANDOFF_BDD.md` e prepara entrada para Execution.

## 3. Artefatos Principais

- `specs/bdd/drafts/behavior_mapping.md`
- `specs/bdd/**/*.feature`
- `specs/bdd/tracks.yml`
- `specs/bdd/README.md`
- `specs/bdd/HANDOFF_BDD.md`
- `tests/bdd/test_*_steps.py`
- `tests/bdd/conftest.py`
- `pytest.ini`

## 4. Symbiotas Relevantes

- `bdd_coach`  
  - Deriva comportamentos, escreve/organiza features, cria tracks.yml, prepara skeleton de automação.
- `tdd_coder` / `test_writer`  
  - Usam features BDD para construir suíte de testes na fase Execution (TDD).
- `jorge_forge`  
  - Audita ao final da fase se especificações e rastreabilidade seguem o ForgeProcess.

