# 🏆 2100 chemin Ste-Foy Open

Tableau de bord à deux pour suivre, en mode compétition amicale, nos tâches ménagères, nos activités sportives et nos sorties en amoureux. Application web installable sur l'écran d'accueil iPhone, avec synchronisation en temps réel entre nos deux téléphones.

## Fonctionnalités

- **Pointage** : chaque activité vaut des points, avec tableau de score, couronne 👑 pour le meneur, total de la semaine et série de jours 🔥.
- **3 domaines** : Ménage, Sport, Sorties — chacun avec ses activités et ses points.
- **Tableau « Qui fait quoi »** : section dépliable montrant combien de fois chacun a fait chaque activité.
- **Temps réel** : une activité enregistrée sur un téléphone apparaît sur l'autre en quelques secondes.
- **Persistance** : les données sont stockées en ligne (Supabase) et conservées d'une session à l'autre.
- **Code secret** : un écran d'accès protège l'app à l'ouverture.

## Comment ça marche

- `tracker.html` : toute l'application (interface + logique) dans un seul fichier.
- **Supabase** : base de données + temps réel (table `activities`).
- **Netlify** : hébergement du fichier, relié à GitHub pour le déploiement automatique.

La configuration (URL Supabase, clé publique, code secret) se trouve en haut du `<script>` dans `tracker.html`, dans la section `CONFIG SUPABASE`.

## Mettre à jour le site

1. Modifier `tracker.html`.
2. Dans **GitHub Desktop** : écrire un résumé → **Commit to main** → **Push origin**.
3. Netlify redéploie automatiquement (~1 min). Rafraîchir l'app sur les téléphones.

> Garder le fichier nommé `tracker.html` (ne pas renommer en `index.html`), sinon l'URL change et les icônes déjà installées sur l'écran d'accueil cessent de fonctionner.

## Installer sur iPhone

1. Ouvrir l'URL Netlify dans **Safari**.
2. Bouton **Partager** → **Sur l'écran d'accueil**.
3. Ouvrir l'app, entrer le code secret une fois (mémorisé ensuite).

## Base de données (Supabase)

Table `activities` :

| colonne | type | description |
|---|---|---|
| id | text | identifiant unique de l'entrée |
| player | int | 1 = William, 2 = Paola |
| cat | text | domaine (menage / sport / sorties) |
| emoji | text | émoji de l'activité |
| label | text | nom de l'activité |
| pts | int | points gagnés |
| ts | bigint | horodatage (millisecondes) |

Un déploiement ne touche jamais aux données : seul le code change.

## Notes

- La clé Supabase utilisée est la clé **publique (anon)**, conçue pour vivre côté client.
- Le code secret est une barrière légère (protège des curieux, pas d'un expert) — suffisant pour un usage perso.
- Les noms des joueurs sont pour l'instant locaux à chaque appareil (défauts : William et Paola).
