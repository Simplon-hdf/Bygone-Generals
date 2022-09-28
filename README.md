# Bygone-Generals

Brief CDA "Pire2Pire" team Bygone-generals

## Table des mattiere

1. [Intro](#Intro)
2. [Menaces et objectif des attaques](#menaces-et-objectif-des-attaques)
2.1. [Compromission des ressources](#compromission-des-ressources)
2.2. [Vol de données](#vol-de-donn%C3%A9es)
2.3. [Déni de service](#d%C3%A9ni-de-service)
2.4. [Point d’eau](#point-deau)
3. [Développement continue](#d%C3%A9veloppement-continue)
4. [Les défense mise en place contre les attaques](#les-d%C3%A9fense-mise-en-place-contre-les-attaques)
4.1. [La défense en profondeur](#la-d%C3%A9fense-en-profondeur)
4.2. [L’entête sécurisé (CORS / http/ HTTPS/ TLS)](#lent%C3%AAte-s%C3%A9curis%C3%A9-cors--http-https-tls)
4.3. [Le moindre privilège](#le-moindre-privil%C3%A8ge)
4.4. [La politique RGPD](#la-politique-rgpd)
4.5. [Stratégie de sauvegarde](#strat%C3%A9gie-de-sauvegarde)
4.6. [Journalisation](#journalisation)
4.7. [L’authentification](#lauthentification)
5. [Source](#source)


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
---------------------
##	**Les défense mise en place contre les attaques**
---------------------
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

#### RSI

Pour la création de votre applciation on va utiliser des CDN pour gagner en performance et économiser de la bande passante. Cependant cela peu comporter un risque. Si quelqu'un prend le control du CDN, il pourra injecter du contenu malveillant. C'est pour cela que nous allons mettre en place une vérification du contenu pour s'assurer de  l'integrité des fichier télécharger. C'est ce qu'on appelle le **RSI** (Subresource Integrity). Grace a un haschage spécifier, il ira vérifier que le contenue télécharger sera identique a ceux qui est attendu. Si le haschage est diférent alors il bloquera le contenu. 
  
####	**CSP**
Une Content Security Policy (CSP) ou stratégie de sécurité de contenu a pour but d’améliorer la sécurité des sites web. Pour cela, elle détecte et réduit un certain nombre d’attaques dont les attaques Cross-Site Scripting (XSS) et les injections de code

Grâce à la CSP, on va pouvoir restreindre l'accès aux ressources atteignables des domaines ou sous-domaines sous forme d'autorisation.  
On peut le mettra en place via une configuration du serveur afin d'ajouter un en-tête (header) HTTP Content-Security-Policy aux réponses. Mais pour éviter de toucher au serveur, on pourra le mettre en place via les balises <meta> HTML en lui indiquant les règles qu'on voudra mettre en place.

Permettront de maitriser les **requêtes silencieuses**. Elles permettent de demander au navigateur d’émettre des requêtes sans passer par l’exécution de code JavaScript ou CSS. Ce qui est potentiellement dangereux si elles ne sont pas maitrisées. Car elles peuvent aller à la fuite d'information, comme exploiter les failles CRSF, voir des attaques DDoS. 

#### **X-frame (clickjaking)**

Vu que l'application contiens des cours privé, que seul des personnes inscrit chez vous pourrons suivre. On va mettre en place un x-frame. Le but et de vous proteger des copie frauduleux de votre site par un iframe.
On appelle ça du **Clickjacking**. leurs but de créer un site via ce fameux iframe qui est une fenetre dans un site qui pointe vers votre application. Il l'utilise pour cacher des bouton ou rajouter des bouton pour inciter les utilisateur a cliquer. Une fois fait, ça lancera un script qui provoqueront des actions qui ce feront à leurs insu. Pour les proteger, on mettra une options "X-Frame-Options: deny". Cela empechera la page d'être utiliser dans un iframe. Il sera possible de modifier ce parametre, si on s'apercoit lors de la mise en place de votre application qu'on a besoin de faire un iframe. On mettra un paramettre qui permetra seulement à votre domaine, ou une page bien précis l'autorisation d'utiliser un iframe.

#### **Précaution d’usage des cookie**

#### **Cloisonnement des web worker (on a pas ce point je crois part hachemi)**

#### **sécurisation des API**

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

### **Le moindre privilège**

Pour une meilleure sécurisation de votre application, nous allons appliquer le principe du moindre privilège. Cela fait référence à un concept de sécurité dans lequel on accorde à un utilisateur le niveau d’accès (ou les permissions) minimum requis pour accomplir son travail. Mais aussi qu'une fonction n'aura que les donnée et ressource nécessaire à son déroulement et rien d'autre.
Cela permet de réduire la surface exposée aux cyberattaques.
On éliminera les privilèges d’administrateur local inutiles et s’assurer que tous les utilisateurs humains et non humains dispose uniquement des privilèges nécessaires

Pour faciliter la mise en place des droits pour chaque utilisateur, nous allons appliquer la méthode **RBAC** (Role based Access Control).
Nous allons créer des rôles avec des autorisations, droits. Pour faciliter la gestion des utilisateurs en compartimentant les accès donnés, que cette personne pourra atteindre. Ce qui fera une couche de sécurité sur les accès donnée. L'avantage supplémentaire est de gagner du temps par la suite, pour éviter de devoir attribuer des droits l'un après l'autre à chaque apprenant, formateur ou employer. Il suffira d'attribuer les rôles aux personnes qui pourront être modifiées.
Ca optimisera l’efficacité opérationnelle, protègera les données des risques de fuite ou de vol, réduit le travail d’administration et d’assistance informatique.

### **La politique RGPD**

Une plateforme comme la vôtre est une cible majeure contre les **attaques malveillantes**, donc elle doit se protéger davantage.

La plateforme de formation en ligne présente des données à caractère personnel de ses utilisateurs et ainsi doit obligatoirement respecter le **Règlement Général sur la Protection des Données** (RGPD), qui établie des règles sur la collecte et l’utilisation des données de l'utilisateur.
Il a été conçu autour de 3 objectifs :

* renforcer les droits des personnes
* responsabiliser les acteurs traitant des données
* crédibiliser la régulation grâce à une coopération renforcée entre les autorités de protection des données

Ainsi évité le vol de données en respectant toutes les recommandations citées ci-dessus.
Ce qui incite la platefrome a mettre en place une stratégie de sécurité adaptée.

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



###	**L’authentification**

-------------------
## **Source**
