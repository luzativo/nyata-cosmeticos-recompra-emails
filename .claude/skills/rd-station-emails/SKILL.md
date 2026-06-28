---
name: rd-station-emails
description: >-
  Base de conhecimento e checklist para criar, editar ou revisar QUALQUER e-mail
  (HTML) para a plataforma RD Station Marketing — para qualquer cliente,
  inclusive a própria Luzativo. Use SEMPRE antes de produzir, ajustar ou validar
  um e-mail de RD Station: define padrões técnicos, layout/responsividade,
  tipografia, imagens, botões, links, copy anti-spam, entregabilidade, erros
  conhecidos e o checklist final obrigatório. Gatilhos: "criar e-mail",
  "e-mail marketing", "RD Station", "campanha de e-mail", "newsletter",
  "fluxo/automação de e-mail", "recompra", "boas-vindas", "HTML de e-mail".
---

# Skill universal — E-mails para RD Station Marketing

Fonte única de consulta e validação antes de criar qualquer e-mail na RD Station.
**Base de conhecimento viva**: sempre que um novo problema for identificado ou uma
boa prática validada, incorpore aqui (ver seção "Como evoluir esta Skill").

> ⚠️ **Princípio que rege quase tudo:** muitos clientes abrem no **app do Gmail**,
> frequentemente com contas que não são @gmail (contas IMAP/empresariais — o
> ambiente "GANGA"). Nesse cenário o app **ignora todo o bloco `<style>` do
> `<head>`, inclusive as media queries.** Logo, **nada crítico** (caber na tela,
> legibilidade de fonte, empilhamento, centralização, cor de fundo) pode depender
> de `<style>`/media query: tem que estar **inline e/ou na estrutura HTML**. A
> media query é só **reforço** para clientes que a suportam (Apple Mail, Gmail com
> conta Google, etc.).

---

## Como atuar (fluxo obrigatório da IA)

Sempre que pedirem para criar/editar/revisar um e-mail de RD Station:

1. **Consulte esta Skill antes de produzir.**
2. **Aplique automaticamente** todas as regras obrigatórias (seções abaixo).
3. **Alerte** se a solicitação violar uma boa prática (ex.: pediram CTA em CAIXA
   ALTA, ou inserir link de descadastro manual) e **explique o porquê**.
4. **Suavize copy com risco de spam** quando autorizado, de forma cirúrgica
   (só o necessário, sem reescrever a mensagem).
5. **Rode o checklist final** (seção 12) antes de entregar.
6. **Pergunte antes** se faltar informação essencial (destino, links de produto,
   imagens, paleta do cliente, se é e-mail com ou sem oferta, etc.).
7. **Valide a estrutura** do HTML gerado (tags balanceadas, comentários MSO
   abertos/fechados, sem classes órfãs, sem texto < 13px).

---

## 1. Estrutura do e-mail

- **Tabelas, não divs de layout.** E-mail = HTML de tabelas (`role="presentation"`,
  `cellspacing=0 cellpadding=0 border=0`). Divs servem só para detalhes (filetes,
  preheader).
- **Cabeça padrão:** `<!DOCTYPE html>` + `<html lang="pt-BR">`, `<meta charset>`,
  `<meta viewport width=device-width, initial-scale=1>`, `X-UA-Compatible`,
  condicional MSO `OfficeDocumentSettings` (PixelsPerInch 96) e o `<style>` com
  resets (`-webkit-text-size-adjust:100%`, `mso-table-lspace/rspace:0`,
  `img{display:block;border:0;height:auto}`).
- **Container fluido + ghost table (OBRIGATÓRIO):** não use `width="600"` fixo.
  Use largura fluida com `max-width`, protegida por ghost table para o Outlook
  (que ignora `max-width`). Isso garante caber na tela **mesmo sem media query**
  (resolve o "zoom-out que deixa a fonte minúscula").

  ```html
  <!--[if mso]>
  <table role="presentation" cellspacing="0" cellpadding="0" border="0" width="600"><tr><td>
  <![endif]-->
  <table role="presentation" cellspacing="0" cellpadding="0" border="0"
         width="100%" class="mobile-full"
         style="width:100%; max-width:600px; background-color:#FFFFFF; border-radius:10px; overflow:hidden;">
    <!-- conteúdo -->
  </table>
  <!--[if mso]>
  </td></tr></table>
  <![endif]-->
  ```
