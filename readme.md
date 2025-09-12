# Profiler Hyper Complet

Une application front-end légère pour générer des indices comportementaux et de personnalité (MBTI, Ennéagramme, Dark Triad, styles d'attachement, screening TDA/H). Toutes les données restent côté client : rien n'est envoyé à un serveur.

---

## Fonctionnalités

- Questionnaire MBTI simple (12 questions) et estimation de type + confiance
- Ennéagramme : choix du type principal, comportements sous stress et instinct dominant
- Échelle Dark Triad (Machiavélisme, Narcissisme, Psychopathie) via sliders
- Style d'attachement (radio)
- Screening TDA/H rapide (6 items, échelle 0–4)
- Rapport textuel synthétique généré localement
- Export / import du résultat au format JSON
- Interface responsive et entièrement côté client (fichier unique : Profil.html)

---

## Aperçu

Ouvrir `Profil.html` dans votre navigateur :
- Remplir les sections requises (MBTI, Ennéagramme, instinct, attachement)
- Cliquer sur « Analyser » pour générer le rapport et visualiser les scores
- Exporter le JSON via le bouton « Exporter JSON »

---

## Installation / exécution

Aucune dépendance serveur requise. Vous pouvez lancer l'application de deux façons :

1. Ouvrir directement
   - Double-cliquer sur `Profil.html` ou l'ouvrir depuis votre navigateur préféré.
   - Recommandé : navigateur moderne (Chrome, Edge, Firefox, Safari).

2. Servir via un petit serveur HTTP (optionnel, utile pour certains environnements)
   - Avec Python 3 :
     - Ouvrir un terminal dans le dossier du projet et exécuter : `python -m http.server 8000`
     - Aller à `http://localhost:8000/Profil.html`

---

## Utilisation

- Les sections MBTI, Ennéagramme (type + instinct) et Attachement doivent être complétées avant l'analyse.
- Les sliders Dark Triad et TDA/H permettent d'ajuster l'intensité des réponses.
- Le rapport généré est indicatif et non médical : il donne des pistes et suggestions basées sur des heuristiques.

---

## Export / Import

- Export : génère un fichier JSON contenant l'instantané des résultats (`profil-YYYY-MM-DD.json`).
- Import : charge un fichier JSON déjà exporté et affiche son rapport. Note : l'import n'essaie pas de restaurer automatiquement les réponses du formulaire pour l'instant.

---

## Structure du projet

- `Profil.html` : fichier principal (HTML, CSS, JS embarqués) — tout le code est côté client.
- `readme.md` : ce fichier.

---

## Personnalisation rapide

Le fichier `Profil.html` contient des tableaux de constantes en début de script (`MBTI_ITEMS`, `ENNEA_MAIN`, `DARK_ITEMS`, etc.). Pour :
- Modifier les questions / textes : éditez ces constantes.
- Changer les seuils heuristiques : repérez les fonctions `analyze*` et `generateReport`.

---

## Confidentialité & limites

- Toutes les données restent dans votre navigateur et ne sont pas transmises.
- Cet outil fournit uniquement des indices comportementaux, non un diagnostic médical ou psychologique. En cas de doute important, consulter un professionnel qualifié.

---

## Contribution

Suggestions et améliorations bienvenues :
- Corrections de textes et traductions
- Amélioration des heuristiques d'analyse
- Restauration complète des réponses lors d'un import JSON

Pour contribuer, forkez le dépôt, faites vos modifications et proposez une pull request.

---

## Licence

MIT — voir le fichier `LICENSE` si présent.

---

Merci d'utiliser The Profiler. Utilisez-le de manière responsable et respectueuse.