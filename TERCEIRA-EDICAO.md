# Backlog para a 3ª edição

Levantamento feito em 23/09/2026, durante a revisão de código da 2ª edição. O que
está aqui foi visto e deixado de lado de propósito: é trabalho de estrutura e de
conteúdo, não de correção. A revisão da 2ª edição cuidou só do código e do texto
que descreve o código.

## Capítulos incompletos

- `11.0-Cleaning.qmd` é órfão: não é incluído por `11-Manipulating-data.qmd` nem
  listado em `_quarto.yml`. Está pela metade: lista quatro problemas dos dados
  brutos e resolve só o primeiro (renomear colunas). É o único lugar que usa
  `janitor` e `dataset/raw-data.csv`. Decidir: terminar e incluir, ou apagar.
- `13.8-Survival-Analysis.qmd`: "A ser escrito". `survival` e `survminer` já estão
  instalados.
- `02-Instalation.qmd`: o capítulo inteiro são três links.
- `05`, seção "Manipulando Vetores": título sem conteúdo, seguido de um `###`
  (nível invertido).
- `08`, seção "Funções anônimas": sem nenhum exemplo de código.
- `14`: Poisson só tem uma lista, sem código; a binomial aparece na tabela mas não
  tem seção.

## Seções prometidas e não escritas

- `15`: MCMC anunciado na introdução; o intervalo de confiança do bootstrap é
  anunciado e não calculado (o capítulo termina nos histogramas).
- `12`: "A tabela abaixo mostra os tipos possíveis de `pch`" — a tabela não existe.
- `13.6`: o plano de regressão 3D com plotly está em chunk `eval=FALSE`; "é usado na
  seguinte sequência:" fica sem continuação; "Como veremos adiante, `tidy()` também
  pode ser aplicada a objetos htest" — nunca é mostrado; a seção "Pacote stargazer"
  é só código, sem texto.
- `13.7`: introduz odds mas nunca calcula nem interpreta odds ratio (`exp(coef())`).
- `11.3`: "Vamos definir 3 categorias de carros:" sem a lista; promete que o
  `forcats` resolve a exclusão silenciosa de níveis e não mostra.
- `13.5`: anuncia três formas de montar a tabela (matrix, data.frame, tibble) e
  mostra duas.

## Duplicações entre capítulos

- `cut()`: seção inteira repetida em `11.3` e `11.5`, com os mesmos erros.
- `summary(mtcars)` e conversão com `as.factor`: `11.5` e `11.6`, quase literal
  ("19 carros automáticos e 13 manuais" nas duas).
- `by()` versus `group_by()`: `11.2` e `11.5`.
- `count()`: `11.2` e `11.4`.
- `fct_recode()`: `11.3` e `11.4`. O conceito de factor aparece em `05`, `11.3` e `11.4`.
- Operador `:` e `seq()`: `05`, `07` e `15`. Pipe: `05` e `07`. `na.rm`: `08`, `11.1`,
  `11.5`. `pivot_longer()`: `06`, `11.1`, `13.2`, `13.4`. `as.factor()`: `05` e `10`.
  `esoph`: `05` e `11.6`. Descrição do `diabetes`: `06`, `11.6`, `16`.
- Dentro do próprio `12`: duas seções "Conclusão". Dentro do `15`: moeda/`sample`
  duas vezes e dois parágrafos idênticos sobre `set.seed()`. Dentro do `08`: o
  parágrafo de abertura repete mais adiante.
- Recodificação ensinada de três jeitos: `05` (`recode_factor`, agora `case_match`),
  `11.2` (`case_match`) e `11.3`/`11.4` (`fct_recode`).

## Capítulo 16 (Datasets)

Não lista `USArrests` (06), `esoph` (05, 11.6), `diamonds` (12), `father.son` do
UsingR (13.6), `chickens.csv` do readr (10) nem `raw-data.csv` (11.0).

## Afirmações conceituais a rever

