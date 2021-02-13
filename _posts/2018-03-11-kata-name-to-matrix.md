---
layout: post
published: true
title: Ne lisez pas encore ces textes
tags:
  - textes
  - kata
---
Ils sont du mec qui a inventé ce blog (ce qui m'a permis de le mettre en oeuvre) et je vais les mettre à jour dans quelques jours, dans quelques semaines, ou peut-être jamais allez savoir.

## En fait, de quoi s'agit-il ?

Prolixe publicateur de pages internet, je m'intéresse beaucoup aux CMS (Content Managment Systems) et mon vice premier est de tester les outils de publication de contenu web au point que certains me qualifient de serial testeur. LOL !
Cest comme cela que je suis tombé sur la page https://beautifuljekyll.com d'un certain Dean Attali qui propose un constructeur de site de son invention que je suis en train de tester.

Il y raconte que son site Web est alimenté par GitHub Pages / Jekyll et peut être créé gratuitement en moins de 5 minutes . Au sens propre mais ça reste à prouver. Cela fait au moins deux heures que j'ai commencé cette page. ;)

Bon, je n'ai pas encore tout compris, son truc ne fonctionne apparement qu'avec les outils Github (tout le monde ne sait pas s'en servir, je ne trouve pour le moment cela pas trés pratique, mais c'est sympa et donne une belle occasion d'apprendre quelque chose.

Demain, en principe, je vous raconterai comment ça fonctionne et publierai mon avis sur les avanages et les inconvénients.

En attendant, les textes qui suivent sont ceux de son blog que j'ai cloné mais que je garde pour le moment pour étudier le fonctionnement de son machin.

A suivre soon. :-)

**Textes d'origine**

Lien du kata : https://www.codewars.com/kata/5a91e0793e9156ccb0003f6e

Le but de ce Kata est de retourner une matrice (`Array` d'`Arrays`) en fonction du `String` passé en entrée.
Example: "Bill" ==> [["B", "i"], ["l", "l"]]  
Example: "Frank" ==> [["F", "r", "a"], ["n", "k", "."], [".", ".", "."]]

{: .box-warning}
**Warning:** Si vous voulez faire le kata, ne lisez pas la suite 

### Ma solution

Avec `x` le string à convertir en matrice,  ma solution est la suivante :

~~~ruby
def matrixfy(x)
  return "name must be at least one letter" if x.length == 0
  chars = x.chars
  matrix_size = Math.sqrt(chars.length).ceil
  uncompleted_matrix = chars.each_slice(matrix_size).to_a
  uncompleted_matrix << [] if uncompleted_matrix.length != matrix_size
  uncompleted_matrix.map{ |matrix_elment| matrix_elment.length != matrix_size ? matrix_elment + ('.' * (matrix_size - matrix_elment.size )).chars : matrix_elment }
end
~~~

Le dernier map est un peu trop verbeux à mon gout et l'instruction `uncompleted_matrix << [] if uncompleted_matrix.length != matrix_size` devrait pouvoir se faire en même temps qu'une autre opération.

### La solution "best practices" la plus upvote

Elle tient en une ligne:
~~~ruby
x.empty? ? "name must be at least one letter" : x.ljust((x.length ** 0.5).ceil ** 2, '.').each_char.each_slice((x.length ** 0.5).ceil).to_a 
~~~
Ce n'est pas la solution la plus explicite, mais elle tient en ligne et est élégante.

Et cela m'a permis de découvrir la foncion `ljust`:  
If integer is greater than the length of str, returns a new String of length integer with str left justified and padded with padstr; otherwise, returns str.

~~~
"hello".ljust(20)           #=> "hello               "
"hello".ljust(20, '1234')   #=> "hello123412341234123"
~~~

J'aurais bien aimé la connaitre avant de débuter le Kata 😉
