---
title: Datatón - DataGénero
author: 'Macarena Quiroga'
date: '2021-05-20'
slug: dataton
categories: []
tags: [datos]
subtitle: 'Datatón Transfeminista sobre Datos Faltantes'
summary: ''
authors: []
lastmod: '2021-05-20T21:06:34-03:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
draft: true
---

El pasado jueves 20/5 participé del Datatón Transfeminista sobre Datos Faltantes organizado por [DataGénero](https://www.datagenero.org/#/). El lema central fue *Sin igualdad de datos, no hay igualdad de género*. Para eso, se propusieron cuatro mesas:
1. "Las chicas superpoderosas": esta mesa se focalizó en la participación de las mujeres en el poder legislativo. Se dividó el trabajo en tres áreas: Congreso Nacional, Congresos Provinciales y panorama regional de América Latina.
2. "Faltamos nosotres, campeón": esta mesa apuntó a visibilizar la ausencia de datos oficiales sobre la población trans y no binaria. Dentro de las líneas de trabajo se plantea el impacto que esto puede tener en las vidas de las personas que pertenecen a estos grupos, la identificación de los datos faltantes y la definición de un plan de trabajo para resolver esta problemática.
3. "En cualquier lugar": esta mesa se preguntó por el acceso a la información sobre los derechos sexuales y reproductivos. Como objetivo, se propusieron caracterizar los indicadores de la cantidad y la calidad de este acceso y su cumplimiento, el procesamiento de los datos existentes y analizar la situación regional de América Latina.
4. "Poder, ¿Poder? Poder Judicial": esta mesa planteó el debate sobre el rol que tiene el Poder Judicial en nuestras vidas y cómo impacta su federalismo en las problemáticas específicas de mujeres y personas LGBTI+. Nuevamente, el foco central está en preguntarnos la cantidad y la calidad de los datos disponibles, y cómo apuntar a pensar los datos (y su falta) desde una perspectiva de género.

***

Empezamos con una presentación general a cargo de [Ivana Feldfeber](https://twitter.com/ivanafeld), co-fundadora y directora general de DataGénero, donde charlamos acerca del encuadre general del proyecto. Luego, pasamos a las mesas específicas.

En mi caso, yo me sumé a la mesa *Las chicas superpoderosas*. No soy especialista en política ni mucho menos en los tejes y manejes de las cámaras legislativas. Pero no puedo negar que hay algo de la dinámica que me llama la atención. Esta mesa estuvo liderada por [Carolina Glasserman Apicella](https://twitter.com/caroglassap): nos presentamos y elegimos un área. 

Elegí el área de Congreso Nacional, por la sola razón de que conozco más nombres. Luego de charlar acerca de las distintas aristas del tema, dado que teníamos solo 50 minutos para trabajar, decidimos enfocarnos en la conformación de las comisiones permanentes dentro de la Cámara de Diputados. Nos hicimos las siguientes preguntas:
* ¿Cuántas comisiones tienen presidentas o vicepresidentas mujeres?
* ¿Qué cantidad de mujeres, de hombres y de disidencias tiene cada comisión? ¿Qué porcentaje del total conforman?
* ¿En qué comisiones hay más cantidad de mujeres que de hombres y viceversa?

A partir de la información disponible en el [sitio web oficial de la Cámara de Diputados](https://www.diputados.gov.ar/comisiones/index.html), pudimos confeccionar [una base de datos](https://docs.google.com/spreadsheets/d/1FwgJIDgD5COObM2uc0bVg2fk6YU5THD4Cj4xAjqRuNU/edit?usp=sharing).



```r
tibble(dipnac)
```

```
## # A tibble: 46 x 10
##      NUM COMISIONES         PRESIDENCIA TOTAL MUJERES `PORCENTAJE DE MU~ VARONES
##    <dbl> <chr>                    <dbl> <dbl>   <dbl>              <dbl>   <dbl>
##  1     1 ASUNTOS CONSTITUC~           0    35      17               48.6      18
##  2     2 LEGISLACION GENER~           1    31      15               48.4      16
##  3     3 RELACIONES EXTERI~           0    43      17               39.5      26
##  4     4 PRESUPUESTO Y HAC~           0    49      13               26.5      36
##  5     5 EDUCACION                    1    35      24               68.6      11
##  6     6 CIENCIA, TECNOLOG~           0    30      15               50        15
##  7     7 CULTURA                      1    30      21               70         9
##  8     8 JUSTICIA                     0    30      12               40        18
##  9     9 PREVISIÓN Y SEGUR~           0    30      13               43.3      17
## 10    10 ACCIÓN SOCIAL Y S~           0    45      25               55.6      20
## # ... with 36 more rows, and 3 more variables: PORCENTAJE DE VARONES <dbl>,
## #   DISIDENCIAS <lgl>, PORCENTAJE DE DISIDENCIAS <lgl>
```

La primera pregunta que podemos responder es: **¿qué pasa con las presidencias de las comisiones?** La respuesta es que hay una mayor cantidad de comisiones presididas por hombres (26) que por mujeres (19), sin contar una comisión cuya presidencia no está especificada.
<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

Frente a esto, la segunda pregunta que podemos hacernos es **¿cuáles son las comisiones que tienen presidentas mujeres? ¿De qué asuntos se ocupan?**


```
## # A tibble: 19 x 10
##      NUM COMISIONES          PRESIDENCIA TOTAL MUJERES `PORCENTAJE DE M~ VARONES
##    <dbl> <chr>               <labelled>  <dbl>   <dbl>             <dbl>   <dbl>
##  1     2 LEGISLACION GENERAL 1              31      15              48.4      16
##  2     5 EDUCACION           1              35      24              68.6      11
##  3     7 CULTURA             1              30      21              70         9
##  4    11 FAMILIAS, NIÑEZ Y ~ 1              31      28              90.3       3
##  5    12 DE LAS PERSONAS MA~ 1              31      20              64.5      11
##  6    13 LEGISLACION PENAL   1              30      13              43.3      17
##  7    14 LEGISLACION DEL TR~ 1              31      15              48.4      16
##  8    18 FINANZAS            1              31       8              25.8      23
##  9    20 COMERCIO            1              30       8              26.7      22
## 10    25 ASUNTOS MUNICIPALES 1              31      17              54.8      14
## 11    26 INTERESES MARITIMO~ 1              30       8              26.7      22
## 12    27 COMISIÓN DE VIVIEN~ 1              31      11              35.5      20
## 13    29 JUICIO POLÍTICO     1              30      14              46.7      16
## 14    32 ECONOMÍA            1              31      10              32.3      21
## 15    33 MINERÍA             1              30       7              23.3      23
## 16    39 ASUNTOS COOPERATIV~ 1              31      12              38.7      19
## 17    43 SEGURIDAD INTERIOR  1              31       8              25.8      23
## 18    45 DISCAPACIDAD        1              30      20              66.7      10
## 19    46 MUJERES Y DIVERSID~ 1              30      25              83.3       5
## # ... with 3 more variables: PORCENTAJE DE VARONES <dbl>, DISIDENCIAS <lgl>,
## #   PORCENTAJE DE DISIDENCIAS <lgl>
```
A grandes rasgos podemos ver que las temáticas son muy variadas: comisiones de temáticas sociales (Educación, Cultura, Familia, niñez y juventud, De las personas mayores, Comisión de vivienda, Asuntos cooperativos, Discapacidad, Mujeres y diversidad), de economía y producción (Finanzas, Comercio, Economía, Minería), de asuntos jurídico-legislativos (Legislación General, Penal y del Trabajo, Juicio Político) y estatales (Asuntos Municipales, Intereses Marítimos y Seguridad Interior).

La tercera pregunta que nos hacemos apunta a la composición de esas comisiones: **¿cuántos varones y cuántas mujeres componen cada una?**


```
## Warning: Removed 46 rows containing missing values (position_stack).
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />
De las 46 comisiones, solo 11 tienen más mujeres que hombres en su composición. **¿Cómo se distribuye la presencia de mujeres en las comisiones?**


```
## # A tibble: 46 x 10
##      NUM COMISIONES         PRESIDENCIA TOTAL MUJERES `PORCENTAJE DE MU~ VARONES
##    <dbl> <chr>              <labelled>  <dbl>   <dbl>              <dbl>   <dbl>
##  1    11 FAMILIAS, NIÑEZ Y~ 1              31      28               90.3       3
##  2    46 MUJERES Y DIVERSI~ 1              30      25               83.3       5
##  3     7 CULTURA            1              30      21               70         9
##  4     5 EDUCACION          1              35      24               68.6      11
##  5    45 DISCAPACIDAD       1              30      20               66.7      10
##  6    12 DE LAS PERSONAS M~ 1              31      20               64.5      11
##  7    28 PETICIONES, PODER~ 0              31      19               61.3      12
##  8    44 LIBERTAD DE EXPRE~ 0              31      18               58.1      13
##  9    10 ACCIÓN SOCIAL Y S~ 0              45      25               55.6      20
## 10    25 ASUNTOS MUNICIPAL~ 1              31      17               54.8      14
## # ... with 36 more rows, and 3 more variables: PORCENTAJE DE VARONES <dbl>,
## #   DISIDENCIAS <lgl>, PORCENTAJE DE DISIDENCIAS <lgl>
```
Al mirar cuáles son las comisiones que tienen más del 50% de mujeres en su composición, encontramos temáticas históricamente feminizadas: las niñeces, adolescencias y juventudes, el cuidado de las personas mayores y con discapacidades, la atención a la diversidad, cultura y educación. Si miramos el gráfico de forma invertida, la conclusión es similar:


```
## # A tibble: 46 x 10
##      NUM COMISIONES          PRESIDENCIA TOTAL MUJERES `PORCENTAJE DE M~ VARONES
##    <dbl> <chr>               <labelled>  <dbl>   <dbl>             <dbl>   <dbl>
##  1    15 DEFENSA NACIONAL     0             31       5              16.1      26
##  2    23 TRANSPORTES          0             31       5              16.1      26
##  3    16 OBRAS PUBLICAS      NA             31       7              22.6      24
##  4    33 MINERÍA              1             30       7              23.3      23
##  5    17 AGRICULTURA Y GANA~  0             35       9              25.7      26
##  6    18 FINANZAS             1             31       8              25.8      23
##  7    43 SEGURIDAD INTERIOR   1             31       8              25.8      23
##  8     4 PRESUPUESTO Y HACI~  0             49      13              26.5      36
##  9    20 COMERCIO             1             30       8              26.7      22
## 10    26 INTERESES MARITIMO~  1             30       8              26.7      22
## # ... with 36 more rows, and 3 more variables: PORCENTAJE DE VARONES <dbl>,
## #   DISIDENCIAS <lgl>, PORCENTAJE DE DISIDENCIAS <lgl>
```
Las comisiones con menor cantidad de mujeres tratan temáticas como la organización militar y la seguridad interior, la infraestructura de transporte y de obrar públicas, y la producción minera, agropecuaria, las finanzas, el presupuesto y el comercio.

La última pregunta que nos hacemos es **¿dónde están las disidencias en las comisiones?** Y la respuesta es unívoca:


```r
sum(dipnac$DISIDENCIAS)
```

```
## [1] NA
```
La presencia de disidencias en las comisiones es **NA**. No hay registros de la presencia de disidencias dentro de las comisiones. Y como bien plantean desde DataGénero: los datos son personas y la presencia de datos oficiales dicen mucho sobre aquellas cuestiones sobre las cuales los organismos que los recopilan están interesados.


***

Este pequeño análisis descriptivo de la composición de las comisiones termina aquí. Hay mucho más por pensar, pero la clave está en ver que las discusiones siguen estando generizadas. El sesgo está presente: si no hay mujeres en las comisiones, ¿cómo podremos aportar a la discusión? ¿Qué pasa con la representatividad? ¿Qué efectos positivos o negativos tiene la apertura dada por la ley de paridad de género?
