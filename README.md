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
  - [`nyata-email-04-prova-social-e-identidade.html`](emails/nyata-email-04-prova-social-e-identidade.html)
    — E-mail 04 · Prova social e identidade.
  - [`nyata-email-05-rotina-completa-kit.html`](emails/nyata-email-05-rotina-completa-kit.html)
    — E-mail 05 · Rotina completa (Kit).
  - [`nyata-email-06-vegana-low-no-poo.html`](emails/nyata-email-06-vegana-low-no-poo.html)
    — E-mail 06 · Vegana e Low/No Poo.
  - [`nyata-email-07-recompra-ciclo-oleo.html`](emails/nyata-email-07-recompra-ciclo-oleo.html)
    — E-mail 07 · Recompra ciclo (Óleo).
  - [`nyata-email-08-recompra-fechamento-oleo.html`](emails/nyata-email-08-recompra-fechamento-oleo.html)
    — E-mail 08 · Recompra fechamento (Óleo).
  - [`nyata-email-09-cross-sell-leave-in.html`](emails/nyata-email-09-cross-sell-leave-in.html)
    — E-mail 09 · Cross-sell Leave-in Defrizante.

## Resumo do problema corrigido

No celular a fonte ficava pequena demais por duas razões somadas: (1) layout de
largura fixa que dependia da media query para caber na tela — quando o cliente
de e-mail ignorava a media query, o e-mail era reduzido para caber e o texto
encolhia junto; e (2) tamanhos-base pequenos sem aumento de fonte no mobile.

A correção usa **container fluido** (cabe na tela mesmo sem media query),
**fontes-base maiores** e uma **media query que aumenta as fontes** no celular.
Detalhes em [`PADRAO-EMAILS-MOBILE.md`](PADRAO-EMAILS-MOBILE.md).
