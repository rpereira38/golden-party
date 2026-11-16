# Golden Party — Matilde & Rúben

Frontend: GitHub Pages · Backend: Google Apps Script · Dados: Google Sheets · Ficheiros: Google Drive.

## Estado
Fase 1 (backend): registo, upload resumável, gostos, estado da competição, galeria/ranking, admin básico. Ver `Code.gs`.
Fases 2–5: frontend convidados, painel admin, exportações, QR/partilha, revelação do vencedor.

## Instalar backend (fase 1)
1. Copiar `Code.gs` para o projeto Apps Script (substitui o ficheiro de teste) e usar o `appsscript.json` fornecido.
2. Preencher IDs em `setupProperties()`, executar, apagar os IDs do código. Idem para `setAdminPassword()`.
3. Nova implantação da Aplicação Web (executar como proprietário; acesso: qualquer pessoa) e atualizar o URL no frontend.
4. Testes locais: `node tests/logic.test.js`.

## Fase 2 (frontend)
- `index.html` — app dos convidados (registo, upload com otimização WebP no browser, galeria masonry, gostos, ranking, vencedor).
- `admin.html` — admin mínimo (login, painel, datas da competição). Não está ligada a partir da app pública.
Publicar ambos na raiz do repositório (GitHub Pages).

## Fase 3
- Backend 1.1.0-fase3: pedidos de remoção, admin (participantes, fotografias, remoções, notificações, atividade, armazenamento, exportações CSV/ZIP, libertar nome).
- Nova folha `Removals` — criada ao executar `ensureSchema()` uma vez no editor.
- `admin.html` completo; `index.html` com botão Partilhar e pedido de remoção (⚑).
- Remoção é sempre lógica e reversível: nenhum ficheiro é apagado do Drive.

## Fase 4
- Backend 1.2.0-fase4: cache de 20 s para galeria/estado/configuração (invalidada em cada escrita), `toggleLike` sem releituras dentro do bloqueio, espera de bloqueio de 25 s.
- Frontend: revelação do vencedor com confetti (respeita `prefers-reduced-motion`), contraste AA, foco visível, `aria-live`, rótulos, repetição automática se o servidor estiver ocupado, política CSP e `no-referrer`.
- Testes: `node tests/logic.test.js`, `node tests/like.test.js` (locais/simulados) e `tests/load-test.js` (ensaio real, ver cabeçalho do ficheiro).
