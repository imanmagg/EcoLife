# Fiche technique — EcoLife (projet Éco-Challenge)

> **Binôme :** Iman Maggouh Essabiri · Walid Meziane

---

## 1. Le projet en une phrase

**EcoLife** est un site WordPress qui propose aux **20-30 ans** des **défis écologiques concrets** (alimentation, transport, déchets, énergie, numérique). L'utilisateur crée un **compte**, relève des défis, **suit sa progression** et voit l'**impact réel** de ses actions (kg de CO₂ évités).

**Méthode utilisée pour chaque élément :**
- **QUOI ?** ce que nous produisons
- **COMMENT ?** avec quel outil
- **POURQUOI ?** ce que cela apporte à l'utilisateur ou au projet

---

## 2. Pages à produire

| Page | QUOI ? | COMMENT ? | POURQUOI ? (besoin utilisateur) |
|---|---|---|---|
| **Accueil** | Présentation du concept, défi de la semaine, compteur global de CO₂ évité par la communauté, appel à l'action « Je relève un défi » | Page WordPress + modèle de page (template) du thème enfant | Comprendre en 5 secondes ce qu'est EcoLife et avoir envie de commencer |
| **Catalogue des défis** | Liste de tous les défis sous forme de cartes, avec filtres (thème, difficulté, durée) | Type de contenu personnalisé « Défi » (Custom Post Type) + taxonomies + bloc Query Loop | Trouver rapidement un défi adapté à son mode de vie et à son temps disponible |
| **Fiche défi** (modèle unique) | Description, étapes, durée, difficulté, impact estimé, bouton « Je relève ce défi » | Modèle `single-defi` dans l'éditeur de site + champs personnalisés | Savoir exactement quoi faire et pourquoi ça compte |
| **Inscription / Connexion** | Formulaires de création de compte et de connexion | Gestion des utilisateurs native de WordPress (rôle « Abonné ») + extension de formulaire de connexion front-end | Sauvegarder ses défis et personnaliser l'expérience (décision prise en C5) |
| **Mon espace** (tableau de bord) | Défis en cours / terminés, barre de progression, badges, total de CO₂ évité, suggestions personnalisées | Page protégée (accès réservé aux connectés) + métadonnées utilisateur + JavaScript | Voir ses progrès = motivation à continuer |
| **Questionnaire de profil** | 5-6 questions (transport, alimentation, logement…) au premier login | Formulaire en plusieurs étapes (JS) + réponses stockées dans le profil | Permettre à la fonction IA de proposer des défis pertinents |
| **À propos** | Qui nous sommes, notre mission, nos sources | Page WordPress simple | Crédibilité et transparence |
| **Contact** | Formulaire de contact | Extension de formulaire (ex. Contact Form 7 ou WPForms Lite) | Poser une question, proposer un défi |
| **Mentions légales & confidentialité** | Mentions légales, politique de confidentialité, cookies | Page de confidentialité native de WordPress, adaptée | Obligation légale (RGPD), confiance de l'utilisateur |
| **Page 404** | Message sympa + lien vers les défis | Modèle `404` du thème enfant | Ne pas perdre l'utilisateur |

**Pourquoi le back-end WordPress ?** Il est imposé par le cadre technique, mais il a de vrais avantages pour notre projet : gestion des comptes intégrée, contenus faciles à ajouter sans coder (nous pourrons ajouter de nouveaux défis en quelques minutes), énorme communauté et documentation, gratuit.

---

## 3. Sections et composants

