# Bygone-Generals

Brief CDA "Pire2Pire" team Bygone-generals

## Table des mattiere
1. [Intro](#Intro)
2. [Menaces et objectif des attaques](#menaces-et-objectif-des-attaques)  
   2.1. [Compromission des ressources](#compromission-des-ressources)  
   2.2. [Vol de données](#vol-de-données)  
   2.3. [Déni de service](#déni-de-service)  
   2.4. [Point d’eau](#point-deau)
3. [Développement continue](#développement-continue)
4. [Les défense mise en place contre les attaques](#les-défense-mise-en-place-contre-les-attaques)  
  4.1. [La défense en profondeur](#la-défense-en-profondeur)  
  4.2. [L’entête sécurisé (CORS / http/ HTTPS/ TLS)](#lentête-sécurisé-cors--tls--http--https)  
  4.3. [Le moindre privilège](#le-moindre-privilège)  
  4.4. [La politique RGPD](#la-politique-rgpd)  
  4.5. [Stratégie de sauvegarde](#stratégie-de-sauvegarde)  
  4.6. [Journalisation](#journalisation)  
  4.7. [L’authentification](#lauthentification)  
5. [Source](#source)

-----------------------------
##	**Intro**
------------------------------------
##	**Menaces et objectif des attaques**
----------------------------
###	**Compromission des ressources**
Cette attaque a pour but de modifier l'intégrité de votre application. Pour ce faire, il va trouver un moyen d'entrer pour modifier une certaine partie de votre application pour changer les donner ou rajouter des informations supplémentaires qui pourront être malveillantes.  
  
###	**Vol de données**
Cette attaque est là pour voler les données (authentifiants, informations personnelles, informations bancaires, etc.). Dans un but souvent lucratif et aboutit la plupart du temps à des usurpations d’identité ou à des paiements frauduleux.  
  
###	**Déni de service**

Envoi massif de requête sur l’application par un réseau d’ordinateur infecté (botnet) dans le but de saturer le service et le rendre inaccessible.

###	**Point d’eau**
C’est une attaque qui est en général, la plus discrète. Le but est de piéger les utilisateurs qui sont habitués à l'application. Une fois leurs pièges posés. Ils n'auront qu'à attendre un utilisateur tomber au piège pour activer le programme malveillant mit en place.    
Par exemple:  
Si on souhaite attaquer un site d'un boulanger, on peut facilement s'assurer que le boulanger visite un site sur un nouveau four à pain en promotion. Alors que ce ne serait qu'un leur pour mettre en place un cheval de Troie sur ça machine. 
  
---------------------
##	**Développement continue**
----------------------
Nous allons mettre en place un système de test unitaire pour tester le code pour vérifier que rien ne soit cassé à chaque patch de l'application, ainsi qu'une intégration continue pour les automatiser. Cette procédure va permettre de ne pas oublier d'éléments lors de la mise en production et donc ainsi améliorer la qualité du produit. 

---------------------
##	**Les défense mise en place contre les attaques**
--------------------
### **La défense en profondeur**

#### **DDOS Attack**

Pour identifier efficacement toute tentative d’attaque DDOS, nous allons analyser le traffic afin de détecter les activités suspectes.
Nous pouvons également stocker nos données et services sur des serveurs différents afin d’éviter la saturation complète des services.
De plus, nous pouvons utiliser un limiteur de traffic pour éviter les requêtes trop fréquentes.

#### **Les injections**

Nous allons mettre en place le moyen de vous proteger contre les ataque de type d'injection.

Sur chaque entréer (un champs ou un utilisateur va marquer une donnée) effectuer par un utilisateur on va vérifier, filtrer, et effectuer un échappement de caractères, pour vérifier de l'integrité de la données.
A cela on rajoutera les bonne pratique utiliser dans le language back choisi pour proteger la requete et les donnée qui s'y trouve pour l'integreté de votre base de donnée.

Avec cette méthode cela vous protegera contre ces deux type d'injection le SQLi et le XSS stockées

* ##### **SQLi**

Il s'agit d'attaques visant la base de données. Les moyens d'entrés sont tous simplement les différentes requête utiliser pour communiquer entre la base de données et l'utilisateur. Et au vu de l'application il y aura beaucoup de requete que des utilisateurs pourront effectuer.
Le problème de ces ataques, c'est s'il arrive a entréer dedans les hacker pourront lire, altérer ou détruire la base de données.

* ##### **XSS**

Cross-Site Scripting est une attaque qui permet d'injecter des donnés dans une page web qui va l'interpréter. Elle est de forme HTML ou JavaScript. Elle est implémenté dans les application grâce à une entrée (exemple une zone commentaire).
Ce type d'ataque est prévue pour visée les utilisateurs qui viendront sur votre application et notre votre application en elle même.
Si un de vos apprenant est mal intentionné. Il pourrai mettre en commentaire à un de vos cours un script qui pourra recuperer par exemple des cookies de connecxion d'utilisateur qui arrivera dans la page car le navigateur interpretera le commentaire et effectura le script.
En faisant la méthode expliquer un peu plus haut, ce type d'ataque sera arreté.
Mais ceci est une des ataque XSS possible.

 #### **RSI**

Pour la création de votre applciation on va utiliser des CDN pour gagner en performance et économiser de la bande passante. Cependant cela peu comporter un risque. Si quelqu'un prend le control du CDN, il pourra injecter du contenu malveillant. C'est pour cela que nous allons mettre en place une vérification du contenu pour s'assurer de  l'integrité des fichier télécharger. C'est ce qu'on appelle le **RSI** (Subresource Integrity). Grace a un haschage spécifier, il ira vérifier que le contenue télécharger sera identique a ceux qui est attendu. Si le haschage est diférent alors il bloquera le contenu. 
  
####	**CSP**
Une Content Security Policy (CSP) ou stratégie de sécurité de contenu a pour but d’améliorer la sécurité des sites web. Pour cela, elle détecte et réduit un certain nombre d’attaques dont les attaques Cross-Site Scripting (XSS) et les injections de code

Grâce à la CSP, on va pouvoir restreindre l'accès aux ressources atteignables des domaines ou sous-domaines sous forme d'autorisation.  
On peut le mettra en place via une configuration du serveur afin d'ajouter un en-tête (header) HTTP Content-Security-Policy aux réponses. Mais pour éviter de toucher au serveur, on pourra le mettre en place via les balises <meta> HTML en lui indiquant les règles qu'on voudra mettre en place.

Permettront de maitriser les **requêtes silencieuses**. Elles permettent de demander au navigateur d’émettre des requêtes sans passer par l’exécution de code JavaScript ou CSS. Ce qui est potentiellement dangereux si elles ne sont pas maitrisées. Car elles peuvent aller à la fuite d'information, comme exploiter les failles CRSF, voir des attaques DDoS. 

#### **X-frame (clickjaking)**

Vu que l'application contiens des cours privé, que seul des personnes inscrit chez vous pourrons suivre. On va mettre en place un x-frame. Le but et de vous proteger des copie frauduleux de votre site par un iframe.
On appelle ça du **Clickjacking**. leurs but de créer un site via ce fameux iframe qui est une fenetre dans un site qui pointe vers votre application. Il l'utilise pour cacher des bouton ou rajouter des bouton pour inciter les utilisateur a cliquer. Une fois fait, ça lancera un script qui provoqueront des actions qui ce feront à leurs insu. Pour les proteger, on mettra une options "X-Frame-Options: deny". Cela empechera la page d'être utiliser dans un iframe. Il sera possible de modifier ce parametre, si on s'apercoit lors de la mise en place de votre application qu'on a besoin de faire un iframe. On mettra un paramettre qui permetra seulement à votre domaine, ou une page bien précis l'autorisation d'utiliser un iframe.

Quant à eux, les cookies ont de multiples usages : ils peuvent servir dans notre cas à la gestion des sessions, c’est-à-dire que l’utilisateur n’est pas forcément obligé de se connecter régulièrement, la personnalisation, c’est-à-dire les préférences de l’utilisateur, le thème et autres paramètres et enfin enregistrer et analyser le comportement des utilisateurs, afin de déterminer un comportement anormal.

---------------------------

### **L’entête sécurisé (CORS / TLS / HTTP / HTTPS)**

#### **SOP: Same origin Policy**

Dans le but de d’encadrer les origines des requêtes faites à notre application, nous allons mettre en place des règles grâce aux **CORS (Cross origin ressource sharing)**:
Nous Mettrons en place des Request with Credentials, validant et limitant l’ouverture de notre API.

Cela nous sécurisera des **CSRF (Cross Site Request Forgery)**:
Qui tente de faire exécuter une requête à l’utilisateur en la cachant dans un formulaire par exemple.

Nous mettrons également en place un protocole **HTTPS** afin de protéger l'intégrité ainsi que la confidentialité des données lors du transfert d'informations entre l'ordinateur de l'internaute et le site.

Nous y parviendrons par le biais des **TLS (Transport Layer Security)**:
Les données envoyées à l'aide du protocole HTTPS sont sécurisées via le protocole TLS qui offre trois niveaux clés de protection :

* ##### **Le chiffrement** :

Consiste à coder les données échangées pour les protéger des interceptions illicites.

* ##### **L'intégrité des données** :

Les informations ne peuvent être ni modifiées, ni corrompues durant leur transfert, que ce soit délibérément ou autrement, sans être détectées.

* ##### **L'authentification** :

Prouve que les internautes communiquent avec le bon site Web.

#### **HSTS (HTTP Strict Transport Security)**

Force le site à n’interagir qu’avec un protocole HTTPS et bloque HTTP.

-------------------

### **Le moindre privilège**

Pour une meilleure sécurisation de votre application, nous allons appliquer le principe du moindre privilège. Cela fait référence à un concept de sécurité dans lequel on accorde à un utilisateur le niveau d’accès (ou les permissions) minimum requis pour accomplir son travail. Mais aussi qu'une fonction n'aura que les donnée et ressource nécessaire à son déroulement et rien d'autre.
Cela permet de réduire la surface exposée aux cyberattaques.
On éliminera les privilèges d’administrateur local inutiles et s’assurer que tous les utilisateurs humains et non humains dispose uniquement des privilèges nécessaires

Pour faciliter la mise en place des droits pour chaque utilisateur, nous allons appliquer la méthode **RBAC** (Role based Access Control).
Nous allons créer des rôles avec des autorisations, droits. Pour faciliter la gestion des utilisateurs en compartimentant les accès donnés, que cette personne pourra atteindre. Ce qui fera une couche de sécurité sur les accès donnée. L'avantage supplémentaire est de gagner du temps par la suite, pour éviter de devoir attribuer des droits l'un après l'autre à chaque apprenant, formateur ou employer. Il suffira d'attribuer les rôles aux personnes qui pourront être modifiées.
Ca optimisera l’efficacité opérationnelle, protègera les données des risques de fuite ou de vol, réduit le travail d’administration et d’assistance informatique.

--------------------------

### **La politique RGPD**

Une plateforme comme la vôtre est une cible majeure contre les **attaques malveillantes**, donc elle doit se protéger davantage.

La plateforme de formation en ligne présente des données à caractère personnel de ses utilisateurs et ainsi doit obligatoirement respecter le **Règlement Général sur la Protection des Données** (RGPD), qui établie des règles sur la collecte et l’utilisation des données de l'utilisateur.
Il a été conçu autour de 3 objectifs :

* renforcer les droits des personnes
* responsabiliser les acteurs traitant des données
* crédibiliser la régulation grâce à une coopération renforcée entre les autorités de protection des données

Ainsi évité le vol de données en respectant toutes les recommandations citées ci-dessus.
Ce qui incite la platefrome a mettre en place une stratégie de sécurité adaptée.

-----------------------------

### **Stratégie de sauvegarde**


La plateforme doit adopter une stratégie de sauvegarde de ce fait, il a une certaine stratégie à adopter, notamment « la sauvegarde 3-2-1 », qui repose sur trois règles :

* Trois copies de données : ce lot de copies comporte les données originales que l’on souhaite sécuriser, et au minimum deux sauvegardes.
* Deux types de stockage différents : les deux copies de données sauvegardées doivent être conservées sur deux supports de stockage distincts. Cela permet de minimiser les risques de défaillance qui pourraient potentiellement survenir sur un support unique. On peut retrouver parmi les différents type de stockage : un disque dur interne, un disque dur externe, une bande magnétique, une clé USB ou encore une sauvegarde dans le cloud.
* Une copie hors site : il est impératif de conserver au moins, une copie des données en dehors de la plateforme. En effet, nul n’est à l’abri d’un sinistre (inondation, incendie, tempête, court-circuit…), d’un acte de malveillance (cyberattaque, ransomware…) ou encore d’une erreur humaine.

### **Journalisation**

La journalisation est un élément primordial pour assurer la sécurité des traitements de données, qui est obligation posée par l’article 5 du RGPD. 
Il est nécessaire d’avoir un système de journalisation (c’est-à-dire un enregistrement dans des « fichiers journaux » ou « logs ») des activités des utilisateurs, des anomalies et des événements liés à la sécurité. Ces journaux doivent conserver les évènements sur une période glissante ne pouvant excéder six mois (sauf obligation légale, ou risque particulièrement important) :
- La journalisation doit concerner, au minimum, les accès des utilisateurs en incluant leur identifiant, la date et l’heure de leur connexion, et la date et l’heure de leur déconnexion.
- Dans certains cas, il peut être nécessaire de conserver également le détail des actions effectuées par l’utilisateur, les types de données consultées et la référence de l’enregistrement concerné.
- Informer les utilisateurs de la mise en place d’un tel système, après information et consultation des représentants du personnel.
- Protéger les équipements de journalisation et les informations journalisées contre les accès non autorisés, notamment en les rendant inaccessibles aux personnes dont l’activité est journalisée.
- Établir des procédures détaillant la surveillance de l’utilisation du traitement et examiner périodiquement les journaux d’événements pour y détecter d’éventuelles anomalies.
- Assurer que les gestionnaires du dispositif de gestion des traces notifient, dans les plus brefs délais, toute anomalie ou tout incident de sécurité au responsable de traitement.
- Notifier toute violation de données à caractére personnel à la CNIL et, sauf exception prévue par le RGPD, aux personnes concernées pour qu’elles puissent en limiter les conséquences

------------------------------


## Stratégie de sécurisation de l'authentification


Ce rapport traite des stratégies de sécurité à mettre en place concernant l'authentification et les autorisations.

### Politique de gestion des facteurs Auth, focus sur l'User

La stratégie d'autorisations reposera sur 5 rôles séparés au minimum :

    -low-privilege (simple visiteur)
    -user (utilisateur enregistré et authentifié)
    -teacher (formateurs)
    -moderators (modérateurs)
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
        
	note: bien que l'ANSI recommande un mot de passe le plus long possible une limite maximale arbitraire de 
	50 caractères sera mise en place,afin de limiter en première intention dans cette couche,
	l'impact des attaques DDOS.

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

### Concernant les formateurs

Au vu des privilèges plus élevés des Teachers, ceux-ci devront, en plus des mesures relatives aux Users, IMPERATIVEMENT utiliser une authentification à double facteur,
et fournir un numéro de téléphone vérifié (dans le respect des RGPD et sans aucun but commercial)

Les Teachers auront des autorisations de modification de leur espace "créateur" afin d'organiser et simplement mettre à jour leur travail de formation, certaines tâches requiereront une validation par la modération (exemple : empêcher des posts malveillants de contenu audiovisuel pornographique)

### A propos des Admins

Tout les logins spéciaux de tâches d’administration seront :

	-chiffrés avec une clef synchrone changeante régulièrement en entreprise, 
	les employés 	devront changer leur mot de passe crypté régulièrement.

A terme, et afin de faciliter le travail constant des equipes, sans compromettre la sécurité des accès sensibles, nous recommandons la mise en place d'une sécurité multi facteurs avec facteurs physiques du type:

    1 Badge + mot de passe fort sur des machines dédiées
    2 Biométrie + badge + mot de passe fort sur des machines dédiées
    
de changer constament le facteur "badge" qui sera remis en main propre aux employés acrédités toute les deux semaines par exemple.





-------------------
## **Source**
-------------------
https://www.ssi.gouv.fr/uploads/2013/05/anssi-guide-recommandations_mise_en_oeuvre_site_web_maitriser_standards_securite_cote_navigateur-v2.0.pdf  

https://www.ssi.gouv.fr/guide/recommandations-relatives-a-lauthentification-multifacteur-et-aux-mots-de-passe/#:~:text=Privilégier%20l%27utilisation%20de%20l,fort%20de%20mots%20de%20passe.  

https://www.cnil.fr/fr/definition/cookie


https://www.economie.gouv.fr/entreprises/reglement-general-sur-protection-des-donnees-rgpd


https://www.associations.gouv.fr/IMG/pdf/fiche_pratique_rgpd.pdf

