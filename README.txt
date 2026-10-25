# Recherche Immo by Chris — version 2

## Ce que fait cette version
- Interface adaptée aux mobiles et aux ordinateurs.
- Formulaire location/achat, ville, type de bien, budget, pièces, chambres, mots-clés.
- Fonction serveur Vercel (`/api/search`) qui appelle un fournisseur de recherche web via son API.
- Présente les résultats immobiliers provenant des domaines autorisés listés dans `api/search.js`.
- Le compteur indique le nombre de résultats retournés et filtrés, jamais un faux total d'annonces.
- La clé API reste côté serveur, jamais dans le HTML public.

## Important : activation nécessaire
Le site statique peut être déployé gratuitement, mais pour lire les résultats automatiquement il faut une clé API du moteur de recherche. Ce projet est préconfiguré pour Serper.dev qui annonce 2 500 requêtes d'essai gratuites sans carte bancaire (offre susceptible d'évoluer). Ce n'est pas une API immobilière officielle : c'est un moteur de recherche web. Il ne garantit ni l'exhaustivité, ni la disponibilité des annonces.

1. Crée un compte sur https://serper.dev/ et récupère la clé API.
2. Dans Vercel, ouvre le projet `Recherche Immo by Chris`.
3. Va dans **Settings → Environment Variables**.
4. Ajoute `SERPER_API_KEY` avec la clé obtenue. Ne la mets jamais dans `index.html`.
5. Enregistre puis redéploie le projet (Deployments → dernier déploiement → Redeploy).
6. Le projet Vercel doit contenir ces trois éléments à la racine :
   - `index.html`
   - `api/search.js`
   - `vercel.json`

## Déploiement depuis un dépôt GitHub
Téléverse ces trois fichiers et le dossier `api` dans le dépôt connecté à Vercel, puis lance un déploiement. Si ton projet actuel n'est qu'un fichier HTML déposé manuellement, il faut le remplacer par ce petit projet avec le dossier `api` : une fonction serveur ne peut pas être créée avec le seul fichier `index.html`.

## Limites honnêtes
- Les sites immobiliers ne proposent pas tous une API publique libre d'accès. Le code ne contourne pas leurs protections et n'extrait pas directement leurs bases de données.
- Le rayon géographique et certains critères sont transmis comme mots-clés de recherche ; ce n'est pas un filtre cartographique garanti.
- Le nombre affiché est celui des résultats immobiliers identifiés parmi les résultats du moteur, pas un décompte exhaustif du marché.
- Une annonce peut avoir expiré ou changer : toujours vérifier la page source.
- Les domaines sont filtrés côté serveur pour ne présenter que les sites listés dans `ALLOWED_ORIGINS`. Tu peux modifier cette liste plus tard.

## Dépannage
- « moteur pas configuré » : variable `SERPER_API_KEY` absente ou redéploiement oublié.
- « clé invalide » : vérifier la clé dans Serper.dev et la variable Vercel.
- Aucun résultat : élargir la ville/mots-clés ou modifier le type de bien.
