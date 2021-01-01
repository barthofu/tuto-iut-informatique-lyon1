# Tuto Git

Ce tuto n'est pas destiné à comprendre comment git marche, mais à mettre en place un environnement propice à sa bonne utilisation :smile:

Petit rappel tout de même des commandes basiques importantes de git en **local** :

- `git add -A` : valide les changements que tu as opéré sur tes fichiers (le `-A` valide d'un coup tous les changements de tous les fichiers). Vois ça comme 2 boites : votre boite dite **unstaged** (en gros ce qui n'est pas encore validé, dès que tu fais des changements ils vont dans cette boite là) et la boite **staged** dans laquelle vont être déplacé les changements précédemment situés dans la boite unstaged via cette commande `add`.
- `git commit -m "ajout du header"` : la commande principale de git qui vous permet de sauvegarder pour de bon tous les changements validés présents dans la boite **staged**. En gros, vois ça comme un checkpoint qui crée une sauvegarde de ton projet quand tu effectues la commande. Comme pour n'importe quel point de sauvegarde dans un jeu tu pourras y revenir plus tard, et faire d'autres opérations qu'on ne détaillera pas ici. Plus tu fais de commit, mieux c'est (vous voyez peut-être pas intérêt actuellement mais ça deviendra plus clair quand tu commenceras à travailler sur des projets à plusieurs).

Tout ça, que ce soit l'historique des différentes versions de ton projet créées lors de commits, les branch (qu'on a pas détaillé ici), etc sont contenus dans un sous dossier `.git` de ton projet. Ce dossier, c'est ce qui permet de transformer ton simple "dossier" de projet en "dépôt" (ou **repo** en anglais) que git et toutes les applications/systèmes liés peuvent reconnaître.

C'est bien beau tout ce bazar mais là on est encore tout en local sur ton ordinateur, on sait toujours pas bien comment fonctionne tout l'aspect **remote** de git.

Une remote, ça va tout simplement être un serveur en ligne qui va héberger ton repo. Au lieu qu'il soit sur ton ordinateur, il sera (à l'identique) sur un serveur. Les hébergeurs les plus connus sont *Github*, *Gitlab*, *Gitbucket* ou encore le plus stylé de tous : *Gitdab* (oui ça existe).

Dans ce tuto on va approfondir avec le cas de github, puis dans une deuxième partie on va y ajouter gitlab :wink:



## Github

Premièrement, il te faut un compte github.

Ensuite, tu vas te rendre dans l'onglet "Your repositories" (= tes repos) puis cliquer sur "new". Tu vas ensuite renseigner son nom (pas d'espace, on met des tirets à la place), mettre une description si tu le souhaites puis le créer. 

Là ça va t'afficher plein de trucs un peu osef, tu peux dès à présent *ouvrir un cmd*.

Une fois le cmd ouvert, rends-toi dans ton dossier de projet avec la commande `cd C:\chemin\vers\ton\projet` .

Si ton dossier de projet n'est pas déjà un repo git, initialise le avec la commande `git init`, puis met un fichier random (tu peux mettre un .txt par exemple) et faire un premier commit (appelé "Initial commit" généralement).

Tu as donc maintenant 2 entités : 

- ton repo local, qui est le dossier dans lequel il y a ton projet entier.
- ton repo dit **remote** (expliqué précédemment) qui est hébergé sur github mais qui est aussi totalement vide.

Le but ça va donc être de copier ce qu'il y a sur ton repo local vers ton repo remote.

Pour se faire, on va commencer par ajouter la remote à la configuration de ton repo local avec la commande suivante :

```bash
git remote add origin https://github.com/tonpseudogithub/nomdetonrepo.git
```

(le .git à la fin est important)

Ok maintenant ton repo local est bien lié à ton repo remote. 
Tu peux remarquer avec la commande `git branch -a` que tu as désormais 2 branches :

- main
- remotes/origin/main

Où **main** est la version locale de ton projet et **remotes/origin/main** est la version à distance pointant vers ton repo hébergé sur github.

Maintenant que tout est lié, il ne reste plus qu'à "copier" avec la commande :

```bash
git push origin main
```

Push signifie *pousser* en français. On va littéralement pousser la version locale de notre repo sur la remote. 

Au moment où tu vas effectuer la commande, windows devrait t'afficher une pop-up (ou alors te rediriger vers une page web) te demandant de te connecter sur github. C'est normal, actuellement le système git installé sur ton ordinateur ne sait absolument que c'est toi qui essaie de push vers la remote. Tu le sais peut-être déjà, mais n'importe qui peut récupérer ton repo remote depuis github (sauf si celui-ci est en privé mais il faut github premium pour ça), donc il faut bien qu'il sache que c'est toi qui essaie de push (les identifiants seront ensuite sauvegardés sur ton ordinateur t'inquiètes pas y'en a pas besoin à chaque fois).

Une fois fait, le repo devrait se push tranquillou.

Tu peux maintenant aller voir ton repo sur github et, magie, il sera indentique à ton repo local !

Maintenant imaginons que tu as un deuxième ordinateur (ordi 2) et que tu veuilles continuer à coder avec après avoir bossé sur ton ordi 1. 
Il te faudra donc :

- avant de quitter ordi 1, fait un **push**

- si tu n'as pas encore ton repo sur ton ordi 2 :

  - rends-toi dans le dossier où tu veux mettre ton projet puis effectue la commande : `git clone https://github.com/tonpseudogithub/nomdetonrepo.git`
  - si tu n'as jamais connecté ton git avec ton github sur ordi 2 : fait un push (même si c'est dans le vide vu que tu as déjà la version la plus récente du repo) pour te connecter avec tes identifiants sur github.

