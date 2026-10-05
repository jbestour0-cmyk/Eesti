# Eesti sõnad

Flashcards d'estonien (PWA hors-ligne). Ouvrir https://jbestour0-cmyk.github.io/eesti/ puis « Ajouter à l'écran d'accueil ».

Tout tient dans `index.html` (HTML/CSS/JS sans dépendance ni build) ; `sw.js` met l'appli en cache pour le hors-ligne.

## Fonctionnalités

- **Révisions espacées (SM-2)** : nouvelles cartes + cartes à revoir chaque jour, sens ET→FR, FR→ET ou mixte, réponse retournée ou écrite.
- **XP et niveaux** : +15 « Facile », +10 « Bien », +5 « Difficile », +2 « Raté », ×2 si la réponse écrite est exacte. Sept niveaux aux titres estoniens : Turist, Külaline, Uustulnuk, Elanik, Tallinlane, Eestlane, Põliseestlane. La progression créée avant les XP reçoit 10 XP par mot déjà vu.
- **Fin de session** : confettis, XP gagnés, meilleure série de bonnes réponses.
- **Sons** de réussite et d'échec générés par la Web Audio API (aucun fichier audio).
- **Badges** (onglet Badges) : séries de jours, mots vus/maîtrisés, thèmes complétés, réponses écrites exactes, session parfaite… Les badges verrouillés montrent leur progression.
- **Expression du jour** sur l'accueil (~40 expressions avec explication culturelle), choisie selon la date.
- **Carte qui se retourne** en 3D au moment de la réponse (désactivée automatiquement si « réduire les animations » est activé sur le téléphone).
- **Une couleur par thème**, sur la carte et dans la liste des thèmes (lisible en clair et en sombre). Couleurs dans `THEME_COLORS`.
- **Onglet Jeux** (n'affecte pas les révisions SM-2) :
  - *Paires* : 6 mots estoniens et 6 traductions à relier le plus vite possible ; chrono, +2 s par erreur, record par thème, XP selon le temps.
  - *Vrai ou faux* : 60 secondes, un mot et une traduction juste ou fausse ; score, record, 2 XP par bonne réponse.
- Chaque fonctionnalité (et chaque jeu) se désactive dans **Réglages → Fonctionnalités**.

## Sauvegarde

La progression est dans le `localStorage` du navigateur, clé `eesti.sonad.v1`. Les nouveaux champs (`xp`, `badges`, `stats`, nouveaux réglages) sont ajoutés avec des valeurs par défaut par `merge()` : une ancienne sauvegarde reste lisible. Réglages → Sauvegarde permet de copier/importer la progression.

## Ajouter des mots

Éditer le tableau `THEMES` dans `index.html`. Chaque mot : `["estonien", "français", "PRO-non-cia-tion"]`.

- Prononciation pour francophone : la syllabe accentuée en MAJUSCULES (toujours la première du mot en estonien), les petits mots outils en minuscules.
- Plusieurs traductions séparées par ` / `, précisions entre parenthèses.
- Ne pas modifier le texte estonien d'un mot existant : il sert d'identifiant (`theme|mot`) pour la progression.

Ajouter une expression du jour : tableau `PHRASES`, format `["estonien", "traduction", "explication"]`.

Après une modification, incrémenter `CACHE` dans `sw.js` pour forcer la mise à jour.