- **Preheader oculto** logo após `<body>` (controla o texto de prévia na inbox):

  ```html
  <div style="display:none; max-height:0; overflow:hidden; mso-hide:all; font-size:1px; line-height:1px; color:#FUNDO; opacity:0;">
    Frase de prévia objetiva.
    &zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;
  </div>
  ```
  (Repita `&zwnj;&nbsp;` para impedir que o corpo "vaze" para a prévia. `color`
  = cor do fundo do e-mail.)

---

## 2. Configurações da RD Station

- **Use o editor de HTML/código** do RD (não o arrastar-e-soltar) para preservar
  o `<style>` do `<head>` e as media queries.
- **Link de descadastro:** ⛔ **NUNCA inserir manualmente** o link de descadastro
  na copy/HTML. A **RD Station adiciona automaticamente** esse elemento
  obrigatório no envio. Inserir manual gera **duplicidade**. (Confirmado: já vem
  por padrão na conta.)
- **Não confie em media query** para o resultado final — ver princípio GANGA no
  topo. Teste sempre pelo **preview/teste de envio do próprio RD em um celular
  real** antes de disparar (ambiente mais fiel ao cliente final).
- Mantenha os resets `-webkit-text-size-adjust:100%` e `-ms-text-size-adjust:100%`
  para impedir reajustes indesejados de fonte.

---

## 3. Layout e responsividade

- **Cabe na tela sem depender de media query** (container fluido + ghost table).
- **Não dependa de media query para mudar layout** (empilhar colunas, esconder
  itens, centralizar). No Gmail app não funciona. Faça por **estrutura**.
- **Blocos de 2+ colunas (imagem ao lado de texto, "cards" lado a lado, duplas):**
  empilhe **por estrutura** (uma `<tr>`/linha por item, imagem em cima e
  texto/CTA embaixo, largura cheia). Motivo: no Gmail app a coluna de texto ao
  lado de uma imagem fixa fica espremida (~75–130px). Exceção tolerável: dois
  "satélites" muito simples (imagem + 1 rótulo + 1 link curto) podem ficar lado
  a lado.
- **Listas em linha que quebram feio** (faixa de benefícios, selos): ver seções 4
  e 6 — use `nowrap` por item ou empilhe por estrutura.
- **Centralização confiável:** para centralizar conteúdo, use `width="100%"` +
  `td align="center"`; **não** dependa de `margin:0 auto`/`align="center"` na
  `<table>` (o Gmail app não centraliza).
- **Fundos coloridos:** todo `<td>` com cor de fundo deve repetir a cor no
  atributo `bgcolor` além do `background-color` inline (Outlook pode descartar o
  CSS → "texto branco sobre branco"). Vale para faixas, rodapé, células de botão,
  barrinhas de acento, círculos de ícone, ribbons/selos.
- **Divisores:** não use `<div border-top width:60%>` (Outlook ignora largura % e
  `margin:auto`). Use uma tabela centralizada:
  ```html
  <table role="presentation" align="center" width="60%" style="width:60%; margin:0 auto;">
    <tr><td style="border-top:1px solid #COR; font-size:0; line-height:0;">&nbsp;</td></tr>
  </table>
  ```
- **Barra de acento em blocos de destaque:** não use `border-left` numa `<table>`
  (Outlook não renderiza). Use célula estrutural antes do conteúdo:
  `<td width="4" bgcolor="#COR" style="background-color:#COR;"></td>`.
- **Sempre validar desktop E mobile** antes de publicar (preview do RD + celular
  real). No Outlook, `border-radius` e `overflow` são ignorados (cantos retos) —
  tradeoff aceito.

---

## 4. Tipografia

⚠️ **O tamanho que vale no celular é o `font-size` INLINE** (Gmail app ignora a
media query). Defina o inline já no valor mínimo. A media query pode repetir o
mesmo valor (ou um pouco maior) como reforço — **nunca para encolher**.

