# Projeto Legado Mestre Moura

Documentação do projeto: contexto, decisões, estrutura e como operar.

## O que é isso

Uma campanha pra ajudar o Mestre Ednaldo Moura ("Seu Moura") — Faixa Preta 4º Grau de Jiu-Jitsu, Comendador da Comunidade e Brasão de Maringá — a competir no **Campeonato Master do Rio de Janeiro em dezembro de 2026**.

**É uma surpresa.** O Seu Moura ainda não sabe que este projeto existe. A ideia é validar a ideia com ele primeiro (mostrando esta página), e só depois — se ele topar — sair captando apoio de empresas de verdade.

## Decisões importantes (não mude sem repensar o porquê)

- **Sem instituto/associação por enquanto.** Captação via PIX-CPF informal, tratada como "colaboração pessoal", não patrocínio corporativo formal. Sem nota fiscal nessa fase.
- **Nome do programa: "Círculo de Apoio"**, não "Empresas Fundadoras" — decisão deliberada porque "Empresas Fundadoras" implica contrapartida formal (nota fiscal) que ainda não conseguimos emitir. Ver commit `f2c5421` e histórico de conversa pra contexto completo.
- **Nomes de empresas-alvo não aparecem na página pública** — só os setores (construção, saúde, cooperativas, etc.). Isso evita expor empresas que ainda não foram contatadas como se já tivessem confirmado apoio.
- **Aberto a virar Instituto Seu Moura no futuro**, mas só depois do Rio — ver seção "E depois do Rio?" no site.
- **Sigilo até dezembro.** O link não deve ser divulgado além de quem recebe diretamente.

## Status atual

- Site no ar, conteúdo completo (história, trajetória, títulos, galeria, missão, orçamento, Círculo de Apoio).
- **Primeiro apoiador confirmado: JPX Digital Tecnologia Ltda.**
- 30 empresas-alvo mapeadas (`materiais/empresas.csv`), nenhuma contatada ainda (exceto JPX Digital).
- Media Kit, roteiro de vídeo, Kit WhatsApp, apresentação de slides — todos prontos.
- Vídeo final (edição) e abordagem às empresas: **ainda não iniciados**, aguardando o Seu Moura topar a ideia.

## URLs ao vivo

- https://seumoura.jpxdigital.com.br (principal)
- https://projeto-moura.jpxdigitaltec.workers.dev (mesmo conteúdo, domínio alternativo)

Contato usado no botão "Chamar no WhatsApp": **(18) 93085-2246**

## Estrutura do repositório

```
index.html              → a landing page (site principal)
img/                     → logo e foto do Seu Moura
robots.txt               → bloqueia indexação por buscadores
wrangler.jsonc           → configuração de deploy (Cloudflare Workers)
.assetsignore            → arquivos excluídos do deploy (.git, .wrangler, etc.)
materiais/
  media-kit.md           → Media Kit completo em texto (11 páginas)
  media-kit.html          → mesmo conteúdo, formatado, pronto pra exportar em PDF (Ctrl+P no navegador)
  apresentacao-slides.md  → texto dos 10 slides + script de abordagem comercial
  apresentacao.html       → os 10 slides navegáveis/exportáveis em HTML
  roteiro-video.md        → roteiro do vídeo de 1 minuto (aproveitando acervo do Instagram)
  kit-whatsapp.md         → PDF de 2 páginas pra envio rápido no WhatsApp
  empresas.csv            → planilha das 30 empresas-alvo, com gatilho comercial de cada uma
```

## Como publicar mudanças

O deploy **não** depende do GitHub — é direto via Cloudflare, usando o `wrangler` autenticado nesta máquina (conta `jpxdigitaltec@gmail.com`):

```bash
cd /home/petruzz/projeto-moura
wrangler deploy
```

Isso publica instantaneamente nas duas URLs (workers.dev + domínio customizado). O `git push` é só pra manter histórico no GitHub (`jpetroniom/projeto-moura`, repositório público) — não afeta o que está no ar.

```bash
git add <arquivos>
git commit -m "mensagem"
git push origin main
```

## Deploy — detalhes técnicos

- Hospedado como Cloudflare Worker com static assets (`assets.directory: "."` no `wrangler.jsonc`).
- Domínio customizado `seumoura.jpxdigital.com.br` configurado via `routes` no `wrangler.jsonc` — está na mesma conta Cloudflare que gerencia `jpxdigital.com.br`, então o DNS foi criado automaticamente, sem mexer no site principal (`jpx-digital-site`, que está em código congelado por homologação — este projeto é **completamente isolado** dele).
- `.assetsignore` impede que `.git`, `.wrangler` e `.claude` sejam publicados como arquivos estáticos (evita expor internals do repositório).

## Próximos passos (quando o Seu Moura topar)

1. Preencher `materiais/empresas.csv` com contatos reais e começar a abordagem (usar `apresentacao-slides.md` como script).
2. Editar o vídeo de 1 minuto (roteiro em `materiais/roteiro-video.md`) usando o acervo do Instagram.
3. Trocar a nota da galeria ("sem tratamento ainda") depois que as fotos/vídeos forem editados.
4. Se o projeto crescer: decidir entre manter PIX-CPF, abrir MEI, ou estruturar o Instituto Seu Moura (visão de longo prazo já mencionada no site).
