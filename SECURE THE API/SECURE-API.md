# Deni de service / DDOS Attack:

Description: 
Envoi massif de requête sur l’application par un réseau d’ordinateur infecté (botnet) dans le but de saturer le service et le rendre inaccessible.

Solution:
Analyser et comprendre son traffic pour détecter des activités suspectes.
Stocker nos données dans différentes serveurs pour éviter une coupure générale
Limitation du traffic (ex: Express-Rate-Limit)


# SOP: Same origin Policy

Description:
Méchanisme de sécurité (natif à tout les navigateurs modernes) bridant les requêtes et script essayant d’interagir avec des domaines n’ayant pas la même origine.


# CORS: Cross origin ressource sharing

Description:
Autorise les requêtes issues d’origine differentes.
Peut être configuré pour n’autoriser que les requêtes comportant un header précis.

Solution:
Mettre un place des Request with Credentials, validant et limitant l’ouverture de notre API.

# CSRF: Cross Site Request Forgery

Description:
Faire exécuter une requête à l’utilisateur en la cachant dans un formulaire par exemple :
￼

Solution:
Impossible sur les navigateurs modernes grâce à Same Origin Policy (SOP).
Rendu possible si les CORS sont modifiés et ouvert:
￼


# Sécurisation d’API:



# HTTPS:



# TLS:



# HSTS:



# CSP:

