# Windmap Wallonie — Frontend

Carte interactive de **constructibilité éolienne** en Wallonie. Application statique (un seul `index.html`, Leaflet) qui interroge en direct l'API Windmap.

- **Frontend** (ce repo) → déployé sur **Netlify** (statique, HTTPS).
- **Backend** → API FastAPI + PostGIS sur le serveur : `https://204.168.158.209.nip.io`
  (3,96 M de parcelles, filtrage et score recalculés à chaque requête).

## Déployer sur Netlify (2 min)

1. Crée un **nouveau repo GitHub** et pousse ces fichiers :
   ```bash
   git init
   git add .
   git commit -m "Windmap frontend"
   git branch -M main
   git remote add origin https://github.com/<toi>/windmap4M.git
   git push -u origin main
   ```
2. Sur **app.netlify.com** → *Add new site* → *Import an existing project* → choisis ce repo.
3. Réglages : **rien à changer** (pas de build, publish = racine). → *Deploy*.
4. Netlify te donne une URL `https://<nom>.netlify.app` — c'est ton lien de test.

## Changer l'URL de l'API

L'adresse du backend est en haut de `index.html` :
```js
const API = "https://204.168.158.209.nip.io";
```
Quand tu brancheras un vrai domaine (ex. `windmap-api.tondomaine.be`), remplace cette ligne et re-pousse.

## Comment lire la carte

- **Vert foncé → clair** : parcelles constructibles, du meilleur au moyen score (vent pondéré par le risque juridique communal).
- **Rouge** : exclu par une contrainte **dure** (habitat, Natura 2000, captage, radar…).
- Curseur **hauteur machine** : ajuste le recul à l'habitat (500 + hauteur/2).
- **Contraintes actives** : coche/décoche pour voir l'effet de chaque couche.
- Clique une parcelle pour le détail (score, proba permis, vent, surface).

> Les parcelles se chargent à partir du niveau de zoom 11 (pour rester fluide).