- si tu as déjà le repo sur ton ordi 2 et que git est déjà connecté à github :

  - ```bash
    git pull origin main
    ```

    Pull (*retirer* en anglais) est exactement l'inverse du push : il va copier le repo distant sur votre repo local, pour récupérer la dernière version de ce dernier (on aura donc les changements qui ont été précédemment push sur ordi 1)

Une fois avoir fini de coder sur l'ordi 2, refaites les mêmes étapes mais à l'inverse (push sur ordi 2 puis pull sur ordi 1) et tu auras tout le temps la dernière version de votre projet qu'importe l'ordinateur où tu te trouves :wink:

## GitKraken

Mais tu te dis peut-être : ça serait cool d'avoir une belle interface graphique qui montre l'arbre des commits (liste tous les commits quoi), qui permette de stage (= add) et de commit facilement les changements, ou encore de push/pull avec un seul bouton.

C'est là que *GitKraken* intervient !

Télécharge le via [ce lien](https://www.gitkraken.com) puis une fois installé et lancé, connecte toi à ton compte github (dans *settings* -> *integrations* -> *github*).

Tu pourras ensuite effectuer tout un pannel d'actions via le menu principal : créer un repo local ou distant (sur github par exemple), ouvrir un repo déjà existant, en cloner un, etc

Ici nous allons choisir l'option *open a repo* puis sélectionner notre repo local. Une fois ouvert tu devrais avoir une interface un peu comme celle ci :

![image-20201217202825318](https://i.imgur.com/L2WbCB3.png)



La zone principale de l'interface présente *l'arbre des commits*, en gros c'est l'historique de chaque commit.

Explication plus détaillée de l'interface :

1. WIP ça veut dire Work in Progress. En gros c'est tous les changements non "commités", qu'ils soient validé ou non dans la boite **staged**.
2. Cette zone de l'écran te permets de **stage** les changements. Le bouton "stage all files", permet, assez explicitement, de stage les changements de tous tes fichiers. Une fois appuyé, tu verras tous les éléments présents dans la boite "unstaged files" se déplacer dans la boite "staged files".
3. Tu devras ici préciser le titre de ton commit (équivalent à ce que tu mettais après le -m avec la commande `commit`) voire même une description si t'es deter (pas du tout obligatoire).
4. Les fameux boutons pour push/pull. 
5. Ici s'affiche le nom de la branche (main dans notre cas). L'icône d'ordinateur signifie que c'est à cet endroit que ce site notre version locale, quant-à la petite image à gauche il s'agit de la photo de profil github qui indique donc que c'est également là que se situe la version distante de notre repo hébergée sur github.

Normalement avec ces informations tu es désormais paré à utilisé GitKraken ~~presque~~ comme un pro !



## GitKraken + GitLab universitaire

L'université n'utilise pas le gitlab classique, mais une version spécifique à eux et hébergée sur leurs propres serveurs (c'est pour cela qu'on s'y connecte via l'url https://forge.univ-lyon1.fr). 

Tu peux t'y connecter simplement via ligne de commande en suivant le même procédé que pour github (quand il te demander tes identifiants renseigne ton numéro étudiant commençant par **p** et ton mot de passe sésame).

Cependant, la version gratuite de GitKraken ne propose pas ce service (*settings* -> *integrations* -> *gitlab self-managed* et tu veras que ça te demande d'upgrade en pro) mais pas de panique ! Il y a une solution à tout :wink:

En effet il existe un magnifique pack fait par github et nommé sobrement **Github Student Pack** qui réunis des dizaines et des dizaines d'offres étudiantes en rapport avec l'informatique. Et dans ces offres il se trouve que GitKraken version pro est disponible !

Etapes à suivre pour l'activer :

1. Rends-toi sur [ce lien](https://education.github.com/pack).
2. Clique sur *Get your Pack*.
3. Cela va te mener sur une fenêtre te proposant de choisir quelle adresse mail utiliser, il faudra en **ajouter une nouvelle** puis cliquer sur le petit **here** en bleu qui est un lien menant à tes paramètres github.
4. Une fois dans les paramètres github, **rajoute ton adresse universitaire**.
5. Va ensuite la confirmer sur ta boite mail universitaire.
6. Une fois tout ceci fait, tu peux fermer cet onglet et retourner sur notre onglet du student pack sans oublier de le **rafraichir**.
7. Si tout se passe bien, ton adresse mail universitaire devrait apparaître.
8. Il ne te reste plus qu'à renseigner la zone de texte qui te demande pourquoi tu veux ce pack, dit juste par exemple "*for school projects*".
9. Confirme.
10. Et maintenant attend (ça peut pas prendre quelques heures voir 1 journée). Github t'enverra un message de confirmation par mail sur la boite principale de ton compte github (pas sur ton adresse universitaire).
11. Une fois activé, rends-toi à nouveau dans les paramètres de GitKraken, puis dans *integrations* et enfin dans *GitLab Self-Managed*.
12. Clique maintenant sur "get premium" et re-connectes toi avec github.
13. Tu devrais maintenant avoir accès.

Maintenant que tu as GitKraken Pro (et au passage le pack étudiant github contient la version premium de github, donc tu pourras créer des repo **privés** sur github), il reste plus qu'à y connecter ton compte GitLab :

1. Rends-toi sur ce lien : https://forge.univ-lyon1.fr
2. Connectes-toi à ton compte universitaire (pXXXXXXX en identifiant et ton mot de passe sésame).
3. *settings* -> *access tokens*
4. Crée un nouveau token comme ceci :
   - Name : *GitKraken*
   - Expires at : *une date random dans à peu près 2 ans*
   - Coche : *api* et *read_user*
5. Une fois créé, copie le et colle le sur gitkraken (*settings* -> *integrations* -> *gitlab self-managed*)

Tu peux maintenant utiliser GitKraken avec le gitlab de l'université !

