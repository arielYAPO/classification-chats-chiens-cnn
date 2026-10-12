# Classification d'images de chats et de chiens

Projet de classification binaire d'images réalisé avec TensorFlow/Keras. Le travail compare un CNN construit de zéro à une approche de transfer learning avec MobileNetV2, puis étudie plusieurs réglages : résolution, augmentation de données, Batch Normalization, Dropout et fine-tuning.

## Équipe et répartition du travail

- **Kadjio MBALLA** : préparation et exploration des données, prétraitement des images et développement du CNN de référence.
- **Karel BOU FERRAA** : mise en place du transfer learning avec MobileNetV2 et comparaison des expériences.
- **Ariel YAPO** : fine-tuning, évaluation finale et interprétation des métriques.
- **Travail collectif** : choix méthodologiques, analyse des résultats, vérification du notebook et préparation de la présentation.

Le projet a été réalisé principalement en local avant la création de ce dépôt. L'historique Git ne représente donc pas les contributions individuelles ; la répartition ci-dessus décrit le travail effectué par l'équipe.

## Résultats principaux

| Modèle | Résultat de validation |
|---|---:|
| CNN construit de zéro, images 96 × 96 | 65,5 % d'accuracy |
| MobileNetV2 gelé, entraînement prolongé | 95,1 % d'accuracy |

Le modèle final évalué une seule fois sur le jeu de test obtient :

- **Accuracy : 94,3 %**
- **Précision : 94,5 %**
- **Rappel : 94,0 %**
- **F1-score : 94,2 %**
- **Matrice de confusion :** `[[189, 11], [12, 188]]`

Les expériences à 128 × 128 et le fine-tuning ont ensuite été conservés comme analyses complémentaires. Leurs résultats de validation ne remplacent pas le score officiel du jeu de test.

## Contenu du dépôt

```text
classification-chats-chiens-cnn/
├── notebooks/
│   ├── classification_chats_chiens_cnn.ipynb
│   └── experiences_completes.ipynb
├── artifacts/             # graphiques utilisés dans les notebooks
├── models/
│   └── mobilenetv2_frozen.keras
├── requirements.txt
└── README.md
```

- `classification_chats_chiens_cnn.ipynb` est le notebook final à lire et à présenter.
- `experiences_completes.ipynb` conserve le détail des essais et des recherches.
- `mobilenetv2_frozen.keras` est le modèle sélectionné pour l'évaluation officielle.

## Données

Le dataset n'est pas inclus dans le dépôt. Le contenu du dossier `cats_and_dogs_filtered` doit être placé dans `data/` avec la structure suivante :

```text
data/
├── train/
│   ├── cats/
│   └── dogs/
└── validation/
    ├── cats/
    └── dogs/
```

Le dossier d'entraînement fourni contient 2 000 images. Il est séparé de manière stratifiée en 1 600 images d'entraînement et 400 images de test, avec `random_state=42`. Les 1 000 images du dossier `validation` servent au réglage des modèles.

## Installation et exécution

Avec Python installé :

```bash
python -m venv .venv
```

Sous Windows PowerShell :

```powershell
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
jupyter lab
```

Ouvrir ensuite `notebooks/classification_chats_chiens_cnn.ipynb` et exécuter les cellules dans l'ordre. Les chemins sont construits relativement au dossier du projet.

## Méthode

Le notebook suit les étapes suivantes : préparation des données, séparation entraînement/validation/test, entraînement d'un CNN de référence, comparaison d'optimisations, transfer learning avec MobileNetV2, évaluation finale puis fine-tuning exploratoire. Les décisions sont justifiées à partir de l'accuracy, de la loss, de la précision, du rappel, du F1-score, de la matrice de confusion et du temps de calcul.
