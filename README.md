# Eesti sõnad

Flashcards d'estonien (PWA hors-ligne). Ouvrir https://jbestour0-cmyk.github.io/Eesti/ (attention au E majuscule) puis « Ajouter à l'écran d'accueil ».

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
  - *Dictée* : l'appli prononce 10 mots estoniens, tu les écris (bouton « Lentement »). Grisée avec une explication si le téléphone n'a pas de voix estonienne.
  - *Remettre dans l'ordre* : 5 phrases estoniennes de 3 à 6 mots, mélangées en boutons, à remettre dans l'ordre.
- **Mode Expert** (Réglages → Sessions) : 8 secondes par carte (temps écoulé = « Raté »), réponse écrite obligatoire dans les deux sens, ni écoute ni prononciation avant la réponse. FR→ET : même tolérance qu'avant sur les accents. ET→FR : n'importe quelle variante séparée par « / » est acceptée, sans tenir compte des parenthèses, des articles (le, la, l', un, une) ni de la casse. Les mots vus pour la toute première fois restent en mode découverte.
- **Niveau 2** : 239 mots et phrases de niveau intermédiaire répartis dans les thèmes, plus un thème « Conversation » (Vestlus). Débloqué quand 70 % des mots du niveau 1 ont été vus.
- Chaque fonctionnalité (et chaque jeu) se désactive dans **Réglages → Fonctionnalités**.

## Sauvegarde

La progression est dans le `localStorage` du navigateur, clé `eesti.sonad.v1`. Les nouveaux champs (`xp`, `badges`, `stats`, nouveaux réglages) sont ajoutés avec des valeurs par défaut par `merge()` : une ancienne sauvegarde reste lisible. Réglages → Sauvegarde permet de copier/importer la progression.

## Ajouter des mots

Éditer le tableau `THEMES` dans `index.html`. Chaque mot : `["estonien", "français", "PRO-non-cia-tion"]`.

- Prononciation pour francophone : la syllabe accentuée en MAJUSCULES (toujours la première du mot en estonien), les petits mots outils en minuscules.
- Plusieurs traductions séparées par ` / `, précisions entre parenthèses.
- Ne pas modifier le texte estonien d'un mot existant : il sert d'identifiant (`theme|mot`) pour la progression.

Mots de niveau 2 : tableau `LEVEL2`, un bloc par thème `{ theme:"food", level:2, words:[…] }`, même format, avec un 4e champ optionnel `verify` (texte libre) quand une tournure doit être validée. Les entrées `verify` sont signalées « ⚑ à faire valider » dans le Lexique.

Nouveau thème : l'ajouter à `THEMES` (avec `words:[]` s'il n'a que du niveau 2) et lui donner une couleur dans `THEME_COLORS`. Il sera automatiquement coché pour les sauvegardes existantes.

Ajouter une expression du jour : tableau `PHRASES`, format `["estonien", "traduction", "explication"]`.

Après une modification, incrémenter `CACHE` dans `sw.js` pour forcer la mise à jour.

## À faire valider par un Estonien

Entrées de niveau 2 marquées `verify` :

| Thème | Estonien | Français | Doute |
|---|---|---|---|
| Chiffres & prix | Kas see on soodushinnaga? | C'est en promotion ? | tournure naturelle en magasin ? |
| Logement & démarches | Ma tahaksin aja kinni panna. | Je voudrais prendre rendez-vous. | « aja » ou « aega kinni panema » ? |
| Route & permis | parema käe reegel | priorité à droite | terme utilisé en auto-école ? |
| Salle & boxe | Hoia lõug all! | Garde le menton baissé ! | « lõug all » ou « lõug alla » ? |
| Salle & boxe | konks | crochet (boxe) | nom du coup en boxe estonienne |
| Santé & urgences | Mul on pähkliallergia. | Je suis allergique aux noix. | ou « allergia pähklite vastu » ? |

Prononciations : l'appli place toujours l'accent sur la 1re syllabe. Quelques mots d'emprunt déjà présents au niveau 1 sont en réalité accentués plus loin (par ex. *politsei*, *aitäh*, *kontor*) : à corriger si tu veux être exact. Le niveau 2 évite ces mots.
