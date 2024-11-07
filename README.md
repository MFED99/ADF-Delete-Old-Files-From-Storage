
# Suppression des fichiers anciens dans Azure Blob Storage avec Azure Data Factory
## 💡 Description du Projet
L'objectif de ce projet est de montrer comment j'ai utilisé Azure Data Factory (ADF) pour supprimer automatiquement les fichiers anciens présents dans Azure Blob Storage. Ce processus est utile pour la gestion de l’espace de stockage, en supprimant des fichiers obsolètes ou inutiles, et il permet de garder l’environnement de stockage propre et optimisé.

## 👣 Structure du Projet
Étapes du Flux de Travail

### Création du Linked Service :
J'ai commencé par configurer un Linked Service pointant vers Azure Blob Storage, où se trouvent les fichiers à gérer. Cette connexion permet à ADF d'accéder aux fichiers dans le Blob Storage et de réaliser les actions nécessaires.

### Création des Datasets :
Pour ce projet, j'ai créé deux Datasets qui pointent vers le même compte de stockage et le même dossier dans Azure Blob Storage.

Le premier Dataset contient un paramètre à entrer pour spécifier le dossier ou les fichiers à traiter.
Le second Dataset ne contient pas de paramètre et est utilisé pour obtenir la liste des fichiers dans le dossier cible.

#### Conception du Pipeline :
J'ai conçu un pipeline automatisé pour supprimer les anciens fichiers. Les étapes sont les suivantes :

#### Activity Get Metadata :
J'ai utilisé l'activité Get Metadata pour récupérer tous les noms des fichiers présents dans le dossier ciblé par le premier Dataset. Cette étape permet d'obtenir une liste des fichiers "enfant" présents dans le dossier spécifié.

#### Activity ForEach :
Une fois que la liste des fichiers est récupérée, l’activité ForEach permet de parcourir tous les fichiers et de vérifier s'ils répondent à une certaine condition (par exemple, s'ils sont anciens en fonction de leur date de création ou de modification).

#### Activity Delete :
Dans le cadre de chaque itération de l'activité ForEach, une activité Delete est exécutée pour supprimer les fichiers qui répondent à la condition définie. Cette activité utilise un Dataset avec paramètre, où le paramètre est le nom du fichier à supprimer (obtenu lors de l'itération ForEach).

### Paramétrisation Flexible :
L'utilisation de paramètres dans les Datasets permet de rendre ce processus flexible et réutilisable pour différents dossiers ou différents critères de sélection des fichiers à supprimer. Le paramètre d'entrée dans le Dataset permet de spécifier dynamiquement le chemin des fichiers à traiter, et le paramètre de sortie est utilisé pour identifier quel fichier supprimer.

## 📈 Fonctionnalités et Avantages

- Automatisation et Orchestration : Le processus de suppression des fichiers anciens est entièrement automatisé, ce qui réduit les erreurs humaines et les tâches manuelles répétitives.
- Optimisation de l'Espace de Stockage : En supprimant les fichiers obsolètes, l'espace de stockage dans Azure Blob Storage est optimisé, ce qui permet de gérer plus efficacement les ressources.
- Scalabilité : Azure Data Factory est capable de gérer de grands volumes de fichiers et s’adapte bien à des environnements de production où la gestion des fichiers dans un Blob Storage devient critique.
- Flexibilité des Critères : Grâce aux paramètres et à la logique définie dans le pipeline, il est facile d’ajuster les critères de sélection des fichiers à supprimer (par exemple, les fichiers plus vieux qu’une certaine date).
