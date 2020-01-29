# Création d'une base de données à partir d'un modèle explicite

Dans ce TD, nous allons réaliser une base de données de mémoires universitaires inspirée de [cette documentation](https://ausonius.u-bordeaux-montaigne.fr/memoires/dictionnaire.php) de l'Institut Ausonius

Soit le **modèle conceptuel** suivant: 

![](/img/mcd.png)

et son **model physique** correspondant: 

![](/img/mpd.png)

Implémentez cette base de données en Postgresql > 9.6. Outre les relations indiqués dans ces modèles, vous veillerez au points suivants. 

## Contraintes d'intégrité

* Il ne peut y avoir deux mémoires portant le même titre (`titre_mémoire`) au sein de la même université (`univ_soutenance`)
* `date_modification_fiche` sera mis à jour automatiquement [](https://x-team.com/blog/automatic-timestamps-with-postgresql/)
* Un mémoire a forcément une année de début (`etude_annee_debut`). Par défaut, si non renseigné, cette année ne sera jamais plus que l'année de création de la fiche. Il n'a, en revanche, pas forcément d'année de fin (abandon)

## Indexation

* `cote_memoire`
* `diplome_memoire`


## 
