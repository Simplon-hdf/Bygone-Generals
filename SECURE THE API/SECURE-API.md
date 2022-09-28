# Sécurisation d’API:

## Deni de service / DDOS Attack:

#### Description: 
Envoi massif de requête sur l’application par un réseau d’ordinateur infecté (botnet) dans le but de saturer le service et le rendre inaccessible.

#### Solution:
Analyser et comprendre son traffic pour détecter des activités suspectes.
Stocker nos données dans différentes serveurs pour éviter une coupure générale
Limitation du traffic (ex: Express-Rate-Limit)


## SOP: Same origin Policy

#### Description:
Méchanisme de sécurité (natif à tout les navigateurs modernes) bridant les requêtes et script essayant d’interagir avec des domaines n’ayant pas la même origine.


### CORS: Cross origin ressource sharing

#### Description:
Autorise les requêtes issues d’origine differentes.
Peut être configuré pour n’autoriser que les requêtes comportant un header précis.

#### Solution:
Mettre un place des Request with Credentials, validant et limitant l’ouverture de notre API.

### CSRF: Cross Site Request Forgery

#### Description:
Faire exécuter une requête à l’utilisateur en la cachant dans un formulaire par exemple :

#### Solution:
Impossible sur les navigateurs modernes grâce à Same Origin Policy (SOP).
Rendu possible si les CORS sont modifiés et ouvert:￼




## HTTPS:
Hypertext Transfer Protocol Secure : est un protocole de communication Internet qui protège l'intégrité ainsi que la confidentialité des données lors du transfert d'informations entre l'ordinateur de l'internaute et le site.

### HSTS:
HTTP Strict Transport Security: 
Force le site à n’interagir qu’avec un protocole HTTPS et bloque HTTP

### TLS:
Les données envoyées à l'aide du protocole HTTPS sont sécurisées via le protocole Transport Layer Security (TLS), qui offre trois niveaux clés de protection :
1. Le chiffrement : consiste à coder les données échangées pour les protéger des interceptions illicites. 
2. L'intégrité des données : les informations ne peuvent être ni modifiées, ni corrompues durant leur transfert, que ce soit délibérément ou autrement, sans être détectées.
3. L'authentification : prouve que les internautes communiquent avec le bon site Web.


# CSP:

Une Content Security Policy (CSP) ou stratégie de sécurité de contenu a pour but d’améliorer la sécurité des sites web.

Pour cela, elle détecte et réduit un certain nombre d’attaques dont les attaques Cross-Site Scripting (XSS) et les injections de code.
