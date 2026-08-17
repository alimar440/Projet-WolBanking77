# WolBanking77

Classification de 77 intentions bancaires en langue wolof, avec comparaison entre
une baseline de machine learning et un Transformer multilingue.

## Donnees

Les fichiers sont attendus sous `data/` :

- `5k_split/train/train.csv` et `5k_split/test/test.csv` : 4 000 / 1 000 exemples.
- `full/train/train.csv` et `full/test/test.csv` : 7 832 / 1 959 exemples.

Les notebooks utilisent la colonne `input_wo` comme texte et `label` comme cible.
Pour changer de jeu de donnees, modifier `DATASET = "5k_split"` dans les notebooks.

## Execution dans Google Colab

Le notebook unique est `notebooks/WolBanking77_Colab.ipynb`. Il clone le projet depuis
GitHub dans Colab, puis monte Google Drive pour sauvegarder les checkpoints, rapports
et figures dans `MyDrive/WolBanking77_runs`.

1. Poussez ce projet, y compris les donnees, dans votre depot GitHub.
2. Ouvrez le notebook dans Colab et renseignez `GITHUB_REPOSITORY_URL`.
3. Activez un GPU Colab avant l'entrainement Transformer.
4. Executez les cellules de haut en bas.

Le meilleur checkpoint est sauvegarde dans Drive apres chaque amelioration du macro-F1
de validation. La documentation detaillee est dans `docs/GUIDE_COLAB.md`.

## Mesures retenues

- Accuracy : performance globale.
- Macro F1 : moyenne des F1 par intention, adaptee aux eventuels desequilibres.
- Rapport de classification et matrice de confusion : analyse des intentions confondues.
