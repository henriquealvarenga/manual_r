# Backlog para a 3ª edição

Levantamento feito em 23/09/2026, durante a revisão da 2ª edição. Aquela revisão
cuidou do código, do texto que descreve o código, dos erros de português, das
afirmações conceituais e das duplicações entre seções. O que sobrou aqui exige
escrever conteúdo novo ou tomar decisões editoriais.

Marque cada item com `[x]` conforme for resolvido.

## O que falta escrever

Cada item diz onde está a promessa, o que o texto atual anuncia e o que precisa
ser produzido.

### Capítulos e seções vazios

- [ ] **13.8 Análise de sobrevivência** (`13.8-Survival-Analysis.qmd`). Só tem "A ser
  escrito". Escrever a seção inteira: conceito de tempo até o evento e censura,
  curva de Kaplan-Meier com `survfit()` e `ggsurvplot()`, teste de log-rank e
  regressão de Cox com `coxph()`. Os pacotes `survival` e `survminer` já estão
  instalados. Precisa de um dataset (o `lung` do `survival` serve) e de entrada no
  capítulo 16.
- [ ] **02 Instalação** (`02-Instalation.qmd`). O capítulo inteiro são três links.
  Escrever o passo a passo de instalação do R, do RStudio e do Quarto, com
  screenshots, e atualizar os links para posit.co.
- [ ] **11.0 Limpeza de dados** (`11.0-Cleaning.qmd`). Arquivo órfão: não é incluído
  por `11-Manipulating-data.qmd` nem listado em `_quarto.yml`. Lista quatro
  problemas dos dados brutos (nomes de colunas, NA, vírgula decimal, categorias) e
  resolve só o primeiro. Decidir: terminar os três itens restantes e incluir na
  seção 11, ou apagar o arquivo, o `dataset/raw-data.csv` e o pacote `janitor` da
  lista do README.
- [ ] **05 "Manipulando Vetores"**. O título existe sem conteúdo e é seguido de um
  `###` com nível invertido. Escrever a seção (indexação, `[ ]`, `which()`,
  `rev()`, `sort()`, `append()`) ou apagar o título.
- [ ] **08 "Funções anônimas"**. A seção não tem nenhum exemplo de código.
  Acrescentar exemplos com `function(x)` e com a sintaxe curta `\(x)`, e um uso
  típico com `sapply()` ou `purrr::map()`.
- [ ] **14 Distribuição de Poisson**. Só tem uma lista, sem código. Escrever a seção
  no mesmo padrão das outras: `dpois()`, `ppois()`, `qpois()`, `rpois()` com gráfico.
- [ ] **14 Distribuição binomial**. Aparece na tabela do fim do capítulo, mas não
  tem seção. Escrever no mesmo padrão: `dbinom()`, `pbinom()`, `qbinom()`, `rbinom()`.

### Promessas feitas no texto e não cumpridas

- [ ] **15 MCMC**. A introdução anuncia "Cadeias de Markov Monte Carlo (MCMC)" e o
  capítulo nunca chega lá. Escrever a seção ou retirar a promessa da introdução.
- [ ] **15 Intervalo de confiança do bootstrap**. O texto diz que vai "calcular o
  intervalo de confiança da média" e termina nos histogramas. Acrescentar o
  cálculo com `quantile(means, c(0.025, 0.975))` e a comparação com o IC do
  `t.test()` da amostra original.
- [ ] **12 Tabela de `pch`**. "A tabela abaixo mostra os tipos possíveis de `pch`" e
  a tabela não existe. Gerar a figura com os 26 símbolos (um chunk com
  `plot(0:25, pch = 0:25)` resolve) ou uma tabela.
- [ ] **13.6 Plano de regressão em 3D**. O chunk com plotly está em `eval=FALSE`
  porque plotly não renderiza em PDF. Decidir: gerar uma figura estática (por
  exemplo com `scatterplot3d` ou `persp()`), ou manter o plotly só no HTML com
  um bloco condicional ao formato.
- [ ] **13.6 "é usado na seguinte sequência:"**. A frase fica sem continuação.
  Escrever a sequência (definir o modelo, `lm()`, `summary()`, diagnóstico,
  previsão) ou apagar a frase.
