
# Modélisation d'une base de données

Dans cette execice, vous allez aider l'entreprise **Und3** à se doter d'une base de données Postgresql modélisée sur mesure pour ses besoins.

## Description de l'entreprise

**Und3** est une société de service.

### Clientelle

En tant que société de service, **Und3** ne fonctionne qu'en B2B (*Business to Business*). Cela implique que l'ensemble de ses **clients** sont des entreprises avec: 

* un nom de dirigeant
* une raison sociale
* une adresse
* un identifiant unique (**SIRET** pour les entreprises françaises, equivalent étranger pour les quelques entreprises étrangères)

### Agences, regionalisation

Chaque agence: 

* a un directeur
* se situe à une adresse
* est rattachée à une région et une seule

Plusieurs agences peuvent se partager une même région. Cependant, lorsque cela est le cas, une et une seule agence est alors considérée comme l'**agence principale**. Ce découpage en region est, pour des raisons comptables et fiscale, primordial.

### Organisation de la masse salariale

Les salariés ont un salaire annuel, un nom, un prénom et sont liés à une agence.

A **Und3**, il y a trois types *disjoints* d'employés:

* les **fonctionels** (managers, directeurs, comptables): gèrent les aspects internes et organisationels des agences
* les **commerciaux**: en communication avec les clients, ils négocient les **contrats**
* les **consultants**: sont placés chez les clients. Chaque consultant a un manager référent

## Activité de l'entreprise

## Besoins fonctionnels

### Suivi de l'activité des consultants 

Tout consultant est tenu de tenir à jour son **rapport d'activité**. Celui-ci indique, pour chaque demi-journée de jour de travail à quoi cette dernière a été consacrée. Il existe trois types d'activités possible

* **absence**: le consultant a pris un jour de RTT, est malade, en congé, *etc*
* sur site: le consultant se trouve dans l'une des agences **Und3** et travaille sur un sujet interne
* en mission chez le client: dans ce cas, la demi journée doit être liée à un **contrat** en cours de validité

Un directeur d'agence ou manager doit pouvoir être en mesure de récupérer aisément les activités des consultants de leur agence.

### Contrats et facturation au client

Un **contrat** est un acte liant une agence à un client sur une période déterminé en implicant la présence d'un consultant.  

* client
* consultant 
* date de début
* date de fin
* taux journalier (a.k.a *tjm*)

Ils sont typiquement générés/édités par les commerciaux. La **facturation**, assurée par les comptables ou directeurs d'agences (en l'absence de comptable pour les plus petites agences) est effectuée à la fin de chaque mois sur la base:
 
* des contrats (tjm)
* de la présence sur site des consultants engagés pas les contrats

Chaque facture est donc liée à un contrat et doit comporter les informations suivantes:

* identifiant du contrat
* date d'émission de la facture
* date de l'éventuelle dernière modification de la facture
* identité de l'éméteur ou éditeur de la facture
* somme à payer
* somme versée

## Intégration au SI et sécurisation


