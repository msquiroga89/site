---
title: 'Contribución a #TidyTuesday, semana 33'
author: 'Macarena Quiroga'
date: '2021-08-15'
slug: contribución-a-tidytuesday-semana-33
categories: []
tags:
  - rstats
  - tidytuesday
  - dataviz
  - español
subtitle: ''
summary: ''
authors: []
lastmod: '2021-08-15T21:59:46-03:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: yes
projects: [ciencia-de-datos]
---

<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/d3/d3.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/colorbrewer/colorbrewer.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/colorbrewer/colorbrewer.js"></script>
<link href="{{< blogdown/postref >}}index_files/streamgraph/streamgraph.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/streamgraph-binding/streamgraph.js"></script>

Hacía mucho tiempo que no participaba de \#TidyTuesday: un poco por falta de tiempo, otro poco porque los datasets que publicaban no me motivaban, y un poco porque ya me daba vergüenza subir siempre lo mismo. Pero hoy, después de haberle dedicado tres horas de mi domingo al [livestream de Kierisi sobre Machine Learning](https://www.twitch.tv/videos/1119311136), me quedé con ganas de seguir programando.

(Para quienes no sepan: \#TidyTuesday es un proyecto colaborativo que consiste en trabajar cada semana con un set de datos reales para practicar visualización y otras habilidades del mundo de la ciencia de datos. Pueden encontrar más información en su [repositorio de GitHub](https://github.com/rfordatascience/tidytuesday/blob/master/data/2021/2021-08-10/readme.md) y bajo el [hashtag en twitter](https://twitter.com/hashtag/TidyTuesday?src=hashtag_click).)

Empecemos con la organización general:

``` r
library(tidytuesdayR)
library(tidyverse)
library(hrbrthemes)
library(streamgraph)
library(htmlwidgets)
library(webshot)

tuesdata <- tidytuesdayR::tt_load('2021-08-10')
```

    ## 
    ##  Downloading file 1 of 3: `ipd.csv`
    ##  Downloading file 2 of 3: `chain_investment.csv`
    ##  Downloading file 3 of 3: `investment.csv`

``` r
investment <- tuesdata$investment
chain_investment <- tuesdata$chain_investment
ipd <- tuesdata$ipd


# Análisis Exploratorio ----------------------------------------------------

glimpse(investment)
```

    ## Rows: 6,106
    ## Columns: 5
    ## $ category  <chr> "Total basic infrastructure", "Total basic infrastructure", …
    ## $ meta_cat  <chr> "Total infrastructure", "Total infrastructure", "Total infra…
    ## $ group_num <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ year      <dbl> 1947, 1948, 1949, 1950, 1951, 1952, 1953, 1954, 1955, 1956, …
    ## $ gross_inv <dbl> 4974.662, 6486.770, 7376.143, 7943.959, 8961.233, 9707.590, …

``` r
glimpse(chain_investment) # cuánto cambió a lo largo del tiempo, actualizado
```

    ## Rows: 6,035
    ## Columns: 5
    ## $ category        <chr> "Total basic infrastructure", "Total basic infrastruct…
    ## $ meta_cat        <chr> "Total infrastructure", "Total infrastructure", "Total…
    ## $ group_num       <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ year            <dbl> 1947, 1948, 1949, 1950, 1951, 1952, 1953, 1954, 1955, …
    ## $ gross_inv_chain <dbl> 73278.62, 83218.25, 95760.00, 103642.40, 102264.39, 10…

``` r
glimpse(ipd)
```

    ## Rows: 6,106
    ## Columns: 5
    ## $ category      <chr> "GDP", "GDP", "GDP", "GDP", "GDP", "GDP", "GDP", "GDP", …
    ## $ meta_cat      <chr> "GDP", "GDP", "GDP", "GDP", "GDP", "GDP", "GDP", "GDP", …
    ## $ group_num     <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
    ## $ year          <dbl> 1947, 1948, 1949, 1950, 1951, 1952, 1953, 1954, 1955, 19…
    ## $ gross_inv_ipd <dbl> 12.250, 12.946, 12.942, 13.064, 13.950, 14.254, 14.436, …

``` r
investment %>% group_by(category) %>% count()
```

    ## # A tibble: 60 × 2
    ## # Groups:   category [60]
    ##    category                                n
    ##    <chr>                               <int>
    ##  1 Air transportation                     71
    ##  2 All federal                            71
    ##  3 Conservation and development           71
    ##  4 Education                              71
    ##  5 Federal                               639
    ##  6 Federal electric power structures      71
    ##  7 Health                                 71
    ##  8 Highways and streets                   71
    ##  9 Office buildings, NAICS 518 and 519    71
    ## 10 Other federal                          71
    ## # … with 50 more rows

``` r
investment %>% group_by(meta_cat) %>% count()
```

    ## # A tibble: 16 × 2
    ## # Groups:   meta_cat [16]
    ##    meta_cat                             n
    ##    <chr>                            <int>
    ##  1 Air /water /other transportation   852
    ##  2 Conservation and development       213
    ##  3 Digital                            355
    ##  4 Education                          426
    ##  5 Electric power                     426
    ##  6 Health                             497
    ##  7 Highways and streets               142
    ##  8 Natural gas /petroleum power       213
    ##  9 Power                              213
    ## 10 Public safety                      355
    ## 11 Sewer and waste                    142
    ## 12 Social                             426
    ## 13 Total basic infrastructure         568
    ## 14 Total infrastructure               426
    ## 15 Transportation                     710
    ## 16 Water supply                       142

El dataset de esta semana era sobre inversiones en EEUU durante el período de tiempo que va desde 1947 hasta 2017. Tengo que confesar que tampoco me motivaba mucho la temática; además, los tres dataframes que traían eran muy parecidos y con algunas terminologías sobre economía que no entendía del todo. Pero sí tenía ganas de hacer algo, y eso fue suficiente.

Decidí no procrastinar demasiado y hacer por lo menos dos gráficos sobre algún terreno conocido, así que elegí educación.

#### Primera pregunta: ¿cómo cambió la inversión federal en educación a lo largo de este período de tiempo?

Este fue, digamos, el gráfico conocido y fácil: elegí hace un gráfico de líneas para mostrar la evolución de la inversión y elegí un solo tópico para innovar: dejar los demás valores de la variable categórica “áreas de inversión” en gris, y resaltar solamente el área de educación.

``` r
investment %>% 
  filter(category=="Federal") %>% 
  mutate(highligth = ifelse(meta_cat=="Education", "Education", "Other")) %>% 
  group_by(meta_cat, year) %>% 
  ggplot(aes(x = year, y = gross_inv, group = meta_cat, size = highligth))+
  geom_line()+
  scale_color_manual(values = c("#69b3a2", "lightgrey"))+
  scale_size_manual(values=c(1.5,0.2))+
  theme_ipsum()+
  theme(legend.position = "none")+
  labs(x="", y="",
       title="Evolución de la inversión federal en educación",
       caption = "Data: Bureau of Economic Analysis | Plot: @_msquiroga | #TidyTuesday")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

Estoy bastante satisfecha con el resultado. En general, suelo preferir los gráficos coloridos y con mucha información, pero justamente la sensación es que terminan siendo confusos y con la información solapada. En cambio, este gráfico me pareció claro y con un diseño sobrio.

#### Segunda pregunta: ¿cómo evolucionaron las distintas fuentes de inversión a lo largo del tiempo?

Primero pensé en hacer un gráfico similar al anterior: un gráfico de áreas apiladas. Pero mirando R Graph Gallery, uno de los mejores recursos de visualización que existen, pensé que podía ser una buena idea probar con el paquete StreamGraph para hacer, bueno, gráficos “de corriente” interactivos. En general no soy muy amiga de usar otros paquetes que no sean ggplot2, no por fundamentalista, sino solamente porque es lo que más manejo. Pero bueno, hay que innovar.

``` r
graph <- investment %>% 
  filter(meta_cat == "Education") %>% 
  streamgraph(., key = "category", value = "gross_inv", date="year") %>% 
  sg_legend(TRUE, "Fuente de inversión")
graph
```

<div id="htmlwidget-1" class="streamgraph html-widget" style="width:672px;height:480px;"></div>
<div id="htmlwidget-e990506aec7c8f74b817-legend" style="width:672" class="streamgraph html-widget-legend"><center><label style='padding-right:5px' for='htmlwidget-e990506aec7c8f74b817-select'></label><select id='htmlwidget-e990506aec7c8f74b817-select' style='visibility:hidden;'></select></center></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"data":{"key":["Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures","Federal","Private","S&L higher education","S&L K-12","S&L libraries","S&L other educational structures"],"value":[40,174,45.585,183.603,3.098,1,48,253,122.755,491.826,5.126,3,58,269,186.289,746.872,8.214,5,63,294,225.741,907.802,9.29,6,64,345,300.764,1212.46,9.294,7,71,351,318.632,1285.602,7.272,8,74,426,340.13,1369.058,9.355,8,70,529,423.375,1704.767,12.396,10,60,466,486.991,1956.55,15.665,12,56,562,509.418,2047.803,15.736,13,59,525,562.564,2263.145,17.76,14,69,574,572.026,2302.083,18.837,14,82,525,529.999,2129,18.999,13,95,566,494.999,2311,30,18,105,609,645.001,2386,33.001,25,118,680,738,2228,39,28,137,678,1030.999,2418,38.001,42,146,751,1187,2562,44,68,160,787,1353.001,2870,51.001,106.999,155,987,1796.001,3442.001,64.999,139.999,143,1048,1966.001,3896,92,159,133,1147,1857.001,4094,92,153,115,1083,1969.001,3788,92.999,154,123,925,2201.001,3213,94,242,151,1008,2159.001,3210,91.001,232,170,1063,2411,3082.999,84,255,204,983,3144.002,3290.001,91,225,233,737,2994,4055,97,297,269,653,1939.001,5009,130,466.001,281,717,1992,4504,120.999,433.999,321,742,1732.999,3944,98.001,318,383,878,1749,4438,120,300,400,1088,1825,4974.001,136,293.001,443,1585,2124,5342,158.999,327,450,1707,2308.001,4711,159,252,395,1936,2194,4587,146.001,186.001,393,2127,1998.998,4530,144,279,437,2257,2361,5049,178,353,377,2677,2743.999,6050.999,188,226,397,3230,3094,7141,230,146,431,4700,3148.999,7284.001,269.001,161.999,390,3776,3567.001,8962,335,207,383,4278,3926,10371,357,290,450,4800,3902.001,11724.999,441,259,572,4934,4480,14249,479,188,653,5134,5231,14769,417,168,724,5319,5419.001,13465.999,377,160,709,5500,5778,14326,376,205,717,6246,6632.999,18808,426.999,246,755,7643,6500,21594,549.999,267,356,9825,7420.999,24501,583.001,298,306,10881,8166,27715,574,277,277,10400,9142,31593.999,528,282,366,12662,10171,35025.999,574,395,536,13844,11508,39617.999,661,497,750,14200,13398,40285,757.999,498,657,14341,15257,41250,868,435,754,13604,17030,42702,916,349,343,13912,17918.001,46318,1078,318,289,14601,19300.001,51334,1016,402,383,17149,21171.998,54974.001,1070.999,466,389,18250,23781.8,56519.999,1002.8,412.799,433,17472,25838.601,51314,1077.6,954.6,379,14163,26151.4,44605,971.4,1455.4,455,14188,26619.2,41172,866.199,1018.2,463,16260,26337.999,38039,825,677,539,15396,25127.999,36960,699,707,491,15431,24720.999,39354,757,707,426,16146,26366.999,43779.001,924,615,276,18008,27835,48404,972,468,215,18885,27874,51863.999,797.001,420],"date":["1947-01-01","1947-01-01","1947-01-01","1947-01-01","1947-01-01","1947-01-01","1948-01-01","1948-01-01","1948-01-01","1948-01-01","1948-01-01","1948-01-01","1949-01-01","1949-01-01","1949-01-01","1949-01-01","1949-01-01","1949-01-01","1950-01-01","1950-01-01","1950-01-01","1950-01-01","1950-01-01","1950-01-01","1951-01-01","1951-01-01","1951-01-01","1951-01-01","1951-01-01","1951-01-01","1952-01-01","1952-01-01","1952-01-01","1952-01-01","1952-01-01","1952-01-01","1953-01-01","1953-01-01","1953-01-01","1953-01-01","1953-01-01","1953-01-01","1954-01-01","1954-01-01","1954-01-01","1954-01-01","1954-01-01","1954-01-01","1955-01-01","1955-01-01","1955-01-01","1955-01-01","1955-01-01","1955-01-01","1956-01-01","1956-01-01","1956-01-01","1956-01-01","1956-01-01","1956-01-01","1957-01-01","1957-01-01","1957-01-01","1957-01-01","1957-01-01","1957-01-01","1958-01-01","1958-01-01","1958-01-01","1958-01-01","1958-01-01","1958-01-01","1959-01-01","1959-01-01","1959-01-01","1959-01-01","1959-01-01","1959-01-01","1960-01-01","1960-01-01","1960-01-01","1960-01-01","1960-01-01","1960-01-01","1961-01-01","1961-01-01","1961-01-01","1961-01-01","1961-01-01","1961-01-01","1962-01-01","1962-01-01","1962-01-01","1962-01-01","1962-01-01","1962-01-01","1963-01-01","1963-01-01","1963-01-01","1963-01-01","1963-01-01","1963-01-01","1964-01-01","1964-01-01","1964-01-01","1964-01-01","1964-01-01","1964-01-01","1965-01-01","1965-01-01","1965-01-01","1965-01-01","1965-01-01","1965-01-01","1966-01-01","1966-01-01","1966-01-01","1966-01-01","1966-01-01","1966-01-01","1967-01-01","1967-01-01","1967-01-01","1967-01-01","1967-01-01","1967-01-01","1968-01-01","1968-01-01","1968-01-01","1968-01-01","1968-01-01","1968-01-01","1969-01-01","1969-01-01","1969-01-01","1969-01-01","1969-01-01","1969-01-01","1970-01-01","1970-01-01","1970-01-01","1970-01-01","1970-01-01","1970-01-01","1971-01-01","1971-01-01","1971-01-01","1971-01-01","1971-01-01","1971-01-01","1972-01-01","1972-01-01","1972-01-01","1972-01-01","1972-01-01","1972-01-01","1973-01-01","1973-01-01","1973-01-01","1973-01-01","1973-01-01","1973-01-01","1974-01-01","1974-01-01","1974-01-01","1974-01-01","1974-01-01","1974-01-01","1975-01-01","1975-01-01","1975-01-01","1975-01-01","1975-01-01","1975-01-01","1976-01-01","1976-01-01","1976-01-01","1976-01-01","1976-01-01","1976-01-01","1977-01-01","1977-01-01","1977-01-01","1977-01-01","1977-01-01","1977-01-01","1978-01-01","1978-01-01","1978-01-01","1978-01-01","1978-01-01","1978-01-01","1979-01-01","1979-01-01","1979-01-01","1979-01-01","1979-01-01","1979-01-01","1980-01-01","1980-01-01","1980-01-01","1980-01-01","1980-01-01","1980-01-01","1981-01-01","1981-01-01","1981-01-01","1981-01-01","1981-01-01","1981-01-01","1982-01-01","1982-01-01","1982-01-01","1982-01-01","1982-01-01","1982-01-01","1983-01-01","1983-01-01","1983-01-01","1983-01-01","1983-01-01","1983-01-01","1984-01-01","1984-01-01","1984-01-01","1984-01-01","1984-01-01","1984-01-01","1985-01-01","1985-01-01","1985-01-01","1985-01-01","1985-01-01","1985-01-01","1986-01-01","1986-01-01","1986-01-01","1986-01-01","1986-01-01","1986-01-01","1987-01-01","1987-01-01","1987-01-01","1987-01-01","1987-01-01","1987-01-01","1988-01-01","1988-01-01","1988-01-01","1988-01-01","1988-01-01","1988-01-01","1989-01-01","1989-01-01","1989-01-01","1989-01-01","1989-01-01","1989-01-01","1990-01-01","1990-01-01","1990-01-01","1990-01-01","1990-01-01","1990-01-01","1991-01-01","1991-01-01","1991-01-01","1991-01-01","1991-01-01","1991-01-01","1992-01-01","1992-01-01","1992-01-01","1992-01-01","1992-01-01","1992-01-01","1993-01-01","1993-01-01","1993-01-01","1993-01-01","1993-01-01","1993-01-01","1994-01-01","1994-01-01","1994-01-01","1994-01-01","1994-01-01","1994-01-01","1995-01-01","1995-01-01","1995-01-01","1995-01-01","1995-01-01","1995-01-01","1996-01-01","1996-01-01","1996-01-01","1996-01-01","1996-01-01","1996-01-01","1997-01-01","1997-01-01","1997-01-01","1997-01-01","1997-01-01","1997-01-01","1998-01-01","1998-01-01","1998-01-01","1998-01-01","1998-01-01","1998-01-01","1999-01-01","1999-01-01","1999-01-01","1999-01-01","1999-01-01","1999-01-01","2000-01-01","2000-01-01","2000-01-01","2000-01-01","2000-01-01","2000-01-01","2001-01-01","2001-01-01","2001-01-01","2001-01-01","2001-01-01","2001-01-01","2002-01-01","2002-01-01","2002-01-01","2002-01-01","2002-01-01","2002-01-01","2003-01-01","2003-01-01","2003-01-01","2003-01-01","2003-01-01","2003-01-01","2004-01-01","2004-01-01","2004-01-01","2004-01-01","2004-01-01","2004-01-01","2005-01-01","2005-01-01","2005-01-01","2005-01-01","2005-01-01","2005-01-01","2006-01-01","2006-01-01","2006-01-01","2006-01-01","2006-01-01","2006-01-01","2007-01-01","2007-01-01","2007-01-01","2007-01-01","2007-01-01","2007-01-01","2008-01-01","2008-01-01","2008-01-01","2008-01-01","2008-01-01","2008-01-01","2009-01-01","2009-01-01","2009-01-01","2009-01-01","2009-01-01","2009-01-01","2010-01-01","2010-01-01","2010-01-01","2010-01-01","2010-01-01","2010-01-01","2011-01-01","2011-01-01","2011-01-01","2011-01-01","2011-01-01","2011-01-01","2012-01-01","2012-01-01","2012-01-01","2012-01-01","2012-01-01","2012-01-01","2013-01-01","2013-01-01","2013-01-01","2013-01-01","2013-01-01","2013-01-01","2014-01-01","2014-01-01","2014-01-01","2014-01-01","2014-01-01","2014-01-01","2015-01-01","2015-01-01","2015-01-01","2015-01-01","2015-01-01","2015-01-01","2016-01-01","2016-01-01","2016-01-01","2016-01-01","2016-01-01","2016-01-01","2017-01-01","2017-01-01","2017-01-01","2017-01-01","2017-01-01","2017-01-01"]},"markers":null,"annotations":null,"offset":"silhouette","interactive":true,"interpolate":"cardinal","palette":"Spectral","text":"black","tooltip":"black","x_tick_interval":10,"x_tick_units":"year","x_tick_format":"%Y","y_tick_count":5,"y_tick_format":",g","top":20,"right":40,"bottom":30,"left":50,"legend":true,"legend_label":"Fuente de inversión","fill":"brewer","label_col":"black","x_scale":"date","sort":true,"order":"none"},"evals":[],"jsHooks":[]}</script>

El hecho de que el resultado fuera un html y no una imagen me resultó un poco problemático: no pude compartirla en twitter con su versión interactiva. Pero por suerte aquí sí (y de paso leí un poco más sobre widgets en el libro [RMarkdown: The definitive guide).](https://bookdown.org/yihui/rmarkdown/html-widgets.html)

#### A mejorar:

El gráfico “de corriente” se ve muy lindo, pero es poco claro (de hecho, lo que se ve en el primer gráfico, que es la inversión federal, casi no se ve en el segundo). Es decir, las cantidades desproporcionadas deberían poder verse igual, a pesar de ser desproporcionadas. Por otro lado, el recuadro selector desapareció aquí, en RMarkdown, a pesar de que lo veo bien en el widget que descargo. No tengo idea de a qué se debe.
