# Nyata Cosméticos — E-mails de recompra (RD Marketing)

Série de e-mails de recompra/pós-venda usados no RD Marketing.

## Conteúdo

- **[`PADRAO-EMAILS-MOBILE.md`](PADRAO-EMAILS-MOBILE.md)** — padrão de
  legibilidade no celular. Explica por que a fonte ficava pequena no mobile e
  define os tamanhos mínimos e a estrutura HTML a seguir em todos os e-mails.
- **E-mails da série** (em `emails/`), todos no padrão:
  - [`nyata-email-01-boas-vindas-oleo-reparador.html`](emails/nyata-email-01-boas-vindas-oleo-reparador.html)
    — E-mail 01 · Boas-vindas Óleo Reparador (modelo de referência).
  - [`nyata-email-02-passo-antes-do-oleo-manteiga.html`](emails/nyata-email-02-passo-antes-do-oleo-manteiga.html)
    — E-mail 02 · Passo antes do óleo (Manteiga).
  - [`nyata-email-03-cross-sell-manteiga-nutritiva.html`](emails/nyata-email-03-cross-sell-manteiga-nutritiva.html)
    — E-mail 03 · Cross-sell Manteiga Nutritiva.

## Resumo do problema corrigido

No celular a fonte ficava pequena demais por duas razões somadas: (1) layout de
largura fixa que dependia da media query para caber na tela — quando o cliente
de e-mail ignorava a media query, o e-mail era reduzido para caber e o texto
encolhia junto; e (2) tamanhos-base pequenos sem aumento de fonte no mobile.

A correção usa **container fluido** (cabe na tela mesmo sem media query),
**fontes-base maiores** e uma **media query que aumenta as fontes** no celular.
Detalhes em [`PADRAO-EMAILS-MOBILE.md`](PADRAO-EMAILS-MOBILE.md).
