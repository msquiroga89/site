---
title: 'Contribución al #TidyTuesday semana 34: comandos de voz en StarTrek'
author: 'Macarena Quiroga'
date: '2021-08-20'
slug: contribución-al-tidytuesday-semana-34-comandos-de-voz-en-startrek
categories: []
tags: 
  - rstats
  - tidytuesday
  - dataviz
  - español
subtitle: ''
summary: ''
authors: []
lastmod: '2021-08-20T08:59:39-03:00'
featured: no
image:
  caption: ''
  focal_point: 'left'
  preview_only: true
projects: []
---

¡Dos semanas al hilo! ¡Bien por mí! Decidí que voy a intentar participar todas las semanas del \#TidyTuesday, aunque sea un solo gráfico sencillo. Lo importante es sostener la práctica y, además, intentar elegir al menos **un área** que explorar en cada caso.

(Para quienes no sepan: \#TidyTuesday es un proyecto colaborativo que consiste en trabajar cada semana con un set de datos reales para practicar visualización y otras habilidades del mundo de la ciencia de datos. Pueden encontrar más información en su [repositorio de GitHub](https://github.com/rfordatascience/tidytuesday/blob/master/data/2021/2021-08-10/readme.md) y bajo el [hashtag en twitter](https://twitter.com/hashtag/TidyTuesday?src=hashtag_click).)

El dataset de esta semana está compuesto por los comandos de voz que utilizan los distintos personajes de StarTrek. Entiendo que debe haber sido una gran oportunidad para quienes trabajan con análisis de texto; yo, irónicamente, no tengo idea de eso, aunque me interesa. Y encima no vi StarTrek, así que tampoco tuve demasiados conocimientos previos como para saber cómo sacarle jugo a este dataset.

Por lo tanto, para ser fiel a mi objetivo, decidí hacer un gráfico simple: contar cuántos enunciados se emitieron, organizarlos por tipo de enunciado y dividirlo según el tipo de personaje que lo enunció (persona o computadora). A partir de eso, pensé qué modificaciones visuales podía incorporar. Entender bien cómo funciona `theme()` siempre fue un desafío; en general, intento elegir un theme que me gusta y quedarme con él, porque no tengo muchas habilidades visuales.

##### 

#### Entonces, ¿qué aprendí esta semana?

- Hice un [lollipop chart](https://www.r-graph-gallery.com/lollipop-plot.html); si bien ya los había usado anteriormente, esta vez me dediqué a leer un poco más sobre ellos. Aprendí que algunas personas consideran que el incremento en el atractivo visual del gráfico disminuye su precisión (porque el círculo de la punta es más impreciso que la línea recta de una barra).

- Modifiqué muchos componentes del tema: aprendí que una cosa es el color del fondo del gráfico y otro el fondo de toda la imagen. Cambié la tipografía y el tamaño de fuente de todo el gráfico; reforcé el funcionamiento de las etiquetas en gráficos faceteados.

- Aprendí la función `tidytext::reorder_within()`, que originalmente surgió de [este blogpost de Tyler Rinker](https://trinkerrstuff.wordpress.com/2016/12/23/ordering-categories-within-ggplot2-facets/) y luego incorporada al paquete `tidytext` (en [este post de Julia Silge](https://juliasilge.com/blog/reorder-within/) se explica con más detalle el proceso). Pero como con un gran poder viene una gran responsabilidad, esta función me duplicó las etiquetas de los factores (vaya une a saber por qué), así que tuve que modificarlas... a mano. En fin.


#### El código


```r
library(tidyverse)
library(tidytext)
library(ggthemes)

tuesdata <- tidytuesdayR::tt_load(2021, week = 34)
```

```
## 
## 	Downloading file 1 of 1: `computer.csv`
```

```r
computer <- tuesdata$computer

computer <- computer %>% 
  mutate_all(.funs = tolower) %>%  # para unificar filas
  mutate_if(is.character, as.factor)

computer$char_type <- factor(computer$char_type, levels = c("computer", "person"), 
                             labels = c("Computadora", "Persona")) # ordena

computer %>% 
  group_by(char_type, type) %>% 
  summarise(count = n()) %>%  # cantidad de comandos
  mutate(type = reorder_within(type, count, char_type)) %>% # ordenados por cantidad
  ggplot(aes(x=reorder(type, count), y = count))+
  geom_point(color = "red")+
  geom_segment(aes(x=reorder(type, count), xend =type, y=0, yend=count, color = "red"))+
  facet_wrap(~char_type, 
             scales = "free", # para que no haya espacios vacíos entre las facetas
             labeller = labeller( # título del facet
               Computadora = computer,
               Persona = person))+
  coord_flip()+
  scale_y_reordered()+ # reordena los elementos dentro del facet
  scale_x_discrete(labels = c("response___Computadora" = "Respuesta",
                              "alert___Computadora" = "Alerta",
                              "info___Computadora" = "Información",
                              "countdown___Computadora" = "Cuenta Regresiva",
                              "clarification___Computadora" = "Clarificación",
                              "progress___Computadora" = "Progreso",
                              "conversation___Computadora" = "Conversación",
                              "command___Persona" = "Orden",
                              "wake word___Persona" = "Palabra Raíz",
                              "statement___Persona" = "Declaración",
                              "question___Persona" = "Pregunta",
                              "conversation___Persona" = "Conversación",
                              "password___Persona" = "Contraseña",
                              "comment___Persona" = "Comentario"))+
  theme_few()+
  theme(plot.background = element_rect(fill = "black"), # fondo de la imagen
        panel.background = element_rect(fill = "black"), # fondo del gráfico
        axis.text = element_text(color = "white", size = 12), # texto de los ejes
        plot.title = element_text(color = "white", 
                                  size = 20, 
                                  hjust = 5.5), # título del gráfico
        plot.caption = element_text(color = "white"), # fuente
        legend.position = "none", # quito el cuadro de referencias
        text = element_text(family = "Kefa"), # tipografía de todo el gráfico
        panel.grid.major.x = element_line(size = 4), # achica el espacio entre ticks
        strip.text = element_text(size = 12) # tamaño de título de facet
  )+
  labs(x = "", y = "",
       title = "¿Qué tipo de enunciados genera cada uno?",
       caption = "Fuente: Speech Interactions | http://www.speechinteraction.org/TNG/ | @_msquiroga"
    )
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-1.png" width="672" />

¡Espero que les sirva!
