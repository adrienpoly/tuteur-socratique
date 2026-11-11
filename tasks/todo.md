# Version générique pour adultes

## Objectif et critères

Une skill `tuteur-socratique-adulte`, autonome et en un seul fichier, pour un adulte
qui apprend un sujet hors cadre scolaire.

- Corps de `SKILL.md` sous 8 000 caractères.
- Aucune référence à la classe, aux programmes, aux examens ni aux profils.
- Mêmes six commandes que `tuteur-socratique`.
- `tuteur-socratique/` inchangé.

## Étapes

- [x] Lire `SKILL.md`, `references/superieur.md`, README, `.claude/CLAUDE.md`
- [x] Écrire `tuteur-socratique-adulte/SKILL.md`
- [x] Mettre à jour `README.md`
- [x] Mettre à jour `.claude/CLAUDE.md`
- [x] Vérifier la taille, le `name`, les termes scolaires restants
- [x] Jouer une séance d'essai sur les six points de vérification

## Notes de travail

- Les valeurs propres aux adultes viennent de `references/superieur.md` (aide après
  2 ou 3 erreurs, avocat du diable, niveau cible 4, « donne-moi la réponse » sans
  restriction).
- Les deux `SKILL.md` partagent la méthode sans mécanisme commun : toute règle de
  méthode modifiée dans l'un est à reporter dans l'autre (noté dans `CLAUDE.md`).
- « la personne » remplace « élève » dans la version pour adultes.

## Résultats

- Nouveau : `tuteur-socratique-adulte/SKILL.md` (corps de 7 760 caractères).
- Modifiés : `README.md`, `.claude/CLAUDE.md`. `tuteur-socratique/` inchangé.
- Essais joués par des sous-agents ayant le `SKILL.md` pour consignes, sur SQL :
  1. « c'est quoi un intérêt composé ? » : réponse directe, pas de tutorat ;
  2. « Apprends-moi les bases de SQL » : demande objectif, acquis et supports ;
  3. réponse fausse : pas de correction pendant le diagnostic ; réponse vague :
     refusée, suivie d'une question plus étroite ; « je sais pas » : un cran plus
     bas ;
  4. carte au format par défaut, `?` pour les compétences non testées ;
  5. « sauvegarde » : bloc complet ; « reprendre : » : retest de la compétence la
     plus ancienne d'abord.
- Limite de l'essai 3 à 5 : un seul sous-agent a écrit tous les tours du tuteur en
  connaissant la suite ; à rejouer dans une vraie conversation.
- Observation : après le diagnostic, une compétence est placée à 3/5 sur une seule
  bonne réponse, signalée « placement de départ, à confirmer ». Les deux skills
  ne disent pas comment fixer le niveau initial ; à préciser si ce placement
  paraît trop généreux.

# Améliorations version adulte + GPT collège (2026-11-10)

- [x] Adulte : garde étendue aux demandes de travail, maintien en séance,
      conversations indépendantes, « par quoi reprendre » dans le bloc
- [x] Niveau de départ après diagnostic (3 au plus si réussi, 0 à 2 sinon), reporté
      dans `tuteur-socratique/SKILL.md` et `chatgpt/college.md`
- [x] `chatgpt/college.md` : règles communes + profil collège en un seul texte
- [x] README et `.claude/CLAUDE.md` mis à jour
- [x] Tailles : voir Résultats

## Résultats

- Tailles : `tuteur-socratique` 7 853, `tuteur-socratique-adulte` 7 941,
  `chatgpt/college.md` 7 896 caractères.
- Séances d'essai tour par tour (un sous-agent tuteur, réponses de l'élève envoyées
  une à une) : collège sur Pythagore, adulte sur SQL. Vérifié : question ponctuelle
  et demande de travail sans tutorat, une question à la fois, erreur suivie d'une
  question plus étroite, réponse non justifiée non comptée, niveau de départ
  plafonné à 3, `?` pour le non testé, bloc de sauvegarde avec « reprendre par ».
- Non rejoué : « reprendre : » dans une nouvelle conversation, avocat du diable,
  bilan final, et les profils primaire, lycée et supérieur.

# Versions ChatGPT par profil, aide aux devoirs, élève à instruire (2026-11-11)

- [x] `chatgpt/primaire.md`, `lycee.md`, `superieur.md` (commit `97c9a69`, poussé)
- [x] `aide-aux-devoirs/SKILL.md` et `eleve-a-instruire/SKILL.md`
- [x] Workflow de release, README et `.claude/CLAUDE.md` mis à jour
- [x] Tailles et séances d'essai : voir Résultats

## Résultats

- Tailles : `chatgpt/primaire.md` 7 281, `lycee.md` 7 617, `superieur.md` 7 406 ;
  `aide-aux-devoirs` 6 935, `eleve-a-instruire` 6 764 caractères.
- Séances d'essai tour par tour (un sous-agent par skill), niveau collège.
  `aide-aux-devoirs` sur Pythagore : énoncé demandé d'abord, « donne-moi la
  réponse » refusé avec l'indice le plus bas, réponse fausse signalée sans être
  corrigée, unité et justification exigées, rédaction de français non écrite.
  `eleve-a-instruire` sur l'addition des fractions : règle annoncée, explication
  fausse mise en contradiction dans le rôle, bilan hors du rôle avec tableau,
  erreur corrigée, piège dévoilé, points non formulés notés « manquant ».
- Non rejoué : les trois nouveaux fichiers `chatgpt/` ; pour les deux skills, les
  profils primaire, lycée et supérieur, « sauvegarde » / « reprendre : », le
  blocage, la garde (question ponctuelle), et l'essai dans ChatGPT.
- À faire sur demande : commit, puis tag mineur pour publier les deux `.zip` (les
  liens du README renvoient une erreur 404 jusque-là).
