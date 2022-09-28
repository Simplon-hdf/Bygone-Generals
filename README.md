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
  4.2. [L’entête sécurisé (CORS / http/ HTTPS/ TLS)](#lentête-sécurisé-cors--http-https-tls)  
  4.3. [Le moindre privilège](#le-moindre-privilège)  
  4.4. [La politique RGPD](#la-politique-rgpd)  
  4.5. [Stratégie de sauvegarde](#stratégie-de-sauvegarde)  
  4.6. [Journalisation](#journalisation)  
  4.7. [L’authentification](#lauthentification)  
5. [Source](#source)

##	**Intro**
------------------------------------
##	**Menaces et objectif des attaques**
----------------------------
###	**Compromission des ressources**

###	**Vol de données**

###	**Déni de service**

###	**Point d’eau**

##	**Développement continue**
---------------------
##	**Les défense mise en place contre les attaques**
---------------------
### **La défense en profondeur**
#### **Les injections**
Nous allons mettre en place le moyen de vous proteger contre les ataque de type d'injection.

Sur chaque entréer (un champs ou un utilisateur va marquer une donnée) effectuer par un utilisateur on va vérifier, filtrer, et effectuer un échappement de caractères, pour vérifier de l'integrité de la données.
A cela on rajoutera les bonne pratique utiliser dans le language back choisi pour proteger la requete et les donnée qui s'y trouve pour l'integreté de votre base de donnée.

Avec cette méthode cela vous protegera contre ces deux type d'injection le SQLi et le XSS stockées

- ##### **SQLi**
Il s'agit d'attaques visant la base de données. Les moyens d'entrés sont tous simplement les différentes requête utiliser pour communiquer entre la base de données et l'utilisateur. Et au vu de l'application il y aura beaucoup de requete que des utilisateurs pourront effectuer.
Le problème de ces ataques, c'est s'il arrive a entréer dedans les hacker pourront lire, altérer ou détruire la base de données.

- ##### **XSS**
Cross-Site Scripting est une attaque qui permet d'injecter des donnés dans une page web qui va l'interpréter. Elle est de forme HTML ou JavaScript. Elle est implémenté dans les application grâce à une entrée (exemple une zone commentaire).
Ce type d'ataque est prévue pour visée les utilisateurs qui viendront sur votre application et notre votre application en elle même.
Si un de vos apprenant est mal intentionné. Il pourrai mettre en commentaire à un de vos cours un script qui pourra recuperer par exemple des cookies de connecxion d'utilisateur qui arrivera dans la page car le navigateur interpretera le commentaire et effectura le script.
En faisant la méthode expliquer un peu plus haut, ce type d'ataque sera arreté.
Mais ceci est une des ataque XSS possible.

####	**CSP**

-------------------- 
__La partie du CSP que tu as florian__

--------------------
Permettront de maitriser les **requêtes silencieuses**. Elles permettent de demander au navigateur d’émettre des requêtes sans passer par l’exécution de code JavaScript ou CSS. Ce qui est potentiellement dangereux si elles ne sont pas maitrisées. Car elles peuvent aller à la fuite d'information, comme exploiter les failles CRSF, voir des attaques DDoS. 

#### **Xframe (clickjaking)**
Vu que l'application contiens des cours privé, que seul des personnes inscrit chez vous pourrons suivre. On va mettre en place un x-frame. Le but et de vous proteger des copie frauduleux de votre site par un iframe.
On appelle ça du **Clickjacking**. leurs but de créer un site via ce fameux iframe qui est une fenetre dans un site qui pointe vers votre application. Il l'utilise pour cacher des bouton ou rajouter des bouton pour inciter les utilisateur a cliquer. Une fois fait, ça lancera un script qui provoqueront des actions qui ce feront à leurs insu. Pour les proteger,  on mettra une options "X-Frame-Options: deny". Cela empechera la page d'être utiliser dans un iframe. Il sera possible de modifier ce parametre, si on s'apercoit lors de la mise en place de votre application qu'on a besoin de faire un iframe. On mettra un paramettre qui permetra seulement à votre domaine, ou une page bien précis l'autorisation d'utiliser un iframe.

#### **Précaution d’usage des cookie**
####	**Cloisonnement des web worker (on a pas ce point je crois part hachemi)**
####	**sécurisation des API**

###	**L’entête sécurisé (CORS / http/ HTTPS/ TLS)**

###	**Le moindre privilège**

###	**La politique RGPD**

###	**Stratégie de sauvegarde**

###	**Journalisation**

###	**L’authentification**
