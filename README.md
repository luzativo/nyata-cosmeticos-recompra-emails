# Nyata Cosméticos — E-mails de recompra (RD Marketing)

Série de e-mails de recompra/pós-venda usados no RD Marketing.

## Conteúdo

- **[`PADRAO-EMAILS-MOBILE.md`](PADRAO-EMAILS-MOBILE.md)** — padrão de
  legibilidade no celular. Explica por que a fonte ficava pequena no mobile e
  define os tamanhos mínimos e a estrutura HTML a seguir em todos os e-mails.
- **[`emails/oleo-reparador.html`](emails/oleo-reparador.html)** — modelo de
  referência (Óleo Reparador Amor Crescido) já corrigido conforme o padrão.

## Resumo do problema corrigido

No celular a fonte ficava pequena demais por duas razões somadas: (1) layout de
largura fixa que dependia da media query para caber na tela — quando o cliente
de e-mail ignorava a media query, o e-mail era reduzido para caber e o texto
encolhia junto; e (2) tamanhos-base pequenos sem aumento de fonte no mobile.

A correção usa **container fluido** (cabe na tela mesmo sem media query),
**fontes-base maiores** e uma **media query que aumenta as fontes** no celular.
Detalhes em [`PADRAO-EMAILS-MOBILE.md`](PADRAO-EMAILS-MOBILE.md).
