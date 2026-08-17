# Guide Google Colab - WolBanking77

## Objectif

Ce projet classe des requetes bancaires ecrites en wolof dans l'une des 77 intentions
de WolBanking77. Il compare une baseline de Machine Learning a un Transformer
multilingue : XLM-RoBERTa.

## Organisation des fichiers

Le code et les donnees viennent de GitHub. Google Drive ne contient que les sorties
de l'execution : checkpoints, rapports CSV/JSON et graphiques. Cette separation evite
de versionner des poids de modeles volumineux dans GitHub et rend les entrainements
reproductibles.

```
GitHub -> /content/WolBanking77                 code et data
Drive  -> /content/drive/MyDrive/WolBanking77_runs
           models/                             meilleur checkpoint Transformer
           reports/                            metriques, figures, rapports
```

## Avant l'execution

1. Creez un depot GitHub contenant ce projet, y compris `data/5k_split` ou
   `data/full`.
2. Copiez l'URL HTTPS du depot, par exemple
   `https://github.com/votre-compte/WolBanking77.git`.
3. Ouvrez `notebooks/WolBanking77_Colab.ipynb` dans Google Colab.
4. Dans Colab, choisissez `Runtime > Change runtime type > T4 GPU`.
5. Renseignez `GITHUB_REPOSITORY_URL` dans la premiere cellule de code.

Un depot prive demande une authentification GitHub. Il est preferable de ne pas
enregistrer un token personnel directement dans le notebook.

## Pipeline

1. Le notebook clone le projet depuis GitHub et monte Drive.
2. Les CSV sont lus depuis le clone, a partir de `input_wo` et `label`.
3. Le nettoyage ne modifie que les espaces et elimine les textes vides ou repetes.
4. La baseline utilise TF-IDF (mots et caracteres) puis LinearSVC.
5. Le Transformer utilise XLM-RoBERTa avec une validation stratifiee de 10 % du train.
6. Le meilleur checkpoint, selon le macro-F1 de validation, est immediatement ecrit
   dans Google Drive pendant l'entrainement.
7. Le test officiel est utilise une seule fois, apres l'entrainement, pour comparer
   les deux modeles.

## Mesures

- `accuracy` : proportion globale de predictions correctes.
- `macro_f1` : moyenne des F1 de toutes les intentions. C'est la mesure principale,
  car chaque intention compte autant, meme si les classes n'ont pas exactement le
  meme nombre d'exemples.

## Resultats

Apres execution, consultez `WolBanking77_runs/reports` dans Drive pour les graphiques,
rapports de classification et fichiers de comparaison. Le meilleur Transformer est
dans `WolBanking77_runs/models/xlmr_<dataset>/`.
