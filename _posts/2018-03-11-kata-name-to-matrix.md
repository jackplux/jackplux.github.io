---
layout: post
published: true
title: kata-name-to-matrix
tags:
  - ruby
  - kata
---
J'aime bien faire des katas de programmation pour m'entrainer, j'utilise le site [Codewars](https://www.codewars.com) qui va à l'essentiel et propose de nombreux entrainements.

## Le kata name to matrix

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

J'aurais bien aimé la connaitre avant de débuter le Kata ;)
