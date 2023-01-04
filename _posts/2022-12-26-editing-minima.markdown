---
layout: post
title:  "Editing Minima"
categories: updates
tags: design jekyll css
image: assets/images/2022-12-26-theme-change.jpg
---

{% comment %} primero tuve que salir del master del repositorio e ir a la version "stable"

luego copie los archivos de la carpeta _sass y el main.scss de la carpeta assets. Creo que lo voy a modificar en el origen, y no en el main. {% endcomment %}

I had already prepared [a mood board, a color palette]({% post_url 2022-12-18-mood-board %}) and selected [a font]({% post_url 2022-12-22-fonts %}). Today was time to figure out how to apply changes to the minima theme.

From the research I did, there are many different ways of approaching customizations to the theme. I went with this method (works for me for now - might change it in the future):

1. Downloaded the _sass folder from the [minima "2.5-stable" branch in the remote repo](https://github.com/jekyll/minima/tree/2.5-stable).
2. I put that that folder in the corresponding location in my repo. Any file in my repository matching name & location with the theme original file will be used instead of the theme's default file ([same logic applied here]({% post_url 2022-12-20-liquid-feature-image %})).
3. I applied changes to font, text and background color in _sass/minima.scss, and to code formatting in _sass/minima/base.scss.

I am starting to see the feel of the mood board in the site. Still far away from having the design completed.

I think I might not be doing the css changes in the strictly most orderly way. But I will come back to it soon and improve it. Today it just feels great to see some changes in the style.

It's a good moment to to raise that the design is a bit inspired in the [advent of code webpage](https://adventofcode.com/).

