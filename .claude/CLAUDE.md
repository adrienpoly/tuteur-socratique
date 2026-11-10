# CLAUDE.md

Ce dépôt contient une skill de tutorat socratique en français, pour les élèves et
étudiants du CP au supérieur. Il n'y a pas de code : uniquement des fichiers
Markdown lus par un modèle (Claude, ou ChatGPT via un GPT personnalisé).

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
```

## Où mettre quoi

- `SKILL.md` : ce qui vaut pour tous les âges (garde d'intention, démarrage, carte
  de compétences, boucle d'enseignement, évaluation, commandes, sauvegarde).
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

## Contraintes

- **Taille de `SKILL.md`** : le corps, sans l'en-tête YAML, doit rester sous
  8 000 caractères pour tenir dans les instructions d'un GPT personnalisé. Vérifier
  après chaque modification :

  ```bash
  awk 'f>=2{print} /^---$/{f++}' tuteur-socratique/SKILL.md | wc -m
  ```

  Si la limite approche, déplacer du contenu vers les profils plutôt que de
  comprimer les règles.
- **En-tête YAML** : `name` doit rester identique au nom du dossier
  (`tuteur-socratique`). La `description` décide du déclenchement de la skill :
  elle doit garder les phrases déclencheuses en français et l'exclusion des
  questions ponctuelles.
- **Pas de contenu de programme en dur** : ne pas écrire les modalités d'un examen
  (épreuves, coefficients, dates) ni le détail d'un programme. Ils changent, et le
  tuteur demande à l'élève ce qui est attendu dans sa classe.
- **Commandes** : les commandes de l'élève (« ma progression », « plus dur »,
  « plus facile », « donne-moi la réponse », « sauvegarde », « reprendre : ») sont
  citées dans `SKILL.md`, dans les profils et dans le README. Tout changement se
  fait aux trois endroits.
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
  « niveau », « profil », « séance », « bloc de sauvegarde ».
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

Pour une modification de `SKILL.md`, refaire aussi la vérification de taille
ci-dessus.

## Git

Ne pas commiter ni pousser sans demande explicite.
