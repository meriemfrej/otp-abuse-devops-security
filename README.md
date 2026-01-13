Description Projet 
visant à protéger un système OTP contre les abus via des solutions DevOps et côté infrastructure.

Problème de sécurité
Le système OTP est abusé par des bots, ce qui provoque :
- Coûts SMS élevés
- Problèmes de réception pour les vrais utilisateurs
- Création de faux comptes

Solutions proposées
- Limitation de fréquence (rate limiting) sur les endpoints OTP
- Blocage des comportements abusifs au niveau du proxy / gateway
- Surveillance des requêtes et des coûts SMS
- Alertes pour détecter rapidement les abus

Résultat
Ces mesures permettent :
- de limiter les attaques automatisées
- de protéger le service pour les vrais utilisateurs
- de réduire les coûts SMS
- sans modifier le code de l’application
