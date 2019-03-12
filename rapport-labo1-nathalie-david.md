

# SER Laboratoire 1

Nathalie Mégevand & David Simeonovic


## Introduction

Pour ce laboratoire, nous sommes mandater par la Fédération Suisse des Echecs. Nos travaille est de structurer et créer un document XML répondant à leur demande :   
    - La FSE souhaite enregistrer dans un document XML toutes les parties d'échecs ayant été jouées dans le cadre de différents tournois.

## DTD + choix

Nous avons choisie de mettre le FSE comme racine de notre xml car c'est l'organisation qui gère les tournois d'echecs. La balise FSE peut contenir 1 ou plusieurs tournois.

Nous avons ensuite le tournois. Il contient un nom, plusieurs participants, 0-1-plusieurs parties d'echecs ainsi qu'un vainqueur.

La balise participant a en attribut l'identifiant du joueur et contient les balise :   
    - Nom    
    - Prenom   
    - ELO (classement du joueur)   

La balise "parties" contient toutes les partie d'echecs du tournois. Chaque partie et séparé par la balise "partie".

Une partie contient en attribut le score (1-0 | 0.5-0.5 | 0-1). Elle stoque une balise "Date" qui renseigne la date et l'heure du début de la partie. Nous avons aussi une balise "arbitre" qui contient le nom et le prénom de l'arbitre. Nous avons les balise "Blanc" et "Noir" qui contiennent en attribut l'identifion de joueurs qui permet d'éviter de la redondance. Puis contient une balise coup qui stoque tous les coups de la partie.

Pour les déplacemenets, nous avons implémenter 2 types de balises :   
    - Deplacement   
    - Roque    
La balise "deplacement" comporte plusieurs attributs :   
    - Piece : permet de savoir le type de la pièce qui a excécuté le déplacement (pas obligatoire)  
    - Elimation : permet de savoir si le déplacement a engendré une elimination d'une pièce adverse (pas obligatoire)   
    - Promotion : permet de savoir si le déplacement a engendré une promotion (pas obligatoire)     
    - Situation : permet de savoir si le déplacement a engendré une echec et mat, match nulle (pas obligatoire)      
Nous avons choisie de les stocker en tant qu'attribut afin de contrôler les valeurs possibles

La balise "roque" est une balise vide et possède un seul attribut :   
    - Type : permet de savoir si c'est un petit ou un grand roque   

## Capture d'écran (XML respecte DTD)

![GitHub Logo](success.png)

## Réponses au questions

### Imaginons que vous souhaitez enregistrer le classement ELO que chaque joueur d’une partie avait au moment où elle a été jouée, qu’est-ce qu’il faudrait modifier dans votre DTD ?

Il suffit d'ajouter un élément <ELO passe> </ELO passe> à l'élément Participant.

### Est-ce possible dans votre DTD de représenter le fait qu’il ne peut y avoir que 20 parties au maximum dans un tournoi ? Si oui, comment ?

Il est possible de définir dans la DTD que le tournoi contient vingt fois la balise partie de manière optionnelle : <!ELEMENT tournoi (partie, partie?, partie? etc.
Mais pour être honnête c'est plutôt moche, autant faire cette vérification avant/après avoir parsé le document.

### Est-ce possible dans votre DTD de représenter le fait que les 2 joueurs d’une partie doivent être différents ? Si oui, comment ?
Dans la manière dont nous avons implémenter les joueurs cela n'est pas possible. Car les balise Nom et Prenom peuvent contenir n'importe quoi car elle ont été définie comme contenant des #CDATA.

## Conclusion
La principale chose à retenir de ce laboratoire est que la DTD nous permet le contrôle sur une certaine structure du document XML, mais pas sur son véritable contenu, ni sur sa cohérence. Dans notre exemple il n'y a aucun moyen de s'assurer que les coups soient légaux ou même que le bon type de donnée soit rentré. Il est, par exemple, possible de rentrer la valeur "A" pour l'heure du tournois ou même "1234" pour le nom d'un participant. Les attributs permettent un certains contrôle sur les valeurs entrées grâce aux valeurs énumérées entrées dans la DTD. Au final, tout le travail de validité et de cohérence devra être fait par le parseur. Néanmoins ce format permet justement de créer un parseur en définissant une structure clair que le parseur pourra interpréter.