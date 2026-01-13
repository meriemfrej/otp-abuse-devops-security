# Analyse de sécurité – Abus OTP

1. Type d’attaque / abus
Le système OTP est abusé par des scripts ou des bots :
- Envoi massif de demandes OTP potentiellement du brute-force
- Tentatives répétées de vérification d’OTP 
- Création de faux comptes

2. Pourquoi les systèmes SMS / numéro de téléphone sont faciles à abuser
- Les numéros peuvent être générés ou réutilisés facilement
- Les endpoints OTP sont publics
- Sans limitation de fréquence, les bots peuvent envoyer beaucoup de requêtes
- Chaque SMS a un coût réel

3. Principaux risques pour l’entreprise

Risques techniques
- Surcharge du service OTP
- Les utilisateurs légitimes ne reçoivent pas leurs codes
- Risque de blocage par le fournisseur SMS

Risques business
- Coûts SMS très élevés
- Création de faux comptes
- Mauvaise expérience utilisateur et perte de confiance
