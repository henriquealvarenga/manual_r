# Manual R

**Manual Básico da Linguagem R** — Introdução à análise de dados com a
linguagem R, RStudio e Quarto para área da saúde. Segunda edição.

Publicado em <https://henriquealvarenga.com/manual_r/> · ISBN 978-65-01-14142-8

## Como trabalhar neste livro

```
editar o .qmd  →  quarto render  →  git push
```

O `quarto render` gera a pasta `docs/`, que é versionada. O push dispara o
workflow `.github/workflows/publish.yml`, que publica `docs/` no GitHub Pages.
O GitHub não renderiza nada: o livro é renderizado na máquina do autor, onde os
pacotes de R já estão instalados.

### Configuração que não está neste repositório

Em **Settings → Pages → Build and deployment**, a fonte precisa estar em
**GitHub Actions**. Não existe arquivo que registre isso — é estado guardado
numa tela do GitHub. Trocar para "Deploy from a branch" faz o workflow falhar
no passo de deploy, sem nenhuma pista no código.

### Pacotes de R necessários

O livro carrega 24 pacotes, mas um deles é o `grid`, que já vem com o R. Os
outros 23 precisam ser instalados numa máquina nova:

```r
install.packages(c(
  "bestglm", "broom", "dplyr", "forcats", "GGally", "ggforce", "ggplot2",
  "gridExtra", "janitor", "kableExtra", "magrittr", "plotly", "pROC",
  "psych", "purrr", "readr", "skimr", "stargazer", "tibble", "tidyr",
  "tidyverse", "UsingR", "vcd"
))
```

Também é preciso ter o [Quarto](https://quarto.org) instalado. A saída em PDF
depende de uma distribuição LaTeX — `quarto install tinytex` resolve.

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

**O detalhe importante:** o Quarto decide reexecutar olhando **apenas o `.qmd`
listado em `chapters:`**. Duas situações passam despercebidas por ele:

- **arquivos incluídos.** O capítulo 13 monta-se a partir de nove arquivos
  `13.x` trazidos por `{{< include >}}`. Editar um deles não altera o
  `13-Statistical-Analysis.qmd`, então o Quarto serve o resultado congelado e a
  sua mudança simplesmente não aparece.
- **dados.** Alterar um arquivo de `dataset/` sem tocar no capítulo deixa o
  site mostrando os resultados antigos.

Nos dois casos, a saída é invalidar o cache. Para um capítulo só, apague a
pasta dele em `_freeze/` e renderize:

```sh
rm -rf _freeze/13-Statistical-Analysis
quarto render
```

Para reexecutar o livro inteiro:

```sh
quarto render --no-freeze
```

Os resultados congelados ficam em `_freeze/`, que é versionado de propósito.

## Formatos de saída

O `_quarto.yml` gera **HTML** (o site publicado) e **PDF**.

**Não existe saída em docx, e não é esquecimento.** As tabelas do livro usam
`kableExtra` (`kbl()` seguido de `kable_classic()` e `row_spec()`), que só
produz HTML e LaTeX. Com `docx` declarado no `_quarto.yml`, o render **para com
erro**:

```
Functions that produce HTML output found in document targeting docx output.
```

O `prefer-html: true` sugerido pela mensagem não resolve de verdade: ele deixa
o render terminar, mas as tabelas somem do arquivo do Word.

Se um dia for preciso mesmo entregar em Word, o caminho é trocar o motor de
tabelas por um que atravesse os três formatos — o `flextable` é o candidato —
e isso significa reescrever as tabelas e os trechos de texto que as explicam.

Para a Amazon não é necessário: a KDP prefere **EPUB** para o Kindle e exige
**PDF** para o miolo do impresso. O EPUB é HTML por baixo, então o `kableExtra`
funciona nele sem nenhuma adaptação. Bastaria acrescentar ao `_quarto.yml`:

```yaml
  epub:
    cover-image: cover.png
    toc: true
    number-sections: true
```

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