- `13.0`: "p > α indica que os dados seguem distribuição normal" (quatro vezes);
  Kolmogorov-Smirnov com média e DP estimados da própria amostra (Lilliefors).
- `11.1`: diz que imputar pela média evita inflar o desvio padrão.
- `13.7`: "normalizar é crucial" na logística e não na linear; "não há como
  calcular r²" na logística (há pseudo-R²).
- `14`: interpreta `dunif(5, ...)` como probabilidade de "ser igual a 5".
- `13.6`: chama de "multivariada" a regressão multivariável (vários preditores).

## Estilo de nomes

- `05` recomenda separar palavras com ponto e desaconselha underline e camelCase; o
  resto do livro usa os três (`peso_kg`, `tipoSanguineo`, `result.long`).
- Português e inglês misturados (`mydata`, `mean_glicose`, colunas `sex/age` ao
  lado de `sexo/idade`; rótulos "Male/Female" e "Masculino/Feminino").
- Objetos que sombreiam funções do R: `c`, `data`, `df`, `coef`.

## Datas, versões e ferramentas fixas no texto

- `01`: "Em maio de 2024, 20.000 pacotes", "junho de 2024, 2300 pacotes", pesquisa
  Rexer de 2015, "RStudio PBC", R4DS 1ª edição em r4ds.had.co.nz (a 2ª está em
  r4ds.hadley.nz), "efficientr.programming" e "clauswilke.com/dataviz" sem esquema.
- `00`: "407 avaliações na Amazon", "POSIT".
- `02` e `01`: links rstudio.com (hoje posit.co).
- `03`: seção sobre R Notebook (formato em desuso), "criado há poucos anos".
- `09`: "dez/2018 e mai/2024", contagens de downloads.
- Screenshots do RStudio em `images/` que envelhecem com a interface.
- Imagens sem uso: `Plane.png`, `arguments.jpg`, `Tabelas do  Livro.numbers`.

## Erros de português na prosa

Só os evidentes, por arquivo (não corrigidos na revisão da 2ª edição):

- **01**: "progamação", "Willey", "no Starch", "gens", "distribuidos", "liguagem", "contrição"
- **03**: "Enviroment" (também em 10)
- **05**: "Frequentente", "estancamento do câncer" (estadiamento), "tando", "Poe exemplo", "voê", "informções", "prescisar"
- **06**: "linhasa" (também em 11.6), "tiblles", "esão"
- **08**: "funcção", "pretented", "de nra base", "ouput", "sofisticdas"
- **09**: "Enviroment Protection Agency"
- **10**: "importatos", "element que separal", "intensificados", "preferírel", "intrepretou"
- **11.1**: "usare", "não suporte"
- **11.2**: "vriáveis", "bestaras", "coódigo", "dadoc", "à um objeto"
- **11.3**: "naão", "É ainda que", pacote "aligner" (não existe), "colpasar", "tible"
- **11.6**: frase que começa com "do pacote `psych`", "espoa"
- **12**: "Gráficos fom ggplot", "tibgle", "sobrbe", "acoerd", "nõa"
- **13.0**: "Shapiro-Wilki", "Kolmorov-Smirnov"
- **13.3**: "vamo"
- **13.5**: "unicaldal", "chícaras"
- **13.6**: "regressão regressão", "armazendo"
- **13.7**: "fundamdental", "vito"
- **14**: "sento", "funçõa"
- **15**: frase incompleta na abertura, "Dicutiremos", "númeroso", "server", "Boostrap", "aavaliar", "calculado calculado"

## Miscelânea técnica

- `str()` de tibble do readr imprime `<pointer: 0x…>`, que muda a cada render
  (caps. 06, 10, 11.6). Trocar por `glimpse()` ou `str(as.data.frame(...))`.
- `15`: `trials <- 10000000` cria um data.frame de 10 milhões de linhas.
- Formato EPUB para a Amazon (ver README).
