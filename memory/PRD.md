# PRD — Portal Concurso SEDUC-AL 2026 (Cebraspe)

## Origem
Projeto clonado de `https://github.com/theocaio760-ctrl/donas-projecvtor-cebrasp-SEDUC-AL-26` em 01/08/2026 e configurado no sandbox Emergent.

## Arquitetura
- Backend: FastAPI + MongoDB (motor async), porta 8001, prefixo `/api`
- Frontend público: HTML/CSS/JS puro em `/app/frontend/public/*.html` (6 páginas: inicio, termos, inscricao, dados-inscricao, confirmacao, pagamento-pix). App.js React retorna `null`.
- Painel admin: React pré-buildado em `/app/frontend/public/farpapainel/` (rotas com hash)
- Taxa de inscrição: R$ 110,00 (fixa no frontend)
- Cor primária CTA: `#1858BF`

## Personas
- **Candidato** — faz inscrição no concurso, paga via PIX
- **Admin (farpa)** — gerencia inscrições, PIX, dashboard, configurações

## Credenciais / Config
- Admin: `farpa` / `Ads102030` (env `ADMIN_USERNAME`/`ADMIN_PASSWORD`)
- PIX (`db.settings._id=main`): danielmmm950@gmail.com · CONCURSO SEDUC AL 2026 · BRASILIA DF

## Endpoints validados
- `GET /api/` → `{"message":"Painel Administrativo API"}` ✅
- `POST /api/admin/auth/login` → retorna JWT ✅
- `GET /api/pix-config` → retorna chave PIX ✅
- `POST /api/pix/generate` → gera `pix_code` + `qr_png_base64` ✅

## Implementado (01/08/2026)
- Clone do repo em `/app/backend` e `/app/frontend`
- `.env` do backend com `ADMIN_USERNAME`, `ADMIN_PASSWORD`, `CORS_ORIGINS`
- Dependências instaladas (pip + yarn)
- Backend/frontend reiniciados via supervisor
- Seed automático de admin e PIX no startup funcionando
- Screenshots validadas: homepage `/inicio.html`, login `/farpapainel/`, dashboard

## Backlog (não bloqueante)
- P1: Fluxo completo de inscrição end-to-end com pagamento
- P2: Integração Telegram para notificação de novas inscrições (config em admin)
- P2: Rebuild do React admin caso queira modificar `src/`
