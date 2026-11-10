# CLAUDE.md

Ce dépôt contient deux skills de tutorat socratique en français : `tuteur-socratique`
pour les élèves et étudiants du CP au supérieur, et `tuteur-socratique-adulte`, une
version générique pour un adulte qui apprend un sujet hors cadre scolaire. Il n'y a
pas de code : uniquement des fichiers Markdown lus par un modèle (Claude, ou ChatGPT
via un GPT personnalisé).

## Structure

```
README.md                          présentation et installation, pour les humains
tuteur-socratique/
├── SKILL.md                       règles communes à tous les profils
└── references/
    ├── primaire.md                CP à CM2
    ├── college.md                 6e à 3e
    ├── lycee.md                   2de à Tle, CAP, bac pro
    └── superieur.md               après le bac, adultes
tuteur-socratique-adulte/
└── SKILL.md                       version générique pour adultes, sans profil
chatgpt/
└── college.md                     instructions d'un GPT collège, en un seul texte
```

## Où mettre quoi

- `tuteur-socratique/SKILL.md` : ce qui vaut pour tous les âges (garde d'intention,
  démarrage, carte de compétences, boucle d'enseignement, évaluation, commandes,
  sauvegarde).
- `references/<profil>.md` : ce qui dépend de l'âge (ton, durée de séance, nombre
  de compétences, moment où l'on aide, avocat du diable, affichage de la carte,
  niveau cible, limites de « donne-moi la réponse »). Les règles du profil
  l'emportent sur les règles communes.
- Ne duplique pas une règle commune dans un profil. Si une règle doit varier selon
  l'âge, `SKILL.md` renvoie au profil (« selon le profil ») et chaque profil donne
  sa valeur.
- Les quatre profils gardent les mêmes rubriques, dans le même ordre, de « Public »
  à « Donne-moi la réponse ». Une rubrique propre à un seul profil (comme
  « Sauvegarde » en primaire) se place à la fin.
- `tuteur-socratique-adulte/SKILL.md` : tout ce qui concerne la version pour
  adultes, dans ce seul fichier. Il reprend la méthode de `tuteur-socratique/SKILL.md`
  et les valeurs du profil supérieur, sans classe, programme ni examen. Une règle de
  méthode (boucle d'enseignement, évaluation, carte, commandes) modifiée dans l'une
  des deux skills est à reporter dans l'autre.
- `chatgpt/college.md` : fusion de `tuteur-socratique/SKILL.md` et de
  `references/college.md`, sans en-tête YAML, à coller tel quel dans les
  instructions d'un GPT. Toute règle modifiée dans l'une de ses deux sources est à
  y reporter. Le fichier entier doit rester sous 8 000 caractères
  (`wc -m chatgpt/college.md`).

## Contraintes

- **Taille des `SKILL.md`** : le corps de chacun, sans l'en-tête YAML, doit rester
  sous 8 000 caractères pour tenir dans les instructions d'un GPT personnalisé.
  Vérifier après chaque modification :

  ```bash
  for f in tuteur-socratique tuteur-socratique-adulte; do
    awk 'f>=2{print} /^---$/{f++}' "$f/SKILL.md" | wc -m
  done
  ```

  Si la limite approche dans `tuteur-socratique`, déplacer du contenu vers les
  profils plutôt que de comprimer les règles.
- **En-tête YAML** : `name` doit rester identique au nom du dossier
  (`tuteur-socratique`, `tuteur-socratique-adulte`). La `description` décide du
  déclenchement de la skill : elle doit garder les phrases déclencheuses en français
  et l'exclusion des questions ponctuelles. Celle de la version pour adultes renvoie
  vers `tuteur-socratique` pour qui a une classe ou un examen, afin que les deux
  skills ne se déclenchent pas sur la même demande.
- **Pas de contenu de programme en dur** : ne pas écrire les modalités d'un examen
  (épreuves, coefficients, dates) ni le détail d'un programme. Ils changent, et le
  tuteur demande à l'élève ce qui est attendu dans sa classe.
- **Commandes** : les commandes de l'élève (« ma progression », « plus dur »,
  « plus facile », « donne-moi la réponse », « sauvegarde », « reprendre : ») sont
  citées dans les deux `SKILL.md`, dans les profils et dans le README. Tout
  changement se fait aux quatre endroits.
