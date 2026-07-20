# Colin QA — Dashboard

Dashboard de acompanhamento dos testes de qualidade do **Colin**, assistente agrícola com IA da Triskin. Consolida os resultados de todas as fazendas, níveis de avaliação e bugs conhecidos em uma única interface.

## O que é o Colin

Colin é um assistente de gestão rural que atende via chat (WhatsApp e web). Ele responde perguntas sobre safra, mecanização, custos, clima e operação das fazendas, consultando dados reais de cada propriedade em tempo real.

## Fazendas cobertas

| Fazenda | Casos | Aprovação |
|---|---|---|
| Jaçanã | 84 | 87% |
| WS | 78 | 88% |
| Apoloni | 69 | 81% |
| Piccini | 71 | 72% |

## Framework de testes — 3 Níveis

Os testes seguem um framework de três níveis de complexidade crescente:

| Nível | Nome | O que avalia |
|---|---|---|
| **N1** | Consulta | Colin consegue localizar e apresentar informações corretas? |
| **N2** | Contexto Operacional | Colin consegue resumir e contextualizar a operação? |
| **N3** | Diagnóstico Operacional | Colin explica causas, identifica problemas e antecipa riscos? |

Cada nível contém 10 perguntas de mecanização por fazenda, testadas com foco no mês corrente.

## Suites de teste

Além dos níveis de mecanização, o dashboard cobre:

- **Casos Críticos** — perguntas de alto impacto que não podem falhar
- **Perguntas Fundamentais** — safra, produtividade, custos, receita
- **Continuidade de Conversa** — comportamento em sessões multi-turn
- **Sinalização de Ausência** — Colin sinaliza ausência sem inventar dados
- **Regressão GPT** — comparativo entre versões de modelo (GPT-5.4 → 4.1)
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

- **Última execução:** 17/07/2026 às 10:50
- **N1:** Validado
- **N2:** Em progresso
- **N3:** Em validação

## Bugs de alta prioridade

| ID | Descrição |
|---|---|
| BUG-01 | Contaminação de contexto em sessões multi-turn |
| BUG-02 | Saldo operacional retorna safra errada (regressão pós 03/07) |
| BUG-03 | Lista de máquinas truncada silenciosamente — Apoloni |
| BUG-08 | Inconsistência de produtividade Soja 2025 — Jaçanã |

## Visualizar

Abra o `dashboard.html` diretamente no navegador, ou ative o **GitHub Pages** em:

> Settings → Pages → Source: `main` / `/ (root)` → Save

---

*Desenvolvido pela equipe de QA — Triskin · Colin Project*