| Elemento                        | Tamanho mínimo (inline) |
|---------------------------------|:-----------------------:|
| Título / H1                     | 26–28px (mobile MQ 26)  |
| Corpo de texto                  | **17px**                |
| Texto de apoio / cards          | **16px**                |
| Linha de oferta / destaque      | 20–22px                 |
| Botões (CTA principal)          | 16–17px                 |
| Rótulos / eyebrow (CAIXA ALTA)  | **13px**                |
| Faixa de benefícios (topo)      | **14px**                |
| Selos de confiança              | 15px                    |
| P.S.                            | 16px                    |
| Rodapé (texto/link)             | **14px**                |
| Rodapé (letra miúda / LGPD)     | **13px**                |

> **Regra de ouro:** **nenhum texto de conteúdo abaixo de 13px** e **corpo nunca
> abaixo de 17px** — no inline. (Fontes < 16px podem disparar zoom automático em
> alguns clientes.)

- **Nunca encolher fonte no mobile via media query** (ex.: `.x{font-size:12px}`
  em `@media`). Se a MQ for ignorada fica no inline; se for respeitada, encolhe —
  os dois casos são ruins. Remova regras de MQ que reduzem fontes.
- **Fonte:** `Arial, Helvetica, sans-serif` (segura em todos os clientes).
- **Órfãos tipográficos:** evite uma palavra curta sozinha na última linha de um
  título. Una as duas últimas palavras com `&nbsp;` (ex.: `começa&nbsp;agora`) —
  funciona em qualquer largura sem `<br>` forçado.
- **Quebra de leitura:** em itens "Rótulo: descrição" longos, considere um `<br>`
  antes do rótulo para separar "o que é" de "o detalhe" (ex.: `...aos fios.<br>
  <strong>Sinal:</strong> ...`).

---

## 5. Imagens

- **Otimizadas e leves** (não usar arquivos pesados — afeta carregamento e
  entregabilidade). Hospede em servidor confiável (no caso Nyata, o S3 do editor
  do RD).
- **Sempre `alt`** descritivo e **coerente com o destino do link** (ex.: não
  escrever "no Instagram" se a imagem leva ao YouTube).
- **`display:block`, `border:0`, `height:auto`** + `width` em atributo E em style.
- **Responsivas:** para imagens grandes use `width="100%"` + `style="max-width:Npx"`;
  imagens pequenas/decorativas podem ter largura fixa.
- **Sem distorção/corte:** respeite a proporção (não force height); confira a foto
  no preview.
- **Equilíbrio texto/imagem** (ver Entregabilidade): nunca um e-mail só de imagem.
- **Dark mode:** logos JPG têm fundo branco "embutido" e podem aparecer como
  retângulo branco; logos brancos podem sumir se o fundo for clareado. Prefira PNG
  transparente e trave o fundo do rodapé com `bgcolor`.

---

## 6. Botões (CTAs)

- **Estrutura "bulletproof":** cor de fundo e `border-radius` no `<td>` (com
  `bgcolor` + `background-color`), `padding` e `font` no `<a display:inline-block>`.
  ```html
  <td bgcolor="#771B8C" style="background-color:#771B8C; border-radius:6px;">
    <a href="..." target="_blank" style="display:inline-block; padding:16px 42px; font-size:16px; color:#FFFFFF; text-decoration:none; font-weight:bold;">Texto do botão</a>
  </td>
  ```
- **Tamanho do texto do CTA:** 16–17px (não menor).
- **Texto do CTA em caixa normal**, orientado à ação ("Quero o meu Kit",
  "Conhecer a linha"). ⛔ **Evitar CAIXA ALTA** (gatilho de spam e leitura pior).
- **Área de toque** generosa no mobile (padding ~15–17px vertical).
- **Faixa de benefícios** (cashback · frete · Pix): envolva cada item em
  `<span style="white-space:nowrap">` para nunca quebrar no meio de "Frete grátis
  acima de R$399"; tamanho 14px; `bgcolor` no `<td>`.
- **Selos de confiança:** empilhe **por estrutura** (uma `<tr>` por selo, tabela
  `width:100%` + `td align=center`), nunca em linha única dependente de wrap.

---

## 7. Links