- **README** : le tableau des profils et la section ChatGPT reprennent des valeurs
  des profils (durées, nombre d'erreurs avant l'aide, taille de `SKILL.md`). Les
  mettre à jour en même temps.

## Style d'écriture

- Tout est en français, avec les accents et la typographie française (guillemets
  « », espace avant `:` `;` `?` `!`).
- Les fichiers de la skill s'adressent au modèle à la deuxième personne du
  singulier, à l'impératif. Le modèle tutoie l'élève.
- Chaque règle dit quoi faire et, quand ce n'est pas évident, pourquoi. Pas de
  majuscules d'insistance en dehors du « UNE question à la fois » existant.
- Vocabulaire constant : « élève » (pas « apprenant », « utilisateur »),
  « compétence » (pas « sous-compétence », « skill »), « carte de compétences »,
  « niveau », « profil », « séance », « bloc de sauvegarde ». Dans la version pour
  adultes, « la personne » remplace « élève ».
- Lignes coupées vers 85 caractères.

## Vérifier une modification

Il n'y a pas de tests automatiques. Après un changement de comportement, jouer une
courte séance par profil touché, en tenant le rôle de l'élève, et vérifier au
minimum :

1. une question ponctuelle (« c'est quoi une fraction ? ») ne lance pas le tutorat ;
2. le tuteur demande la classe, puis s'arrête après chaque question, sans indice ;
3. une réponse fausse reçoit une question plus étroite, pas la réponse ;
4. une réponse vague n'est pas validée et aucun niveau ne monte sur une seule
   réussite ;
5. la carte s'affiche au format du profil, avec `?` pour ce qui n'est pas testé ;
6. « sauvegarde » puis « reprendre : » dans une nouvelle conversation commence par
   un retest.

Pour la version pour adultes, les mêmes points s'appliquent, avec l'objectif et
l'expérience à la place de la classe au point 2 et la carte par défaut au point 5.

Pour une modification d'un `SKILL.md`, refaire aussi la vérification de taille
ci-dessus.

## Git

Ne pas commiter ni pousser sans demande explicite.

## Publication

Les utilisateurs de l'app Claude installent les skills à partir des `.zip` attachés
à la dernière release GitHub. Un changement fusionné dans `main` ne leur parvient
donc qu'après la publication d'une nouvelle version.

Ne publier que sur demande explicite, comme pour un commit. Étapes :

1. Vérifier que `main` est à jour, sans changement en attente, et que les
   vérifications ci-dessus (taille, séance d'essai) ont été faites.
2. Choisir le numéro à partir du dernier tag (`git tag --sort=-v:refname | head -1`) :
   correctif pour une reformulation sans effet sur le comportement, mineur pour une
   règle ajoutée ou modifiée, majeur pour un changement des commandes ou du format
   du bloc de sauvegarde, qui casse la reprise d'une séance sauvegardée.
3. Créer et pousser le tag depuis `main` :

   ```bash
   git tag vX.Y.Z && git push origin vX.Y.Z
   ```

4. Le tag déclenche `.github/workflows/release.yml`, qui compresse chaque dossier de
   skill et crée la release avec `tuteur-socratique.zip` et
   `tuteur-socratique-adulte.zip`. Vérifier le résultat :

   ```bash
   gh run list --workflow release.yml --limit 1
   gh release view vX.Y.Z --json assets -q '.assets[].name'
   ```

Le README pointe vers `releases/latest/download/<skill>.zip` : ne pas renommer un
dossier de skill ni un `.zip` sans mettre à jour le workflow et ces liens. Une
nouvelle skill s'ajoute à la boucle du workflow, à la commande `gh release create`
et aux liens du README. `chatgpt/college.md` n'est pas dans les `.zip` : il se copie
depuis le dépôt.
