## XSS

### Description

Cross-Site Scripting
le but de cette ataque est d'injecter des données dans une page web qui va l'interpreter. elle est de form HTML ou javascript en l'implémentant dans les sites grace a une entré (exemple une zone commentaire). La personne visée par ce genre d'ataque n'est pas le site en lui même, mais les utilisateurs qui vont utiliser le site derriere pour récuperer tous type d'informations (sessions, mot de passe,...) ou effecteuer des actions en leur nom.

### Solutions

Pour éviter le problème sur les entrée utilisateurs:

* on va d'abord mettre les bonne balises HTML par raport à ceux qui est demandé (un email, on mettra en place un imput mail)
* On mettre en place un systeme de vérification des champs pour une deuxiemes couche que ceux qui est attendu sois valide. Via un systeme d'expression regulière pour valider la donné
* Et on fera un échappement des caractere approprié au résultat attendu pour éviter que des balises ou certain caractere speciaux puisse être interpretter par le navigateur en tant que balises HTML ou script
* (CSRF)

## SQLi

### Description

Il s'agit d'ataque visant la base de données. Les moyen d'entré sont tous simplement les diférentes requetes utilser pour communiquer entre la base de données et l'utilisateur.
Si on ne protege pas nos requetes il vont pouvoir par le bien de requete SQL entrer dans la base de données pour lire, alterer ou suprimer notre Base de données. C'est pour cette raison qu'on va la proteger avec les moyens suivant.

### Solutions

Comme pour le XSS il y a des étapes qui vont y resemblé.

* on philtrer chaque donnée venant d'un utilisateur pour avoir le résultat attendu et conforme
* on échappement des caracteres
* on ne mettra pas les donnée brut de l'utilisateur dans la requete. On utilisera des methodes lier au language utiliser dans le back pour proteger au maximum les requete et éviter les injections.

https://www.ionos.fr/digitalguide/serveur/securite/injection-sql-bases-et-mesures-pour-se-proteger/

## SRI

### Description

C'est une fonctionnalité qui permet au navigateur de vérifier l'integrité du contenue pour vérifier qu'il n'a pas était modifier par un tier.
Pour cela le navigateur va vérifier que la clef du fichier sois identique a celui de l'integrity de la balise visé.

exemple :
Utiliser un CDN pour héberger des fichiers tels que les scripts et les feuilles de style qui sont partagés entre plusieurs sites permet d'améliorer les performances du site et d'économiser de la bande passante. Cependant, utiliser des CDN comporte un risque : si un attaquant prend le contrôle du CDN, il pourra injecter du contenu malveillant dans les fichiers, et il pourra donc aussi potentiellement attaquer tous les sites qui récupèrent les fichiers sur ce CDN.

SRI vous permet d'atténuer le risque de ce genre d'attaques, en veillant à ce que les fichiers de votre application aient été livrés sans modification d'un tiers ayant injecté du contenu supplémentaire dans les fichiers.

### Solutions

* ajouter la valeur "integrity" a chaque élément script ou link

https://developer.mozilla.org/fr/docs/Web/Security/Subresource\_Integrity

## Clickjacking

### Description

Cette ataque est utiliser grace à un site trompeur que vous aurez par lien internet que ce soit mail, dans les reseau sociaux ou autres. Il s'agit d'une copie d'un site souvent grace a un iframe qui va inciter un utilisateur a cliquer sur un bouton qu'il aurait créer et rajouter sur cette page. Mais qui va être un piege car en cliquant dessus vous allez declenchez une action qui va permettre au site frauduleu des d'engendrer une action a l'insu de l'utilisateur.
Pour éviter toutes copye de site de votre application on mettra en place un DENY pour éviter qu'il puisse être utiliser ailleurs.

### Solutions

Pour ce proteger de ce genre d'action on va mettre en place un X-Frame-Option il y en a trois sorte:

* X-Frame-Options: deny = va interdire l'inclusion de la page (iframe)
* X-Frame-Options: sameorigin = qui autorise que ceux qui on le même domaine a l'inclure
* X-Frame-Options: allow-from https://........com = permet de definir qui à les autorisations pour l'inclure

## Requêtes silencieuses

ce sont des requete qui peuvent être lancer via certain type de balise pour lancer des requete sans lancer de javascript ou CSS. ce sont des failles qui peux potentiellement laisser passer des informations. (CSRF)

Pour éviter ce genre de probleme nous allons mettre en place une configuration **CSP** pour limiter ce genre de probleme et gerrer nos acces vers l'extérieur

## Strict mode

### Description

Le mode strict va permettre d'augmenter les regles de restriction qui vont changer la sémentique normale de JavaScript. Ceux qui aura pour impact une plus grande complexiter lors de l'écriture. En revanche ça forcera une écriture plus propre car toutes les erreurs silencieuses vont bloquer le script au lieu qu'il interprete à ça manière.

un exemple:
il va interdire de mettre des variable ou elle n'ont pas initialiser en amont.

## RBAC

### Description

Le but de la philosophie du RBAC est de créer des role avec des autorisation, droits, pour facilité la gestion des utilisateur en comportimentant les accés données que cette personne pourra atteindre ce qui fera une couche de sécurité sur les accés données. Cela fara aussi gagner du temps pour éviter de devoir atribuer des droit l'un après l'autres à chaque apprenant, formateur ou employer. Il suffirat d'atribuer un role aux personnes qui pourra être modifier dans le futur facilement pour lui permetre certain accé à des fonctionnalité.

User -> Role -> Permission -> Application

## Moindres privilèges

### Description

Le principe du moindre privilège fait référence à un concept de sécurité dans lequel on accorde à un utilisateur le niveau d’accès (ou les permissions) minimum requis pour accomplir son travail.
Cela veux dire aussi qu'une fonction n'aura que les donnée et ressource necessaire à son déroulement et rien d'autres.
Cela permet de réduir la surface exposée aux cyberattaques.

### Solutions

Éliminer les privilèges d’administrateur local inutiles et s’assurer que tous les utilisateurs humains et non humains disposent uniquement des privilèges nécessaires pour accomplir leur travail.
Séparer les comptes administrateur des comptes standard et isoler les sessions des utilisateurs à privilèges.

https://www.cyberark.com/fr/what-is/least-privilege/

## RGPD

### Description

Le **RGPD** est une règlementation européenne obligatoire qui refond et renforce les droits et la protection des données à caractère personnel des personnes physiques. Il harmonise les règles en Europe en offrant un cadre juridique unique aux professionnels. Il permet de développer leurs activités numériques au sein de l’UE en se fondant sur la confiance des utilisateurs.

