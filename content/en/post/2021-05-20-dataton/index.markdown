---
title: Datatón - DataGénero
author: 'Macarena Quiroga'
date: '2021-05-20'
slug: dataton
categories: []
tags:
  - data
  - gender
  - datathon
  - rstats
  - english
subtitle: 'Transfeminist Datathon about Missing Data'
summary: 'Review of my participation during the event organized by Datagénero.'
authors: []
lastmod: '2021-05-20T21:06:34-03:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
# draft: false
---

Last Thursday, the 20th of June, I took part of the Transfeminist Datathon about Missing Data, organized by [DataGénero](https://www.datagenero.org/#/). The motto was *Without data equality, there is no gender equality*. To do so, four tables were implemented:

1. "Las chicas superpoderosas [Powerpuff Girls]": this table focused on women participation in legislative power. Work was divided in three areas: National Congress, Provincial Congress and regional picture in Latin America.
2. "Faltamos nosotres, campeón [We're missing, sport]": this table aimed to make visible the lack of official data about trans and non-binary people. In the main strands of work was mentioned the impact that this can have in these groups of people, the identification of missing data and the formulation of a work plan to resolve this issue.
3. "En cualquier lugar[Anywhere]": this tables asked about access to information about sexual and reproductive rights. The mail goal was to characterize quality and quantity indicators of this access and to analyze the regional picture in Latin America.
4. "Poder, ¿Poder? Poder Judicial [Power, ¿power? Legislative Power]": this table considered the debate over the role of the Legislative Power over our lives and how to think about data (and missing data) from a gender perspective.

***

The event started with a general introduction by [Ivana Feldfeber](https://twitter.com/ivanafeld), co-founder and general director of DataGénero, where we talked about the general framework of the project. Then, we went through the specific tables.

In my case, I joined the *Las chicas superpoderosas [Powerpuff girls]*. I'm no politics specialist and I'm not so fond of the ins and outs of the legislative chambers. But I can't deny that there's something about it that struck me. This table was led by [Carolina Glasserman Apicella](https://twitter.com/caroglassap): we introduced ourselves and we pick an area.

I chose National Congress area, for the only reason that it's the topic I know best. After talking about the different facets of the issue, and because we only had 50 minutes to work, we decided to focus on the composition of the permanent committees of the Cámara de Diputados [Chamber of Deputies]. We asked ourselves the following questions:

* How many committees have female presidents or vice-presidents?
* What percentage of men, women and dissident groups have each committee? 
* In which committee are there more women than men and viceversa?

On the basis of the information available at the [official website of the Chamber of Deputies](https://www.diputados.gov.ar/comisiones/index.html), we were able to create a [dataframe](https://docs.google.com/spreadsheets/d/1FwgJIDgD5COObM2uc0bVg2fk6YU5THD4Cj4xAjqRuNU/edit?usp=sharing).



```r
tibble(dipnac)
```

```
## # A tibble: 46 × 10
##      NUM COMISIONES         PRESIDENCIA TOTAL MUJERES `PORCENTAJE DE MU… VARONES
##    <dbl> <chr>                    <dbl> <dbl>   <dbl>              <dbl>   <dbl>
##  1     1 ASUNTOS CONSTITUC…           0    35      17               48.6      18
##  2     2 LEGISLACION GENER…           1    31      15               48.4      16
##  3     3 RELACIONES EXTERI…           0    43      17               39.5      26
##  4     4 PRESUPUESTO Y HAC…           0    49      13               26.5      36
##  5     5 EDUCACION                    1    35      24               68.6      11
##  6     6 CIENCIA, TECNOLOG…           0    30      15               50        15
##  7     7 CULTURA                      1    30      21               70         9
##  8     8 JUSTICIA                     0    30      12               40        18
##  9     9 PREVISIÓN Y SEGUR…           0    30      13               43.3      17
## 10    10 ACCIÓN SOCIAL Y S…           0    45      25               55.6      20
## # … with 36 more rows, and 3 more variables: PORCENTAJE DE VARONES <dbl>,
## #   DISIDENCIAS <lgl>, PORCENTAJE DE DISIDENCIAS <lgl>
```

The first question we were able to answer was **what happens with the committee presidency?** The answer is that there is a larger amount of committees with a male president (26) than with a female president (19), without considering the one committee that didn't specify its presidency.
<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

In the face of this, the second question we asked ourselves was **which are the committees with female presidents? What topics do they cover?**


```
## # A tibble: 19 × 10
##      NUM COMISIONES          PRESIDENCIA TOTAL MUJERES `PORCENTAJE DE M… VARONES
##    <dbl> <chr>               <labelled>  <dbl>   <dbl>             <dbl>   <dbl>
##  1     2 LEGISLACION GENERAL 1              31      15              48.4      16
##  2     5 EDUCACION           1              35      24              68.6      11
##  3     7 CULTURA             1              30      21              70         9
##  4    11 FAMILIAS, NIÑEZ Y … 1              31      28              90.3       3
##  5    12 DE LAS PERSONAS MA… 1              31      20              64.5      11
##  6    13 LEGISLACION PENAL   1              30      13              43.3      17
##  7    14 LEGISLACION DEL TR… 1              31      15              48.4      16
##  8    18 FINANZAS            1              31       8              25.8      23
##  9    20 COMERCIO            1              30       8              26.7      22
## 10    25 ASUNTOS MUNICIPALES 1              31      17              54.8      14
## 11    26 INTERESES MARITIMO… 1              30       8              26.7      22
## 12    27 COMISIÓN DE VIVIEN… 1              31      11              35.5      20
## 13    29 JUICIO POLÍTICO     1              30      14              46.7      16
## 14    32 ECONOMÍA            1              31      10              32.3      21
## 15    33 MINERÍA             1              30       7              23.3      23
## 16    39 ASUNTOS COOPERATIV… 1              31      12              38.7      19
## 17    43 SEGURIDAD INTERIOR  1              31       8              25.8      23
## 18    45 DISCAPACIDAD        1              30      20              66.7      10
## 19    46 MUJERES Y DIVERSID… 1              30      25              83.3       5
## # … with 3 more variables: PORCENTAJE DE VARONES <dbl>, DISIDENCIAS <lgl>,
## #   PORCENTAJE DE DISIDENCIAS <lgl>
```
Broadly speaking, we can see that the topics are diverse: committees with social topics (Education, Culture, Family, childhood and youth, About older people, Housing Committee, Cooperative affairs, Disability, Women and diversity), economy and production topics (Finances, Commerce, Economy, Mining), legal and legislative topics (General, Criminal and Work Legislation, Impeachments) and state topics (Municipal affairs, Marine interests and Homeland security).

The third question we asked ourselves was related to the composition of those committees: **how many men and how many women does each committee has?**

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />
Of the 46 committees, only 11 of them have more women than men in their composition. **How is the distribution of the presence of women in those committees?**


```
## # A tibble: 46 × 10
##      NUM COMISIONES         PRESIDENCIA TOTAL MUJERES `PORCENTAJE DE MU… VARONES
##    <dbl> <chr>              <labelled>  <dbl>   <dbl>              <dbl>   <dbl>
##  1    11 FAMILIAS, NIÑEZ Y… 1              31      28               90.3       3
##  2    46 MUJERES Y DIVERSI… 1              30      25               83.3       5
##  3     7 CULTURA            1              30      21               70         9
##  4     5 EDUCACION          1              35      24               68.6      11
##  5    45 DISCAPACIDAD       1              30      20               66.7      10
##  6    12 DE LAS PERSONAS M… 1              31      20               64.5      11
##  7    28 PETICIONES, PODER… 0              31      19               61.3      12
##  8    44 LIBERTAD DE EXPRE… 0              31      18               58.1      13
##  9    10 ACCIÓN SOCIAL Y S… 0              45      25               55.6      20
## 10    25 ASUNTOS MUNICIPAL… 1              31      17               54.8      14
## # … with 36 more rows, and 3 more variables: PORCENTAJE DE VARONES <dbl>,
## #   DISIDENCIAS <lgl>, PORCENTAJE DE DISIDENCIAS <lgl>
```
When we look at those committees that have more than 50% women members, we found historically feminized topics: childhood, adolescence and youth, elder and disabled people care, attention to diversities, culture and education. If we look at the graphic the other way, the conclusion is the same:


```
## # A tibble: 46 × 10
##      NUM COMISIONES          PRESIDENCIA TOTAL MUJERES `PORCENTAJE DE M… VARONES
##    <dbl> <chr>               <labelled>  <dbl>   <dbl>             <dbl>   <dbl>
##  1    15 DEFENSA NACIONAL     0             31       5              16.1      26
##  2    23 TRANSPORTES          0             31       5              16.1      26
##  3    16 OBRAS PUBLICAS      NA             31       7              22.6      24
##  4    33 MINERÍA              1             30       7              23.3      23
##  5    17 AGRICULTURA Y GANA…  0             35       9              25.7      26
##  6    18 FINANZAS             1             31       8              25.8      23
##  7    43 SEGURIDAD INTERIOR   1             31       8              25.8      23
##  8     4 PRESUPUESTO Y HACI…  0             49      13              26.5      36
##  9    20 COMERCIO             1             30       8              26.7      22
## 10    26 INTERESES MARITIMO…  1             30       8              26.7      22
## # … with 36 more rows, and 3 more variables: PORCENTAJE DE VARONES <dbl>,
## #   DISIDENCIAS <lgl>, PORCENTAJE DE DISIDENCIAS <lgl>
```
Committees with the less female members deal with topics like military organization, homeland security, transportation and public works infrastructure, mining production, agriculture, finances, budgets and trade.

The last question we asked ourselves was: **where are the dissident groups in the committees?** And the answer was unambiguous:


```r
sum(dipnac$DISIDENCIAS)
```

```
## [1] NA
```
The presence of dissident groups in the committees is **NA** ("Not Available"). There are no records of gender dissident groups in the committees. And, as it was said by DataGénero: data is people and the presence of official data says a lot about those issues that interests the organizations that recollect them.

***

This brief descriptive analysis of the committees composition ends here. There's still a lot to think about, but the key is to understand that the debates in the legislative chambers are "genderized". The bias is present: if there aren't women in the committees, how can we contribute to the discussion? What happens with representation? What positive or negative effects has the launch of the gender parity law?

With these questions on mind, during the next publications I will ask myself:
1. To which parties does the women deputies belong?
2. How are women allocated across the committees? Are there female and male deputies that belong to the same committees?
3. How many deputies seats renew in the next term of office? How many of them belong to women?
