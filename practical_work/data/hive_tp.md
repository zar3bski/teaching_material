# TP Hive

## Environnement
* Hortonworks sandbox v. 3.0 (log en tant que l'utilisateur `raj_ops`)
* HDFS 3.1.1
* [Hive](https://youtu.be/0FcDXL5Aw0o?list=RD1yS1ay045B4) 3.1.0

## Description des données

Les données de ce TP sont tirées de [ce dataset Kaggle](https://www.kaggle.com/citylines/city-lines#cities.csv). Vous les retrouverez dans ce répos en `/data/city-lines.zip`. Le dataset se compose de 7 csv. N'hésitez pas à consulter la page ppour plus de détails. 

## Assignment

Pour cet *assignment*, vous veillerez à écrire l'ensemble des requêtes hql nécessaires à la réalisation des différentes tâches dans un fichier du nom de `init_city_lines.hql` (peu importe où vous l'écrirez, tant que vous êtes en mesure de me l'envoyer à la fin du tp). Ce script me permettra d'évaluer la bonne réalisation du TP (donc n'oubliez rien).

### Chargement des données en HDFS

Après décompression du **zip**, par la méthode de votre choix, chargez les données sur l'**HDFS** en `/user/raj_ops/city_lines`. Assurez-vous que les **droits d'accès** ne vous gêneront pas pour la suite

### Création de la BDD et des tables externes primaires

Vous allez **créer une BDD** du nom de `city_lines` ainsi qu'**une table pour chacun des CSV suivants**: 

* cities.csv
* stations.csv
* lines.csv
* track_lines.csv

(assurez-vous d'identifier le **caractère séparateur** des champs)

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

**NB**: soyez attentifs au type des données et souvenez que les [timestamps](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Types#LanguageManualTypes-timestamp) ne sont pas des strings comme les autres

### Création de tables transactionnelles

Nous allons créer 2 tables transactionnelles peuplées par les données extraites des **tables primaires**. Ces tables, internes, devront être stockées au format ORC. 

Souvenez-vous, une table transactionnelle supporte `INSERT`. Il est par conséquent relativement simple de la peupler à l'aide d'un `SELECT`: 

```sql
INSERT INTO nom_de_votre_table_transactionnelle 
SELECT qqchose FROM une_autre_table
WHERE une_certaine_condition
```

#### Old French stations

Voici le schéma attendu pour cette table: 

`old_french_station` : 

| nom du champ | type            | description                                            | 
|--------------|:---------------:|:------------------------------------------------------:|
| station_id   | **INT**         | id de la station                                       |
| station_name | **STRING**      | nom de la station                                      |
| city_name    | **STRING**      | nom de la ville                                        |
| build_time   | **INT**         | le nombre d'années nécessaires à la construction       |
| coord        | **STRING**      | les coordonnées géographiques de la station            |


La table ne devra contenir que des données relatives aux stations:
* situées en France 
* contruites avant le premier choc pétrolier (1973) (vérifiez `opening`)
* encore en activité (vérifiez que `closure` diffère de 999999)

#### Recent American lines

`recent_american_lines` : 

| nom du champ | type            | description                                              | 
|--------------|:---------------:|:--------------------------------------------------------:|
| line_id      | **INT**         | id de la ligne                                           |
| city_name    | **STRING**      | nom de la ville                                          |
| line_name    | **STRING**      | nom de la ligne (utilisez `url_name` plutôt que `name`)  |
| section_nb   | **INT**         | le nombre de segments dans sur ligne                     |


La table ne devra contenir que des données relatives aux lignes:
* situées aux États Unis
* dont au moins une section à été rénovée depuis le 31 Mars 2018 (voir `updated_at` dans `station_lines`)

