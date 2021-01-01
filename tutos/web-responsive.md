# Tuto Responsive

Il y a trois aspects à comprendre et maitriser pour faire du responsive :

- utiliser des unités variables au lieu d'unités absolues (fixes comme le px ou le pt par exemple) :

  - vh -> pourcentage de la hauteur de la fenêtre (40vh correspond à 40% de la hauteur de la fenêtre par exemple)
  - vw -> pareil que vh mais pour la longueur
  - % -> wallah je comprends pas comment ça marche cette merde

- utiliser clamp(). C'est une méthode qui prend 3 arguments : **clamp(a, b, c)** où chaque argument est une taille. **b** est la taille variable tandis que **a** et **c** sont des tailles fixes (px, rem, etc) définissant le minimum (a) et le maximum (b). C'est extrêmement utile puisque mettre uniquement une taille variable peut poser des problèmes (beaucoup trop petit ou beaucoup trop grand) et il est très important de pouvoir définir des limites.

  ex : `font-size: clamp(0.7rem, 2vw, 2rem);`

- utiliser les media queries. Une media query c'est quelque chose comme ça : 

  ```css
  body {
      background-color: blue;
  }
  
  @media (max-width: 728px) {
      
      body {
          background-color: red;
      }
  }
  ```

  Cela permet de définir des règles qui ne s'appliqueront que lorsqu'une certaine "condition" est respectée. Dans cet exemple, si la longueur de l'écran est en dessous de 728px, le background du body changera du bleu au rouge.

  Pour savoir quelle max-width mettre pour quel résolution d'écran, il faut utiliser la console de développement en utilisant f12 (ou clic droit -> inspecter l'élément) sur une page web. 
  
  Il ne vous reste plus qu'à cliquer sur cet icone en haut à gauche de la console : ![image-20210101224831961](https://i.imgur.com/02hmpmg.png)
  
  
  
  Ce qui devrait vous donner une interface de ce style : 
  
  ![image-20210101224924910](https://i.imgur.com/Dk7Yi4i.png)
  
  
  
  Il ne vous reste plus qu'à cliquer sur les différents segments de cette barre pour voir comment le site que tu fais réagis en fonction des différentes tailles :
  
  ![image-20210101225020979](https://i.imgur.com/gKCo3Qd.png)





Maintenant que vous connaissez ces outils, voici dans quelles situations les utiliser :

- les media queries s'utilisent si on veut changer une règle CSS en fonction de la taille de l'écran. Par exemple, quelque chose affiché en flexbox avec une direction **row** en taille desktop sera souvent affiché en direction **column** en taille mobile. Ou encore si un élément doit disparaitre en vue mobile (par exemple du texte informatif assez long et pas très important).
- clamp() s'utilise un peu de partout, surtout en ce qui concerne la taille des textes et des images. Il peut aussi être utilisé dans une certaine mesure avec les *margin* et les *padding*
- il faut mieux utiliser des unités variables au maximum.