Leed
====

Leed (contraction de Light Feed) est un agrégatteur RSS libre et minimaliste qui permet la consultation de flux RSS de manière rapide et non intrusive.

- Application : Leed (Light Feed)
- Version : 1.1 Beta
- Auteur : Valentin CARRUESCO aka Idleman (idleman@idleman.fr)
- Page du projet : http://dizplay.idleman.fr/pages/project?project=18
- Licence : CC by-nc-nd (http://creativecommons.org/licenses/by-nc-nd/2.0/fr/) 
- Nb : les travaux dérivés peuvent être autorisés avec accord de l'auteur


Présentation
====

  Leed (contraction de Light Feed) est un agrégatteur RSS libre et minimaliste qui permet la consultation de flux RSS de manière rapide et non intrusive.
	
Toutes les tâches de traitements de flux sont effectuées de manière invisible par une tâche synchronisée (Cron), ainsi, l'utilisateur ne subit pas les lenteurs dues à la récupération et au traitement de chacuns des flux suivis.

A noter que Leed est compatible toutes résolutions, sur pc, tablettes et smartphone et fonctionne sous tous les navigateurs avec son skin par défaut.
	
Le script est également compatible avec les fichiers d'exports/imports OPML ce qui rend la migration de tous les agrégateurs réspectant le standard OPML simple et rapide.

Pré-requis
====

- Serveur Apache conseillé (Non testé sur les autres serveurs types Nginx ...)
- PHP 5.3 minimum (facultatif, conseillé)
- MySQL
- Un peu de bon sens :)


Installation
====

1. Récuperez le projet sur le dépot SVN de la version courante : http://hades.idleman.fr/svn/leed (non stable) ou télécharger la dernière archive zip : http://dizplay.idleman.fr/Projects/Archives/leed.zip (stable)
2. Placez le projet dans votre repertoire web et appliquez une permission chmod 775 (nb si vous êtes sur un hebergement ovh, préférez un 0755 ou vous aurez une erreur 500) sur le dossier et son contenu
3. Depuis votre navigateur, accedez à la page d'installation install.php (ex : http://votre.domaine.fr/leed/install.php) et suivez les instructions.
4. Une fois l'installation terminée, supprimez le fichier install.php par mesure de sécurité
5. [Optionnel] Si vous souhaitez que les mises a jour de flux se fassent automatiquement, mettez en place un cron (sudo crontab -e pour ouvrir le fichier de cron) et placez y un appel vers la page http://votre.domaine.fr/leed/action.php?action=synchronize ex : 
		0 * * * * wget -q -O /var/www/leed/logsCron "http://127.0.0.1/leed/action.php?action=synchronize&code=votre_code_synchronisation"
		Pour mettre à jour vos flux toutes les heures à la minute 0 (il est conseillé de ne pas mettre une fréquence trop rapide pour laisser le temps au script de s'executer).
		<Nb> : Si vous n'avez pas accès a la commande wget sur votre serveur, vous pouvez essayer la commande suivante : 
		0 * * * * /usr/bin/wget -O /var/www/leed/logsCron
		"http://127.0.0.1/leed/action.php?action=synchronize&code=votre_code_synchronisation" >
		/dev/null 2>&1
6. Le script est installé, merci d'avoir choisis Leed, l'agrégatteur RSS libre et svelte :p.


Questions courantes	(F.A.Q)
====
	
1. Pourquoi afficher le mot de passe en clair lors de l'installation?
--
J'ai laissé le mot de passe en clair parce que je considère que l'administrateur est un peu malin n'ira pas installer son leed juste au moment ou quelqu'un se trouve derrière lui.
Or, etant donné qu'il n'y a pas de champs confirmation de mot de passe (que je trouvait inutile pour une action ponctuelle telle que l'installation), il peux être intéressant de voir ce que l'on écrit pour éviter les méprises :)
nb : le mot de passe est a tout moment crypté en base de données et n'est jamais re-affiché en clair par la suite, seule la saisie d'un nouveaux mot de passe par l'admin est visible.
A mon sens c'est loin d'être une faille de sécurité, juste une habitude que j'ai dérangée (c'est mon petit côté vicelard) je part du principe que l'admin n'est pas assez idiot pour laisser voir son mot de passe lors de l'installation, mais assez distrait pour faire une faute de frappe. :D

2.Pourquoi y a t'il des erreurs partout style 'unknow table xxx' lorsque je lance leed?
----
Question bête mais : avez vous pensé à installer le script? Je vous invite à reverifier l'étape 3 de la section installation de ce même README.

3.Pourquoi y a t'il des erreurs partout style 'permission denied' lorsque je lance leed?
-----
Question bête mais : avez vous pensé à configurer les droits sur le script? Je vous invite à reverifier l'étape 2 de la section installation de ce même README. Si l'erreur persiste, tentez avec un chmod 777 sur l'intégralité du dossier et des sous fichiers

4.Qu'à leed de plus que TinyTinyRSS ou RSSLounge?
----
Rien, il en fait même moins, et c'est d'ailleurs ce qui fait sa force ! 
Leed ne peux pas être considéré comme un concurrent de ce genre de scripts, mais si vous tenez à la comparaison, dites vous que leed applique la mentalité KISS (Keep It Simple Stupid) et se cantonne à ce qu'il sait faire, pour le faire mieux et plus vite. 

5.Qu'est ce qu'un CRON? Comment le mettre en place?
----
Un CRON est le nom que l'on donne a une tâche planifiée sous linux, il s'agit donc d'une tâche qui vas automatiquement se répéter (sans intervention d l'utilisateur) afin d'executer la page de mises a jour des flux de leed.
Pour mettre en place un CRON, assurez vous que vous êtes bien maître de votre serveur ou, dans le cas ou vous avez un simple hebergement type OVH, free, 1&1 etc.., que votre hebergeur propose un système de tâches planifiées dans le panel d'amdinistration de votre compte.
Pour mettre en place un CRON depuis votre serveur, suivez les instructions de l'installateur de Leed ou renseignez vous sur la façon de créer un CRON ici : http://doc.ubuntu-fr.org/cron
Pour mettre en place un CRON depuis un panel d'administration d'hébérgement (OVH, free, 1&1 etc..), renseignez vous auprès de votre hébérgeur.

6.Ne pourrait-on pas afficher des favicons de sites à côté des flux?
----
Leed tire sa force de sa simplicité et de sa rapidité, le téléchargement et l'affichage des favicons pour un grand nombre de flux irait à l'encontre des deux principes énoncés, il est donc peu envisageable d'ésperer cette option pour le moment. 

Librairies utilisées
==

- Responsive / Cross browser : Initializr (http://www.initializr.com)
- Javascript : JQuery (http://www.jquery.com)
- Moteur template : RainTPL (http://www.raintpl.com)
- Parseur RSS : SimplePie (http://simplepie.org)