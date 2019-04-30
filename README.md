# siteDeFeurs

Lafleur est une application développée en PHP, celle-ci génère un panier électronique de fleurs de différents types.

Application fait avec une implémentation MVC (model view controller).

Pour faire fonctionner cette SUPER APPLI moche je l'avoue au niveau design :'( , il faudra importer la base de donnée (BDD) sur votre Wamp, mamp ...
Bien modifier si besoin (root ... et n'oublies pas de balancer ton PORT !) fichier util/class.pdoLafleur.inc.php

Il y aura peut-être une deuxième version à venir (pas sur !)

EXPLICATIONS :
Ce modèle de développement distingue 3 fonctionnalités:
1. LA VUE :
Représente ce qui est exposé à l'utilisateur, en général il s'agit de HTML statique ou généré par du php ; il y a deux sortes de vue :
* Les pages d'information navigables grâce à des liens
* Les formulaires de saisies d'informations ; ces formulaires peuvent être présentées à plusieurs reprises pour confirmation ou signalement d'erreurs.

Une vue propose une partie commune à chaque pase et des zones liées à la demande de l'utilisateur.(BANDEAU / MENU / CONTENU)

2. LE CONTROLLER :
Ce sont les controleurs qui vont être à l'écoute des requêtes de l'utilisateur et fournir ainsi la vue externe correspondante.
Pour celà, il faudra à tout moment connaître l'état de l'application c'est-à-dire le contexte de la demande: "le page demandée fait suite à quelle action précise
de l'utilisateur ?"
C'est au controleur de connaître l'étât applicatif en testant une variable qui sera nommée $action, provenant d'une reqête POST ou GET.
Ainsi le controleur se présentera souvent sous le format suivant:

$action = $_REQUEST['action'];
switch($action)
{
    case 'ceci' :
        include("vues/v_ceci.php");
        include("vues/v_encorececi.php");
     case 'cela'' :
        include("vues/v_cela.php");
}

On pourrait trouver qu'il y a parfois redondance d'instructions dans les controleurs; ceci est justifié par un désir de clarté dans la présentation des responsabilités
des options des controleurs.

3. LE MODEL
C'est la couche (bibliothèque) qui accède à la BDD, ici nous avons utilisé une classe PDO, dédiée à l'accès aux données.
Création d'un tableau en deux dimensions
La vue qui va utiliser cette fonction va parcourir le tableau et insérer du code HTML.

Cette technologie charge en mémoire un tableau de données (couche modèle),
le controleurs va fournir ce tableau à la vue qui parcours le tableau pour placer la couche de présentation (en HTML).
Ce fonctionnement a bien sur un coût en terme d'utilisation de ressources machine (prix à payer pour un développement plus cohérent)
Par contre ceci diminue les temps de connexion à la BDD. Les frameworks (zend, symfonie) qui mettent en oeuvre cette technologie de manière plus industrielle 
utilisent des mécanismes de cache (sur disque) oud de chargement partiels.
Dans la couche modèle peuvent figurer aussi des fonctions métiers, règles de gestion du contexte.

4. MISE EN OEUVRE DE L'APPLICATION
La page index joue le role de controleur principal; celui-ci de dispatcher vers les trois cas d'utilisation

5. DECMARCHE CONSEILLEE
   5.1 Définir les cas d'utilisation.

D'abord en décomposant l'application en petites fonctionalités (gérer un produit, éditer un état, passer une commande, etc...).
 Trouver les acteurs, dessiner le diagramme des cas d'utilisation.
   
   5.2 Préciser chaque cas d'utilisation

Indiquer textuellement les interactions entre l'utilisateur et le système ; par exemple le premier cas d'utilisation (consultation des produits ) pourrait se présenter ainsi :

Nom du cas : consulter les articles (fleurs)
Acteur : un internaute
Scénario normal (le plus fréquent)

1. L'internaute demande à consulter les articles
2. Le système retourne la liste des catégories
3. L'internaute sélectionne une catégorie
4. Le système retourne la liste des articles de la catégorie choisie

Scénario étendu
5. L'internaute demande à déposer un article dans son panier
6. le système ajoute l'article au panier

Scénario particulier
   6.1 L'article figure déjà dans le panier : le système en informe l'utilisateur


On remarque que l'on retrouvera bien les trois actions (en gras) présentes dans le contrôleur du cas d'utilisation.

De même pour la gestion du panier

Nom du cas : gérer le panier
Acteur : l'internaute
Scénario normal

1. L'internaute demande à voir son panier
2. Le système retourne la liste des articles du panier

Scénario étendu

3. L'internaute demande la suppression d'un article
4. Le système retire l'article du panier (après confirmation)
5. L'internaute demande à passer commande
6. Le système retourne un formulaire pour saisies
7. L'internaute remplit le formulaire et l'envoie
8. Le système enregistre la commande

Scénario particulier

2.1 Le panier est vide : le système en informe l'utilisateur
8.1 Le système constate une erreur de saisie ; il en informe l'internaute, retour à 6

Nous retrouvons les 4 actions et la gestion d'erreur alternative dans le contrôleur présenté plus haut.

Cette phase de description textuelle est donc très importante.
          5.3 Imaginer les vues externes

Il s'agit ici de dessiner comment se présenteront chaque page, telle que la voie l'internaute. 
Ceci permet de mettre en évidence les sous-vues qui peuvent être partagées par plusieurs cas d'utilisation, cf plus haut pour le bandeau principal ou l'affichage de la sous-vue des erreurs.
         5.4 Construire l'architecture physique de l'application.

Créer les répertoires, les contrôleurs vides de code, le contrôleur principal, etc...
         5.5 Ecrire le contrôleur principal

C'est le fichier index.php avec le switch pointant sur chaque cas d'utilisation.


******************************************************************************************************************************************************************
						                            CE QUI Y A DANS LE PROJET
******************************************************************************************************************************************************************
Annotations:
- Structure de base PHP	(for if/else)					        |	oui
- Tableau PHP							                        |	oui
- Classe et objet						                        |	oui
- Utilisation d'une librairie dans le code source			    |	NAN !!!!!!
- Utilisation d'une librairie via composer                      |   NAN PLUUUUUSSSS !!!!
- Opération CRUD						                        |	oui
- Mise en place MVC						                        |	oui
- Mise en place FC						                        |	oui
- présence d'un Readme.md de qualité						    |	oui
- Le programme fonctionne au lancement ?				        |	oui pour moi ^^
- Namespace (BONUS)						                        |	non
- DI -> injection de dépendances -> service container (BONUS)	|	oui cf c_gestionPanier.php
- Intéret du design pattern					                    |	oui dans le readme.md
- Service container et injection de dépendance			        |
