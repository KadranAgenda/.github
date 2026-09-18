<div align="center">

# Kadran

**Un agenda personnel, multi-utilisateurs, qui vit chez vous.**

Calendrier · Tâches · Rappels · Bot Discord · Widget

</div>

---

## C'est quoi ?

Kadran, c'est un agenda en ligne personnel — pensé pour tourner en local, sur sa propre machine, plutôt que chez un tiers. Pas de compte email, pas de mot de passe : on se connecte avec Discord, et c'est tout.

Autour du calendrier lui-même gravitent un **bot Discord** (pour gérer ses tâches et se faire notifier sans ouvrir le navigateur) et un **widget d'écran d'accueil** (pour voir sa journée d'un coup d'œil). Les trois projets de cette organisation forment un seul produit :

| Repo | Rôle | Stack |
|---|---|---|
| **[Site](https://github.com/Kadran/kadran)** | Le cœur : le calendrier web, l'API, toute la logique métier | Laravel 13 · Blade · Tailwind v4 · SQLite |
| **[Bot](https://github.com/Kadran/bot)** | Bot Discord — tâches, rappels, agenda en DM/slash-commands | TypeScript · discord.js v14 |
| **[Widget](https://github.com/Kadran/widget)** | Widget d'écran d'accueil (Android) — lecture seule, appairage par QR code | Android |

---

## Site — le calendrier

L'application principale : un vrai calendrier (mois / semaine / jour), sans rechargement de page, avec glisser-déposer des événements, blocs de temps pour les tâches, recherche de créneaux libres et import ICS/EDT.

- **Récurrence virtuelle** — une règle simple (fréquence + intervalle + fin), jamais d'occurrences stockées : tout est recalculé à la volée pour la fenêtre affichée.
- **Multi-utilisateur, sans mot de passe** — authentification Discord OAuth uniquement, avec une liste blanche d'IDs Discord optionnelle.
- **Recherche de créneaux libres** — donnez une durée, une plage horaire, Kadran calcule les trous dans votre planning.
- **Import ICS** et **synchro d'emploi du temps IUT**, avec suivi des changements (ajouts, annulations, changements de salle...).
- **Rappels** qui fonctionnent même sans tâche planifiée qui tourne en fond — notification navigateur ou DM Discord.

## Bot — Discord

Un pont léger entre Discord et l'API de Kadran : pas de logique métier propre, juste des commandes.

- `/tache`, `/taches`, `/fait` — créer, lister, cocher ses tâches.
- `/agenda`, `/semaine`, `/libre` — consulter son planning et ses créneaux libres, en lecture seule.
- Compréhension du langage naturel en DM (dates en français via `chrono-node`).
- Boucles de sondage pour pousser rappels, digests du matin/soir et récap des changements d'emploi du temps.

## Widget — écran d'accueil

Un widget qui affiche l'agenda du jour sans ouvrir l'app. Authentifié par un **token personnel et révocable**, distinct du secret partagé du bot : un widget perdu ou compromis ne compromet qu'un seul compte, et se révoque en un clic depuis les paramètres. L'appairage se fait par QR code, sans rien saisir à la main.

---

## Philosophie

Kadran est un projet personnel, pas un SaaS : tout tourne en local, les données restent chez vous, et chaque brique (site, bot, widget) ne parle à l'extérieur que via l'API du site lui-même. Le nom vient du cadran d'une horloge — l'idée d'un temps qu'on regarde d'un coup d'œil.