- Todos os `href` com `target="_blank"` e URL completa/correta (coerente com o
  produto citado).
- **Encoding de URLs** com acentos/espaços (ex.: `%C3%93leo`, `%20`) — confira que
  abrem.
- **Não inserir link de descadastro manual** (ver seção 2).
- Cores de link legíveis e com contraste suficiente (ver seção 9/contraste).

---

## 8. Copywriting (anti-spam)

Toda copy passa por análise para reduzir risco de spam. Ajustes **cirúrgicos** —
só o necessário, sem descaracterizar a mensagem. Evite/cuide de:

- **CAIXA ALTA** em excesso (sobretudo em CTA/título/assunto). → caixa normal.
- **Excesso de "!"** (pontos de exclamação). Use com parcimônia.
- **Promessas exageradas / superpromessas:** "resultado extraordinário",
  "transforma seu dia a dia", "garante", "milagroso". → suavizar para algo
  concreto ("ajuda a", "potencializa", "para um resultado ainda melhor").
- **Urgência artificial agressiva:** "Não perca", "Aproveite agora", "última
  chance". Em e-mails de fechamento/reposição, urgência moderada é ok; evite o
  tom alarmista.
- **Claims regulados (ANVISA/CDC):** evite alegações de proteção/saúde absolutas
  e termos técnicos não comprovados. Ex.: trocamos "filtro solar UVB ... sem
  preocupação" por "filtro UV, que ajuda a proteger os fios da ação do sol".
  Confirme com a área regulatória/rótulo o que é oficialmente suportado.
- **Palavras "gatilho" de spam:** grátis em excesso, "promoção imperdível",
  "100% garantido", "clique aqui já", "$$$", "renda extra", etc. "Frete grátis"
  legítimo é ok.
- **Excesso de emojis.**
- **Equilíbrio texto/imagem** (ver seção 9).
- **Escrita natural, objetiva e humana.** Conteúdo > pressão de venda.

---

## 9. Entregabilidade

- **Equilíbrio texto/imagem:** nunca e-mail "só imagem"; tenha texto real em HTML
  (filtros penalizam imagem-pesada / pouco texto).
- **Preheader preenchido** (melhora abertura).
- **Assunto honesto** (sem clickbait, sem CAPS, sem "RE:/FW:" falso, sem excesso
  de pontuação/emoji).
- **HTML limpo e válido** (tags balanceadas, sem código quebrado) — HTML
  malformado derruba reputação e renderização.
- **Imagens leves** (carregamento rápido).
- **Contraste/acessibilidade (WCAG AA ≥ 4,5:1 para texto normal):** texto pouco
  legível prejudica engajamento. Pares já corrigidos no histórico (use como
  referência):
  | Evitar | Usar | Sobre fundo |
  |---|---|---|
  | `#6B938E` (~3,4:1) | `#9FC0BB` (~6:1) | verde-escuro `#02403B` |
  | `#D8565B` (~3,6:1) | `#C0353B` (~5:1) | claro `#FFF4F4` |
  | `#999999` (~2,9:1) | `#767676` (~4,5:1) | branco |
  | branco sobre `#8DC542` (~2:1) | branco sobre `#5A7A2E` | selo/pill verde |
  | `#9B86AD` / `#9B6BAA` / `#8A7E95` (baixo) | `#6E6175` (~4,7:1) | claro |
- **Descadastro presente** (a RD injeta) — exigência legal/anti-spam.
- **Não usar URL encurtada suspeita** nem domínios de baixa reputação.

---

## 10. Boas práticas (resumo de padrões validados)

- Container fluido + ghost table (cabe na tela sem MQ).
- Tamanhos **inline** aos mínimos da seção 4.
- Faixa de benefícios com `nowrap` por item; selos empilhados por estrutura.
- `bgcolor` em todo `<td>` colorido; divisores e barras de acento em tabela/célula.
- Preheader oculto com espaçador.
- MQ apenas como **reforço** (aumentar fonte / padding mobile 22px / centralizar);
  **nunca** para reduzir fonte ou comandar layout crítico.
- Manter `class` apenas se a regra existir na MQ (sem **classes órfãs**).
- Copy anti-spam (seção 8); descadastro automático (seção 2).
- Testar em celular real via RD antes de disparar.

