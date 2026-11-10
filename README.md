# Tuteur socratique

Une skill pour Claude (utilisable aussi avec ChatGPT) qui transforme l'assistant en
tuteur personnel pour les élèves et étudiants français, du CP au supérieur.

Le tuteur n'explique pas le cours : il pose des questions, une à la fois, qui
obligent l'élève à raisonner, prévoir et justifier. Il suit la progression sur une
carte de compétences et ne valide un niveau que sur des réussites réelles.

## Ce que fait la skill

- **Diagnostic de départ** : 3 à 5 questions pour situer l'élève avant d'enseigner
  quoi que ce soit.
- **Carte de compétences** : le sujet est découpé en compétences concrètes, chacune
  suivie sur 6 niveaux (0 à 5) avec le compte des réussites qui le justifient.
- **Méthode socratique** : une question à la fois, pas de réponse donnée à la
  première erreur, mais une question plus étroite qui fait apparaître la
  contradiction.
- **Évaluation exigeante** : un niveau se gagne sur au moins deux réussites
  indépendantes, dont une sans aide. Une réponse vague n'est pas une réponse juste.
- **Révisions espacées** : les compétences déjà vues sont retestées sans prévenir,
  et systématiquement à la reprise d'une séance sauvegardée.
- **Gestion du blocage** : retour à une question plus simple, exemple résolu, pause.
- **Bilan final** : une question par compétence et un problème de synthèse.
- **Ancrage français** : programmes officiels, classe de l'élève, examens (brevet,
  bac, partiels, concours), notations et terminologie françaises, exigence de
  rédaction.

## Quatre profils

Le tuteur demande la classe au début de la séance et charge le profil correspondant.

| Profil | Classes | Séance | Aide directe | Carte | Particularités |
|---|---|---|---|---|---|
| [Primaire](tuteur-socratique/references/primaire.md) | CP à CM2 | 10 à 15 min | après 2 erreurs, indice dès la première | étoiles | phrases courtes, exemples concrets, pas d'avocat du diable, résumé pour l'adulte |
| [Collège](tuteur-socratique/references/college.md) | 6e à 3e | 20 à 30 min | après 2 erreurs | barres + échelle du socle commun | brevet, pas de résultat final donné sur un devoir à rendre |
| [Lycée](tuteur-socratique/references/lycee.md) | 2de à Tle, CAP, bac pro | 30 à 45 min | après 3 erreurs | barres, niveaux sur 5 | épreuves du bac, méthodes (dissertation, commentaire, démonstration), entraînement en temps limité |
| [Supérieur](tuteur-socratique/references/superieur.md) | après le bac, adultes | 45 à 60 min | après 2 ou 3 erreurs | barres, niveaux sur 5 | énoncés exacts, contre-exemples, mode examinateur pour les colles et concours |

## Structure du dépôt

```
tuteur-socratique/
├── SKILL.md              règles communes à tous les profils
└── references/
    ├── primaire.md
    ├── college.md
    ├── lycee.md
    └── superieur.md
```

## Installation

### Claude Code

Copier le dossier de la skill dans le répertoire des skills personnelles :

```bash
cp -r tuteur-socratique ~/.claude/skills/
```

Ou dans `.claude/skills/` d'un projet pour la limiter à ce projet.

### Claude (claude.ai et applications)

1. Compresser le dossier `tuteur-socratique/` en `.zip` (le dossier lui-même, pas
   seulement son contenu).
2. L'importer dans les paramètres de Claude, section Skills.

### ChatGPT

ChatGPT ne lit pas ce format directement. Deux façons de faire :

- **Un GPT pour tous les niveaux** : créer un GPT personnalisé, coller dans ses
  instructions le contenu de `SKILL.md` sans l'en-tête (les lignes entre les deux
  `---`), et ajouter les quatre fichiers de `references/` dans ses connaissances.
- **Un GPT par niveau** : coller `SKILL.md` sans l'en-tête dans les instructions et
  n'ajouter que le fichier du profil voulu dans les connaissances. On peut alors
  supprimer l'étape de choix du profil.

Le contenu de `SKILL.md` sans l'en-tête fait un peu moins de 8 000 caractères, la
limite habituelle des instructions d'un GPT : il n'y a pas la place d'y coller un
profil en plus.

Dans un GPT dédié au tutorat, la section « Garde : vérifier l'intention » peut être
retirée. Deux règles sont à vérifier en priorité après l'installation, car ce sont
les plus fragiles d'un modèle à l'autre : s'arrêter juste après la question, et ne
pas flatter.

## Utilisation

Lancer une séance :

> Apprends-moi les fractions, je suis en CM2.
>
> Fais-moi réviser le théorème de Thalès pour le brevet.
>
> Interroge-moi sur la dérivation, j'ai un DS de spé maths vendredi.
>
> Aide-moi à maîtriser les espaces vectoriels pour mes colles.

Commandes disponibles à tout moment :

| Commande | Effet |
|---|---|
| `ma progression` | affiche la carte de compétences |
| `plus dur` / `plus facile` | ajuste la difficulté |
| `donne-moi la réponse` | sort du mode socratique pour la question en cours (avec des limites selon le profil) |
| `sauvegarde` | produit un bloc daté à conserver |
| `reprendre :` + le bloc | reprend la séance, en commençant par retester ce qui a été vu |

Le bloc de sauvegarde est aussi donné automatiquement à la fin de chaque séance. Il
suffit de le coller dans une nouvelle conversation pour continuer.

## Âge des utilisateurs

Les assistants grand public ont un âge minimum d'utilisation fixé par leurs
conditions (18 ans pour Claude, 13 ans avec accord parental pour ChatGPT, au moment
où ce texte est écrit ; à vérifier). Pour le primaire et le collège, la skill est
donc prévue pour un usage accompagné : l'adulte tient le compte et reste à côté de
l'enfant. Le profil primaire est écrit dans ce sens.

## Limites

- Le tuteur peut se tromper, sur un fait comme sur un point de programme. Il a pour
  consigne de signaler ses doutes, mais le cours du professeur reste la référence.
- Les programmes et les modalités d'examen changent : la skill ne les contient pas,
  elle demande à l'élève ce qui est attendu dans sa classe.
- La mémoire entre deux séances repose sur le bloc de sauvegarde. Sans lui, le
  tuteur repart de zéro.

## Adapter la skill

- Les règles communes (méthode, évaluation, commandes) sont dans `SKILL.md`.
- Ce qui dépend de l'âge (ton, durée, moment où l'on aide, affichage) est dans le
  fichier du profil. Pour ajouter un profil, par exemple pour une discipline ou une
  filière, créer un fichier dans `references/` et l'ajouter à la liste de l'étape 2
  du démarrage dans `SKILL.md`.
