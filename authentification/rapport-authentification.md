# Stratégie de sécurisation de l'authentification


Ce rapport traite des stratégies de sécurité à mettre en place concernant l'authentification et les autorisations.

### Politique de gestion des facteurs Auth, focus sur l'User

La stratégie d'autorisations reposera sur 4 rôles séparés au minimum :
    -low-privilege (simple visiteur)
    -user (utilisateur enregistré et authentifié)
    -teacher (formateurs)
    -admins (administrateurs/debug/dev team)

L'ANSI recommande evidemment un mot de passe fort, mais aussi que celui-ci ne soit pas trop contraignant pour l'utilisateur, afin de l'inciter à retenir plusieurs mots de passe usuels,pratiques et fort lui-même.
L'authentification multi-facteur tendant à se démocratiser, et ajoutant une couche d'authentification multi-composante supplémentaire( différent types de FACTEURS ), notre politique envers les utilisateurs sera donc:

    -rappel constant des règles de sécurité(phishing, communication avec employés etc)
    -proposer et encourager la pratique de la double authentification avec des solutions de tokens temporaires telles que:
    Authy , Google authenticator, etc.
    -rendre l'authentification multi-facteur OBLIGATOIRE pour les formateurs
    -limiter les essais consecutifs d'authentification
    -A l’inscription : vérification d’e mail 
    -Forcer l’utilisateur à respecter une politique de Mot de passe:
    	-12 caractères minimum
	    -numériques+alphabétique+caractères spéciaux(1 minimum de chaque)
	    -pas de suites logiques de nombre (456789)
	    -pas plus de 2 caractères semblables à la suite (aaa – 222)
        note: bien que l'ANSI recommande un mot de passe le plus long possible une limite maximale arbitraire de 50 caractères sera mise en place,
	afin de limiter en première intention dans cette couche, l'impact des attaques DDOS.

A l’inscription, le mot de passe utilisateur subira un Hachage SHA256 du mdp utilisateur avec un salage fort et UNIQUE, il n'y aura donc aucun mot de passe stocké en textuel sur nos serveurs, afin de miniser l'exploitabilité de la couche Data.
Cette décision implique l'absence de possibilité de RECUPERATION de mot de passe, et la mise en place d'un système de REINITIALISATION de mot de passe.

Nous mettrons en place une demande d’autorisation à code alphanumérique 6 caractères par l’e mail de contact quand l’User se connecte pour la première fois depuis un nouveau périphérique ET l'envoi d’une alerte mail PASSIVE (ou par téléphone selon le choix de l’User *1) quand une tentative de connexion à lieu depuis un nouveau périphérique.

Les sessions seront toujours temporaires par mesure sanitaire de sécurité, mais seront par défaut longues afin de ne pas entraver l'utilisation régulière, par défaut la validité d'une session authentifiée, sera révoquée:
    -tout les mois
    -à la moindre MAJ de l'application
Nous mettrons en place une possibilité de révocation de session et de facteurs d'authentification d'urgence pour les administrateurs.

Chaque requete concernant l'authentification devra être loguée avec des erreures type, et une validation type.

Afin d'habituer l'Utilisateur à gérer sa sécurité de compte, tout en améliorant l'ergonomie d'utilisation,nous proposerons à l'Utilisateur des préférences de contact pour:
	-le reset password
	-les alertes de conexion

Les Users n'auront que des privilèges de consultation, et de modification de leurs paramètres personnels d'ergonomie/de compte client.

### concernant les formateurs

Au vu des privilèges plus élevés des Teachers, ceux-ci devront, en plus des mesures relatives aux Users, IMPERATIVEMENT utiliser une authentification à double facteur,
et fournir un numéro de téléphone vérifié (dans le respect des RGPD et sans aucun but commercial)

Les Teachers auront des autorisations de modification de leur espace "créateur" afin d'organiser et simplement mettre à jour leur travail de formation, certaines tâches requiereront une validation par la modération (exemple : empêcher des posts malveillants de contenu audiovisuel pornographique)

### A propos des Admins

Tout les logins spéciaux de tâches d’administration seront :
	-chiffrés avec une clef synchrone changeante régulièrement en entreprise, les employés 	devront changer leur mot de passe crypté régulièrement.

A terme, et afin de faciliter le travail constant des equipes, sans compromettre la sécurité des accès sensibles, nous recommandons la mise en place d'une sécurité multi facteurs avec facteurs physiques du type:
    1 Badge + mot de passe fort sur des machines dédiées
    2 Biométrie + badge + mot de passe fort sur des machines dédiées
de changer constament le facteur "badge" qui sera remis en main propre aux employés acrédités toute les deux semaines par exemple.



