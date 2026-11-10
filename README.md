# Tuteur socratique

Deux skills pour Claude (utilisables aussi avec ChatGPT) qui transforment
l'assistant en tuteur personnel :

- `tuteur-socratique` : pour les élèves et étudiants français, du CP au supérieur ;
- `tuteur-socratique-adulte` : une version générique pour un adulte qui veut
  apprendre un sujet de son choix, hors cadre scolaire.

Le tuteur n'explique pas le cours : il pose des questions, une à la fois, qui
obligent l'élève à raisonner, prévoir et justifier. Il suit la progression sur une
carte de compétences et ne valide un niveau que sur des réussites réelles.

## Ce que font les skills

- **Diagnostic de départ** : 3 à 5 questions pour situer l'élève avant d'enseigner
  quoi que ce soit. Une réussite au diagnostic place une compétence au niveau 3 au
  plus.
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
- **Ancrage français** (`tuteur-socratique` seulement) : programmes officiels,
  classe de l'élève, examens (brevet, bac, partiels, concours), notations et
  terminologie françaises, exigence de rédaction.

## Quatre profils scolaires

Le tuteur demande la classe au début de la séance et charge le profil correspondant.

| Profil | Classes | Séance | Aide directe | Carte | Particularités |
|---|---|---|---|---|---|
| [Primaire](tuteur-socratique/references/primaire.md) | CP à CM2 | 10 à 15 min | après 2 erreurs, indice dès la première | étoiles | phrases courtes, exemples concrets, pas d'avocat du diable, résumé pour l'adulte |
| [Collège](tuteur-socratique/references/college.md) | 6e à 3e | 20 à 30 min | après 2 erreurs | barres + échelle du socle commun | brevet, pas de résultat final donné sur un devoir à rendre |
| [Lycée](tuteur-socratique/references/lycee.md) | 2de à Tle, CAP, bac pro | 30 à 45 min | après 3 erreurs | barres, niveaux sur 5 | épreuves du bac, méthodes (dissertation, commentaire, démonstration), entraînement en temps limité |
| [Supérieur](tuteur-socratique/references/superieur.md) | après le bac, adultes | 45 à 60 min | après 2 ou 3 erreurs | barres, niveaux sur 5 | énoncés exacts, contre-exemples, mode examinateur pour les colles et concours |

## Version pour adultes

`tuteur-socratique-adulte` reprend la même méthode (diagnostic, carte de
compétences, évaluation exigeante, révisions espacées, bilan final, mêmes
commandes) sans rien de scolaire. Elle tient en un seul fichier, sans profil.

- **Démarrage** : au lieu de la classe, le tuteur demande pourquoi la personne veut
  apprendre le sujet, ce qu'elle veut savoir faire à la fin, ce qu'elle connaît déjà
  et les supports qu'elle utilise.
- **Découpage** : selon la logique du domaine et l'usage visé, pas selon un
  programme.
- **Questions** : tirées du métier ou du projet de la personne ; l'expérience
  déclarée ne vaut pas preuve.
- **Réglages** : séance de 30 à 60 minutes, aide directe après 2 ou 3 erreurs,
  avocat du diable, niveau cible 4 (5 sur demande), « donne-moi la réponse » sans
  restriction.

Pour un étudiant ou un adulte en formation qui prépare un examen, préférer
`tuteur-socratique` et son profil supérieur.

## Structure du dépôt

```
tuteur-socratique/
├── SKILL.md              règles communes à tous les profils
└── references/
    ├── primaire.md
    ├── college.md
    ├── lycee.md
    └── superieur.md
tuteur-socratique-adulte/
└── SKILL.md              version générique pour adultes, en un seul fichier
chatgpt/
└── college.md            règles communes + profil collège, à coller dans un GPT
```

## Installation

### Claude Code

Copier le dossier de la skill voulue (ou les deux) dans le répertoire des skills
personnelles :

```bash
cp -r tuteur-socratique tuteur-socratique-adulte ~/.claude/skills/
```

Ou dans `.claude/skills/` d'un projet pour la limiter à ce projet.

### Claude (claude.ai et applications)

1. Télécharger le `.zip` de la skill voulue :
   - [tuteur-socratique.zip](https://github.com/adrienpoly/tuteur-socratique/releases/latest/download/tuteur-socratique.zip)
     (élèves et étudiants, du CP au supérieur) ;
   - [tuteur-socratique-adulte.zip](https://github.com/adrienpoly/tuteur-socratique/releases/latest/download/tuteur-socratique-adulte.zip)
     (adultes, hors cadre scolaire).
2. L'importer tel quel, sans le décompresser, dans les paramètres de Claude,
   section Skills.

Ces fichiers sont produits à chaque version publiée. Pour installer une version
modifiée, compresser soi-même le dossier de la skill (le dossier lui-même, pas
seulement son contenu) et importer ce `.zip`.

### ChatGPT

ChatGPT ne lit pas ce format directement. Trois façons de faire :

- **Un GPT pour tous les niveaux** : créer un GPT personnalisé, coller dans ses
  instructions le contenu de `SKILL.md` sans l'en-tête (les lignes entre les deux
  `---`), et ajouter les quatre fichiers de `references/` dans ses connaissances.
- **Un GPT par niveau** : coller `SKILL.md` sans l'en-tête dans les instructions et
  n'ajouter que le fichier du profil voulu dans les connaissances. On peut alors
  supprimer l'étape de choix du profil.
- **Un GPT pour adultes** : coller dans les instructions le contenu de
  `tuteur-socratique-adulte/SKILL.md` sans l'en-tête. Il n'y a aucun fichier à
  ajouter dans les connaissances.
- **Un GPT pour le collège** : coller dans les instructions tout le contenu de
  `chatgpt/college.md`, qui réunit les règles communes et le profil collège en un
  seul texte de moins de 8 000 caractères. Aucun fichier à ajouter.

Le contenu de chaque `SKILL.md` sans l'en-tête fait un peu moins de 8 000
caractères, la limite habituelle des instructions d'un GPT : il n'y a pas la place
d'y coller un profil en plus.

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

Avec la version pour adultes :

> Apprends-moi les bases de SQL, je veux écrire seule les requêtes de mon équipe.
>
> Je veux apprendre à lire un bilan comptable, interroge-moi.

Commandes disponibles à tout moment :

| Commande | Effet |
|---|---|
| `ma progression` | affiche la carte de compétences |
| `plus dur` / `plus facile` | ajuste la difficulté |
| `donne-moi la réponse` | sort du mode socratique pour la question en cours (avec des limites selon le profil scolaire) |
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

- Les règles communes (méthode, évaluation, commandes) sont dans
  `tuteur-socratique/SKILL.md`.
- Ce qui dépend de l'âge (ton, durée, moment où l'on aide, affichage) est dans le
  fichier du profil. Pour ajouter un profil, par exemple pour une discipline ou une
  filière, créer un fichier dans `references/` et l'ajouter à la liste de l'étape 2
  du démarrage dans `SKILL.md`.
- La version pour adultes est un fichier indépendant : une règle de méthode modifiée
  dans l'une des deux skills est à reporter dans l'autre.
- Pour publier une version : pousser un tag `vX.Y.Z`. Le workflow
  `.github/workflows/release.yml` crée la release et y attache les deux `.zip`.
