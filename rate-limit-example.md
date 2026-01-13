## Task 1 — Rate limiting (configuration)
Choix : Nginx 
- Limiter 'POST /auth/send-otp' à "3 requêtes par numéro de téléphone / 10 minutes".  
- Limiter 'POST /auth/verify-otp' à "5 tentatives par numéro / 10 minutes".  
- Retourner HTTP + 'Retry-After' pour forcer un (blocage temporaire) côté client (et permettre un couplage WAF/ban). 


## Task 2 — Protections infrastructure (explication courte)
 Où implémenter le rate limiting ?
- Au plus proche de l’entrée (edge): reverse proxy (Nginx), API Gateway ou WAF, avant l’application et avant l’appel au fournisseur SMS, afin de stopper les bots tôt et réduire les coûts. 
- Idéalement 'en couches':
  - WAF/CDN (filtrage bots, règles L7),
  - API Gateway/Proxy (quotas/rate limiting),
  - puis application

Pourquoi le traiter au niveau DevOps / infra ?
- Parce que c’est transversal (protège tous les services exposés) et rapide à déployer via configuration, sans attendre un cycle de dev. 
- Parce que le risque est une consommation non restreinte (coûts SMS + saturation), et l’infra est l’endroit naturel pour absorber/filtrer le trafic abusif.
- Parce que l’infra centralise aussi logs/metrics/alerting, ce qui est indispensable pour détecter l’abus et réagir vite.

## Task 3 — Monitoring & Alerting

3 métriques à monitorer

Taux de requêtes OTP → “Pour détecter rapidement un pic anormal de requêtes”

Taux d’échec OTP → “Pour repérer les tentatives de brute force”

Volume SMS → “Pour repérer un abus qui coûte cher (SMS pumping)”

2 alertes pour détecter l’abus

1. Alerte "OTP spike / SMS pumping"  
   - Action : escalade (on-call), durcissement temporaire des limites, blocage WAF ciblé (IP/ASN/pays si pertinent).

2. Alerte "Brute force verify OTP"  
   - Action : augmenter la friction côté edge (blocage temporaire plus long), investigation (logs), mise en liste de surveillance.
  
