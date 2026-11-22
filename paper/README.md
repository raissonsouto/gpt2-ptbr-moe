# Artigo — Atividade 1 (PPGCC/UFCG)

Estudo experimental: o que um Mixture of Experts ganha sobre o GPT-2 denso,
na mesma escala e com o mesmo orçamento. Artigo no template SBC, até 8 páginas.

## Compilar

```sh
pdflatex main && bibtex main && pdflatex main && pdflatex main
```

## Estrutura

- `main.tex`: artigo
- `references.bib`: referências (entradas `[VERIFICAR]` pendentes)
- `figuras/`: curvas de loss, utilização dos especialistas etc.
- `sbc-template.sty`, `sbc.bst`: template oficial da SBC
