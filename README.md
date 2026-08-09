# Manual R

**Manual Básico da Linguagem R** — Introdução à análise de dados com a
linguagem R, RStudio e Quarto para área da saúde. Segunda edição.

Publicado em <https://henriquealvarenga.com/manual_r/>

## Como trabalhar neste livro

```
editar o .qmd  →  quarto render  →  git push
```

O `quarto render` gera a pasta `docs/`, que é versionada. O push dispara o
workflow `.github/workflows/publish.yml`, que publica `docs/` no GitHub Pages.
O GitHub não renderiza nada: o livro é renderizado na máquina do autor, onde os
pacotes de R já estão instalados.

## Atenção: o freeze olha o código, não os dados

O `_quarto.yml` liga o `freeze` do Quarto:

```yaml
execute:
  freeze: auto
```

Isso faz cada capítulo ser reexecutado **apenas quando o próprio `.qmd` muda**.
Sem isso, todo render produzia diferença em `docs/` mesmo sem ninguém editar
nada — os capítulos 15 e 16 sorteiam números sem semente (de propósito, pois
ensinam justamente que o resultado muda a cada execução), e o `str()` de um
tibble do `readr` imprime um endereço de memória que muda a cada sessão do R.

**O detalhe que pega:** a decisão de reexecutar considera o `.qmd`, e não os
dados. Se um arquivo de `dataset/` for alterado sem que o capítulo seja tocado,
o site continuará mostrando os resultados antigos. Nesse caso, force a
reexecução de tudo uma vez:

```sh
quarto render --no-freeze
```

Os resultados congelados ficam em `_freeze/`, que é versionado de propósito.

## Estrutura

| Caminho | O que é |
|---|---|
| `*.qmd` | Capítulos. Os `13.x` são incluídos por `13-Statistical-Analysis.qmd` |
| `_quarto.yml` | Configuração do livro: capítulos, formatos, freeze |
| `docs/` | Site renderizado — é o que o GitHub Pages publica |
| `_freeze/` | Resultados congelados da execução do R |
| `dataset/`, `images/` | Dados e figuras usados nos capítulos |
| `references.bib` | Bibliografia |

---

Copyright — Henrique Alvarenga da Silva
