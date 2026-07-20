# Colin QA — Dashboard

Dashboard de acompanhamento dos testes de qualidade do **Colin**, assistente agrícola com IA da Triskin. Consolida os resultados de todas as fazendas, níveis de avaliação e bugs conhecidos em uma única interface.

## O que é o Colin

Colin é um assistente de gestão rural que atende via chat (WhatsApp e web). Ele responde perguntas sobre safra, mecanização, custos, clima e operação das fazendas, consultando dados reais de cada propriedade em tempo real.

## Fazendas cobertas

| Fazenda | Casos | Aprovação |
|---|---|---|
| Jaçanã | 94 | 83% |
| WS | 88 | 85% |
| Apoloni | 79 | 78% |
| Piccini | 81 | 58% |

## Framework de testes — 3 Níveis

Os testes seguem um framework de três níveis de complexidade crescente:

| Nível | Nome | O que avalia |
|---|---|---|
| **N1** | Consulta | Colin consegue localizar e apresentar informações corretas? |
| **N2** | Contexto Operacional | Colin consegue resumir e contextualizar a operação? |
| **N3** | Diagnóstico Operacional | Colin explica causas, identifica problemas e antecipa riscos? |

Cada nível contém 10 perguntas de mecanização por fazenda, testadas com foco no mês corrente. Uma bateria extra de 10 perguntas mensais adicionais (**N1 Extra**) foi executada para ampliar a cobertura do N1 com ângulos diferentes.

## Suites de teste

Além dos níveis de mecanização, o dashboard cobre:

- **Casos Críticos** — perguntas de alto impacto que não podem falhar
- **Perguntas Fundamentais** — safra, produtividade, custos, receita
- **Continuidade de Conversa** — comportamento em sessões multi-turn
- **Sinalização de Ausência** — Colin sinaliza ausência sem inventar dados
- **N1 Extra — Foco Mensal** — 10 perguntas adicionais de N1 com ângulos diferentes (consumo, disponibilidade, pico de atividade, manutenção corretiva)
- **Regressão GPT** — comparativo entre versões de modelo (GPT-5.4 → 4.1-mini)
- **Rentabilidade por Talhão** — análise por talhão específico
- **Segurança** — rejeição de prompts fora do escopo agro

## Como ler o dashboard

### Aba Fazendas
Visão geral por propriedade com score geral, breakdown por suite e o stepper de progresso N1 → N2 → N3.

### Aba Níveis
Perguntas dos 3 níveis com status de cobertura por fazenda (`confirmado` / `parcial` / `sem-dado`).

### Aba Bugs
Bugs conhecidos com severidade (`high` / `med`) e descrição do comportamento observado.

### Aba Cobertura
Matriz de views de dados por fazenda — indica se aquela fonte existe e está funcional para cada propriedade.

## Status atual

- **Última execução:** 20/07/2026 às 15:20
- **Modelo testado:** GPT-4.1-mini (branch Michael)
- **N1:** Validado (20 perguntas por fazenda — original + extra)
- **N2:** Em progresso
- **N3:** Em validação
- **Cobertura por período:** Mapeada em 20/07 — regressão detectada em Jaçanã (produtividade e alertas)

## Mapeamento de cobertura por período (20/07/2026)

| Dimensão | Jaçanã | WS | Apoloni | Piccini |
|---|---|---|---|---|
| Produtividade | ⚠️ sem-dado (todos os anos) | ✅ 2023–2025 | ⚠️ só 2024 | ❌ sem dado |
| Custo | ✅ 2023–2025 | ✅ 2023–2025 | ⚠️ 2024–2025 (2026 timeout) | ❌ sem dado |
| Vendas / Receita | ✅ 2022, 2024–2026 | ✅ todos | ✅ 2023–2025 | ⚠️ parcial |
| Plantação | ✅ (gap 2024) | ✅ 2023–2026 | ⚠️ 2022, 2025–2026 | ⚠️ só 2023 |
| Aplicações | ⚠️ só 2025 | ⚠️ só 2025 | ✅ 2024–2025 | ❌ sem dado |
| Máquinas / Frota | ✅ | ✅ | ✅ | ✅ |
| Alertas | ⚠️ jul/26 sem retorno | ✅ | ✅ | ✅ |

> ⚠️ **Regressão JAC:** em 17/07, produtividade 2024 e 2025 estavam ok. Em 20/07, todos os anos falharam — provável impacto do problema de banco reportado.

## Bugs de alta prioridade

| ID | Descrição |
|---|---|
| BUG-01 | Contaminação de contexto em sessões multi-turn |
| BUG-02 | Saldo operacional retorna safra errada (regressão pós 03/07) |
| BUG-03 | Lista de máquinas truncada silenciosamente — Apoloni |
| BUG-08 | Inconsistência de produtividade Soja 2025 — Jaçanã |
| BUG-11 | JAC N1-10 — Query de manutenção trava acima de 300s |
| BUG-12 | Queries de agregação mensal lentas na WS e Apoloni (50–208s) |
| BUG-13 | **Regressão de cobertura** — JAC produtividade (todos os anos) e alertas jul/26 sem retorno |

## Visualizar

Abra o `dashboard.html` diretamente no navegador, ou ative o **GitHub Pages** em:

> Settings → Pages → Source: `main` / `/ (root)` → Save

---

*Desenvolvido pela equipe de QA — Triskin · Colin Project*
