# Lire les DECP consolidées sans se tromper

*Le grain, les montants, les groupements. Victor Lavolé, Temi, novembre 2026.*

Le jeu [« Données essentielles de la commande publique consolidées (format tabulaire) »](https://www.data.gouv.fr/datasets/608c055b35eb4e6ee20eb325/), consolidé par Colin Maudry (decp.info), est la meilleure porte d'entrée vers les marchés attribués en France. Il se lit facilement de travers. Voici les règles que nous appliquons dans Temi, et pourquoi.

## 1. Une ligne n'est pas un marché

- **Une ligne est un couple marché-titulaire.** Un marché attribué à un groupement occupe une ligne par titulaire. Compter des marchés, c'est compter des `uid` distincts. La description du jeu le dit, section « Compter les marchés publics ».
- **Seules les lignes `donneesActuelles = true` comptent.** Les autres, fausses ou vides, sont les versions antérieures d'un marché modifié en cours d'exécution.
- **Un titulaire répété dans un même marché ne compte qu'une fois.** Le cas touche environ 9 000 marchés depuis 2022 ; sans cette règle, le montant partagé de leurs titulaires est sous-estimé.
- **Les attributs du marché se lisent une fois par `uid`.** Quand ses lignes divergent, nous retenons le plus grand `offresRecues`, le premier `montant_rationalise` renseigné et la première valeur non vide pour le reste, dans l'ordre du fichier.

## 2. Le montant : `montant_rationalise`, et seulement s'il est fiable

- **Le montant brut n'est jamais utilisé.** Nous lisons `montant_rationalise`, jamais `montant`.
- **Un montant est fiable s'il est strictement positif et sans anomalie signalée.** Plus de 22 000 marchés sont déclarés à 0 € sans être signalés comme anomalies. Dans le fichier, « pas d'anomalie » se lit comme un `montant_anomalie` vide. Les seules valeurs présentes sont `suspect` et `aberrant` (constaté sur `decp.parquet` le 2 août 2026).
- **Les statistiques de montants portent sur les seuls montants fiables.** C'est le cas de la médiane, des déciles et des totaux, qui affichent leur assiette : « sur N marchés au montant fiable ».
- **Les dénombrements portent sur tous les marchés.** Nombre de marchés, part des PME, part des marchés à offre unique : un montant manquant n'en retire aucun.

Pourquoi exclure plutôt que corriger : un neuvième décile pollué par un montant aberrant est pire qu'un neuvième décile calculé sur moins de marchés, à condition de dire sur combien.

## 3. Les groupements : un partage à parts égales

Le jeu ne dit pas comment le montant se répartit entre cotraitants. Pour attribuer un montant à un titulaire, nous divisons le montant du marché par le nombre de titulaires. C'est une convention, pas une donnée. Elle garantit seulement que la somme des titulaires ne dépasse jamais le total du marché, et nous l'affichons.

## 4. Les titulaires qui sont des personnes

Certains titulaires sont des personnes physiques : entrepreneurs individuels, professions libérales.
- **Dans les totaux, ils comptent.** Ils entrent dans tous les totaux et toutes les parts.
- **Ailleurs, ils n'apparaissent pas.** Nous ne les nommons jamais dans un classement et ne publions aucune localisation individuelle.
- **En cas de doute, nous les traitons comme des personnes.** Le répertoire Sirene aide à les repérer.

## 5. Les nettoyages

- **Les codes département.** « 6 » ou « 006 » deviennent « 06 », la Corse garde 2A et 2B. Un code invalide est mis à vide, la ligne reste.
- **La division CPV.** C'est les deux premiers caractères de `codeCPV`. Une division hors nomenclature est mise à vide.
- **Les lignes sans `dateNotification`.** Elles sont écartées, et comptées.
- **La période.** Nous ne retenons que les marchés notifiés depuis le 1er janvier 2022 : c'est la période sur laquelle nous jugeons la couverture assez régulière.

## 6. L'adresse du fichier

L'adresse de la ressource change. Nous la demandons à l'API de data.gouv.fr à chaque lecture, plutôt que de la figer dans le code.

## Le code

Ces règles sont écrites en SQL pour DuckDB dans [decp-lecture](https://github.com/V08-ai/decp-lecture), avec leurs tests.

## Citer la source

« Données essentielles de la commande publique, consolidation Colin Maudry (decp.info), data.gouv.fr, Licence Ouverte 2.0 ».

Cette note est publiée sous licence [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.fr). Une erreur, une règle à discuter : ouvrez une issue sur ce dépôt ou écrivez à contact@temiapp.com.
