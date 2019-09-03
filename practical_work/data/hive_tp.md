# TP Hive

## Environnement
* Hortonworks sandbox v. 3.0 (log en tant que l'utilisateur `raj_ops`)

## Description des données

Les données de ce TP sont tirés de [ce dataset Kaggle](https://www.kaggle.com/citylines/city-lines#cities.csv). Vous les retrouverez dans ce répos en `/data/city-lines.zip`. Le dataset se compose de 7 csv. N'hésitez pas à consulter la page plus plus de détails. 


## Assignment
Pour cet *assignment*, vous veillerez à écrire l'ensemble des requêtes hql nécessaires à la réalisation des différentes tâches dans un fichier du nom de `init_city_lines.hql` (peu importe où vous l'écrirez, tant que vous êtes en mesure de me l'envoyer par mail à la fin du tp). Ce script me permettra d'évaluer la bonne réalisation du TP (donc n'oubliez rien)

### chargement des données en HDFS

Après décompression du zip, par la méthode de votre choix, chargez les données sur l'HDFS en `/user/raj_ops/city_lines`. Assurez-vous que les droits d'accès ne vous gêneront pas pour la suite

### Création de la BDD et des tables externes primaires

Vous allez créer une BDD du nom de `city lines` ainsi qu'une table par CSV (assurez-vous d'identifier le caractère séparateur des champs)

Pour mémoire, une **table externe** sans partition peut être crée en une requête de la manière suivante: 

```sql
CREATE EXTERNAL TABLE nom_de_votre_table(
	son SHEMA,
)
ROW FORMAT le_format_de_vos_lignes
FIELDS TERMINATED BY le_caractère_séparateur_des_champs
STORED AS TEXTFILE
LOCATION '/chemin/vers/les/donnees'
```

NB: soyez attentifs au type des données et souvenez que les [timestamps](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Types#LanguageManualTypes-timestamp) ne sont pas des strings comme les autres

### Création de tables transactionnelles

Nous allons créer 2 tables transactionnelles peuplées par les données extraites des tables primaires. Ces tables, internes, devront être stockée en ORC. 


#### French stations

Voici le schéma attendu pour cette table: 

| nom du champ | type        | description                                     | 
|--------------|:-----------:|:-----------------------------------------------:|
| station_name | STRING      | nom de la station                               |
| city_name    | STRING      | nom de la ville                                 |