| Composant | QUOI ? | COMMENT ? | POURQUOI ? (adaptation aux supports) |
|---|---|---|---|
| **En-tête + navigation** | Logo, menu principal, bouton « Mon espace » | Partie de modèle (template part) `header` + bloc Navigation | Ordinateur : menu horizontal · Mobile : menu burger qui s'ouvre en plein écran |
| **Héros (bannière d'accueil)** | Titre accrocheur, visuel, bouton d'action | Bloc Couverture (Cover) + composition (pattern) personnalisée | Le texte reste lisible sur petit écran (image recadrée, texte centré) |
| **Carte défi** | Image, titre, pastilles thème/difficulté, impact CO₂ | Pattern Gutenberg réutilisable + style CSS du thème enfant | Grille 3 colonnes (ordi) → 2 (tablette) → 1 (mobile) |
| **Barre de filtres** | Boutons de thèmes, difficulté, durée | HTML + JavaScript (filtrage sans rechargement) | Sur mobile : filtres repliés dans un panneau « Filtrer » pour gagner de la place |
| **Barre de progression** | % du défi accompli | Élément HTML `<progress>` stylé en CSS | Visible et compréhensible sur tous les écrans |
| **Badges** | Récompenses (ex. « Zéro déchet débutant ») | Icônes SVG + logique JS | Légers (SVG) donc rapides à charger, nets sur tous les écrans |
| **Compteur d'impact** | Total de CO₂ évité (perso et communauté) | Bloc personnalisé + JS (animation de comptage) | Chiffres grands et lisibles, se placent en colonne sur mobile |
| **Carte « Suggestion IA »** | Défi recommandé + phrase d'explication | Bloc personnalisé alimenté par la fonction IA | Mis en avant en haut du tableau de bord |
| **Formulaires** | Inscription, connexion, questionnaire, contact | Blocs/extension de formulaire + validation JS | Champs larges et clavier adapté sur mobile (`type="email"`, etc.) |
| **Notifications (toasts)** | Messages courts de confirmation ou d'erreur | Composant JS | Apparaît en bas de l'écran sur mobile, en haut à droite sur ordi |
| **Pied de page** | Liens utiles, réseaux sociaux, mentions légales | Template part `footer` | Liens empilés sur mobile |
| **Bandeau cookies** | Consentement | Extension RGPD (ex. Complianz) | Obligatoire, discret et accessible |

**Pourquoi Gutenberg + un thème enfant ?**
- **Gutenberg (éditeur de blocs)** : natif à WordPress, pas besoin d'un constructeur de pages lourd (Elementor, Divi…). Le site reste plus **rapide** et plus **sobre** — logique pour un site écologique.
- **Thème enfant** (basé sur le thème « bloc » **Twenty Twenty-Five**) : nous pouvons modifier le design et ajouter du code **sans perdre nos changements** lors des mises à jour du thème parent.
- **Approche « mobile d'abord »** : notre cible (20-30 ans) navigue majoritairement sur smartphone, donc nous concevons d'abord pour le mobile puis élargissons.

---

## 4. Contenus, médias et réglages visuels

| Élément | QUOI ? | COMMENT ? | POURQUOI ? (interactions attendues) |
|---|---|---|---|
| **Couleurs** | Palette : vert principal, vert clair, beige naturel, gris foncé pour le texte, une couleur d'accent (orange) pour les boutons | `theme.json` → `settings.color.palette` | Couleurs cohérentes partout ; contraste suffisant pour l'accessibilité (WCAG AA) ; l'accent orange attire le clic |
| **Typographies** | 1 police pour les titres, 1 pour le texte (ex. Poppins + Inter), hébergées localement | `theme.json` → `settings.typography.fontFamilies` | Lisibilité sur écran ; hébergement local = pas d'appel à Google Fonts (plus rapide + RGPD) |
| **Tailles de texte** | Échelle de tailles fluide | `theme.json` → `fontSizes` avec `fluid: true` | Le texte s'adapte automatiquement à la taille de l'écran |
| **Espacements** | Échelle d'espacements (XS → XL) | `theme.json` → `settings.spacing.spacingSizes` | Rythme visuel régulier, zones cliquables assez grandes sur mobile |
| **États interactifs** | Survol, focus, clic sur boutons et cartes | `style.css` du thème enfant (`:hover`, `:focus-visible`, transitions) | L'utilisateur voit que l'élément est cliquable ; navigation clavier possible |
| **Images** | Photos des défis, illustrations | Format **WebP**, compressées, chargement différé (`loading="lazy"`) | Pages légères = rapides sur 4G et moins énergivores |
| **Icônes** | Thèmes, badges, menu | **SVG** | Très légers et nets à toutes les tailles |
| **Textes** | Fiches défis, conseils, sources | Rédaction maison, ton direct et positif (tutoiement) | Parle la langue de la cible, donne envie d'agir sans culpabiliser |

**Pourquoi `theme.json` + CSS ?** `theme.json` centralise tous les réglages visuels en un seul fichier : si nous changeons le vert principal, il change partout (dans le site **et** dans l'éditeur). Le CSS sert pour ce que `theme.json` ne gère pas (animations, états de survol, composants sur mesure). Ce fichier constituera la base de notre **design system**.

---

## 5. Gestion d'états (comment l'interface réagit)

| État | QUOI ? (déclencheur → réaction) | COMMENT ? | POURQUOI ? (information transmise) |
|---|---|---|---|
| **Menu mobile** | Clic sur ☰ → menu ouvert / clic sur ✕ ou touche Échap → fermé | JavaScript + attribut `aria-expanded` | L'utilisateur sait si le menu est ouvert ; compatible lecteurs d'écran |
| **Filtre actif** | Clic sur « Transport » → bouton surligné, cartes filtrées, compteur « 8 défis » | JavaScript (classes CSS + `aria-pressed`) | L'utilisateur voit quels filtres sont appliqués et combien de résultats restent |
| **Aucun résultat** | Filtres trop restrictifs → message « Aucun défi ne correspond » + bouton « Réinitialiser » | JavaScript | Évite une page vide qui semble « cassée » |
| **Défi accepté** | Clic sur « Je relève ce défi » → bouton devient « Défi en cours ✓ » + message de confirmation | JavaScript + requête vers l'API REST WordPress | Confirmation immédiate que l'action est enregistrée |
| **Progression** | Étape cochée → la barre avance, le pourcentage se met à jour | JavaScript | Sentiment d'avancer = motivation |
| **Défi terminé / badge** | 100 % atteint → animation + badge débloqué + CO₂ ajouté au total | JavaScript | Récompense et valorisation de l'effort |
| **Chargement** | Pendant un appel API → squelette de chargement ou indicateur | JavaScript (états `loading` / `success` / `error`) | L'utilisateur sait qu'il doit patienter |
| **Erreur** | Échec réseau ou formulaire mal rempli → message clair en rouge sous le champ | JavaScript (validation) | Comprendre le problème et le corriger |
| **Connecté / déconnecté** | Menu affiche « Connexion » ou « Mon espace » | PHP (`is_user_logged_in`) dans le thème enfant | Accès adapté au statut de l'utilisateur |
| **Questionnaire en étapes** | Étape 1/5 → 2/5… boutons Précédent / Suivant | JavaScript | Un questionnaire découpé paraît moins long |

**Pourquoi JavaScript ?** C'est le langage du navigateur : il permet de réagir **instantanément** aux actions de l'utilisateur, sans recharger la page. Nous utiliserons du **JavaScript natif (vanilla)**, sans bibliothèque lourde, pour garder le site léger. Le site restera utilisable même si un script échoue (amélioration progressive).

---

## 6. Données dynamiques

| Donnée | QUOI ? | COMMENT ? | POURQUOI ? (valeur pour l'Éco-Challenge) |
|---|---|---|---|
| **Catalogue des défis** | Titre, thème, difficulté, durée, étapes, CO₂ évité | Custom Post Type « Défi » + champs personnalisés, exposés via l'**API REST de WordPress** (`/wp-json/wp/v2/defis`) | Un seul endroit pour gérer les défis ; le JavaScript peut les filtrer et les afficher dynamiquement |
| **Progression utilisateur** | Défis en cours, étapes cochées, défis terminés, badges | Métadonnées utilisateur (`user_meta`) + route REST personnalisée | Chaque utilisateur retrouve sa progression sur tous ses appareils |
| **Impact CO₂** | Équivalences parlantes (ex. « = 120 km en voiture ») | **API Impact CO₂ de l'ADEME** (impactco2.fr), gratuite et en français | Rendre l'impact **concret et crédible** grâce à une source officielle |
| **Compteur communautaire** | Somme du CO₂ évité par tous les membres | Calcul côté serveur, mis en cache | Montrer que l'action collective compte |
| **Contrat de données** | Description de la structure d'un défi et de la progression | Fichier **`Contrat.json`** dans le dépôt | Le binôme (et les outils) travaillent sur la même structure ; évite les incohérences entre front et back |

### Exemple de structure — `Contrat.json` (extrait)

```json
{
  "defi": {
    "id": "integer",
    "titre": "string",
    "slug": "string",
    "theme": "alimentation | transport | dechets | energie | numerique",
    "difficulte": "facile | moyen | difficile",
    "duree_jours": "integer",
    "etapes": ["string"],
    "co2_evite_kg": "number",
    "image": "url",
    "source": "url"
  },
  "progression": {
    "user_id": "integer",
    "defi_id": "integer",
    "statut": "en_cours | termine | abandonne",
    "etapes_validees": "integer",
    "date_debut": "date (AAAA-MM-JJ)",
    "date_fin": "date | null"
  },
  "profil": {
    "user_id": "integer",
    "transport_principal": "voiture | transports_en_commun | velo | marche",
    "alimentation": "omnivore | flexitarien | vegetarien | vegan",
    "logement": "seul | coloc | famille",
    "temps_disponible": "faible | moyen | eleve"
  }
}
```

---

## 7. Fonction « intelligente » (IA)

| | |
|---|---|
| **QUOI ?** | Un **« Coach EcoLife »** : à partir des réponses au questionnaire de profil et des défis déjà réalisés, il **recommande 3 défis personnalisés** avec une phrase d'explication (ex. « Tu prends souvent la voiture pour de petits trajets : essaie le défi *1 semaine à vélo* »). |
| **COMMENT ?** | 1. Le profil et l'historique (structurés selon `Contrat.json`) sont envoyés **côté serveur** à une API d'IA (modèle de langage), via une route REST personnalisée ou une extension (ex. AI Engine). 2. L'IA choisit **uniquement parmi les défis existants** du catalogue (liste fournie dans la requête) et renvoie une réponse au format JSON. 3. Le JavaScript affiche le résultat dans la carte « Suggestion IA ». La clé d'API reste sur le serveur (jamais dans le navigateur). Les résultats sont mis en cache pour limiter les appels. |
| **POURQUOI ?** | Ce qu'elle apporte **vraiment** : 1) **éviter la surcharge** — face à 30+ défis, l'utilisateur ne sait pas par où commencer ; 2) **pertinence** — un défi adapté à sa vie a plus de chances d'être réussi ; 3) **motivation** — l'explication personnalisée donne un sens au défi. |
| **Plan B** | Si l'API d'IA n'est pas disponible ou trop coûteuse : un **système de règles simple** (ex. « transport = voiture » → proposer les défis du thème transport, niveau facile). Le site fonctionne toujours, l'IA est un plus et non une dépendance. |
| **Limites assumées** | Pas de données sensibles envoyées (pas de nom, pas d'e-mail) ; l'IA ne peut pas inventer de défi ; les recommandations sont des suggestions, l'utilisateur garde le choix. |

---

## 8. Outils et justification

| Outil | Usage | Pourquoi celui-ci ? |
|---|---|---|
| **WordPress** | Back-end, comptes, contenus | Imposé par le cadre ; gestion des utilisateurs native ; gratuit ; très documenté |
| **Twenty Twenty-Five + thème enfant** | Base graphique | Thème bloc officiel ; personnalisation sans perte lors des mises à jour |
| **Gutenberg / éditeur de site** | Mise en page, patterns, modèles | Natif, léger, pas de constructeur de page lourd |
| **theme.json** | Couleurs, typos, espacements | Réglages centralisés = cohérence + base du design system |
| **CSS** | Styles sur mesure, responsive, états | Contrôle fin là où `theme.json` ne suffit pas |
| **JavaScript (vanilla)** | Interactions, filtres, états, appels API | Réactivité sans rechargement, sans bibliothèque lourde |
| **API REST WordPress** | Échange de données front ↔ back | Déjà intégrée, standard |
| **API Impact CO₂ (ADEME)** | Équivalences d'impact | Gratuite, officielle, en français |
| **API d'IA (modèle de langage)** | Coach EcoLife | Recommandations personnalisées en langage naturel |
| **LocalWP** | Développement en local | Installer WordPress en 1 clic sur nos ordinateurs, sans frais, pour construire et tester le site avant toute mise en ligne |
| **Hébergement en ligne** | Rendre le site accessible sur Internet | **À confirmer avec l'enseignant** (serveur de l'école ou hébergeur externe) ; en attendant, tout le développement se fait en local avec LocalWP |
| **GitHub** | Versionnage, travail en binôme, pull requests | Historique des changements, relecture mutuelle, exigé par le cours |
| **VS Code** | Édition du code | Gratuit, extensions PHP/JS/JSON |
| **Figma** | Wireframes et maquettes | Collaboration à deux en temps réel |
| **Canva** | Visuels et réseaux sociaux | Rapide pour les visuels de promotion |

---

## 9. Contraintes

| Type | Contrainte | Ce que nous faisons |
|---|---|---|
| **Technique** | WordPress obligatoire, thème enfant, Gutenberg | Pas de constructeur de page externe ; code personnalisé dans le thème enfant |
| **Responsive** | Mobile, tablette, ordinateur | Mobile d'abord ; tests sur au moins 3 tailles d'écran |
| **Accessibilité** | Niveau WCAG 2.1 AA visé | Contrastes suffisants, textes alternatifs, navigation au clavier, attributs ARIA, tailles de texte lisibles |
| **RGPD / vie privée** | Comptes utilisateurs = données personnelles | Données minimales (pseudo, e-mail), consentement cookies, politique de confidentialité, aucune donnée personnelle envoyée à l'IA, suppression du compte possible |
| **Sécurité** | Comptes et clés d'API | Mots de passe gérés par WordPress, clés d'API côté serveur uniquement, extensions à jour |
| **Éco-conception** | Cohérence avec le sujet du site | Images WebP compressées, polices locales, peu d'extensions, JS léger, mise en cache — objectif : pages < 1 Mo |
| **Performance** | Chargement rapide sur 4G | Score Lighthouse visé ≥ 85 en performance |
| **Budget** | Projet étudiant | 0 € en développement (outils gratuits) ; l'éventuel coût d'API IA et d'hébergement est repris dans le budget (C4) |
| **Temps** | Calendrier du cours | Priorité aux pages essentielles (accueil, catalogue, fiche défi, compte, mon espace, questionnaire) ; la fonction IA vient ensuite, avec le plan B prêt en secours |
| **Hébergement** | Lieu de mise en ligne pas encore fixé | Développement en local (LocalWP) ; choix de l'hébergement à valider avec l'enseignant |
| **Équipe** | Binôme, niveaux débutants en code | Répartition claire des tâches, relecture de chaque pull request par l'autre membre |
| **Contenu** | Informations écologiques fiables | Chaque défi cite sa source (ADEME, etc.) |

---

## 10. Liens avec les autres cours

| Cours / commande | Lien avec cette fiche |
|---|---|
| **C3 — Note d'intention** | Le concept, la cible et la mission décrits ici en découlent directement |
| **C4 — Équipe / budget** | Répartition des tâches du binôme ; coûts d'hébergement et d'API (section 9) |
| **C5 — Benchmark / SWOT / cible / promotion** | La création de compte et le suivi de progression viennent de nos conclusions ; la cible 20-30 ans justifie l'approche mobile d'abord et le ton |
| **Langues (anglais, néerlandais, espagnol)** | Piste d'évolution : version multilingue du site (Bruxelles = public FR/NL) |

---

## 11. Prochaines étapes

- [ ] Wireframes des pages principales (mobile + ordinateur) — Figma
- [ ] Maquettes haute fidélité
- [ ] Design system (palette, typos, composants) → traduit dans `theme.json`
- [ ] Rédaction du `Contrat.json` complet
- [ ] Installation de WordPress en local + thème enfant
- [ ] Premiers défis rédigés (objectif : 12 au lancement)
