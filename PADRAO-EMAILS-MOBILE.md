# Padrão de e-mails Nyata — legibilidade no mobile (RD Marketing)

Guia para corrigir e padronizar a série de e-mails de recompra. O objetivo é
que **a fonte nunca fique pequena demais no celular**, independentemente do
cliente de e-mail (app do Gmail, Apple Mail, Outlook, etc.).

---

## Por que a fonte ficava pequena no celular

O problema tinha **duas causas somadas**:

1. **Layout de largura fixa (`width="600"`) dependente de media query.**
   O e-mail só cabia na tela porque a regra `.mobile-full { width:100% }`
   estava dentro de um `@media`. Quando um cliente **ignora a media query**
   (acontece com frequência no app do Gmail e em e-mails entregues via RD),
   a tabela continua com 600px numa tela de ~360px. O celular então
   **reduz o e-mail inteiro para caber**, e um texto de 16px é renderizado
   como ~9–10px. É isso que vira "muito pequena".

2. **Tamanhos-base pequenos.** Havia textos de 11px, 12px, 13px, 14px e 15px,
   e a media query **não aumentava nenhuma fonte** no mobile — só ajustava
   padding e o título.

---

## As 3 regras do padrão

### 1. Container fluido (não dependa da media query para caber)

Em vez de:

```html
<table ... width="600" class="mobile-full" style="...">
```

use largura fluida com `max-width`, protegida por um "ghost table" para o
Outlook (que ignora `max-width`):

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

Assim o e-mail **cabe na tela mesmo quando a media query é ignorada** — o que
elimina o zoom-out que encolhia o texto.

### 2. Tamanhos mínimos de fonte

| Elemento                     | Desktop | **Mobile (mín.)** |
|------------------------------|:-------:|:-----------------:|
| Título / H1                  | 28px    | **26px**          |
| Corpo de texto               | 16px    | **18px**          |
| Texto de apoio (cards)       | 15px    | **17px**          |
| Linha de oferta (destaque)   | 20px    | **22px**          |
| Botões (CTA)                 | 15–16px | **17px**          |
| Rótulos / eyebrow (CAIXA ALTA)| 11–12px| **13px**          |
| Faixa de benefícios (topo)   | 12px    | **14px**          |
| Selos de confiança           | 13px    | **14px**          |
| P.S.                         | 14px    | **16px**          |
| Rodapé (texto/link)          | 12–13px | **14px**          |
| Rodapé (letra miúda / LGPD)  | 11px    | **13px**          |

> Regra de ouro: **corpo de texto nunca abaixo de 17px no celular.**
> Textos abaixo de 16px também disparam zoom automático em alguns clientes.

### 3. Media query que **aumenta** as fontes

Cada texto recebe uma classe; a media query aumenta a fonte no mobile.
Como o tamanho inline já é legível no desktop, mesmo que a media query seja
ignorada o texto continua aceitável (e o container fluido garante que cabe).

```css
@media only screen and (max-width: 600px) {
  .mobile-full       { width: 100% !important; }
  .mobile-padding    { padding: 24px 22px !important; }
  .mobile-padding-sm { padding: 18px 22px !important; }

  .hero-h1    { font-size: 26px !important; line-height: 32px !important; }
  .text-body  { font-size: 18px !important; line-height: 28px !important; }
  .text-card  { font-size: 17px !important; line-height: 27px !important; }
  .text-offer { font-size: 22px !important; line-height: 28px !important; }
  .text-eyebrow { font-size: 13px !important; }
  .text-bar     { font-size: 14px !important; line-height: 20px !important; }
  .text-ps      { font-size: 16px !important; line-height: 24px !important; }
  .text-selos   { font-size: 14px !important; line-height: 22px !important; }
  .text-footer       { font-size: 14px !important; line-height: 22px !important; }
  .text-footer-fine  { font-size: 13px !important; line-height: 20px !important; }
  .btn-link          { font-size: 17px !important; }
}
```

Uso nos elementos (mantenha **sempre** o `style` inline + a classe):

```html
<p class="text-body" style="margin:0; font-family:Arial, Helvetica, sans-serif; font-size:16px; line-height:26px; color:#3D3D3D;">
  Texto do corpo...
</p>
```

---

## ⚠️ Importante: o app do Gmail ignora o bloco `<style>`

O **app do Gmail (Android/iOS), sobretudo com contas que não são @gmail**
(contas IMAP/empresariais adicionadas ao app), **ignora todo o `<style>` do
`<head>` — inclusive as media queries.** Ou seja, naquele ambiente:

- O aumento de fonte da media query (regra 3) **não é aplicado**.
- Qualquer `display:block` / `display:none` de media query **não funciona**.

Por isso o que é **crítico precisa estar em estilo inline e na estrutura**:

- O container fluido (regra 1) funciona porque o `width:100%; max-width:600px`
  é **inline** — foi ele que resolveu a fonte pequena (impede o zoom-out).
- Os tamanhos de fonte **inline** (regra 2) devem ser, por si só, legíveis no
  celular — não conte com a media query para aumentá-los. A media query é um
  **reforço** para os clientes que a suportam (Apple Mail, Gmail com conta
  Google, etc.), não a base.

## Listas em linha que quebram feio no celular (ex.: selos)

Trechos como `✓ Vegano · ✓ Liberado para Low Poo e No Poo · ✓ Sem sulfatos`
quebram em pontos esquisitos no celular. Como o empilhamento **não pode
depender de media query** (Gmail app a ignora), faça-o **estruturalmente**:
cada item em sua própria linha de uma tabela, com estilo inline.

```html
<table role="presentation" cellspacing="0" cellpadding="0" border="0" align="center" style="margin:0 auto;">
  <tr>
    <td align="center" style="font-family:Arial, Helvetica, sans-serif; font-size:15px; line-height:22px; color:#5A7A2E; font-weight:bold; letter-spacing:0.5px; padding:4px 0;">
      <span style="color:#8DC542;">&#10003;</span>&nbsp; Vegano
    </td>
  </tr>
  <!-- uma <tr> por selo: Liberado para Low Poo e No Poo / Sem sulfatos -->
</table>
```

Assim cada selo fica numa linha em **todos** os clientes (inclusive Gmail app).
No desktop também ficam empilhados — em 3 linhas centralizadas fica limpo e
intencional, e dá mais destaque a cada atributo.

---

## Como aplicar à série inteira

Para cada e-mail da série:

1. Troque o container fixo `width="600"` pelo bloco **fluido + ghost table**
   (regra 1).
2. Em cada texto, **adicione a classe** correspondente da tabela acima
   (`text-body`, `text-card`, `text-eyebrow`, etc.).
3. Confirme que os tamanhos inline respeitam os mínimos de **desktop** da
   tabela (suba os que estiverem abaixo).
4. Copie o bloco `@media` da regra 3 para o `<style>` do `<head>`.

O arquivo [`emails/oleo-reparador.html`](emails/oleo-reparador.html) já é o
**modelo de referência** com tudo aplicado — use-o como base.

---

## Dicas específicas do RD Marketing

- **Use o editor de HTML/código** do RD (não o arrastar-e-soltar), para que o
  bloco `<style>` e as media queries do `<head>` sejam preservados.
- Mantenha `<meta name="viewport" content="width=device-width, initial-scale=1">`.
- Mantenha `-webkit-text-size-adjust: 100%` e `-ms-text-size-adjust: 100%`
  (já estão no `<style>`) para impedir reajustes indesejados de fonte.
- **Sempre teste pelo preview/teste de envio do próprio RD num celular real**
  antes de disparar — é o ambiente mais fiel ao que o cliente final recebe.
