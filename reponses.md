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
