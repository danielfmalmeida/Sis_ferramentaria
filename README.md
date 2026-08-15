# ToolControl

Sistema de controle de empréstimo de ferramentas com autenticação biométrica e checklist digital de estoque mínimo, substituindo o processo atual em papel e planilhas Excel.

> 📋 **Status:** em planejamento — arquitetura e requisitos definidos, desenvolvimento ainda não iniciado (veja o [roadmap](#roadmap)).

---

## O problema

Hoje o controle de ferramentas e a conferência de estoque de consumíveis são feitos em fichas impressas e planilhas Excel, o que causa:

- Nenhuma rastreabilidade de quem está com qual ferramenta no momento
- Assinaturas em papel fáceis de perder, forjar ou simplesmente não preencher
- Divergência de inventário só percebida quando o item já sumiu
- Alertas de estoque mínimo feitos manualmente, sem histórico consultável

## A solução

Dois fluxos digitais compartilhando a mesma base de dados:

- **Empréstimo → devolução → transferência** de ferramentas, autenticado por biometria digital
- **Checklist de estoque mínimo** com cálculo automático de divergência, impressão direto do app e alerta por e-mail automático

Composto por um app desktop para o dia a dia do almoxarifado, um app web para gestores (dashboards, relatórios, auditoria) e um backend central que garante que os dois sempre mostrem os mesmos dados em tempo real.

## Stack

| Camada | Tecnologia | Observação |
|---|---|---|
| Backend / API | Python + FastAPI | REST + JWT, único ponto de verdade dos dados |
| Banco de dados | PostgreSQL | Suporta bem 300 usuários / 5.000 itens sem esforço |
| App Desktop | Python + PySide6 (Qt) | Roda na estação do almoxarifado, integra leitor biométrico via USB |
| App Web | React + TypeScript + Vite + TailwindCSS | Consumido por gestores/controladores |
| Geração de PDF | WeasyPrint / ReportLab | Template único de checklist e relatórios |
| E-mail | SMTP / serviço transacional | Disparo automático de alerta de divergência |

## Documentação completa

Este README traz a visão geral. Os detalhes técnicos estão em `/docs`:

- [`docs/01-requisitos.md`](docs/01-requisitos.md) — requisitos funcionais e não funcionais
- [`docs/02-arquitetura.md`](docs/02-arquitetura.md) — arquitetura, modelagem de dados, integração biométrica
- `docs/03-api-contratos.md` — contratos de endpoints da API *(a criar)*
- `docs/04-plano-testes.md` — estratégia de testes *(a criar)*

## Roadmap

Desenvolvimento planejado em sprints de 2 semanas:

| Sprint | Entrega |
|---|---|
| 0 | Setup dos repositórios, ambiente, banco de dados, CI básico |
| 1 | Backend: modelagem de dados + CRUD de pessoas/ferramentas/setores |
| 2 | Backend: fluxo de empréstimo/devolução (login simples, sem biometria) |
| 3 | Integração do leitor biométrico (enrolamento + verificação) |
| 4 | App desktop completo: empréstimo/devolução/transferência autenticados |
| 5 | App web: dashboard + relatórios + cadastro |
| 6 | Auditoria, alertas de atraso, exportação de relatórios |
| 7 | Módulo de checklist: catálogo, execução, cálculo de divergência |
| 8 | Checklist: impressão em PDF, e-mail automático de alerta |
| 9 | Checklist: relatório de divergência e histórico |
| 10 | Testes, hardening de segurança, documentação final, piloto |

## Estrutura do projeto

```
toolcontrol/
├── README.md
├── docs/
│   ├── 01-requisitos.md
│   ├── 02-arquitetura.md
│   ├── 03-api-contratos.md
│   └── 04-plano-testes.md
├── backend/            # FastAPI
│   └── seed/
│       └── catalogo_pastilhas_seed.csv
├── desktop/            # PySide6
└── frontend/           # React + Vite + Tailwind
```
