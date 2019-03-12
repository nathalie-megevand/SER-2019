

# SER Laboratoire 1

Nathalie Mégevand & David Simeonovic


## Introduction


## DTD + choix

Une liste de participants avec une id permet de s'y référer par la suite grâce à une attribut IDREF sans redondance. 

Deplacement : Piece, Elimation, Promotion, Situation en tant qu'attribut afin de contrôler les valeurs possibles.

Similairement Roque vide, mais avec un attribut Type.

## Capture d'écran (XML respecte DTD)

## Réponses au questions

### Imaginons que vous souhaitez enregistrer le classement ELO que chaque joueur d’une partie avait au moment où elle a été jouée, qu’est-ce qu’il faudrait modifier dans votre DTD ?

Il suffit d'ajouter un élément <ELO passe> </ELO passe> à l'élément Participant.

### Est-ce possible dans votre DTD de représenter le fait qu’il ne peut y avoir que 20 parties au maximum dans un tournoi ? Si oui, comment ?

Il est possible de définir dans la DTD que le tournoi contient vingt fois la balise partie de manière optionnelle : <!ELEMENT tournoi (partie, partie?, partie? etc.
Mais pour être honnête c'est plutôt moche, autant faire cette vérification avant/après avoir parsé le document.

### Est-ce possible dans votre DTD de représenter le fait que les 2 joueurs d’une partie doivent être différents ? Si oui, comment ?
Dans la manière dont nous avons implémenter les joueurs cela n'est pas possible. Car les balise Nom et Prenom peuvent contenir n'importe quoi car elle ont été définie comme contenant des #CDATA.


## Conclusion
La principale chose à retenir de ce laboratoire est que la DTD nous permet le contrôle sur une certaine structure du document XML, mais pas sur son véritable contenu, ni sur sa cohérence.
Dans notre exemple il n'y a aucun moyen de s'assurer que les coups soient légaux ou même que le bon type de donnée soit rentré. Il est, par exemple, possible de rentrer la valeur "A" pour l'heure du tournois ou même "1234" pour le nom d'un participant. Les attributs permettent un certains contrôle sur les valeurs entrées grâce aux valeurs énumérées entrées dans la DTD.
Au final, tout le travail de validité et de cohérence devra être fait par le parseur. Néanmoins ce format permet justement de créer un parseur en définissant une structure clair que le parseur pourra interpréter.
