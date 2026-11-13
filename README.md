# Ice Please, maquette du site (FR / EN / AR)

Version 9 : la V8 avec un nouveau film sur l'accueil. Elle n'est pas encore en ligne ; la version 8 l'est : **https://nadirkarem.github.io/ice-please-v8/** (brouillon non indexé).

Maquette de refonte du site d'Ice Please Morocco (FAAB & CO), glaçons premium et clear ice pour les professionnels de la boisson. Ce n'est pas le site officiel : les textes reprennent le site actuel, les visuels de synthèse (vidéo, sphère dans un verre de whisky) sont des illustrations, et la page est en `noindex`.

Site statique en HTML, CSS et JavaScript, construit avec [Vite](https://vite.dev). Aucun framework, aucune base de données. La boutique (`/shop`, panier, livraison, paiement simulé, compte) rejoue le parcours d'Odoo dans le navigateur (`src/shop.js`, données dans `localStorage`) ; dans Odoo, c'est la boutique d'Odoo qui sert, habillée avec ce design (`ODOO_BOUTIQUE.md`). Français à la racine, anglais sous `/en/`, arabe sous `/ar/` (mise en page inversée).

## Version 9

La V8, avec un nouveau film sur l'accueil (« Manipulé avec précision. Servi avec perfection. ») :

- **Le film** (15 s, en boucle, sans son) : une sphère posée à la pince dans un verre de whisky, des roses de plusieurs couleurs prises dans des cubes, puis le cube gravé du logo tenu au gant noir. Il se termine par un travelling sur la gravure, qui se fond dans le logo sur fond noir, exactement à la même place, avant de revenir au premier plan.
- **Deux cadrages** : paysage pour les écrans larges, vertical pour un téléphone tenu droit (recadré plan par plan sur le sujet, avec un panoramique sur les roses). Le site choisit, et change si l'on tourne le téléphone.
- **Autour du film** : le titre tient en deux phrases, une par ligne ; les voiles sombres ne couvrent plus que le texte, pour garder la lumière de l'image ; le titre s'efface pendant le dernier plan et le logo, puis revient ; le bouton de pause est un petit rond discret ; le bouton WhatsApp s'efface pendant le film ; la barre du téléphone prend la teinte du béton du film.
- Le film ne se charge que lorsqu'il arrive à l'écran.
- Le montage est documenté dans `tools/film/` (dossier local, non publié).

## Version 8

La V6 (design, photos, vidéos) avec la structure de la V7 :

- **« Nos glaçons » et la boutique ne font plus qu'une page** (`/shop/`) : les cartes de la V6 (photo, nom, texte, flèche ; descriptions à hauteur égale), des filtres par catégorie (sans recherche ni compteur), puis « Notre Vision ». Chaque carte ouvre la page du glaçon, qui le présente et le vend (`/shop/cube-xl/`…) : prix, options et panier sont là.
- **« À propos » est supprimée** ; sa photo (le glaçon signé, tenu dans un gant noir) signe maintenant l'accueil.
- **Accueil** : après l'intro, la vidéo de l'engagement (« Manipulé avec précision. Servi avec perfection. ») ; puis les trois glaçons de base, qui défilent vers la droite pendant qu'on descend (vers la gauche en arabe), avec l'indication « Continuez de défiler » ; puis, sur fond noir, la signature (le glaçon signé au gant noir) et les glaçons sur mesure ; le service avec une photo de l'entreprise (un Ice Stick posé à la pince au bar), Instagram et le contact de la V6.
- **Fond bleu clair** (`#E3F1FA`) au lieu du blanc ; noir (`#04080C`) pour le sur-mesure et la signature, atteint par un long dégradé.
- Les anciennes adresses (`/glacons/`, `/about-us/`, `/cube-xl/`…) redirigent vers les nouvelles.
- Le paquet Odoo de la V6 (`npm run odoo`) n'est pas adapté à cette version.

## Version 6.1

La V6, avec les réglages qui la font se comporter comme une application sur téléphone :

- la barre du haut ne reste plus « survolée » après un toucher : les effets de survol sont réservés à la souris, et elle s'efface de nouveau pendant la lecture ;
- plus de flash gris quand on touche un lien ou un bouton, et chaque commande réagit dès que le doigt se pose ;
- un appui long sur un bouton ne sélectionne plus son texte ;
- les marges et le bouton WhatsApp tiennent compte de l'encoche en paysage, y compris en arabe ;
- le menu défile seul, sans entraîner la page ;
- clavier : les noms et villes commencent par une majuscule, la quantité se valide avec « OK », la recherche avec « Rechercher ».

## Lancer en local

```bash
npm install --legacy-peer-deps
npm run dev      # http://127.0.0.1:5300
npm run build    # génère dist/ (100 pages)
```

Pour tester la construction sous un sous-dossier, comme sur GitHub Pages :

```bash
BASE_PATH=/ice-please-v8 npm run build
BASE_PATH=/ice-please-v8 npx vite preview
```

## Où modifier quoi

| Pour changer… | Fichier |
|---|---|
| un texte (FR, EN, AR) | `content/fr.json`, `content/en.json`, `content/ar.json` (mêmes clés) |
| téléphone, e-mail, Instagram, indexation | `content/site.json` |
| la structure d'une page | `scripts/lib/pages.mjs` |
| l'en-tête, le pied de page, le `<head>` | `scripts/lib/layout.mjs` |
| les adresses des pages | `scripts/lib/routes.mjs` |
| le design | `src/style.css` |
| le comportement (menu, transitions de page, givre, récit, défilement fluide, révélation titre et image, formulaires) | `src/main.js` |
| la boutique : catalogue, prix (vides : « -- MAD »), livraison, paiement | `content/shop.json`, `content/shop.<langue>.json`, `scripts/lib/shop-pages.mjs`, `src/shop.js` |
| l'habillage des pages d'Odoo | `src/odoo-skin.css` |
| les vidéos (MP4, WebM, affiche) | `public/media/` |

## Mise en ligne

GitHub Pages sert la branche `gh-pages`, qui contient le site construit (pas de GitHub Actions) :

```bash
BASE_PATH=/ice-please-v8 npm run build
touch dist/.nojekyll
```

puis le contenu de `dist/` est poussé sur `gh-pages`.
