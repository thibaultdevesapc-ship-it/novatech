# Compte rendu du TP final Git - NovaTech

## Mission 5 - Analyse du projet

1. Identifiant court du premier commit : `e899e84`
2. Commit correspondant à l'ajout de la page Contact : `c7ca6c2` (« Ajout de la page Contact avec son formulaire »)
3. Nombre actuel de commits : 8, fusions comprises (obtenu avec `git rev-list --count HEAD`)
4. Commande utilisée pour afficher l'historique sous forme graphique : `git log --oneline --graph --decorate --all`

Commande utilisée pour examiner précisément un commit de la fonctionnalité Contact : `git show c7ca6c2`

## Mission 8 - Commit local incorrect

Commande choisie : `git reset HEAD~1` (équivalent de `git reset --mixed HEAD~1`). Elle convient ici car le commit « Test affichage » n'a été partagé avec personne : on peut donc le retirer de l'historique sans gêner d'autres développeurs.

Les modifications sont toujours présentes car `git reset` en mode mixte déplace la branche sur le commit précédent et vide la zone de staging, mais ne touche pas aux fichiers de la zone de travail. La règle est donc restée dans `style.css`, comme modification non indexée.

La méthode qui aurait aussi supprimé les modifications du fichier est `git reset --hard HEAD~1`.

## Mission 9 - Commit partagé à annuler

Commande utilisée : `git revert ce8a971`

La méthode est différente de celle de la mission 8 car le commit « Ajout promotion » est considéré comme déjà récupéré par d'autres membres de l'équipe. `git reset` réécrirait l'historique et désynchroniserait leurs dépôts. `git revert` crée au contraire un nouveau commit qui applique l'inverse de la modification : l'historique reste intact, le commit « Ajout promotion » y figure toujours, et tout le monde peut récupérer l'annulation normalement.

## Mission 11 - Correction isolée

Commande utilisée : `git cherry-pick bcbe4c5`

Identifiant du commit récupéré : `bcbe4c5` sur la branche `test/experimentations`. Le cherry-pick crée sur `main` un nouveau commit avec le même contenu, mais un identifiant différent.

Une fusion classique n'était pas adaptée car elle aurait intégré tous les commits de la branche de test, y compris les couleurs expérimentales et le texte de test du pied de page. Le cherry-pick permet de ne récupérer que la correction orthographique.

## Mission 12 - Version stable

Tag créé sur le commit `05d3de2` avec `git tag -a v1.0.0 -m "Première version stable de NovaTech"`, puis affiché avec `git show v1.0.0`.

Signification des trois nombres de 1.0.0 (versionnage sémantique) :

- 1 : version majeure, augmentée lors de changements incompatibles avec la version précédente
- 0 : version mineure, augmentée lors de l'ajout de fonctionnalités compatibles
- 0 : version de correctif, augmentée lors de corrections de bugs compatibles

Version suivante selon le cas :

- Correction de bug mineur : 1.0.1
- Nouvelle fonctionnalité compatible : 1.1.0
- Refonte majeure incompatible : 2.0.0

## Questions finales

### 1. Quelle différence existe-t-il entre la zone de travail, la zone de staging et l'historique ?

La zone de travail contient les fichiers tels qu'on les modifie sur le disque. La zone de staging (ou index) prépare le prochain commit : on y place avec `git add` les modifications à enregistrer. L'historique contient les commits, c'est-à-dire les versions enregistrées du projet.

### 2. Pourquoi est-il préférable de réaliser une fonctionnalité sur une branche dédiée ?

Une branche dédiée isole le travail en cours : la branche principale reste stable et fonctionnelle pendant le développement. On peut faire plusieurs commits, tester ou abandonner la fonctionnalité sans gêner le reste du projet, puis l'intégrer une fois terminée.

### 3. Quelle différence fondamentale existe-t-il entre les deux méthodes d'annulation utilisées dans les missions 8 et 9 ?

`git reset` (mission 8) déplace la branche sur un commit antérieur : le commit annulé disparaît de l'historique de la branche, qui est donc réécrit. `git revert` (mission 9) ajoute un nouveau commit qui applique l'inverse de la modification : l'historique existant est conservé. On réserve donc `reset` aux commits locaux non partagés et on utilise `revert` pour les commits déjà partagés.

### 4. Dans quelle situation est-il utile de mettre temporairement ses modifications de côté ?

C'est utile quand on doit changer de tâche ou de branche alors que le travail en cours n'est pas prêt à être commité, par exemple pour une correction urgente. `git stash` met les modifications de côté et laisse un dépôt propre, puis `git stash pop` permet de les récupérer.

### 5. Pourquoi la récupération d'un commit précis peut-elle être préférable à la fusion complète d'une branche ?

Une fusion intègre tous les commits de la branche, y compris ceux qui ne sont pas prêts ou pas souhaités. `git cherry-pick` permet de ne récupérer qu'une modification précise, comme une correction, sans importer le reste.

### 6. À quoi sert HEAD ?

HEAD est un pointeur vers la position actuelle dans le dépôt : il désigne en général la branche active, et donc son dernier commit. C'est le commit sur lequel se base le prochain commit.

### 7. Que représente HEAD~2 ?

HEAD~2 désigne le commit situé deux générations avant HEAD, en suivant le premier parent de chaque commit : c'est le grand-parent de HEAD.

### 8. À quoi sert un tag Git ?

Un tag marque un commit précis avec un nom stable, généralement pour identifier une version comme `v1.0.0`. Contrairement à une branche, il ne se déplace pas. Un tag annoté contient aussi un auteur, une date et un message.

### 9. Pourquoi des commits petits et précis facilitent-ils la maintenance d'un projet ?

Ils rendent l'historique plus lisible et les modifications plus faciles à relire. Il est aussi plus simple de retrouver l'origine d'un bug, d'annuler une seule modification avec `git revert` ou d'en récupérer une seule avec `git cherry-pick`.

### 10. Pourquoi certains fichiers ne doivent-ils pas être versionnés ?

Certains fichiers contiennent des données sensibles, comme les mots de passe ou clés d'un `.env`, qui ne doivent pas se retrouver dans l'historique. D'autres sont générés automatiquement, comme les logs et le cache : ils alourdissent le dépôt, changent souvent, dépendent de chaque machine et n'ont pas d'intérêt pour le projet.

## Réalisation

Ce TP a été réalisé avec Claude Code : les commits comportent la mention `Co-Authored-By: Claude`.