- [ ] **13.6 `tidy()` em objetos htest**. "Como veremos adiante, `tidy()` também
  pode ser aplicada a objetos htest" e nunca é mostrado. Acrescentar um exemplo
  com `tidy(t.test(...))` ou `tidy(cor.test(...))`.
- [ ] **13.6 Seção "Pacote stargazer"**. É só código, sem texto. Escrever o
  parágrafo que explica o que a tabela mostra e quando usar. Considerar trocar
  por `gtsummary` ou `modelsummary`, que têm manutenção ativa; o `stargazer` está
  parado desde 2022.
- [ ] **13.7 Odds ratio**. A seção introduz odds mas nunca calcula nem interpreta a
  odds ratio. Acrescentar `exp(coef(modelo))` e `exp(confint(modelo))`, com a
  leitura clínica de um coeficiente (por exemplo, o do tabaco).
- [ ] **13.5 Terceira forma de montar a tabela**. O texto anuncia três formas
  (matrix, data.frame, tibble) e mostra duas. Acrescentar o exemplo com `tibble()`
  ou corrigir o texto para "duas".
- [ ] **11.3 Exclusão silenciosa de níveis**. O texto promete que o `forcats`
  resolve o problema de um valor fora dos níveis virar `NA` sem aviso, e não
  mostra. Acrescentar o exemplo com `fct()` (que dá erro em vez de `NA`) ou
  `fct_expand()`.

### Capítulo 16 (lista de datasets)

- [ ] Acrescentar os datasets usados no livro e ausentes da lista: `USArrests`
  (06), `esoph` (05, 11.6), `diamonds` (12), `father.son` do UsingR (13.6),
  `chickens.csv` do readr (10) e, se o 11.0 entrar, `raw-data.csv`.

## Decisões editoriais pendentes

- [ ] Grafia: o 13.5 escreve "chi-quadrado" e o 14 escreve "qui-quadrado".
  Escolher uma e uniformizar.
- [ ] Repetições que ficaram de propósito, como lembrete, e que a 3ª edição pode
  enxugar: operador `:` e `seq()` em 05, 07 e 15; pipe em 05 e 07; `na.rm` em 08,
  11.1 e 11.5; `pivot_longer()` em 06, 11.1, 13.2 e 13.4; `as.factor()` em 05 e 10;
  `esoph` em 05 e 11.6; `fct_recode()` em 11.3 (apresentação) e 11.4 (uso).
- [ ] Estilo de nomes: o 05 recomenda separar palavras com ponto e desaconselha
  underline e camelCase, mas o livro usa os três (`peso_kg`, `tipoSanguineo`,
  `result.long`). Decidir a regra e aplicá-la, ou reescrever a recomendação.
- [ ] Português e inglês misturados nos nomes (`mydata`, `mean_glicose`, colunas
  `sex/age` ao lado de `sexo/idade`; rótulos "Male/Female" e "Masculino/Feminino").
- [ ] Objetos que sombreiam funções do R: `c`, `data`, `df`, `coef`. Renomear.

## Datas, versões e ferramentas que envelhecem

- [ ] `01`: "Em maio de 2024, 20.000 pacotes", "junho de 2024, 2300 pacotes",
  pesquisa Rexer de 2015, "RStudio PBC", R4DS 1ª edição em r4ds.had.co.nz (a 2ª
  está em r4ds.hadley.nz), "efficientr.programming" e "clauswilke.com/dataviz"
  sem esquema.
- [ ] `00`: "407 avaliações na Amazon", "POSIT".
- [ ] `01` e `02`: links rstudio.com (hoje posit.co).
- [ ] `03`: seção sobre R Notebook (formato em desuso) e "criado há poucos anos".
- [ ] `09`: "dez/2018 e mai/2024" e contagens de downloads.
- [ ] Screenshots do RStudio em `images/`, que envelhecem com a interface.
- [ ] Imagens sem uso: `Plane.png`, `arguments.jpg`, `Tabelas do  Livro.numbers`.

## Miscelânea técnica

- [ ] `str()` de tibble do readr imprime `<pointer: 0x…>`, que muda a cada render
  (caps. 06, 10, 11.6). Trocar por `glimpse()` ou `str(as.data.frame(...))`.
- [ ] `15`: `trials <- 10000000` cria um data.frame de 10 milhões de linhas.
- [ ] Formato EPUB para a Amazon (ver README).