---

## 11. Erros conhecidos (e a solução)

| Problema | Causa | Solução |
|---|---|---|
| Fonte minúscula no celular | Layout fixo `width=600` + zoom-out do cliente; fontes só grandes via MQ (ignorada) | Container fluido + ghost table; **font-size inline** nos mínimos |
| Selos/benefícios quebrando em pontos esquisitos | Linha única dependente de wrap | Empilhar selos por estrutura; `nowrap` por item na faixa |
| Texto espremido ao lado da imagem | Bloco 2 colunas dependente de MQ p/ empilhar | Empilhar por estrutura (imagem em cima, texto embaixo) |
| Faixa/rodapé "sem cor" no Outlook (texto somindo) | Só `background-color` inline | Adicionar atributo `bgcolor` no `<td>` |
| Divisor/acento errado no Outlook | `div width:%` / `border-left` em `<table>` | Tabela divisória / célula `td width=4 bgcolor` |
| Título com palavra órfã na 2ª linha | Quebra natural | `&nbsp;` entre as duas últimas palavras |
| CTA em CAIXA ALTA | Estilo shouty | Caixa normal |
| Claim regulado arriscado ("UVB", "garante") | Copy | Suavizar/genericizar; validar com regulatório |
| Link de descadastro duplicado | Inserido manual | Nunca inserir manual (RD injeta) |
| Texto cinza ilegível | Contraste < 4,5:1 | Tabela de cores da seção 9 |
| Classe que encolhe fonte no mobile | `.x{font-size:12px}` na MQ | Remover; usar inline ≥ mínimo |

---

## 12. Checklist final (rodar antes de entregar)

**Estrutura**
- [ ] Container fluido (`width:100%; max-width:600px`) + ghost table MSO.
- [ ] Tags balanceadas; comentários `<!--[if mso]>`/`<![endif]-->` em pares.
- [ ] Preheader oculto com espaçador preenchido.

**Tipografia**
- [ ] Corpo ≥ 17px inline; cards ≥ 16px; nenhum texto de conteúdo < 13px.
- [ ] Nenhuma media query reduzindo fonte; sem classes órfãs.
- [ ] Sem órfão tipográfico no título.

**Layout / responsividade**
- [ ] Blocos multi-coluna empilhados por estrutura (não por MQ).
- [ ] Faixa com `nowrap` por item; selos empilhados por estrutura.
- [ ] `bgcolor` em todos os `<td>` coloridos; divisores/acentos em tabela/célula.
- [ ] Centralização via `width:100%` + `td align=center`.

**Imagens**
- [ ] Otimizadas/leves; `alt` coerente com o link; sem distorção.

**Botões / Links**
- [ ] CTA bulletproof, 16–17px, caixa normal, área de toque ok.
- [ ] `href` corretos, `target=_blank`, URLs com encoding válido.

**Copy / Entregabilidade**
- [ ] Sem CAPS/excesso de "!"/superpromessa/claim regulado/gatilho de spam.
- [ ] Equilíbrio texto-imagem; assunto e preheader honestos.
- [ ] Contraste WCAG AA nos textos.

**RD Station**
- [ ] **Descadastro NÃO inserido manualmente** (RD injeta).
- [ ] Colado no editor de **código HTML** do RD.
- [ ] **Teste de envio em celular real** feito antes do disparo.

---

## Como evoluir esta Skill

Esta é uma **base viva**. Sempre que surgir um novo problema/solução ou uma boa
prática validada:
1. Adicione na seção correspondente (e, se for erro, na tabela da seção 11).
2. Se mudar um mínimo/cor, atualize a tabela da seção 4 ou 9.
3. Registre exemplos de "evitar → usar".

> **Escopo / uso em todos os projetos:** esta Skill vive em
> `.claude/skills/rd-station-emails/`. Para usá-la em **100% dos projetos**,
> copie a pasta para `~/.claude/skills/` (skill pessoal, disponível em qualquer
> repositório) ou empacote como plugin. Detalhes/exemplos específicos de um
> cliente (paleta, links, produtos) ficam no repositório do cliente, não aqui.
