---
layout: post
published: false
title: kata-name-to-matrix
---
J'aime bien faire des katas de programmation pour m'entrainer, j'utilise le site [Codewars](https://www.codewars.com) qui va à l'essentiel.

# Le kata name to matrix

Lien du kata : https://www.codewars.com/kata/5a91e0793e9156ccb0003f6e

Le but de ce Kata est de retourner une matric (`Array` d'`Array`) en fonction du `String` passé en entrée.
Example: "Bill" ==> [["B", "i"], ["l", "l"]]  
Example: "Frank" ==> [["F", "r", "a"], ["n", "k", "."], [".", ".", "."]]

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

Le dernier map est un peu trop verbeu à mon gout et l'instruction `uncompleted_matrix << [] if uncompleted_matrix.length != matrix_size` devrait pouvoir se faire avec. 