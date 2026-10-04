# Logistics Control Portal

🇧🇷 [Português](#português) · 🇺🇸 [English](#english)

> Vitrine pública do projeto. O código real é privado e usa dados internos de uma empresa de transporte; aqui ficam a visão geral, a arquitetura e as decisões de design.
>
> Public showcase. The production code is private and uses a transport company's internal data; this repo documents the overview, architecture and design decisions.

---

## Português

Portal interno que **substituiu o Notion** no controle do fluxo de cargas de um Centro de Serviço Compartilhado (CSC) de transporte rodoviário.

### Principais recursos

- **Fluxo paralelo:** GR (gerenciamento de risco) e Cadastro processam a carga ao mesmo tempo; um nunca bloqueia o outro.
- **Status calculado:** "Emissão liberada" é derivado automaticamente por *trigger* no banco quando as duas áreas finalizam — nunca editável à mão.
- **Painel em tempo real** (Supabase Realtime): KPIs, fluxo por etapa e atividade recente.
- **Permissões multi-setor** com RLS e regras de gravação por coluna ("baldes" por área).
- **Importação de tabela de frete** a partir de Excel, com prévia, cálculo de impostos e sinalização de rotas removidas/novas.
- **Robô de lançamento automático** (userscript) que duplica cargas no sistema do cliente, valida campos e pausa pedindo ajuda quando algo falta.
- **Auditoria de evidências com IA:** lê anexos (SM, teste de rastreador, prints) e confere contra a regra de cada cliente. Visível só ao administrador.
- **Follow-up por WhatsApp** com n8n + WAHA.

### Stack

Vite · React · TypeScript · Tailwind v4 · React Router · Supabase (Postgres, Auth, RLS, Realtime, Storage) · Vercel (frontend + serverless) · Gemini API · n8n · Docker.

### Decisões de design

- Tema escuro único; componentes próprios (`Select` em portal, caixa de erro padrão).
- Limite do plano gratuito da Vercel (12 functions) resolvido roteando ações por um campo `action` numa função só.
- Migrações SQL numeradas e idempotentes (`catchup`).
- Robôs falham de forma segura: preferem não salvar a salvar um valor errado.

---

## English

Internal portal that **replaced Notion** for freight-load control in a road-transport Shared Service Center.

### Key features

- **Parallel workflow:** risk management (GR) and registration work on a load simultaneously; neither blocks the other.
- **Computed status:** "Ready to invoice" is derived by a database trigger once both finish — never manually editable.
- **Real-time dashboard** (Supabase Realtime): KPIs, per-stage flow, recent activity.
- **Multi-department permissions** using RLS and per-column write rules.
- **Freight-table import** from Excel with preview, tax calculation and flags for removed/new routes.
- **Auto-creation bot** (userscript) that duplicates loads in the client system, validates fields and pauses for human help when something is missing.
- **AI-assisted evidence audit:** reads attachments (tracking proof, tracker test, screenshots) and checks them against each customer's rules. Admin-only.
- **WhatsApp follow-up** via n8n + WAHA.

### Stack

Vite · React · TypeScript · Tailwind v4 · React Router · Supabase (Postgres, Auth, RLS, Realtime, Storage) · Vercel · Gemini API · n8n · Docker.

### Design decisions

- Single dark theme with in-house components.
- Vercel Hobby 12-function limit solved by routing actions through one function.
- Numbered, idempotent SQL migrations.
- Bots fail safe: they prefer not saving over saving a wrong value.

---

Author · Autor: [@vicentsna](https://github.com/vicentsna)
