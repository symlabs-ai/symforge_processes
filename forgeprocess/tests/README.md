# Tests — ForgeProcess

Este diretorio contem a estrutura de testes do ForgeProcess.

```
tests/
├── README.md          # Este arquivo
├── bdd/               # Step definitions pytest-bdd (automatizados)
└── e2e/               # Validacao E2E CLI-first (stakeholder)
```

---

## Visao Geral

O ForgeProcess adota uma **estrategia de testes em camadas**:

```
┌─────────────────────────────────────────────────────────────┐
│                    PIRAMIDE DE TESTES                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│         ┌─────────────────┐                                 │
│         │   E2E CLI-First │  ◄── Stakeholder executa        │
│         │   (tests/e2e/)  │      Scripts shell + CLI real   │
│         └────────┬────────┘                                 │
│                  │                                          │
│         ┌────────┴────────┐                                 │
│         │  BDD/Integracao │  ◄── pytest -m e2e              │
│         │  (tests/bdd/)   │      Cenarios Gherkin           │
│         └────────┬────────┘                                 │
│                  │                                          │
│    ┌─────────────┴─────────────┐                            │
│    │      Testes Unitarios     │  ◄── pytest (fast)         │
│    │      (tests/unit/)        │      Mocks e Fakes         │
│    └───────────────────────────┘                            │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## E2E CLI-First (`tests/e2e/`)

### O que e?

Validacao **end-to-end** onde o **stakeholder executa scripts shell** que testam a CLI do produto com **integracoes reais** (nao mocks).

### Por que?

- **Prova de entrega**: Stakeholder ve o sistema funcionando de verdade
- **CLI-first**: Toda funcionalidade e validavel via linha de comando
- **Integracoes reais**: Testa com APIs e servicos de terceiros reais
- **Auditavel**: Logs de evidencia sao gerados automaticamente

### Estrutura

```
tests/e2e/
├── shared/                  # Scripts utilitarios reutilizaveis
│   ├── colors.sh            # Cores para output do terminal
│   ├── setup.sh             # Configuracao de ambiente
│   ├── teardown.sh          # Limpeza pos-testes
│   └── assertions.sh        # Funcoes de assercao
│
├── template/                # Templates para novos ciclos
│   ├── README.template.md
│   ├── run-all.template.sh
│   ├── track-run.template.sh
│   └── feature.template.sh
│
└── cycle-XX/                # Testes por ciclo
    ├── README.md            # Instrucoes para stakeholder
    ├── run-all.sh           # Executa TODOS os tracks
    ├── evidence/            # Logs de execucao (auto-gerados)
    │
    ├── vt-01-checkout/      # ValueTrack
    │   ├── run.sh
    │   ├── 01-checkout-basico.sh
    │   └── 02-checkout-cupom.sh
    │
    └── st-01-observability/ # SupportTrack
        ├── run.sh
        └── 01-logs-structured.sh
```

### Como executar

```bash
# Configurar credenciais (uma vez)
cp .env.e2e.example .env.e2e
# Editar .env.e2e com credenciais reais

# Executar todos os testes do ciclo
./tests/e2e/cycle-01/run-all.sh

# Executar track especifico
./tests/e2e/cycle-01/vt-01-checkout/run.sh

# Executar feature especifica
./tests/e2e/cycle-01/vt-01-checkout/01-checkout-basico.sh
```

### Output esperado

```
═══════════════════════════════════════════════════════
  E2E VALIDATION - CICLO 01
  Data: 2025-12-09 15:30:00
═══════════════════════════════════════════════════════

▶ Executando: vt-01-checkout
  Feature: Checkout basico
  ✓ PASS: Comando deve executar com sucesso
  ✓ PASS: Status deve ser approved
✓ vt-01-checkout: PASSED

▶ Executando: st-01-observability
  Feature: Logs estruturados
  ✓ PASS: Log deve conter timestamp
✓ st-01-observability: PASSED

═══════════════════════════════════════════════════════
  RESULTADO FINAL - CICLO 01
  Tracks PASSED: 2
  Tracks FAILED: 0
  Evidencia: evidence/run-all_20251209_153000.log
═══════════════════════════════════════════════════════
```

### Quando usar

| Momento | Acao |
|---------|------|
| **Durante Sprint** | Criar scripts E2E para features implementadas |
| **Antes do Review** | Testar `./run-all.sh` localmente |
| **No Sprint Review** | Stakeholder executa e valida |
| **Conclusao de Ciclo** | Gate obrigatorio — todos os tracks devem passar |

---

## BDD (`tests/bdd/`)

### O que e?

Step definitions **pytest-bdd** que implementam os cenarios Gherkin definidos em `project/specs/bdd/`.

### Estrutura

```
tests/bdd/
├── conftest.py              # Fixtures compartilhadas
├── test_*_steps.py          # Step definitions por feature
└── cassettes/               # Gravacoes VCR.py para APIs
```

### Como executar

```bash
# Todos os testes BDD
pytest tests/bdd/ -v

# Apenas testes rapidos (mocks)
pytest tests/bdd/ -m "ci_fast"

# Apenas testes de integracao
pytest tests/bdd/ -m "ci_int"

# Apenas testes E2E (APIs reais)
pytest tests/bdd/ -m "e2e"
```

### Tags disponiveis

| Tag | Descricao | Velocidade |
|-----|-----------|------------|
| `@ci-fast` | Mocks, sem dependencias externas | < 5s |
| `@ci-int` | Servicos internos (Docker, Redis) | < 30s |
| `@e2e` | APIs externas reais | Variavel |

---

## Diferenca: `tests/bdd/` vs `tests/e2e/`

| Aspecto | `tests/bdd/` | `tests/e2e/` |
|---------|--------------|--------------|
| **Executor** | pytest (automatizado) | Stakeholder (manual) |
| **Linguagem** | Python + pytest-bdd | Shell scripts |
| **Integracao** | Mocks ou VCR.py | APIs reais |
| **Proposito** | CI/CD, regressao | Validacao de ciclo |
| **Output** | JUnit XML | Logs de evidencia |
| **Quando** | A cada commit | Final do ciclo |

**Ambos sao complementares**:
- `tests/bdd/` garante que o codigo funciona tecnicamente
- `tests/e2e/` garante que o produto funciona para o stakeholder

---

## Referencias

- Processo E2E: `process/delivery/e2e/E2E_VALIDATION_PROCESS.md`
- guia de implementacao E2E:  `process/guides/e2e_test_writing.md`
- Templates: `tests/e2e/template/`
- Guia de Testes: `docs/integrations/forgebase_guides/usuarios/guia-de-testes.md`
